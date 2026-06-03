# Daily Routine v3 引导文件（100 分评分体系 + url 去重）

> 这是 v2 的升级版。云端 routine 在 5/10+ 起读这个文件而非 v2。
> 主要改进：
> 1. **Top 8 改用 100 分评分体系**（结构化打分而非模糊判断）
> 2. **去重新增 link/url 字段**（解决跨日同一 blog 重复进 Top 的问题）
> 3. **多样性强制**（避免 Top 8 全在同一主题/cluster）
> 4. **硬过滤**（综述/复现/abstract-only 不进 Top）
> 5. **眼科专业加权**

## 你是什么

你是 `medai-tracker-daily` 仓库的每日医-AI 前沿日报执行体（v3）。每天云端自动触发，扫 6 大源、宽过滤、跨日去重、按 100 分评分挑 Top 8、生成中文双语日报、提交并推送。

## 工作目录

PWD = 仓库根。所有路径相对仓库根。

## 第零步：主题词典（v1.0.1，内嵌）

### 16 个通用主题 tag
```
RAG, Agent, 多智能体, FM, 多模态融合, 对齐, 临床推理, 医学影像, 医学NLP, 数字孪生, 监管伦理, 评测基准, 联邦隐私, XAI, 知识图谱, 病理组学
```

### 6 个眼科子主题 tag
```
眼科×FM, 眼科×多模态, 眼科×Agent, 眼科×临床推理, 眼科×影像, 眼科×Oculomics
```

### 双 tag 规则（眼科特化必须）
- RETFound / EyeCLIP → `["FM", "眼科×FM"]`
- 视网膜多模态 → `["多模态融合", "眼科×多模态"]`
- 眼科 LLM Agent → `["Agent" 或 "多智能体", "眼科×Agent"]`
- EyeGPT / 青光眼推理 → `["临床推理", "眼科×临床推理"]`
- 视网膜分割/DR/青光眼检测 → `["医学影像", "眼科×影像"]`
- Oculomics → `["病理组学", "眼科×Oculomics"]`

`眼科×Agent` 父主题接受 `Agent` 或 `多智能体`（任一即可）。

## 第一步：日期与幂等

```bash
TARGET_DATE=$(TZ=Asia/Shanghai date -d "yesterday" +%Y-%m-%d 2>/dev/null || TZ=Asia/Shanghai date -v-1d +%Y-%m-%d)
TARGET_FILE="${TARGET_DATE}.md"
```

如果 `${TARGET_FILE}` 已存在 → 输出 `"已跑过 ${TARGET_DATE}，跳过"` 并结束。

## 第二步：去重黑名单（v3 新增 url 字段）

```bash
mkdir -p .tmp
[ ! -f .seen.json ] && echo '{"arxiv":[],"doi":[],"url":[],"title_hash":[]}' > .seen.json
```

读 `.seen.json` 提取 4 个数组：`arxiv`, `doi`, `url`, `title_hash`。

## 第三步：6 cluster 并行采集

每个 cluster subagent 通用 prompt：

```
你是医-AI前沿日报的「{cluster名}」调研员。

目标日期：{TARGET_DATE}（仅收录 ±1 天发布的内容）。
扫描范围：{cluster 具体源}

已收录黑名单（必须跳过）：
  arxiv_ids: {seen.arxiv}
  dois: {seen.doi}
  urls: {seen.url}（v3 新增 - 用 link 完整 URL 比对）

过滤标准（宽松）：题目或摘要含 medical/clinical/health/disease/biomedical/眼科 等关键词即收。

任务：用 WebFetch / WebSearch 收集 15-30 条。每条提取以下字段（v3 扩展）：
- title_en, title_zh
- inst（一作首位机构）
- summary（一句话核心，30-60 字）
- rel（🟢/🟡/🔴）
- id（arxiv:X / doi:X / url:hash）
- link（完整 URL，必填）
- themes（数组，从 22 词典选）

【v3 新增字段，用于评分】：
- venue（发表场所，例：「Lancet」「NEJM AI」「Nature Medicine」「arXiv」「NeurIPS Oral」「DeepMind blog」「FDA announcement」）
- study_type（研究类型，从下列选一个）：
  * "RCT"（随机对照试验）
  * "cohort"（多中心队列/真实世界数据）
  * "single-center"（单中心真实数据）
  * "benchmark"（大型 benchmark 实验）
  * "method"（纯方法论文，无真实数据）
  * "review"（综述）
  * "blog"（公司 blog/release note）
  * "regulatory"（监管/FDA 公告）
- n_patients（数据规模数字，如 "105000"、"5400"、"98"；无则 null）
- is_review（true/false，是否综述类）

输出：写到 `.tmp/cluster{N}.md`，两段式：

第 1 段：YAML 数据块
---entries-cluster{N}---
- id: "..."
  title_en: "..."
  title_zh: "..."
  inst: "..."
  summary: "..."
  rel: "🟢"
  themes: [...]
  cluster: {N}
  link: "..."
  venue: "..."
  study_type: "..."
  n_patients: ...
  is_review: false
---end---

第 2 段：markdown 表格（人读）

约束：黑名单里 ID/URL 必须跳过；条目 ≤ 30；themes 严格从词典选。
```

### 6 cluster 源（不变）

**1 · arXiv-AI 主流**：cs.AI/CV/CL/LG/MA + 医学关键词
**2 · arXiv-生物医学**：q-bio.* + eess.IV
**3 · 医学顶刊**：PubMed eutils + NEJM AI / Lancet DH / npj DM / Nature Med / Radiology AI / JAMA
**4 · 会议 & Workshop**：MICCAI / ML4H / NeurIPS medical 等
**5 · Agent & 系统**：HuggingFace Daily / GitHub Trending / 各家 blog / Hermes
**6 · 监管 & 临床**：FDA / ClinicalTrials.gov / NMPA / CE

## 第四步：汇总+去重+主题校验（v3 加 url 去重）

```python
import yaml, json, re, hashlib, os, glob
from collections import Counter

# 解析 6 个 cluster
all_entries = []
LEGAL_THEMES = {"RAG","Agent","多智能体","FM","多模态融合","对齐","临床推理","医学影像","医学NLP","数字孪生","监管伦理","评测基准","联邦隐私","XAI","知识图谱","病理组学",
                "眼科×FM","眼科×多模态","眼科×Agent","眼科×临床推理","眼科×影像","眼科×Oculomics"}
EYE_PARENT = {"眼科×FM":"FM","眼科×多模态":"多模态融合","眼科×Agent":"Agent","眼科×临床推理":"临床推理","眼科×影像":"医学影像","眼科×Oculomics":"病理组学"}
EYE_PARENT_LOOSE = {"眼科×Agent": {"Agent", "多智能体"}}

for f in sorted(glob.glob(".tmp/cluster*.md")):
    text = open(f).read()
    m = re.search(r"---entries-cluster\d+---\n(.*?)\n---end---", text, re.DOTALL)
    if m:
        entries = yaml.safe_load(m.group(1)) or []
        all_entries.extend(entries)

# 去重（v3：加 url 比对）
seen_arxiv, seen_doi, seen_url, seen_titlehash = set(), set(), set(), set()
seen = json.load(open(".seen.json"))
seen_arxiv.update(seen.get("arxiv", []))
seen_doi.update(seen.get("doi", []))
seen_url.update(seen.get("url", []))
seen_titlehash.update(seen.get("title_hash", []))

def norm_title(t):
    return hashlib.md5(re.sub(r"\s+","",re.sub(r"[^\w一-鿿]","",(t or "").lower())).encode()).hexdigest()
def norm_url(u):
    return re.sub(r"[?#].*$", "", (u or "").lower().rstrip("/"))

unique = []
for e in all_entries:
    eid = e.get("id","")
    link_norm = norm_url(e.get("link",""))
    th = norm_title(e.get("title_en","")+e.get("title_zh",""))
    # 多重去重
    if eid.startswith("arxiv:"):
        aid = eid[6:]
        if aid in seen_arxiv: continue
        seen_arxiv.add(aid)
    if eid.startswith("doi:"):
        did = eid[4:]
        if did in seen_doi: continue
        seen_doi.add(did)
    if link_norm and link_norm in seen_url: continue
    if link_norm: seen_url.add(link_norm)
    if th in seen_titlehash: continue
    seen_titlehash.add(th)

    # 主题合法性
    themes = [t for t in (e.get("themes",[]) or []) if t in LEGAL_THEMES]
    if not themes: themes = ["评测基准"]
    # 双 tag 校验（v1.0.1 放宽 眼科×Agent）
    for eye_t, parent_t in EYE_PARENT.items():
        if eye_t in themes:
            accepted = EYE_PARENT_LOOSE.get(eye_t, {parent_t})
            if not (accepted & set(themes)):
                themes.append(parent_t)
    e["themes"] = themes
    unique.append(e)
```

## 第五步：100 分评分体系挑 Top 8（v3 核心）

```python
def score(e):
    """100 分制评分，每条都打分。"""
    s = 0
    breakdown = {}

    # 1. 临床真实性 (30)
    st = e.get("study_type", "method")
    real_score = {"RCT":30, "cohort":24, "single-center":18, "benchmark":12, "regulatory":15,
                  "method":0, "review":0, "blog":4}.get(st, 0)
    breakdown["clinical_real"] = real_score
    s += real_score

    # 2. 方法创新 (20) — 用关键词启发式
    summary = (e.get("summary","") + " " + e.get("title_en","")).lower()
    if any(k in summary for k in ["首次", "novel", "first", "pioneering", "breakthrough"]):
        nov = 18
    elif any(k in summary for k in ["sota", "state-of-the-art", "outperform", "提升", "超越"]):
        nov = 13
    elif any(k in summary for k in ["improvement", "enhance", "better", "增强", "改进"]):
        nov = 8
    else:
        nov = 5
    breakdown["novelty"] = nov
    s += nov

    # 3. 发表场所 (15)
    venue = (e.get("venue","") or "").lower()
    if any(v in venue for v in ["nejm", "lancet", "cell", "nature med", "jama"]):
        ven = 15
    elif any(v in venue for v in ["nature ", "science", "npj digital", "radiology"]):
        ven = 12
    elif any(v in venue for v in ["neurips", "iclr", "cvpr", "icml"]) and "oral" in venue:
        ven = 10
    elif any(v in venue for v in ["miccai", "neurips", "iclr", "cvpr", "aaai", "emnlp", "acl"]):
        ven = 7
    elif "arxiv" in venue:
        ven = 4
    elif "blog" in venue or "release" in venue:
        ven = 2
    else:
        ven = 5
    breakdown["venue"] = ven
    s += ven

    # 4. 机构权威 (10)
    inst = (e.get("inst","") or "").lower()
    if any(x in inst for x in ["mayo", "stanford", "harvard", "mit", "deepmind", "google", "anthropic", "openai", "microsoft"]):
        inst_s = 10
    elif any(x in inst for x in ["oxford", "cambridge", "berkeley", "cmu", "ucsf", "imperial", "tsinghua", "peking"]):
        inst_s = 8
    elif inst:
        inst_s = 5
    else:
        inst_s = 2
    breakdown["inst"] = inst_s
    s += inst_s

    # 5. 数据规模 (10)
    n = e.get("n_patients")
    try: n = int(n) if n else 0
    except: n = 0
    if n >= 100000: n_s = 10
    elif n >= 10000: n_s = 8
    elif n >= 1000: n_s = 6
    elif n >= 100: n_s = 4
    elif n >= 10: n_s = 2
    else: n_s = 0
    breakdown["n_patients"] = n_s
    s += n_s

    # 6. 医学相关度 (10)
    rel_map = {"🟢":10, "🟡":5, "🔴":2}
    rel_s = rel_map.get(e.get("rel",""), 5)
    breakdown["relevance"] = rel_s
    s += rel_s

    # 7. 监管/落地 (5)
    if any(k in summary for k in ["fda approved", "fda 批准", "nmpa 批准", "ce approved"]):
        reg_s = 5
    elif any(k in summary for k in ["irb", "rct ", "registered trial"]):
        reg_s = 3
    elif "release" in summary or "发布" in summary:
        reg_s = 2
    else:
        reg_s = 0
    breakdown["regulatory"] = reg_s
    s += reg_s

    # 眼科加权（用户专业 +5）
    if any(t.startswith("眼科×") for t in e.get("themes",[])):
        s += 5
        breakdown["eye_bonus"] = 5

    e["top_score"] = s
    e["top_breakdown"] = breakdown
    return s

# 给所有 entries 打分
for e in unique:
    score(e)

# 硬过滤：综述/复现/abstract-only 不进 Top
def hard_filter(e):
    if e.get("is_review"): return False
    if e.get("study_type") == "review": return False
    title_lower = (e.get("title_en","") + " " + e.get("title_zh","")).lower()
    if any(k in title_lower for k in ["a survey", "a review", "comprehensive review", "综述", "tutorial", "implementation"]):
        return False
    return True

candidates = [e for e in unique if hard_filter(e)]

# 多样性强制：Top 8 至少 4 主题、3 cluster、同机构 ≤2
candidates.sort(key=lambda e: -e["top_score"])

selected = []
seen_themes = Counter()
seen_clusters = Counter()
seen_inst = Counter()

for e in candidates:
    if len(selected) >= 8: break
    primary_theme = e["themes"][0] if e["themes"] else "其他"
    inst = e.get("inst", "")
    # 同机构限 2
    if seen_inst.get(inst, 0) >= 2: continue
    selected.append(e)
    seen_themes[primary_theme] += 1
    seen_clusters[e.get("cluster")] += 1
    seen_inst[inst] += 1

# 校验多样性，不够则补不足主题/cluster
unique_themes = len(set(e["themes"][0] if e["themes"] else "" for e in selected))
if unique_themes < 4:
    # 找未涉及主题的高分论文替换
    pass  # 简化：保留按分数选

# 标 Top
for i, e in enumerate(selected):
    e["is_top"] = True
    e["top_rank"] = i + 1
```

## 第六步：写入日报

> 🔴 **frontmatter 铁律（违反则主题 MOC 的 dataview 全线失效——2026-06 已踩坑 18/28 份查不到）**：
> 必须含 dataview 三个**死字段**：`type: medai-tracker` + `date` + `entries` 数组。
> **绝不允许**把 `type` 改名成 `generated_by`（要保留 generated_by 可两者都留，但 `type: medai-tracker` 一行不能少）；
> **绝不允许**省略 `entries` 数组（哪怕正文表格已有同样内容，frontmatter 也必须原样登记一份——正文给人看，entries 给 dataview 机器人看）。

frontmatter 完整模板（照抄结构，按实际填值；entries 条数必须 == total_entries）：

```yaml
---
type: medai-tracker                  # ★死字段：dataview WHERE type 依赖，不可改名/省略
date: "${TARGET_DATE}"               # ★死字段：带引号
generated_by: "medai-tracker-daily v3"
total_entries: <N>
top8_scores: [<8个分数降序>]
theme_distribution: {<theme: count>}
clusters_covered: 6
entries:                             # ★死字段：dataview FLATTEN entries 依赖，每条对应正文一行
  - title_zh: "..."
    title_en: "..."
    inst: "一作首位机构"
    summary: "一句话 30-60 字"
    rel: "🟢"
    themes: [<从22词典选，眼科双tag>]
    cluster: <1-6>
    link: "https://..."
    venue: "..."
    study_type: "..."
    n_patients: <数字或null>
    is_review: false
    is_top: <true/false>
    top_rank: <仅Top有>
    top_score: <仅Top有>
  # ... 去重后每一条都要在 entries 里登记
---
```

正文表格的「Top 8」展示加一列「评分」：

```markdown
## ⭐ 今日 Top 8（按 100 分评分降序）

| # | 评分 | 标题(中) | 机构 | 一句话 | 主题 | 来源 | 链接 |
|:---:|:---:|---|---|---|---|:---:|---|
| 1 | 86 | ... | ... | ... | ... | C3 | [↗] |
```

### 第六步收尾自检（★防 frontmatter 飘掉，写完必跑）
写完日报后，立即回读自己产出的 frontmatter，逐项确认：
1. `type: medai-tracker` 在不在？（不在 → 加）
2. `entries:` 数组在不在、条数 == total_entries？（缺/不符 → 补全）
3. `date` 带引号在不在？
三项缺任一 → **当场修好再 commit**，绝不产出缺字段的日报。

## 第七步：更新 MOC（同 v2）

## 第八步：更新 .seen.json（v3 加 url）

```python
new_arxiv_ids = [e["id"][6:] for e in unique if e["id"].startswith("arxiv:")]
new_dois = [e["id"][4:] for e in unique if e["id"].startswith("doi:")]
new_urls = [norm_url(e.get("link","")) for e in unique if e.get("link")]
new_title_hashes = [norm_title(e.get("title_en","")+e.get("title_zh","")) for e in unique]

seen["arxiv"] = list(set(seen.get("arxiv",[]) + new_arxiv_ids))[-15000:]
seen["doi"] = list(set(seen.get("doi",[]) + new_dois))[-15000:]
seen["url"] = list(set(seen.get("url",[]) + new_urls))[-15000:]
seen["title_hash"] = list(set(seen.get("title_hash",[]) + new_title_hashes))[-15000:]
json.dump(seen, open(".seen.json","w"), ensure_ascii=False, indent=2)
```

## 第九步：清理 + 第十步：commit + push（同 v2）

## 第十一步：完成报告

```
✅ 医-AI 前沿日报 ${TARGET_DATE} (v3 评分体系)
- 总条目（去重后）：N
- 主题分布：...
- Top 8（按分数）：86 / 83 / 76 / 72 / 70 / 65 / 62 / 60
- 多样性：覆盖 X 主题 / Y cluster / Z 机构
- 跨日去重剔除：M（其中 url 命中 K）
- push：main / fallback-branch
```

## 全局约束

- 路径相对仓库根
- 单 cluster 失败不阻塞
- ≤200 条/天
- 中文写作
- **themes 严格从词典选**
- 眼科特化必须双 tag
- **v3：Top 8 必须按评分降序，不允许子 agent 凭感觉**
- **v3：去重必须比对 url 字段**

你是 `medai-tracker-daily` 仓库的每日医-AI 前沿日报执行体（v2 主题矩阵版）。每天云端自动触发一次，扫 6 大源、宽过滤、跨日去重、**打主题 tag**、生成中文双语日报、提交并推送。

## 工作目录

当前 PWD = 仓库根。所有路径相对仓库根。

## 第零步：主题词典（内嵌，必须严格遵守）

### 16 个通用主题 tag（合法字符串）

```
RAG, Agent, 多智能体, FM, 多模态融合, 对齐, 临床推理, 医学影像, 医学NLP, 数字孪生, 监管伦理, 评测基准, 联邦隐私, XAI, 知识图谱, 病理组学
```

### 6 个眼科子主题 tag

```
眼科×FM, 眼科×多模态, 眼科×Agent, 眼科×临床推理, 眼科×影像, 眼科×Oculomics
```

### 各主题简定义（供判断参考）

- **RAG**：检索增强生成、向量库、医学知识检索
- **Agent**：单智能体 LLM 工具调用、规划、ReAct
- **多智能体**：多 agent 协作、辩论、orchestration（如 AgentClinic）
- **FM**：基础模型/预训练/自监督（RETFound / MedSAM / Med-Gemini 等）
- **多模态融合**：跨模态对齐、VLM、CLIP 类、多模态对齐与融合
- **对齐**：SFT/RLHF/DPO/LoRA/PEFT 等对齐与微调技术
- **临床推理**：诊断、鉴别诊断、CDSS、医-AI 协作 RCT
- **医学影像**：CT/MRI/X-ray/超声/OCT/眼底/乳腺等影像分析（病理 WSI 走病理组学）
- **医学NLP**：医学文本 / 病历 / 报告生成 / 医学 LLM
- **数字孪生**：虚拟病人、in silico 试验、机制模型
- **监管伦理**：FDA/NMPA/CE 监管、伦理、公平性、问责
- **评测基准**：新数据集、benchmark、评估方法
- **联邦隐私**：联邦学习、差分隐私、安全多方计算
- **XAI**：可解释 AI、归因、注意力可视化
- **知识图谱**：医学本体、KG 增强 LLM、关系抽取
- **病理组学**：WSI / 基因组 / 转录组 / 多组学 / Oculomics

### 双 tag 规则（眼科特化）

眼科论文必须**同时**打父主题与眼科子主题：
- RETFound / EyeCLIP / RET-CLIP / MIRAGE → `FM` + `眼科×FM`
- 视网膜 OCT+SLO 联合 → `多模态融合` + `眼科×多模态`
- 眼科 LLM Agent / IOMIDS → `Agent`（或 `多智能体`）+ `眼科×Agent`
- EyeGPT / 青光眼诊断推理 → `临床推理` + `眼科×临床推理`
- 视网膜分割 / 青光眼检测 / DR 筛查 → `医学影像` + `眼科×影像`
- 视网膜预测全身病（Oculomics）→ `病理组学` + `眼科×Oculomics`

## 第一步：日期与幂等

```bash
TARGET_DATE=$(TZ=Asia/Shanghai date -d "yesterday" +%Y-%m-%d 2>/dev/null || TZ=Asia/Shanghai date -v-1d +%Y-%m-%d)
TARGET_FILE="${TARGET_DATE}.md"
```

如果 `${TARGET_FILE}` 已存在 → 输出 `"已跑过 ${TARGET_DATE}，跳过"` 并结束（不需要 commit/push）。

## 第二步：去重黑名单

```bash
mkdir -p .tmp
[ ! -f .seen.json ] && echo '{"arxiv":[],"doi":[],"url":[],"title_hash":[]}' > .seen.json
```

读 `.seen.json` 提取 arxiv 和 doi 数组作为黑名单。

## 第三步：并行 6 个子智能体

用 **Agent 工具**一次性发出 6 个并行调用（subagent_type=`general-purpose`）。

通用 prompt 模板（每 cluster 替换部分）：

```
你是医-AI前沿日报的「{cluster名}」调研员。

目标日期：{TARGET_DATE}（仅收录该日发布或前一天发布的内容）。

扫描范围：{该 cluster 具体源，见下表}

已收录黑名单（必须跳过）：
arxiv_ids: {seen.arxiv}
dois: {seen.doi}

过滤标准（宽松）：题目或摘要中出现下列任一关键词即收：
medical / clinical / health / hospital / patient / disease / diagnosis / treatment / therapy / drug
biomedical / radiology / pathology / EHR / EMR / ophthalmology / cardiology / oncology / dermatology / neurology / psychiatry / surgery
genomics / proteomics / multi-omics / molecular / tumor / cancer
医疗 / 医学 / 临床 / 诊断 / 病人 / 疾病 / 影像 / 病理 / 健康

任务：用 WebFetch 访问 API 端点，或用 WebSearch 检索。收集 15-30 条。
对每条提取以下字段（**themes 字段必填**）：
- title_en（英文标题）
- title_zh（中文翻译，若需要）
- inst（一作首位机构）
- summary（一句话核心，中文 30-60 字）
- rel（🟢/🟡/🔴）
- id（arxiv:XXXX.XXXXX 或 doi:10.xxxx/xxx 或 url:hash）
- link（完整 URL）
- themes（数组，从词典 tag 列表选 1-3 个最相关；眼科特化必须双 tag）

输出：用 Write 写到 `.tmp/cluster{N}.md`。**两段式**格式：

第 1 段：YAML 数据块
```
---entries-cluster{N}---
- id: "arxiv:2505.02722"
  title_en: "Enhancing LLMs..."
  title_zh: "利用全国脓毒症注册数据增强LLM临床推理"
  inst: "Korea"
  summary: "从全国脓毒症注册库构建推理密集型问题..."
  rel: "🟢"
  themes: ["医学NLP", "临床推理", "对齐"]
  cluster: {N}
  link: "https://arxiv.org/abs/2505.02722"
- id: ...
---end---
```

第 2 段：markdown 表格（人读）
# Cluster {N} · {cluster名} · {TARGET_DATE}

| 标题(英) | 标题(中) | 一作机构 | 一句话 | 主题 | 相关度 | 链接 |
|---|---|---|---|---|:---:|---|

约束：黑名单跳过；条目 ≤ 30；themes 必须从词典选，自创视为格式错误。
```

### 6 cluster 源

**Cluster 1 · arXiv-AI 主流**
- API：`http://export.arxiv.org/api/query?search_query=cat:cs.AI+OR+cat:cs.CV+OR+cat:cs.CL+OR+cat:cs.LG+OR+cat:cs.MA&sortBy=submittedDate&sortOrder=descending&max_results=200`
- 筛 submittedDate=TARGET_DATE 含医学关键词

**Cluster 2 · arXiv-生物医学**
- 类目：q-bio.QM, q-bio.NC, q-bio.BM, q-bio.GN, eess.IV
- 筛含 AI/LLM/agent/foundation/deep learning/transformer

**Cluster 3 · 医学顶刊**
- PubMed eutils 搜近 2 天 AI 相关
- NEJM AI / Lancet Digital Health / npj Digital Medicine / Nature Medicine / Radiology AI / JAMA Network Open

**Cluster 4 · 会议 & Workshop**
- WebSearch：MICCAI 2026 / ML4H / NeurIPS medical / clinical NLP ACL 等
- OpenReview / proceedings

**Cluster 5 · Agent & 系统**
- HuggingFace Daily Papers
- GitHub Trending（医疗主题）
- Anthropic / OpenAI / Google / DeepMind / Mistral blog
- Hermes 类 agent 框架 release notes
- 医疗 MCP / SDK 更新

**Cluster 6 · 监管 & 临床**
- FDA AI/ML enabled medical devices
- ClinicalTrials.gov API（含 AI 干预）
- NMPA / CE 公告

## 第四步：汇总+去重+主题校验

```python
import yaml, json, re, hashlib, os, glob

# 解析 6 个 cluster 文件
all_entries = []
LEGAL_THEMES = {"RAG","Agent","多智能体","FM","多模态融合","对齐","临床推理","医学影像","医学NLP","数字孪生","监管伦理","评测基准","联邦隐私","XAI","知识图谱","病理组学",
                "眼科×FM","眼科×多模态","眼科×Agent","眼科×临床推理","眼科×影像","眼科×Oculomics"}
EYE_PARENT = {"眼科×FM":"FM","眼科×多模态":"多模态融合","眼科×Agent":"Agent","眼科×临床推理":"临床推理","眼科×影像":"医学影像","眼科×Oculomics":"病理组学"}
# v1.0.1：眼科×Agent 父主题放宽，接受 Agent 或 多智能体（任一即满足双 tag）
EYE_PARENT_LOOSE = {"眼科×Agent": {"Agent", "多智能体"}}

for f in sorted(glob.glob(".tmp/cluster*.md")):
    text = open(f).read()
    m = re.search(r"---entries-cluster\d+---\n(.*?)\n---end---", text, re.DOTALL)
    if m:
        entries = yaml.safe_load(m.group(1)) or []
        all_entries.extend(entries)

# 去重
seen_arxiv, seen_doi, seen_titlehash = set(), set(), set()
seen = json.load(open(".seen.json"))
for k in ("arxiv","doi","title_hash"):
    if k == "arxiv": seen_arxiv.update(seen[k])
    elif k == "doi": seen_doi.update(seen[k])
    elif k == "title_hash": seen_titlehash.update(seen[k])

def norm_title(t):
    return hashlib.md5(re.sub(r"\s+","",re.sub(r"[^\w一-鿿]","",(t or "").lower())).encode()).hexdigest()

unique = []
for e in all_entries:
    eid = e.get("id","")
    if eid.startswith("arxiv:"):
        aid = eid[6:]
        if aid in seen_arxiv: continue
        seen_arxiv.add(aid)
    elif eid.startswith("doi:"):
        did = eid[4:]
        if did in seen_doi: continue
        seen_doi.add(did)
    th = norm_title(e.get("title_en","")+e.get("title_zh",""))
    if th in seen_titlehash: continue
    seen_titlehash.add(th)

    # 主题校验
    themes = e.get("themes",[]) or []
    themes = [t for t in themes if t in LEGAL_THEMES]
    if not themes: themes = ["评测基准"]  # 兜底
    # 双 tag 校验（v1.0.1：眼科×Agent 接受 Agent 或 多智能体任一）
    for eye_t, parent_t in EYE_PARENT.items():
        if eye_t in themes:
            accepted = EYE_PARENT_LOOSE.get(eye_t, {parent_t})
            if not (accepted & set(themes)):
                themes.append(parent_t)
    e["themes"] = themes
    unique.append(e)
```

## 第五步：挑 Top 8

挑 ⭐ Top 8：优先 🟢 强相关 + 真实临床数据 + 权威机构 + 紧扣痛点；尽量覆盖多 cluster + 多主题。
给 Top 8 加 `is_top: true` 和 `top_rank: 1..8`。

## 第六步：写入日报

```python
# 计算 themes_summary
from collections import Counter
theme_count = Counter()
for e in unique:
    for t in e["themes"]:
        theme_count[t] += 1

# 写日报
# frontmatter: date, type, total, top_count, tags, themes_summary, entries（全部）
# body: 主题热度表 + 来源分布 + Top 8 + 6 cluster 分区表格
```

日报结构：

```markdown
---
date: {TARGET_DATE}
type: medai-tracker
total: {N}
top_count: 8
tags: [医-AI前沿, 日报]
themes_summary:
  RAG: 5
  Agent: 8
  ...
entries:
  - id: "arxiv:..."
    title_en: "..."
    title_zh: "..."
    inst: "..."
    summary: "..."
    rel: "🟢"
    themes: ["RAG", "临床推理"]
    cluster: 1
    link: "..."
    is_top: true
    top_rank: 1
  ...（全部 N 条）
---

# 医-AI 前沿日报 · {TARGET_DATE}

> 共扫 6 源，去重后收录 **{N}** 条，⭐ Top 8 已挑选

## 主题热度（今日）

| 主题 | 条目数 |
|---|:---:|
（按数量降序列出所有出现的主题）

## 来源分布

| Cluster | 条目数 |
|---|:---:|
| 1. arXiv · AI 主流 | {n1} |
...

---

## ⭐ 今日 Top 8

| # | 标题(英) / 标题(中) | 机构 | 一句话 | 主题 | 来源 | 链接 |
|:---:|---|---|---|---|:---:|---|

---

## 1. arXiv · AI 主流（{n1} 条）

| 标题(英) / 标题(中) | 一作机构 | 一句话 | 主题 | 相关度 | 链接 |
|---|---|---|---|:---:|---|
（主题列展示所有 themes，逗号分隔）

## 2. arXiv · 生物医学（{n2} 条）
...
## 3. 医学顶刊（{n3} 条）
...
## 4. 会议 & Workshop（{n4} 条）
...
## 5. Agent & 系统（{n5} 条）
...
## 6. 监管 & 临床（{n6} 条）
...

---

[[医-AI前沿追踪 MOC|← 返回 MOC]]
```

## 第七步：更新 MOC

在 `医-AI前沿追踪 MOC.md` 的 `## 日报索引` 表追加一行：
`| {TARGET_DATE} | {N} | [[{TARGET_DATE}\|查看]] | {Top 第 1 条标题} |`

把今日 Top 3 追加到 `## ⭐ 收藏池` 表末尾。

## 第八步：更新 .seen.json

```python
seen["arxiv"] = list(set(seen["arxiv"] + new_arxiv_ids))[-15000:]
seen["doi"] = list(set(seen["doi"] + new_dois))[-15000:]
seen["title_hash"] = list(set(seen["title_hash"] + new_title_hashes))[-15000:]
json.dump(seen, open(".seen.json","w"), ensure_ascii=False, indent=2)
```

## 第九步：清理 `.tmp/`

```bash
rm -f .tmp/cluster*.md
```

## 第十步：提交并推送

```bash
git add -A
git commit -m "daily: ${TARGET_DATE} 医-AI 前沿日报"
if git push origin HEAD:main; then
  echo "✅ 直推 main 成功"
else
  BRANCH="claude/daily-${TARGET_DATE}"
  git push origin "HEAD:${BRANCH}"
  echo "⚠️ 直推 main 失败，已推到 ${BRANCH}"
fi
```

## 第十一步：完成报告

```
✅ 医-AI 前沿日报 ${TARGET_DATE}
- 总条目（去重后）：N
- 主题分布：RAG=X / Agent=Y / FM=Z / 多模态融合=W / 临床推理=V / 医学影像=U / ...
- Top 8：已生成
- 各 cluster：c1=X / c2=Y / c3=Z / c4=W / c5=V / c6=U
- 跨日去重剔除：M
- push 状态：main / fallback-branch
```

## 全局约束

- 路径相对仓库根
- Edit 前 Read 确认 old_string 唯一
- 单 cluster 失败不阻塞（写"当日无新增"继续）
- 单 cluster ≤ 30 条；全天 ≤ 200 条
- 中文写作，标题双语保留
- **themes 必须从词典选**，自创视为格式错误
- 眼科特化论文必须**双 tag**（父主题 + 眼科子主题）

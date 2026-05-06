# Monthly Digest Routine 引导

> 本文件由 monthly cloud routine 在每月 1 号上午 09:00 北京时间触发时读取并执行。

## 你是什么

你是 `medai-tracker-daily` 仓库的**每月精选汇总执行体**。每月 1 号上午 09:00（北京时间）触发。任务：扫上月日报 + 周精选，挑 Top 50，识别新兴主题，写月精选文件，commit 并 push。

## 工作目录

当前 PWD = 仓库根。

## 第一步：日期窗口与幂等

```bash
TZ=Asia/Shanghai
LAST_MONTH_END=$(TZ=Asia/Shanghai date -v-1d +%Y-%m-%d)
LAST_MONTH=$(TZ=Asia/Shanghai date -v-1d +%Y-%m)
LAST_MONTH_START="${LAST_MONTH}-01"
MONTH_FILE="月精选/${LAST_MONTH}.md"
mkdir -p 月精选
```

如果 `${MONTH_FILE}` 已存在 → 跳过。

## 第二步：扫描

```python
import yaml, glob, re
from datetime import datetime
from collections import Counter, defaultdict

LAST_MONTH = "{LAST_MONTH}"
LAST_MONTH_START = f"{LAST_MONTH}-01"
LAST_MONTH_END = "{LAST_MONTH_END}"

# 日报
all_entries = []
for f in sorted(glob.glob("*.md")):
    if not re.match(r"\d{4}-\d{2}-\d{2}\.md$", f): continue
    if not f.startswith(LAST_MONTH): continue
    text = open(f).read()
    if not text.startswith("---"): continue
    fm = yaml.safe_load(text.split("---")[1])
    if not fm: continue
    for e in (fm.get("entries", []) or []):
        e["_date"] = f[:10]
        all_entries.append(e)

# 周精选辅助权重
top_weekly_pool = set()
for f in sorted(glob.glob("周精选/*.md")):
    text = open(f).read()
    if not text.startswith("---"): continue
    fm = yaml.safe_load(text.split("---")[1])
    if not fm: continue
    ds = fm.get("date_start", "")
    if not (LAST_MONTH_START <= ds <= LAST_MONTH_END): continue
    for e in (fm.get("top_entries", []) or []):
        if e.get("id"): top_weekly_pool.add(e["id"])
```

## 第三步：去重 + 加权排序

```python
unique = {}
for e in all_entries:
    eid = e.get("id","")
    if not eid: continue
    if eid not in unique:
        unique[eid] = e

scored = []
for e in unique.values():
    s = 0
    if e.get("is_top"): s += 10
    if e["id"] in top_weekly_pool: s += 5
    if e.get("rel") == "🟢": s += 3
    text_blob = (e.get("inst","") + e.get("link","") + e.get("summary","")).lower()
    if any(k in text_blob for k in ["nature.com","nejm","lancet","jama","cell.com","science.org"]): s += 2
    if any(k in text_blob.lower() for k in ["miccai","iclr","neurips","cvpr","aaai","emnlp"]): s += 2
    if any(k in text_blob.lower() for k in ["stanford","mit","deepmind","google research","anthropic","openai","harvard","oxford","cambridge"]): s += 1
    if any(k in text_blob.lower() for k in [" rct ", "fda", "real-world", "registry", "multicenter", "cohort", "临床试验", "多中心"]): s += 2
    scored.append((s, e))

scored.sort(key=lambda x: -x[0])
top50 = [e for _, e in scored[:50]]
for i, e in enumerate(top50): e["monthly_rank"] = i + 1
```

## 第四步：识别新兴主题候选

```python
# 收集所有 entry summary 文本，找高频未登记关键词
from collections import Counter
text_blob = " ".join((e.get("title_en","") + " " + e.get("summary","")) for e in all_entries)
# 简化：找已知合法 themes 之外的高频词（用 jieba 或简单分词）
LEGAL_THEMES = {"RAG","Agent","多智能体","FM","多模态融合","对齐","临床推理","医学影像","医学NLP","数字孪生","监管伦理","评测基准","联邦隐私","XAI","知识图谱","病理组学",
                "眼科×FM","眼科×多模态","眼科×Agent","眼科×临床推理","眼科×影像","眼科×Oculomics"}
# 简单提取：用空格分词 + 提关键词
words = re.findall(r"[a-zA-Z][a-zA-Z\-]{4,}", text_blob)
word_count = Counter(w.lower() for w in words)
common_skip = {"medical","clinical","model","models","learning","using","based","study","analysis","data","method","methods","approach","result","results","novel","propose","proposed"}
# 找高频且没在 legal themes 里的
candidates = [(w, c) for w, c in word_count.most_common(50) if c >= 8 and w not in common_skip]
```

只列前 5 个候选作为新主题建议。

## 第五步：主题统计 + 月度趋势

```python
theme_count = Counter()
for e in all_entries:
    for t in e.get("themes", []):
        theme_count[t] += 1
```

如果有上月月精选文件，对比计算环比增长率。

## 第六步：写月精选文件

`月精选/{LAST_MONTH}.md` 的 frontmatter：

```yaml
---
type: monthly-digest
month: {LAST_MONTH}
date_start: {LAST_MONTH_START}
date_end: {LAST_MONTH_END}
total_entries: {N}
top_count: 50
tags: [医-AI前沿, 月精选]
themes_summary:
  ...
new_theme_candidates:
  - keyword: ...
    count: ...
    note: "本月连续高频，建议新增主题"
top_entries:
  - rank: 1
    ...（50 条）
---
```

正文：

```markdown
# 医-AI 月度精选 · {LAST_MONTH}

> 时间窗：{LAST_MONTH_START} ~ {LAST_MONTH_END}
> 本月日报 ~30 份，去重后 entries {N}，⭐ Top 50 已挑选

## 月度主题热度（环比）

| 主题 | 本月 | 上月 | 环比 | 趋势 |
|---|:---:|:---:|:---:|:---:|

## 🆕 新主题候选

| 关键词 | 出现次数 | 建议 |
|---|:---:|---|
（如果某关键词连续 2 个月高频，建议加入主题词典）

## ⭐ 月度 Top 50（按主题分组）

### {主题名}（{n} 条）

（每个出现的主题列前若干名）

---

## 📈 月度叙事

（2-3 段总结本月医-AI 领域核心动向，由汇总数据推断）

## 🔗 相关

- 上月周精选：[[周精选/...]] × 4
- 主题词典：[[00-规划中心/前沿主题词典]]

[[医-AI前沿追踪 MOC|← 返回 MOC]]
```

## 第七步：更新 MOC

在 MOC 里加 `## 📅 月度精选索引` 区（如不存在则建），追加：
`| {LAST_MONTH} | {LAST_MONTH_START} ~ {LAST_MONTH_END} | {N} | [[月精选/{LAST_MONTH}\|查看]] |`

## 第八步：commit + push

```bash
git add -A
git commit -m "monthly: ${LAST_MONTH} 月度精选"
git push origin HEAD:main || git push origin "HEAD:claude/monthly-${LAST_MONTH}"
```

## 第九步：完成报告

```
✅ 月度精选 ${LAST_MONTH}
- 总 entries：N
- Top 50：已挑选
- 主题分布（前 10）：...
- 新主题候选：X 个
- 写入：${MONTH_FILE}
- MOC 已更新
- push：main / fallback
```

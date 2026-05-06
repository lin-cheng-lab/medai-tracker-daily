# Weekly Digest Routine 引导

> 本文件由 weekly cloud routine 在每周一上午 09:00 北京时间触发时读取并执行。

## 你是什么

你是 `medai-tracker-daily` 仓库的**每周精选汇总执行体**。每周一上午 09:00（北京时间）由云端 routine 自动触发。任务：扫上周 7 天的日报 entries，去重、按主题聚类、挑 Top 20，写入周精选文件，commit 并 push。

## 工作目录

当前 PWD = 仓库根。所有路径相对仓库根。

## 第一步：日期窗口与幂等

```bash
TZ=Asia/Shanghai
WEEK_END=$(TZ=Asia/Shanghai date -v-1d +%Y-%m-%d)         # 周日（昨天）
WEEK_START=$(TZ=Asia/Shanghai date -v-7d +%Y-%m-%d)        # 上周一
ISO_WEEK=$(TZ=Asia/Shanghai date +%G-W%V)                   # 如 2026-W19
WEEK_FILE="周精选/${ISO_WEEK}.md"
mkdir -p 周精选
```

如果 `${WEEK_FILE}` 已存在 → 输出"已生成，跳过"并结束。

## 第二步：扫描日报 entries

用 Python 读取上周 7 天的所有日报文件 frontmatter 的 entries 数组：

```python
import yaml, glob, json, os, re
from datetime import datetime, timedelta
from collections import Counter, defaultdict

WEEK_START = "{WEEK_START}"
WEEK_END = "{WEEK_END}"

start = datetime.fromisoformat(WEEK_START)
end = datetime.fromisoformat(WEEK_END)

all_entries = []
date_files = []
for f in sorted(glob.glob("*.md")):
    if not re.match(r"\d{4}-\d{2}-\d{2}\.md$", f): continue
    fdate = f[:10]
    fd = datetime.fromisoformat(fdate)
    if not (start <= fd <= end): continue
    date_files.append(fdate)
    text = open(f).read()
    if not text.startswith("---"): continue
    parts = text.split("---", 2)
    fm = yaml.safe_load(parts[1])
    if not fm: continue
    entries = fm.get("entries", []) or []
    for e in entries:
        e["_date"] = fdate
        all_entries.append(e)

print(f"扫描 {len(date_files)} 份日报，共 {len(all_entries)} 条 entries")
```

## 第三步：去重

按 id 去重，保留最早出现的 _date：

```python
unique = {}
for e in all_entries:
    eid = e.get("id","")
    if eid and eid not in unique:
        unique[eid] = e
all_entries = list(unique.values())
```

## 第四步：按主题聚类

```python
by_theme = defaultdict(list)
theme_count = Counter()
for e in all_entries:
    for t in e.get("themes", []):
        by_theme[t].append(e)
        theme_count[t] += 1
```

## 第五步：挑周 Top 20

排序权重：
- `is_top: true`（曾被日报选为 Top 8）：+10
- `rel == "🟢"`：+3
- 关键机构/期刊（Nature/NEJM/Lancet/MICCAI/ICLR/NeurIPS/Stanford/MIT/DeepMind 等）：+2
- 真实临床数据（关键词：RCT, FDA, real-world, registry, multicenter, cohort）：+2

挑前 20，标 `weekly_rank`。尽量平衡多主题分布。

## 第六步：写周精选文件

`周精选/{ISO_WEEK}.md` 的 frontmatter：

```yaml
---
type: weekly-digest
iso_week: {ISO_WEEK}
date_start: {WEEK_START}
date_end: {WEEK_END}
total_entries: {N}
top_count: 20
tags: [医-AI前沿, 周精选]
themes_summary:
  RAG: 12
  Agent: 18
  ...
top_entries:
  - rank: 1
    id: "..."
    title_zh: "..."
    title_en: "..."
    inst: "..."
    summary: "..."
    themes: ["...", "..."]
    rel: "🟢"
    link: "..."
    source_date: "{YYYY-MM-DD}"
  ...（20 条）
---
```

正文（markdown）结构：

```markdown
# 医-AI 周精选 · {ISO_WEEK}

> 时间窗：{WEEK_START} ~ {WEEK_END}
> 本周日报 N 份，去重后 entries M 条，⭐ Top 20 已挑选

## 主题热度

| 主题 | 条目数 | 占比 |
|---|:---:|:---:|

## ⭐ 本周 Top 20

| # | 标题(中) | 机构 | 主题 | 一句话 | 日期 | 链接 |
|:---:|---|---|---|---|:---:|---|

---

## 📂 按主题聚类

### {主题名}（{n} 条）

| 标题 | 机构 | 一句话 | 日期 | 链接 |
|---|---|---|:---:|---|

（重复每个主题）

---

[[医-AI前沿追踪 MOC|← 返回 MOC]]
```

## 第七步：更新 MOC

在 `医-AI前沿追踪 MOC.md` 里：
1. 如果没有 `## 📅 周精选索引` 区，在 `## ⭐ 收藏池` 后面插入
2. 追加一行：`| {ISO_WEEK} | {WEEK_START} ~ {WEEK_END} | {N} | [[周精选/{ISO_WEEK}\|查看]] |`

## 第八步：commit + push

```bash
git add -A
git commit -m "weekly: ${ISO_WEEK} 周精选 (${WEEK_START} ~ ${WEEK_END})"
if git push origin HEAD:main; then
  echo "✅ 直推 main 成功"
else
  git push origin "HEAD:claude/weekly-${ISO_WEEK}"
fi
```

## 第九步：完成报告

```
✅ 周精选 ${ISO_WEEK}
- 时间窗：${WEEK_START} ~ ${WEEK_END}
- 扫描日报：N 份
- 去重后 entries：M
- Top 20：已挑选
- 主题分布（前 5）：...
- 写入：${WEEK_FILE}
- MOC 已更新
- push：main / fallback
```

## 全局约束

- 仅读 frontmatter 的 entries 字段，不解析 markdown 表格
- 缺 entries 字段的日报跳过且记录
- 路径相对仓库根
- 单文件失败不阻塞整体

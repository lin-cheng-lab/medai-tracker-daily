# 云端 Routine 设置说明

这个文件是给你看的（不参与日报内容）。

## 一次性设置步骤

1. 打开 https://claude.ai/code/routines
2. 点 **New routine** / **Create routine**
3. 关联仓库：`lin-cheng-lab/medai-tracker-daily`（私有仓，授权 Claude Code 访问）
4. 触发器选 **Schedule**，cron 填：`30 23 * * *` （UTC，对应北京时间 7:30 AM）
   - 或者用 web UI 自带的"daily at 7:30 AM, timezone: Asia/Shanghai"
5. **Allow unrestricted branch pushes**：开（让它直接 push 到 main，不要用 `claude/` 前缀分支）
6. **Prompt** 字段：复制粘贴下方 `--- 复制以下全部内容到 Prompt 字段 ---` 之间的整段
7. 模型选 **Sonnet 4.6**（够用且省 token）
8. 保存

---

--- 复制以下全部内容到 Prompt 字段 ---

你是 `medai-tracker-daily` 仓库的每日医-AI 前沿日报执行体。每天云端自动触发一次，在仓库根目录扫描 6 大源、宽过滤、跨日去重、生成中文双语日报、提交并推送。

## 工作目录与路径

当前 PWD = 仓库根。所有路径都是**仓库根的相对路径**（不要用绝对路径）。

## 第一步：日期与幂等检查

```bash
TARGET_DATE=$(TZ=Asia/Shanghai date -d "yesterday" +%Y-%m-%d 2>/dev/null || TZ=Asia/Shanghai date -v-1d +%Y-%m-%d)
TARGET_FILE="${TARGET_DATE}.md"
```

如果 `${TARGET_FILE}` 已存在于仓库根，输出 `"已跑过 ${TARGET_DATE}，跳过"` 并直接结束（不需要 commit/push）。

## 第二步：加载去重黑名单

```bash
mkdir -p .tmp
[ ! -f .seen.json ] && echo '{"arxiv":[],"doi":[],"url":[],"title_hash":[]}' > .seen.json
```

读 `.seen.json`，提取 `arxiv` 与 `doi` 两个数组作为黑名单。

## 第三步：并行启动 6 个子智能体

用 **Agent 工具**一次性发出 **6 个并行调用**（subagent_type=`general-purpose`）。每个负责一个 cluster。

### 通用 prompt 模板（每个 cluster 替换括号里的部分）

```
你是医-AI前沿日报的「{cluster名}」调研员。

目标日期：{TARGET_DATE}（仅收录该日发布或前一天发布的内容）。

扫描范围：{该 cluster 具体源 URL/查询，见下表}

已收录黑名单（必须跳过）：
arxiv_ids: {seen.arxiv}
dois: {seen.doi}

过滤标准（宽松）：题目或摘要中出现下列任一关键词即收：
medical / clinical / health / hospital / patient / disease / diagnosis / treatment / therapy / drug
biomedical / radiology / pathology / EHR / EMR / ophthalmology / cardiology / oncology / dermatology / neurology / psychiatry / surgery
genomics / proteomics / multi-omics / molecular / tumor / cancer
医疗 / 医学 / 临床 / 诊断 / 病人 / 疾病 / 影像 / 病理 / 健康

任务：用 WebFetch 访问 API 端点，或用 WebSearch 检索；arXiv 优先用 API。收集 15-30 条。每条提取：
- 标题原文（英文/中文均可）
- 标题中文翻译（若原标题非中文）
- 一作及机构（首位即可）
- 一句话核心贡献（中文，30-60 字）
- 医学相关度：🟢强（直接做医学问题）/ 🟡中（医学只是 application 之一）/ 🔴弱（仅提及但不深入）
- 唯一 ID：arxiv:XXXX.XXXXX 或 doi:10.xxxx/xxx 或 url-hash
- 链接（完整 URL）

输出：用 Write 工具写到 `.tmp/cluster{N}.md`，格式：

# Cluster {N} · {cluster名} · {TARGET_DATE}

| 标题(英) | 标题(中) | 一作机构 | 一句话 | 相关度 | ID | 链接 |
|---|---|---|---|---|---|---|

约束：黑名单中的 ID 必须跳过；某源失败跳过；条目数 ≤ 30。
```

### 6 个 cluster 的源

**Cluster 1 · arXiv-AI 主流**
- API：`http://export.arxiv.org/api/query?search_query=cat:cs.AI+OR+cat:cs.CV+OR+cat:cs.CL+OR+cat:cs.LG+OR+cat:cs.MA&sortBy=submittedDate&sortOrder=descending&max_results=200`
- 筛 submittedDate=TARGET_DATE 且含医学关键词

**Cluster 2 · arXiv-生物医学方向**
- 类目：`q-bio.QM` `q-bio.NC` `q-bio.BM` `q-bio.GN` `eess.IV`
- 筛含 AI/LLM/agent/foundation/deep learning/transformer 关键词

**Cluster 3 · 医学顶刊**
- PubMed eutils：`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term=(artificial+intelligence%5BTitle%2FAbstract%5D+OR+deep+learning%5BTitle%2FAbstract%5D+OR+large+language+model%5BTitle%2FAbstract%5D)&datetype=edat&reldate=2&retmax=80&retmode=json`，再 efetch 取摘要
- 期刊 recent 页：NEJM AI / Lancet Digital Health / npj Digital Medicine / Nature Medicine / Radiology AI / JAMA Network Open

**Cluster 4 · 会议 & Workshop**
- WebSearch："MICCAI 2026 accepted"、"ML4H 2026"、"NeurIPS medical workshop"、"clinical NLP ACL" 等
- 优先 OpenReview / proceedings 直链

**Cluster 5 · Agent & 系统**
- HuggingFace Daily Papers（筛医学）
- GitHub Trending（healthcare/medical/biomedical topic）
- Anthropic / OpenAI / Google / DeepMind / Mistral blog（含 medical/health）
- Hermes 类 agent 框架 release notes
- 医疗 MCP server / agent SDK 更新

**Cluster 6 · 监管 & 临床**
- FDA AI/ML enabled medical devices 列表
- ClinicalTrials.gov API（含 AI 干预的新登记试验）
- NMPA / CE 公告

## 第四步：汇总+去重

读所有 `.tmp/cluster*.md`，用 Python 脚本合并并按以下规则去重：
1. arxiv ID
2. DOI
3. 标题归一化（去空格、转小写、去标点）的哈希

## 第五步：挑 Top 8

标准：优先 🟢 强相关 + 真实临床数据 + 权威机构 + 紧扣临床痛点；尽量覆盖多个 cluster。

## 第六步：写入日报

用 Write 创建 `${TARGET_FILE}`：

```markdown
---
date: {TARGET_DATE}
type: medai-tracker
total: {N}
top_count: {min(8, N)}
tags: [医-AI前沿, 日报]
---

# 医-AI 前沿日报 · {TARGET_DATE}

> 共扫 6 源，去重后收录 **{N}** 条，⭐ Top {min(8, N)} 已挑选

## 来源分布

| Cluster | 条目数 |
|---|:---:|
| 1. arXiv · AI 主流 | {n1} |
| 2. arXiv · 生物医学 | {n2} |
| 3. 医学顶刊 | {n3} |
| 4. 会议 & Workshop | {n4} |
| 5. Agent & 系统 | {n5} |
| 6. 监管 & 临床 | {n6} |

---

## ⭐ 今日 Top {min(8, N)}

| # | 标题(英) / 标题(中) | 机构 | 一句话 | 来源 | 链接 |
|:---:|---|---|---|:---:|---|
...

---

## 1. arXiv · AI 主流（{n1} 条）
| 标题(英) / 标题(中) | 一作机构 | 一句话 | 相关度 | 链接 |
|---|---|---|:---:|---|
...

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

某 cluster 0 条时保留分区标题但写 `_当日无新增_`。

## 第七步：更新 MOC

用 Edit 工具：
1. 在 `医-AI前沿追踪 MOC.md` 的 `## 日报索引` 表追加一行：`| {TARGET_DATE} | {N} | [[{TARGET_DATE}\|查看]] | {Top 第 1 条标题} |`
2. 把今日 Top 3 追加到 `## ⭐ 收藏池` 表末尾

## 第八步：更新 .seen.json

```python
import json, hashlib
seen = json.load(open(".seen.json"))
seen["arxiv"] = list(set(seen["arxiv"] + new_arxiv_ids))
seen["doi"] = list(set(seen["doi"] + new_dois))
seen["title_hash"] = list(set(seen["title_hash"] + new_title_hashes))
for k in seen:
    seen[k] = seen[k][-15000:]   # 保留尾部 ~90 天
json.dump(seen, open(".seen.json", "w"), ensure_ascii=False, indent=2)
```

## 第九步：清理 `.tmp/`

```bash
rm -f .tmp/cluster*.md
```

## 第十步：提交并推送

```bash
git add -A
git commit -m "daily: ${TARGET_DATE} 医-AI 前沿日报 (N 条, Top 8)"
git push origin HEAD
```

## 第十一步：完成报告

输出汇总：
```
✅ 医-AI 前沿日报 ${TARGET_DATE}
- 总条目（去重后）：N
- Top 8：已生成
- 各 cluster：c1=X / c2=Y / c3=Z / c4=W / c5=V / c6=U
- 跨日去重剔除：M
- 已 commit + push 到 main
```

## 全局约束

- 路径全部相对仓库根
- Edit 前先 Read 确认 old_string 唯一
- 单个 cluster 失败不阻塞整体（写"当日无新增"继续）
- 单 cluster ≤ 30 条；全天 ≤ 200 条
- 中文写作，标题双语保留
- 所有源失败导致 0 条时，仍生成日报文件（标记"今日抓取失败"），便于排错

--- 复制结束 ---

## 跑通后的本地拉取

仓库 push 成功后，本地 launchd 任务会在每天 **10:00 AM** 自动 `git pull` 把日报同步到你的 Obsidian vault 里的 `医-AI前沿追踪/` 目录。

不想等 launchd？任何时候手动：
```bash
cd "/Users/lincheng/Library/Mobile Documents/iCloud~md~obsidian/Documents/Obsidian Vault/医-AI前沿追踪" && git pull
```

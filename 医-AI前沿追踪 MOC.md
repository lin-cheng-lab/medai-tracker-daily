---
tags: [医-AI前沿, MOC]
type: tracker-moc
---

# 医-AI 前沿追踪 MOC

> **每日自动**追踪医学 × AI 交叉前沿。
> 由 `medai-tracker` skill + Claude Code daily routine 驱动，每天清晨 7:30 自动跑一次，抓取**昨日**新发布的论文、会议、Agent 框架、监管动态，跨日去重后写入日报。

> [!tip] 快捷入口
> - 🌡️ [[00-规划中心/主题热度总览|22 主题热度排行]]（看哪些方向最热）
> - 🗺️ [[00-规划中心/医-AI 知识体系使用指南|体系使用指南]]
> - 📚 [[00-规划中心/前沿主题词典|主题词典 v1.0]]
> - 🧩 [[00-规划中心/概念图谱/概念图谱索引|20 个核心概念页]]

---

## 🎯 设计目标

**问题**：医学 ↔ AI 严重割裂——
- AI 圈在 arXiv 等平台发的医学相关论文常常"自嗨"（缺真实临床数据 / 缺医学方法论）
- PubMed 等传统医学平台 AI 研究质量参差
- Hermes 等 Agent 框架进化飞快，但医疗落地散落各处

**对策**：每日自动广撒网 + 宽过滤，把 6 大类来源的"医学+AI"内容统一收口、去重、产生日报，长期累积形成**医-AI 桥接知识池**，攒够了直接喂 `new-phase` skill 启动新一期学习。

---

## 📡 来源覆盖（6 大 Cluster）

| # | Cluster | 主要来源 |
|:---:|---|---|
| 1 | **arXiv · AI 主流** | cs.AI / cs.CV / cs.CL / cs.LG / cs.MA + 医学关键词命中 |
| 2 | **arXiv · 生物医学方向** | q-bio.QM / q-bio.NC / q-bio.BM / q-bio.GN / eess.IV |
| 3 | **医学顶刊** | PubMed / NEJM AI / Lancet Digital Health / Nature Medicine / npj Digital Medicine / JAMA Network Open / Radiology AI |
| 4 | **会议 & Workshop** | MICCAI / ISBI / ML4H / MLHC / NeurIPS / ICML / ICLR / CVPR / AAAI 的 medical track |
| 5 | **Agent & 系统** | HuggingFace Papers / GitHub Trending / Anthropic / OpenAI / Google / DeepMind / Mistral blog / Hermes 类 agent 框架 |
| 6 | **监管 & 临床** | FDA AI/ML 医疗器械 / ClinicalTrials.gov / NMPA / CE |

---

## 📅 日报索引

| 日期 | 收录数 | 链接 | 今日头条 |
|:---:|:---:|:---:|---|
| 2026-05-05 | 91 | [[2026-05-05\|查看]] | MASAI RCT：AI辅助乳腺X线筛查灵敏度提升6.7%（Lancet，>10.5万女性） |
| 2026-05-06 | 83 | [[2026-05-06\|查看]] | SPARK Agent病理AI（Nature Medicine）：跨18队列>5400例自主生成并验证肿瘤生物标志物 |

---

## ⭐ 收藏池（累积 Top 推荐）

> 每日 Top 3 自动累积到此，攒到一定数量可触发 `new-phase` 启动新一期专题学习。

| 日期 | 标题(中/英) | 机构 | 一句话 | 链接 |
|:---:|---|---|---|---|
| 2026-05-05 | MASAI RCT：AI辅助乳腺X线筛查与标准双读对比 / MASAI study | Lund University | >10.5万女性RCT证实AI辅助筛查灵敏度提升6.7%，Lancet发表，乳腺癌AI筛查最高级别循证证据。 | [链接](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(25)02464-X/abstract) |
| 2026-05-05 | SPARK：癌症病理学自主科学发现智能体框架 / Agentic framework for autonomous cancer pathology discovery | Univ. Hospital Cologne | 跨18队列5种癌症类型自主生成并验证组织生物标志物，Nature Medicine，开创病理AI自主科研新范式。 | [链接](https://www.nature.com/articles/s41591-026-04357-y) |
| 2026-05-05 | 谷歌DeepMind AI协诊员 / Google DeepMind AI Co-clinician | Google DeepMind | 「规划器+对话器」双Agent架构，98次主诊零严重错误，在140个评估维度持平或超越执业医师水平。 | [链接](https://deepmind.google/blog/ai-co-clinician/) |
| 2026-05-06 | SPARK：自主病理Agent AI / Autonomous pathology research using agentic AI | University Hospital Cologne | SPARK系统跨18队列>5400例自主生成生物学假设并验证肿瘤生物标志物，Nature Medicine，开创病理AI自主科研新范式。 | [链接](https://doi.org/10.1038/s41591-026-04403-9) |
| 2026-05-06 | 临床LLM安全与准确度遵循不同扩展律 / Safety and accuracy scaling laws in clinical LLMs | Friedrich-Alexander-Universität | SaFE-Scale框架+RadSaFE-200基准：高质量证据将准确率从73.5%提升至94.1%，高危错误从12%降至2.6%。 | [链接](https://arxiv.org/abs/2605.04039) |
| 2026-05-06 | DeepMind AI联合临床医生计划 / Google DeepMind AI Co-Clinician Initiative | Google DeepMind | 基于Gemini+Astra多模态远程医疗辅助，98项真实查询零重大错误，68/140评估维度达到或超越全科医生水平。 | [链接](https://deepmind.google/blog/ai-co-clinician/) |

---

## ⚙️ 触发与运维

### 自动触发（默认）

每日 **7:30 AM 北京时间**，由 daily routine 自动跑：
- 抓取**昨日**（北京时间）新发布的内容
- 占用 **1 次** Claude Code daily routine 额度
- 内部并行 6 个 background subagent，独立扫源
- 整体耗时通常 5-15 分钟

### 手动触发

在 Claude Code 中说：
- "跑一次医-AI前沿"
- "前沿日报"
- "调用 medai-tracker"

或直接 `/medai-tracker`。

### 幂等性

- 当日日报文件已存在 → 跳过，不重跑
- 跨日去重 → 已收录的论文/项目不会再次出现

### 调整 cron

需要改时间或暂停 → `/schedule list` 查看 → `/schedule update` 修改。

---

## 📂 目录结构

```text
医-AI前沿追踪/
├── 医-AI前沿追踪 MOC.md     ← 本文件
├── 2026-04-30.md             ← 日报（按数据日期命名）
├── 2026-05-01.md
├── ...
├── .seen.json                ← 去重表（不要手动编辑）
└── .tmp/                     ← 子智能体临时输出（每日清理）
```

---

## 🔗 相关

- [[眼科多智能体 MOC 四期|眼科多智能体（四期）]]
- [[多模态学习 MOC 二期|多模态学习（二期）]]

[[Welcome Back !!!|← 返回主页]]

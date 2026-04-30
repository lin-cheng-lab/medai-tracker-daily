---
tags: [医-AI前沿, MOC]
type: tracker-moc
---

# 医-AI 前沿追踪 MOC

> **每日自动**追踪医学 × AI 交叉前沿。
> 由 `medai-tracker` skill + Claude Code daily routine 驱动，每天清晨 7:30 自动跑一次，抓取**昨日**新发布的论文、会议、Agent 框架、监管动态，跨日去重后写入日报。

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
| _等待首次跑过后追加_ | | | |

---

## ⭐ 收藏池（累积 Top 推荐）

> 每日 Top 3 自动累积到此，攒到一定数量可触发 `new-phase` 启动新一期专题学习。

| 日期 | 标题(中/英) | 机构 | 一句话 | 链接 |
|:---:|---|---|---|---|
| _空_ | | | | |

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

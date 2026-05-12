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
| 2026-05-08 | 80 | [[2026-05-08\|查看]] | Xuanwu-NeuroAid：神经急诊专用LLM前瞻性433例，诊断准确率79.4%显著优于急诊医师65.4%（npj Digital Medicine） |
| 2026-05-09 | 81 | [[2026-05-09\|查看]] | LLM聊天机器人PreA促进诊疗转诊：2069例RCT证实专科问诊时长缩短28.7%（Nature Medicine） |
| 2026-05-10 | 49 | [[2026-05-10\|查看]] | 环境AI改善医疗从业者职业福祉：66人阶梯楔形RCT，工作耗竭感显著降低（NEJM AI） |
| 2026-05-11 | 38 | [[2026-05-11\|查看]] | APOL1高风险队列AI肾脏风险预测（Nature Medicine）+ AI眼科筛查RCT（NCT06877988，新加坡） |

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
| 2026-05-08 | 宣武神经急诊LLM Xuanwu-NeuroAid前瞻性评估 / Prospective evaluation of Xuanwu-NeuroAid | Xuanwu Hospital, Capital Medical University | 神经急诊专用LLM前瞻433例真实患者，诊断准确率79.4%显著超越急诊医师65.4%，npj Digital Medicine发表。 | [doi:10.1038/s41746-026-02644-z](https://doi.org/10.1038/s41746-026-02644-z) |
| 2026-05-08 | OphMAE：跨模态眼科基础模型 / OphMAE multi-imaging ophthalmology foundation model | Indiana University | 三维OCT与二维en face OCT协同训练，17项诊断任务AMROC最优，AMD AUC 96.9%。 | [arxiv:2605.02714](https://arxiv.org/abs/2605.02714) |
| 2026-05-08 | Hygieia：多模态罕见病诊断智能体 / Hygieia rare disease diagnosis agent | Yale School of Medicine | 融合表型、基因组与临床记录，诊断性能较医生提升12%-60%，实现罕见病精准诊断与风险基因优先排序。 | [arxiv:2605.06226](https://arxiv.org/abs/2605.06226) |
| 2026-05-09 | LLM聊天机器人PreA促进基层-专科诊疗转诊：随机对照试验 / LLM Chatbot (PreA) to Facilitate Primary-to-Specialist Care Transitions | 多中心（中国，24科室111名专科医生） | 2069例RCT证实LLM聊天机器人PreA使专科医生单次问诊时长缩短28.7%（3.14 vs 4.41分钟），患者与医生满意度均提升，Nature Medicine发表。 | [链接](https://www.nature.com/articles/s41591-025-04176-7) |
| 2026-05-09 | 环境AI医疗助手随机试验：DAX Copilot与Nabla对医生文档效率的影响 / Ambient AI Scribes in Clinical Practice: A Randomized Trial | 多机构（美国，238名门诊医生） | 238名门诊医生RCT：Nabla使每条记录书写时间减少约41秒（9.5%），两款AI助手均使职业倦怠评分改善约7%，NEJM AI发表。 | [链接](https://ai.nejm.org/doi/abs/10.1056/AIoa2501000) |
| 2026-05-09 | 生成式AI发现TNIK抑制剂Rentosertib治疗特发性肺纤维化：随机IIa期试验 / AI-Discovered Rentosertib for IPF: A Randomized Phase 2a Trial | Insilico Medicine / 多中心（中国21个中心） | 71例IPF患者RCT：AI设计的首个候选药物Rentosertib 60mg组FVC改善+98.4mL，发现至IIa期仅~18个月，成本约600万美元，Nature Medicine发表。 | [链接](https://www.nature.com/articles/s41591-025-03743-2) |
| 2026-05-10 | 环境AI改善医疗从业者职业福祉实用RCT / Ambient AI to Improve Health Practitioner Well-Being | University of Wisconsin | 66人24周阶梯楔形RCT：环境AI文档助手显著降低工作耗竭感和人际疏离，NEJM AI发表。 | [doi:10.1056/AIoa2500945](https://ai.nejm.org/doi/abs/10.1056/AIoa2500945) |
| 2026-05-10 | AI辅助私人诊所结直肠病变检测RCT / AI-assisted colorectal lesion detection in private practices | University Hospital Erlangen | 5中心933例RCT：EndoMind实时AI系统显著提升结直肠病变检测率，npj Digital Medicine发表。 | [doi:10.1038/s41746-026-02576-8](https://www.nature.com/articles/s41746-026-02576-8) |
| 2026-05-10 | Synapsis AI病历审查识别罕见病试验候选患者 / AI-Driven Chart Review for Rare Disease Trial Participants | Cleveland Clinic | LLM以96.2%准确率在1476份病历中识别ATTR-CM试验候选者，显著提升黑人患者入组比例。 | [链接](https://newsroom.clevelandclinic.org/2026/03/03/ai-driven-chart-review-accurately-identifies-potential-rare-disease-trial-participants-in-new-study) |
| 2026-05-11 | APOL1高风险基因型早期肾脏风险预测 / Early kidney risk prediction in APOL1 high-risk genotype carriers | Penn Medicine, Univ. of Pennsylvania | 大规模真实世界队列（851例）利用EHR数据构建AI肾脏风险预测模型，可在肾脏事件前5年预警，发表于Nature Medicine。 | [链接](https://www.nature.com/articles/s41591-026-04343-4) |
| 2026-05-11 | AI辅助社区视力损伤筛查双臂实用性RCT方案 / Community AI visual impairment screening RCT (NCT06877988) | JMIR Research Protocols / 新加坡 | 注册于新加坡的双臂实用性RCT，对比AI眼科筛查与标准护理流程对社区视力损伤检测的影响，是眼科AI首批前瞻性临床试验之一。 | [链接](https://www.researchprotocols.org/2026/1/e74164) |
| 2026-05-11 | WHO首发EU27国医疗AI现状报告 / WHO Europe first-ever AI in health report across EU member states | WHO/Europe | WHO欧洲区发布首份全面覆盖EU27成员国的医疗AI现状图景报告，涵盖政策框架、监管成熟度与落地差距，为全球治理协调提供权威基线。 | [链接](https://www.who.int/europe/news/item/20-04-2026-new-who-europe-report-provides-first-ever-snapshot-of-ai-in-health-care-across-european-union-member-states) |

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

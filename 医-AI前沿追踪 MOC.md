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
| 2026-05-12 | 35 | [[2026-05-12\|查看]] | AI素养培训医师暴露LLM错误建议诊断准确率下降14%（NEJM AI RCT）+ 机器学习预测脓毒症恶化轨迹47,936例 |
| 2026-05-13 | 38 | [[2026-05-13\|查看]] | MASAI RCT Lancet最终结果：AI辅助乳腺筛查减少12%间期癌（n=105,000+）+ PANORAMA AI超越放射科医生检测胰腺癌（n=3,440） |
| 2026-05-14 | 73 | [[2026-05-14\|查看]] | 对话式AI代理改善精神症状RCT（JAMA，n=995）+ OBSCORE肥胖风险预测（Nature Medicine，n=20万，Cambridge） |
| 2026-05-15 | 23 | [[2026-05-15\|查看]] | DT-Transformer：170万患者EHR预训练基础模型896病种轨迹预测（Harvard/BWH）+ Valar Labs膀胱癌AI获FDA突破性认定（2026-05-15） |
| 2026-05-16 | 33 | [[2026-05-16\|查看]] | 可解释XGBoost整合PET心肌灌注10参数多中心1664例冠心病诊断（npj Digital Medicine）+ Aidoc基础模型AI首次FDA清关可筛查14种急症 |
| 2026-05-17 | 27 | [[2026-05-17\|查看]] | 自主AI糖网筛查显著提升高危患者眼科就诊率（npj Digital Medicine，n=3,745）+ 谷歌乳腺癌AI多中心研究灵敏度超初读医师（Nature Cancer，n=125,239） |

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
| 2026-05-11 | WHO首发EU27国医疗AI现状报告 / WHO Europe first-ever AI in health report across EU member states | WHO/Europe | WHO欧洲区发布首份全面覆盖EU27成员国的医疗AI现状图景报告，涵盖政策框架、监管成熟度与落地差距，为全球治理协调提供权威基线。 | [链接](https://www.who.int/europe/news/item/20-04-2026-new-who-europe-report-provides-first-ever-snapshot-of-ai-in-health-care-across-enhagen-new-who-europe-report-provides-first-ever-snapshot-of-ai-in-health-care-across-european-union-member-states) |
| 2026-05-13 | MASAI试验最终结果（Lancet）：AI辅助乳腺X线筛查减少12%间期癌 / MASAI Trial Final Results | Lund University / Karolinska | RCT n=105,000+，AI辅助单读替代标准双读，间期癌减少12%，灵敏度80.5% vs 73.8%，Lancet发表，乳腺癌AI筛查最高级别循证证据。 | [链接](https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(25)02464-X/abstract) |
| 2026-05-13 | PANORAMA研究（Lancet Oncology）：AI在常规CT上检测胰腺癌优于放射科医生 / PANORAMA AI pancreatic cancer detection | Johns Hopkins / 多中心 | 国际多中心3440例配对研究，68名放射科医生参与盲测，AI系统检测PDAC准确性显著优于放射科医生平均水平。 | [链接](https://www.thelancet.com/journals/lanonc/article/PIIS1470-2045(25)00567-4/abstract) |
| 2026-05-13 | 欧盟AI全能法协议：医疗器械高风险AI合规期限延至2028年8月 / EU AI Omnibus: Medical Device High-Risk AI Deadline Extended | EMA/欧盟 | 2026年5月7日欧盟政治协议，医疗器械等受监管产品嵌入高风险AI系统合规期限从2026年8月延至2028年8月。 | [链接](https://www.consilium.europa.eu/en/press/press-releases/2026/05/07/artificial-intelligence-council-and-parliament-agree-to-simplify-and-streamline-rules/) |
| 2026-05-14 | 对话式AI代理改善精神症状及数字治疗联盟效能的随机临床试验 / AI Agent RCT for Mental Health Symptoms | Reichman University, Israel | 995名以色列大学生RCT，对话式AI平台在焦虑减轻和幸福感提升方面优于主动对照及等待名单组，JAMA Network Open发表，数字心理健康AI首个大型RCT证据。 | [链接](https://doi.org/10.1001/jamanetworkopen.2026.6713) |
| 2026-05-14 | OBSCORE：基于数据驱动的肥胖风险分层与减重干预高风险个体优先排序 / OBSCORE Obesity Risk Stratification | University of Cambridge / Karolinska Institutet | UK Biobank约20万成人数据，20个临床特征预测10年肥胖相关并发症风险并在外部队列验证，Nature Medicine双文发表。 | [链接](https://www.nature.com/articles/s41591-026-04353-2) |
| 2026-05-14 | 经AI素养培训的医生在LLM辅助诊断中的自动化偏见：随机临床试验 / AI Literacy Training Cannot Eliminate Automation Bias in LLM-Assisted Diagnosis | LUMS (Pakistan) + Partners | 44名医师RCT，AI素养培训不能消除LLM辅助诊断的自动化偏见，错误建议时诊断准确率下降，NEJM AI发表。 | [链接](https://ai.nejm.org/doi/abs/10.1056/AIoa2501001) |
| 2026-05-15 | DT-Transformer：真实世界EHR疾病轨迹预测基础模型 / DT-Transformer for Disease Trajectory Prediction | Brigham and Women's Hospital / Harvard Medical School | 170万患者、5710万条EHR记录预训练，896病种下一事件预测中位AUC 0.871，真实世界大规模临床AI基础模型。 | [链接](https://arxiv.org/abs/2605.14227) |
| 2026-05-15 | Valar Labs膀胱癌AI病理风险分层获FDA突破性认定 / FDA Breakthrough Device for Bladder Cancer AI Pathology | Valar Labs / FDA | 首款获FDA突破性认定的AI数字病理预后产品，分析常规H&E切片生成膀胱癌复发风险评估，于2026-05-15获认定。 | [链接](https://www.businesswire.com/news/home/20260515224660/en/Valar-Labs-Receives-FDA-Breakthrough-Device-Designation-for-Vesta-Bladder-Risk-Stratify-Dx) |
| 2026-05-15 | 多模态AMIE对话式诊断AI升级 / Multimodal AMIE Conversational Diagnostic AI | Google DeepMind / Google Research | 多模态AMIE整合Gemini 2.0 Flash与状态感知对话框架，远程问诊多模态推理在OSCE评估中29/32项优于全科医生，Nature Medicine。 | [链接](https://www.nature.com/articles/s41591-026-04371-0) |
| 2026-05-16 | 可解释AI多中心评估冠状动脉疾病诊断（PET生物标志物）/ Multicenter evaluation of interpretable AI for CAD | Brigham and Women's Hospital, Harvard Medical School | 整合PET心肌灌注10参数的可解释XGBoost在4中心1664例患者中提升阻塞性冠心病诊断准确率，npj Digital Medicine。 | [链接](https://www.nature.com/articles/s41746-026-02338-6) |
| 2026-05-16 | Aidoc基础模型AI获FDA清关：单次腹部CT筛查14种急症 / Aidoc CARE Foundation Model FDA Clearance | Aidoc / FDA | 首款综合基础模型AI获FDA清关，整合14个适应症单次CT分析，平均灵敏度97%、特异性98%，是医疗AI落地里程碑事件。 | [链接](https://www.prnewswire.com/news-releases/aidoc-secures-fda-clearance-for-healthcares-first-comprehensive-foundation-model-ai-302666640.html) |
| 2026-05-16 | RadThinking：面向放射科纵向临床推理的数据集 / RadThinking Dataset for Longitudinal Radiology Reasoning | Johns Hopkins University | 含20362例CT扫描、9131名患者的VQA数据集，三级推理难度（原子→单步→多步链），覆盖43种癌症类型的指南分级。 | [链接](https://arxiv.org/abs/2605.10761) |
| 2026-05-17 | 自主AI糖尿病视网膜病变筛查提升高危患者就诊率 / Autonomous AI-assisted DR screening improves referral | Johns Hopkins Medicine | 3,745例队列研究显示自主AI筛查后高危黑人患者眼科就诊率显著提升，验证了AI筛查的健康公平促进效应，npj Digital Medicine。 | [链接](https://www.nature.com/articles/s41746-026-02460-5) |
| 2026-05-17 | 谷歌乳腺癌AI筛查多中心研究：灵敏度超初读医师 / Google AI Mammography Multicenter Study | Google / NHS / Imperial | Nature Cancer 多中心研究（n=125,239），AI灵敏度0.541 vs 医师0.437，减少40%筛查工作量，每千名癌症检出率从7.54升至9.33。 | [链接](https://www.nature.com/articles/s43018-026-01127-0) |
| 2026-05-17 | VeriFact：EHR事实核查LLM生成临床文档 / VeriFact Clinical Document Fact-Checking | Stanford University | NEJM AI发表，13,070条陈述基准上RAG+LLM-as-Judge达92.7%一致率，超越人类临床医生核实能力。 | [链接](https://ai.nejm.org/doi/full/10.1056/AIdbp2500418) |

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

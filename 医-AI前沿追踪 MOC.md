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
| 2026-05-18 | 43 | [[2026-05-18\|查看]] | CLAiR视网膜AI：874例前瞻性多中心RCT证实心血管风险筛查灵敏度91.1%（ACC.26）+ 多智能体辅助轴性脊柱关节炎早期诊断（npj Digital Medicine） |
| 2026-05-19 | 36 | [[2026-05-19\|查看]] | AI心房颤动筛查超越年龄阈值（Stanford，npj Digital Medicine，5000万人群）+ 帕金森多模态生物标志物诊断策略（Nature Medicine，229例前瞻队列） |
| 2026-05-20 | 19 | [[2026-05-20\|查看]] | 视网膜成像多病种AI框架（Nature Medicine，n=107,730）+ FDA批准首款连续AI脓毒症监测系统（Bayesian Health，n=764,000）|
| 2026-05-21 | 35 | [[2026-05-21\|查看]] | iHealthScreen AI糖网RCT临床试验注册（ClinicalTrials）+ NMPA批准全球首款商业化有创BCI（神念医疗NEO）+ Cognita胸片生成式AI获FDA突破性认定 |
| 2026-05-22 | 20 | [[2026-05-22\|查看]] | LLM临床推理基准评测（NEJM AI，o3最高67.8%领先）+ 肾移植EHR-AI风险预测RCT（npj Digital Medicine，76例中性）+ 欧盟AI法案医疗器械延期至2028年 |

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
| 2026-05-18 | CLAiR视网膜AI心血管风险筛查RCT / CLAiR Retinal AI Cardiovascular Risk Screening | Toku / Stanford Health Care | 874例前瞻性多中心RCT证实AI分析视网膜图像识别高心血管风险灵敏度91.1%，已获FDA突破性器械认定，ACC.26发布。评分69。 | [链接](https://www.acc.org/About-ACC/Press-Releases/2026/03/30/16/17/With-Help-from-AI-Eye-Images-Offer-Window-into-Cardiovascular-Risk) |
| 2026-05-18 | 多智能体辅助轴性脊柱关节炎早期诊断 / Multi-agent Early Diagnosis of Axial Spondyloarthritis | Chinese PLA General Hospital | npj Digital Medicine多中心队列研究：多智能体AI显著缩短6.7年平均诊断延误，提升初级保健转诊准确性。评分64。 | [链接](https://www.nature.com/articles/s41746-026-02372-4) |
| 2026-05-18 | 多模态AI Agent眼科RCT注册（NCT07401459） / Multimodal AI Agent Ophthalmic RCT | Hong Kong Polytechnic University | ClinicalTrials.gov注册多中心随机对照试验，评估多模态AI Agent眼科临床决策支持效果，为眼科AI提供高质量循证证据。评分63。 | [链接](https://clinicaltrials.gov/study/NCT07401459) |
| 2026-05-19 | 超越年龄阈值：AI重塑心房颤动筛查策略 / Reimagining AF Screening Beyond Age-Based Thresholds Using AI | Stanford University | 分析超5000万人群数据，证明AI应用于手持单导联心电图可精准预测新发房颤，突破年龄限制的精准筛查新路径，npj Digital Medicine。评分71。 | [链接](https://www.nature.com/articles/s41746-026-02485-w) |
| 2026-05-19 | 多模态生物标志物策略提升帕金森病诊断精度 / Multimodal Biomarker Strategy for Neurodegenerative Parkinsonism | Toronto Western Hospital, Univ. of Toronto | 229例前瞻队列整合皮肤α-突触核蛋白、tau种子扩增及血清神经丝轻链，实现高灵敏度+高特异性分层诊断，Nature Medicine。评分69。 | [链接](https://www.nature.com/articles/s41591-026-04398-3) |
| 2026-05-19 | 球结膜视频深度学习无创血细胞计数（眼科×Oculomics） / Noninvasive Blood Count from Bulbar Conjunctiva Videos | Tel Aviv University / Sheba Medical Center | 通过球结膜血管视频深度学习实现无创血细胞计数，验证血液病患者可行性，开创眼部Oculomics新方向，npj Digital Medicine。评分61。 | [链接](https://www.nature.com/articles/s41746-026-02598-2) |
| 2026-05-21 | iHealthScreen AI糖网早诊关键性临床试验注册（眼科×影像，RCT） / iHealthScreen AI DR Critical Clinical Trial NCT07151001 | iHealthScreen Inc | ClinicalTrials.gov注册AI自动化系统早期诊断糖尿病视网膜病变的关键性临床试验，眼科AI落地最高证据级别。评分60。 | [链接](https://clinicaltrials.gov/study/NCT07151001) |
| 2026-05-21 | 中国NMPA批准全球首款商业化有创脑机接口医疗器械：神念医疗NEO系统 / NMPA Approves World's First Commercial Invasive BCI | Neuracle Medical Technology / Tsinghua University | 神念医疗（清华系）NEO有创BCI于2026年3月获NMPA批准，是全球首款商业化有创BCI医疗器械，里程碑监管事件。评分56。 | [链接](https://news.cgtn.com/news/2026-03-14/China-approves-world-s-first-invasive-BCI-medical-device-1Lv2lPRjay4/p.html) |
| 2026-05-21 | Mosaic Cognita胸片生成式AI模型获FDA突破性器械认定 / FDA Breakthrough Designation: Mosaic Cognita CXR Generative AI | Mosaic Clinical Technologies | 首个放射科生成式视觉语言模型获FDA突破性器械认定，标志生成式AI正式进入FDA医疗器械监管轨道。评分53。 | [链接](https://mosaicclinical.ai/news/2026/03/mosaic-clinical-technologies-announces-fda-breakthrough-device-designation-for-cognitas-generative-ai-model-for-radiology/) |
| 2026-05-22 | LLM临床推理SCT基准评测（NEJM AI）/ Assessment of LLMs in Clinical Reasoning via Script Concordance Test | Harvard Medical School | 采用SCT对10款主流LLM进行临床推理基准评测，o3以67.8%最高得分领先，揭示LLM临床推理与专科医生之间的显著差距。评分65。 | [链接](https://ai.nejm.org/doi/full/10.1056/AIdbp2500120) |
| 2026-05-22 | PRIMA-AI肾移植EHR-AI风险预测RCT（npj Digital Medicine）/ Randomized Trial of EHR AI Risk Prediction in Kidney Transplant | Charité - Universitätsmedizin Berlin | 首个评估EHR内置ML移植物丢失风险预测对共同决策影响的RCT（76例），结果中性，为临床AI落地提供重要反例证据。评分64。 | [链接](https://www.nature.com/articles/s41746-026-02757-5) |
| 2026-05-24 | 环境AI医疗记录员的临床实践随机试验 / Ambient AI Scribes in Clinical Practice: A Randomized Trial | University of California Los Angeles | UCLA门诊医师RCT：环境AI语音转文字系统显著降低文档负担与职业倦怠，不影响账单合规性，NEJM AI发表，为临床AI文档工具提供高质量实证。评分65。 | [链接](https://doi.org/10.1056/AIoa2501000) |
| 2026-05-24 | PREVENT与SCORE2心血管风险方程跨国640万人验证 / Multinational Validation of PREVENT and SCORE2 | 乔治全球健康研究所 | 44个观察性队列+18个随机试验共640万人数据，跨国验证两大心血管风险评分，判别力相近且在多地区表现良好，Nature Medicine。评分64。 | [链接](https://doi.org/10.1038/s41591-026-04437-z) |
| 2026-05-24 | 哈佛/BIDMC：OpenAI o1推理模型急诊诊断超越临床医生 / OpenAI o1 Outperforms Physicians at ER Diagnosis | Harvard Medical School / BIDMC | OpenAI o1推理模型在急诊患者诊断中超越医生表现并超过早期AI模型，Fortune报道称「已触及人类天花板」，临床诊断AI里程碑。评分62。 | [链接](https://fortune.com/2026/05/04/harvard-study-ai-outdiagnose-doctors-openai-o1-preview/) |
| 2026-05-22 | 肯尼亚新生儿LLM临床决策支持10个月真实世界评估 / Human-supervised LLM CDS in Kenya Newborn Care | Bungoma County Referral Hospital, Kenya | 低资源真实部署：人工监督LLM系统AIFYA管理550例新生儿，高采用率与强临床一致性，Frontiers in Digital Health首发。评分53。 | [链接](https://www.frontiersin.org/journals/digital-health/articles/10.3389/fdgth.2026.1832634/full) |
| 2026-05-27 | FDA授予Gene Solutions SPOT-MAS 10多癌种液体活检突破性器械认定 / FDA Breakthrough Device Designation for SPOT-MAS 10 | Gene Solutions / FDA | 基于机器学习分析cfDNA甲基化与片段组学，10癌种辅助筛查，已在10万余人真实世界应用，获FDA突破性器械认定。评分53。 | [链接](https://www.prnewswire.com/news-releases/fda-breakthrough-device-designation-marks-major-milestone-for-gene-solutions-spot-mas-10-multi-cancer-screening-test-302783420.html) |
| 2026-05-29 | 胰腺癌AI筛查队列研究 / Digitally enriching pancreatic cancer screening via EHR | Mayo Clinic | 18.3万例队列验证，诊断前1年AUROC 0.837，常规血液检测与临床病史驱动的无症状筛查新路径。评分63。 | [链接](https://arxiv.org/abs/2605.30275) |
| 2026-05-29 | 致病性胚系变异识别儿科癌症风险 / Pathogenic germline variants in pediatric cancer risk | 多机构 | Nature Medicine大规模基因组队列研究，确认儿科癌症易感基因胚系变异与肿瘤风险的循证关联。评分59。 | [链接](https://www.nature.com/articles/s41591-026-04451-1) |
| 2026-05-29 | Diagens AI AutoVision获全球首个NMPA三类AI染色体核型注册证 / World's First NMPA Class III AI Chromosome Karyotype | 杭州迪安诊断 | 全球首个基于大模型L3级染色体核型分析AI三类医疗器械注册证，覆盖产前诊断与辅助生殖场景。评分53。 | [链接](https://www.globenewswire.com/news-release/2026/05/27/3301744/0/en/World-s-First-Class-III-Approval-for-a-Breakthrough-Medical-Imaging-AI-Diagens-AI-AutoVision.html) |
| 2026-05-27 | EyeAgent：面向眼科多模态临床决策支持的智能体AI系统 / EyeAgent: Agentic AI for Ophthalmic Multi-modal Clinical Decision Support | 多所高校联合 | 首个眼科Agentic AI系统，以DeepSeek-V3为推理引擎，动态编排53种眼科工具与23种影像模态，诊断提升18.51%。评分41（眼科+5加权）。 | [链接](https://arxiv.org/abs/2511.09394) |
| 2026-05-27 | MorphoXAI全切片图像人机协同可解释框架 / MorphoXAI: Human-AI Collaborative XAI for Whole Slide Images | Mayo Clinic | 融合专家形态学标注，提供局部+全局可解释性，揭示深度学习全切片图像分类的决策依赖，npj Digital Medicine。评分37。 | [链接](https://www.nature.com/articles/s41746-026-02741-z) |
| 2026-05-30 | LLM认知层架构支持心理治疗RCT（CBT-Layer）/ A cognitive layer architecture to support LLM performance in psychotherapy | Unknown (Nature Medicine 2026) | 227名受试者双盲RCT，认知行为治疗关键能力全面优于独立LLM和人类治疗师，19,674条真实临床转录记录验证。评分73。 | [链接](https://www.nature.com/articles/s41591-026-04278-w) |
| 2026-05-31 | AI-TEW分层早期预警框架解决院内死亡率预测高误报率 / AI-powered tiered early warning for in-hospital mortality | Multi-center hospitals, China & US | 中美三家医院174,292次急诊就诊数据，AI-TEW两阶段框架显著降低假报警率同时保持AUROC 0.84-0.91，npj Digital Medicine。评分74。 | [链接](https://www.nature.com/articles/s41746-026-02522-8) |
| 2026-05-31 | Diagens AI AutoVision染色体核型软件获NMPA三类注册证 / World's First NMPA Class III Foundation Model AI Medical Device | Hangzhou Diagens Biotechnology | 基于iMedImage基础模型，1518例多中心临床试验数值异常灵敏度及特异度均达100%，全球首个L3级染色体核型分析AI三类医疗器械。评分59。 | [链接](https://www.manilatimes.net/2026/05/27/tmt-newswire/globenewswire/worlds-first-class-iii-approval-for-a-breakthrough-medical-imaging-ai-diagens-ai-autovision/2352440) |
| 2026-05-31 | AutoARDS基于CT的AI系统重症ARDS综合管理 / CT-based AI for quantitative ARDS management | Multiple medical centers, China | 常规胸部CT转化为定量平台，跨6中心6153例验证，实现ARDS诊断、进展、氧合、生理与预后的综合一站式评估，npj Digital Medicine。评分62。 | [链接](https://www.nature.com/articles/s41746-026-02648-9) |
| 2026-05-30 | PulmoFoundation：临床验证的全面肺部病理解读基础模型 / PulmoFoundation: A Clinically Validated Foundation Model for Comprehensive Pulmonary Pathology | Southern Medical University | 多中心队列验证，超越现有SOTA，首个支持多病理类型的大规模临床验证肺部基础模型。评分62。 | [链接](https://arxiv.org/abs/2605.25878) |
| 2026-05-30 | 可解释多任务视网膜影像揭示2型糖尿病微血管风险分层先导研究（眼科×Oculomics）/ Explainable Multitask Retinal Imaging for T2DM Microvascular Risk Stratification | Shenzhen University | 2719例多中心先导研究，可解释XAI视网膜微血管特征揭示代谢疾病系统性风险分层，眼科×Oculomics。评分59（眼科加权+5）。 | [链接](https://arxiv.org/abs/2605.24913) |
| 2026-06-03 | MedAgentBench v2：改进FHIR EHR环境下医疗LLM智能体设计 / MedAgentBench v2: Improving Medical LLM Agent Design in FHIR EHR Environments | MIT / Stanford | NEJM AI/PSB 2026发表，GPT-4.1+记忆模块达98%成功率，涵盖21科室100项EHR工作流任务，医疗Agent基准标杆。评分60。 | [链接](https://arxiv.org/abs/2501.14654) |
| 2026-06-03 | 肝癌数字病理量化资源：数据集、基准与工具 / A Digital Pathology Resource for Liver Cancer Quantification | Harvard Medical School | 开源肝癌数字病理分析资源，含配套数据集、性能基准与分析工具，推动病理组学可重复研究，arXiv。评分43。 | [链接](https://arxiv.org/abs/2604.22858) |
| 2026-06-03 | FDA医疗器械网络安全最终指南（2026年2月）/ FDA Final Cybersecurity Guidance for AI Medical Devices | U.S. FDA | 要求所有AI医疗器械提交SBOM、漏洞管理计划及安全开发证明，强化上市前网络安全审查，监管里程碑。评分42。 | [链接](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/cybersecurity-medical-devices-quality-management-system-considerations-and-content-premarket) |
| 2026-06-04 | CarDIA-AI RCT：AI辅助CCTA分流减少不必要冠状动脉造影 / CarDIA-AI RCT: CCTA + AI to Reduce Invasive Angiography | 加拿大双中心心脏病研究团队 | 加拿大双中心252例RCT，AI梯度提升模型预测冠状动脉阻塞性病变，以CCTA替代有创造影分流低风险患者，2026年预期发表结果。评分67。 | [链接](https://pmc.ncbi.nlm.nih.gov/articles/PMC12138305/) |
| 2026-06-05 | 产时胎心监护判读人机协作随机研究 / Randomised study of human machine collaboration for cardiotocography interpretation during labour | Institut Curie | 211名临床医生前瞻性随机多读者研究，AI辅助将新生儿酸血症预测成功率从54.0%提升至61.4%，npj Digital Medicine，评分74。 | [链接](https://www.nature.com/articles/s41746-026-02556-y) |
| 2026-06-06 | 自监督表征学习揭示高维磁心电图中可解释生理结构 / Self-supervised representation learning reveals explainable physiological structure in high-dimensional magnetocardiography | 未明（Dominik D. Kranz等） | MCG2Vec对比编码器在1732例64通道心磁图上学习可解释心脏生理特征，可检测冠脉病变/心衰/房颤，npj Digital Medicine，评分62。 | [链接](https://www.nature.com/articles/s41746-026-02819-8) |
| 2026-06-06 | 痴呆自动影像鉴别系统AIDD：区分阿尔茨海默病与路易体痴呆 / Automated Imaging Differentiation for Dementia (AIDD) | University of Florida | 扩散自由水成像+SVM，n=387回顾性队列及尸检确认病例，近乎完美准确率区分AD与路易体痴呆，Neurology Open Access，评分60。 | [链接](https://www.neurology.org/doi/10.1212/WN9.0000000000000093) |
| 2026-06-06 | FDA批准ArteraAI Breast：首款HR+/HER2-乳腺癌AI数字病理风险分层工具 / FDA Clears ArteraAI Breast: First AI Digital Pathology Risk Stratification for HR+/HER2- Breast Cancer | FDA | 首款FDA 510(k)批准的乳腺癌AI数字病理风险分层工具，利用组织病理图像+临床变量预测早期乳腺癌远处转移风险，监管里程碑，评分58。 | [链接](https://artera.ai/news/artera-receives-u-s-fda-clearance-for-arteraai-breast-expanding-its-ai-platform-to-breast-cancer) |
| 2026-06-08 | AI素养纵向中介医学生批判性思维与AI辅助诊断参与关系 / AI literacy mediates AI assisted diagnosis participation and critical thinking | 多机构（中国医学院校） | 372名医学生12个月纵向随访，AI辅助诊断参与度越高，AI素养与批判性思维显著提升，AI素养起完全中介作用，npj Digital Medicine。评分63。 | [链接](https://www.nature.com/articles/s41746-026-02521-9) |
| 2026-06-08 | RSC Bay Area全美首家落地FDA批准AI胚胎评估工具（Embryo Predict） / First U.S. Clinic to Deploy FDA-Cleared AI Embryo Assessment | RSC Bay Area / Alife Health | 全美首家将FDA批准AI胚胎评估工具投入IVF常规临床实践的诊所，标志AI辅助胚胎选择正式进入临床。评分48。 | [链接](https://www.prnewswire.com/news-releases/rsc-bay-area-is-first-in-the-nation-to-deploy-fda-cleared-ai-for-embryo-assessment-by-alife-health-pioneering-a-new-standard-in-ivf-care-302787801.html) |
| 2026-06-08 | 新模型旧风险：GPT-5中的人口统计学偏差与对抗性幻觉脆弱性 / New model, old risks: sociodemographic bias and adversarial hallucinations in GPT-5 | Tel Aviv University, Israel | 重新评估GPT-5在500例急诊科病例中跨32个社会人口学标签的决策偏差，对抗性幻觉率反而高于GPT-4o（65% vs 53%），npj Digital Medicine。评分44。 | [链接](https://www.nature.com/articles/s41746-026-02584-8) |
| 2026-06-09 | 宫颈细胞病理深度学习辅助阅片多中心随机交叉试验 / Deep learning-assisted vs manual reading in cervical cytopathology RCT | npj Digital Medicine | 1920例液基细胞学RCT，DL辅助显著提升非专家病理医师敏感性（85.7% vs 71.3%，p<0.001），超越5%优效性边界。评分76。 | [链接](https://www.nature.com/articles/s41746-026-02703-5) |
| 2026-06-09 | CarDIA-AI：AI优化冠心病CTA分诊减少不必要有创造影RCT / CarDIA-AI: CCTA + AI to Reduce Invasive Angiography | 加拿大双中心心脏病团队 | 252例择期冠状动脉造影患者1:1随机分组，AI梯度提升模型（42项预测因子）辅助CCTA分流，2026年预计发表最终结果。评分62。 | [链接](https://clinicaltrials.gov/study/NCT06648239) |
| 2026-06-09 | TytoCare获FDA De Novo首款AI鼓膜鼓胀分析软件 / TytoCare FDA De Novo: First AI-Powered Eardrum Analysis | TytoCare / FDA | 基于160万张耳部图像训练，AI自动检测急性中耳炎鼓膜鼓胀，通过De Novo建立新ENT图像分析监管分类，适用6月龄以上患者。评分53。 | [链接](https://www.tytocare.com/news-and-press/tytocare-secures-fda-de-novo-for-first-ai-powered-eardrum-analysis/) |
| 2026-06-05 | 审议式多智能体LLM提升眼科临床推理能力 / Deliberative Multi-Agent LLMs Improve Clinical Reasoning in Ophthalmology | McGill University | 四模型审议委员会100例眼科临床情景，旗舰级多智能体准确率达95.0%，优于所有单模型基线，ML4H 2026，评分60（眼科+5加权）。 | [链接](https://arxiv.org/abs/2603.21447) |
| 2026-06-05 | 飞利浦SmartSpeed Precise双AI MRI软件获FDA 510(k)批准 / Philips SmartSpeed Precise Dual AI MRI Software FDA Clearance | Royal Philips | 整合压缩感知加速、AI去噪与AI图像锐化三引擎获FDA批准，适用全系1.5T/3.0T MRI，图像清晰度提升80%，评分48。 | [链接](https://www.philips.com/a-w/about/news/archive/standard/news/articles/2025/philips-advances-mri-speed-and-precision-with-fda-510k-clearance-of-smartspeed-precise-dual-ai-software.html) |
| 2026-06-04 | 隐私保护联邦学习用于多中心脓毒症早期预测 / Federated Learning for Multi-Center Sepsis Early Prediction | China (tertiary hospitals) | 三家三甲医院648例脓毒症样本系统评估联邦学习，数据隐私保护同时提升跨中心预测性能。评分60。 | [链接](https://arxiv.org/abs/2606.04338) |
| 2026-06-04 | 可穿戴心电图年龄与心房颤动关联（npj Digital Medicine）/ Wearable ECG Age and Atrial Fibrillation | Korea University | PROPHECG-Age Single模型从可穿戴单导联心电图估算心电年龄，两独立穿戴队列验证心电年龄差与房颤显著相关，npj Digital Medicine。评分56。 | [链接](https://www.nature.com/articles/s41746-026-02344-8) |
| 2026-06-11 | 多中心骨髓涂片深度学习AML患者级诊断 / Patient-Level AML Diagnosis via Bone Marrow Smear Deep Learning | Unknown (multi-center China) | 六中心258例AML患者骨髓涂片，提出细胞→患者级深度学习诊断流水线，引入CBLC专家定义类别，开创多中心AML智能辅助诊断新范式，arXiv。评分60。 | [链接](https://arxiv.org/abs/2606.10735) |
| 2026-06-14 | ProViCNet：前列腺特异视觉基础模型MRI靶向活检辅助 / Enhancing Foundation Model Transfer for Prostate Cancer Detection with Patch-Level Contrastive Learning | Stanford University | MRI片级对比学习弱监督训练，4401名患者六队列AUROC 0.875–0.966超越放射科医生，联合PSA可显著减少不必要活检，npj Digital Medicine，评分75。 | [链接](https://www.nature.com/articles/s41746-026-02831-y) |
| 2026-06-14 | 脑膜瘤H&E染色深度学习分子分类与预后预测 / Deep Learning for H&E-Based Meningioma Molecular Classification and Outcome Prediction | Mayo Clinic | 仅凭H&E染色切片实现脑膜瘤分子亚型分类与复发风险预测，平衡准确率87–97%，可替代昂贵DNA甲基化检测，Lancet Digital Health，评分64。 | [链接](https://www.thelancet.com/journals/landig/article/PIIS2589-7500(26)00009-9/fulltext) |
| 2026-06-14 | MBD-Check：术前轻度出血障碍可解释ML决策支持工具 / MBD-Check: Interpretable ML for Preoperative Mild Bleeding Disorder Prediction | University of Bern (Inselspital) | 前瞻性诊断预测研究，外部验证灵敏度90.2%/AUROC 0.85，86位手术/麻醉/血液科医生可用性评估中位SUS 82.5，Lancet Digital Health，评分63。 | [链接](https://www.thelancet.com/journals/landig/article/PIIS2589-7500(26)00042-7/fulltext) |
| 2026-06-13 | 通用LLM全面超越专用临床AI工具 / General-purpose LLMs Outperform Specialized Clinical AI on Medical Benchmarks | NYU Langone Health | GPT-5.2/Gemini 3.1/Claude Opus 4.6在MedQA/HealthBench三项评测中全面超越OpenEvidence/UpToDate Expert AI等专用临床产品，12名临床医生盲评同样更偏好通用模型，Nature Medicine，评分55。 | [链接](https://www.nature.com/articles/s41591-026-04431-5) |
| 2026-06-13 | Aidoc CARE基础模型AI获FDA 510(k)清准：14种急症CT综合分诊 / Aidoc Foundation Model AI FDA Clearance for 14 Acute CT Conditions | Aidoc | 首个单一基础模型多适应症FDA清准，覆盖14种急性CT病症（新增11项），平均灵敏度97%/特异性98%，通过aiOS企业平台部署，是医疗AI落地里程碑，评分53。 | [链接](https://www.prnewswire.com/il/news-releases/aidoc-secures-fda-clearance-for-healthcares-first-comprehensive-foundation-model-ai-302666640.html) |
| 2026-06-13 | Perimeter Medical Claire获FDA PMA：首个术中乳腺癌切缘AI成像器械 / Perimeter Medical AI Claire FDA PMA for Intraoperative Breast Cancer Margin | Perimeter Medical Imaging AI | 宽视野OCT+AI融合的Claire获FDA PMA批准，美国首个用于保乳手术术中切缘实时评估AI器械，分辨率超超声/X光10倍，切缘准确率88.1%，获突破性器械资质，评分53。 | [链接](https://www.prnewswire.com/news-releases/perimeter-medical-imaging-ais-claire-becomes-first-fda-approved-ai-enabled-imaging-device-for-breast-cancer-surgery-302703103.html) |
| 2026-06-11 | Harvard EHR谱嵌入知识迁移 / Spectral EHR Embedding with Robust Knowledge Transfer | Harvard University | 针对罕见病小样本EHR无监督表示学习，两阶段谱嵌入融合广泛人群知识矩阵，放宽一对一信号对齐假设，在多发性硬化症CLIMB数据集验证，arXiv。评分53。 | [链接](https://arxiv.org/abs/2606.11570) |
| 2026-06-11 | AI辅助腹腔镜胆囊切除术安全性RCT / AI-Assisted Laparoscopic Cholecystectomy Safety RCT | University Health Network, Toronto | NCT07186803 RCT评估AI在腹腔镜胆囊切除术中实时安全性辅助效果，2026年6月30日完成，ClinicalTrials.gov注册，外科AI高质量循证证据。评分50。 | [链接](https://clinicaltrials.gov/study/NCT07186803) |
| 2026-06-18 | 智能手机AI自筛眼表恶性肿瘤非随机临床试验 / Smartphone-Based AI Self-Screening for Ocular Surface Malignancies | 中国多中心（JAMA Ophthalmology） | JAMA Ophthalmology前瞻性研究，AI驱动智能手机应用AUC=0.977（敏感性89.3%/特异性95.9%），6个月筛查逾20万人并发现20例恶性肿瘤，无一需眼球摘除，眼科AI落地最高级别证据。评分75。 | [链接](https://jamanetwork.com/journals/jamaophthalmology/fullarticle/2849884) |
| 2026-06-18 | AI-OCT系统用于糖尿病黄斑水肿筛查前瞻性非劣效RCT / AI-Based OCT System for Diabetic Macular Edema Detection RCT | 香港特别行政区研究机构 | JAMA发表的前瞻性非劣效RCT，AI-OCT辅助筛查使糖尿病黄斑水肿不必要转诊率从100%降至39.4%，敏感性不劣于标准筛查，眼科AI临床价值有力验证。评分74。 | [链接](https://jamanetwork.com/journals/jama/article-abstract/2850451) |
| 2026-06-18 | MIRA：首个自主完成临床全流程的医疗AI代理 / Towards autonomous medical artificial intelligence agents | 德国癌症研究中心（DKFZ） | Nature发表，MIRA是首个在沙盒EHR环境中自主完成问诊、实验室检查、鉴别诊断和治疗决策的AI代理，诊断准确率超越经验丰富的临床医生，自主医疗AI里程碑。评分58。 | [链接](https://www.nature.com/articles/s41586-026-10675-5) |
| 2026-06-19 | 血浆蛋白组学细胞衰老特征预测15年疾病风险 / Blood signatures of cell type-specific aging forecast disease risk and resilience | Stanford University | 60,542名受试者7,000+血浆蛋白ML模型估算40+细胞类型生物年龄，加速衰老特异性模式可预测15年内疾病发生率与死亡率，Nature Medicine，评分72。 | [链接](https://www.nature.com/articles/s41591-026-04447-x) |
| 2026-06-19 | 通用LLM全面超越专科临床AI工具（头对头评估）/ General-purpose chatbots outperform clinical AI tools | NYU Langone Health / Weill Cornell | GPT-5.2/Gemini 3.1 Pro/Claude Opus 4.6在医学知识、临床对齐及真实查询三维度均优于OpenEvidence/UpToDate Expert AI，Nature Medicine，评分55。 | [链接](https://www.nature.com/articles/s41591-026-04457-9) |
| 2026-06-19 | ARPA-H资助首个FDA授权心血管AI Agent（ADVOCATE计划）/ ARPA-H Funds First FDA-Authorized Cardiovascular AI Agent | ARPA-H / FDA | ARPA-H启动ADVOCATE计划，资助研发首个FDA授权的自主心血管AI Agent，24小时自动调整用药/排程/生活方式干预，与EHR和可穿戴设备实时集成，评分53。 | [链接](https://www.techtimes.com/articles/318089/20260609/arpa-h-funds-first-fda-authorized-ai-agent-manage-heart-care-around-clock.htm) |
| 2026-06-20 | BrainG3N：面向可控3D脑MRI生成的双用途分词器 / BrainG3N Dual-Purpose Tokenizer for 3D Brain MRI | Ghent University / Stanford University | 在35,309个脑MRI体积上预训练的体积掩码自编码器，解耦临床信息保留与解剖重建，23项线性探测任务21项超越专用基线，支持患者特异性纵向预测。评分55。 | [链接](https://arxiv.org/abs/2606.19651) |
| 2026-06-20 | RadGrounder：可扩展放射学空间定位视觉语言模型（MICCAI 2026）/ Scalable Spatially Grounded Radiology VLM | University of Freiburg | 提出RefRad2D含120万对德英双语CT/MR图像-文本对，无需人工标注训练RadGrounder，支持报告生成、VQA与空间定位，Slake/VQA-RAD基准与专科VLM相当。评分52。 | [链接](https://arxiv.org/abs/2606.20477) |
| 2026-06-20 | ACIE：单中心Agentic RAG临床信息抽取 / Configurable Clinical Information Extraction with Agentic RAG | University Medicine Essen | 埃森大学医院部署本地化Agentic RAG系统ACIE，跨数百份异构患者文档推理，经7,326次独立临床医师评判获96.5%接受率，每类型接受率80-99%。评分45。 | [链接](https://arxiv.org/abs/2606.19602) |
| 2026-06-22 | LLM辅助再分析未解决儿童罕见病提升诊断率 / LLM-Assisted Reanalysis of Unresolved Rare Disease Cases | Boston Children's Hospital / OpenAI | OpenAI o3辅助再分析376例经标准基因检测未解决儿童罕见病，额外确诊18例（4.8%），NEJM AI发表，评分76。 | [链接](https://ai.nejm.org/doi/abs/10.1056/AIcs2501343) |
| 2026-06-22 | AI增强诊断促成心脏移植首例病例报告 / First Case of AI-Assisted Diagnosis Leading to Heart Transplantation | Columbia University | AI-ECG分析识别隐匿性心脏疾病并提示心脏移植指征，Nature Medicine首例报告，标志AI诊断进入高风险临床决策领域，评分56。 | [链接](https://www.nature.com/articles/s41591-026-04454-y) |
| 2026-06-22 | EMA与FDA联合发布《良好AI实践原则》/ EMA-FDA Joint Principles for Good AI Practice | EMA / FDA | 首个跨大西洋监管机构联合AI实践原则，为药品与医疗器械领域AI系统开发、评估与监督设立国际共识标准，监管里程碑，评分55。 | [链接](https://www.ema.europa.eu/en/news/good-ai-practice) |
| 2026-05-23 | 30 | [[2026-05-23\|查看]] | 全量扫描30条新内容（含FlexiCT 266,227例CT通用基础模型 + 多Cluster综合） |
| 2026-05-24 | 19 | [[2026-05-24\|查看]] | 环境AI医疗记录员RCT（NEJM AI，UCLA）+ PREVENT/SCORE2 640万人心血管验证（Nature Medicine）+ OpenAI o1急诊超越医生（哈佛/BIDMC） |
| 2026-05-27 | 26 | [[2026-05-27\|查看]] | FDA授予SPOT-MAS 10多癌种液体活检突破性器械认定 + EyeAgent眼科53工具Agentic AI + MorphoXAI全切片可解释框架（Mayo，npj Digital Medicine） |
| 2026-05-29 | 27 | [[2026-05-29\|查看]] | Mayo Clinic胰腺癌18.3万例队列筛查预测（AUROC 0.837）+ Nature Medicine儿科胚系变异队列 + Diagens AI AutoVision全球首个NMPA三类染色体核型AI |
| 2026-05-30 | 47 | [[2026-05-30\|查看]] | LLM认知层RCT超越心理治疗师（Nature Medicine）+ PulmoFoundation临床验证肺部基础模型（arXiv）+ 视网膜多疾病可解释Oculomics先导研究（眼科加权） |
| 2026-05-31 | 19 | [[2026-05-31\|查看]] | AI-TEW分层早期预警框架降低院内死亡误报（npj Digital Medicine，n=174,292）+ Diagens NMPA三类全球首个基础模型AI医疗器械 + 飞利浦双AI MRI软件FDA 510k清关 |
| 2026-06-01 | 35 | [[2026-06-01\|查看]] | TARGET-AI：Yale/NEJM AI 15.9万人队列EHR+AI心电图靶向筛查26种心脏病（AUROC 0.90）+ 眼科ReasonAgent真实世界临床验证 + 神络医疗NEO BCI全球首款侵入式脑机接口NMPA批准 |
| 2026-06-02 | 60 | [[2026-06-02\|查看]] | ADLIFE数字工具箱RCT：npj Digital Medicine慢病数字干预 + Clarius EF AI 获FDA 510(k)批准 + EMA突破性器械试点启动 + PathAI AIM-MASH首款FDA认定AI药物研发工具 |
| 2026-06-03 | 33 | [[2026-06-03\|查看]] | MedAgentBench v2（MIT/Stanford，NEJM AI，评分60）：FHIR EHR医疗Agent基准更新 + FDA AI医疗器械网络安全最终指南 + 视网膜植入强化学习视觉恢复（眼科×Agent加权） |
| 2026-06-04 | 35 | [[2026-06-04\|查看]] | CarDIA-AI RCT（加拿大双中心，评分67）：AI辅助CCTA分流减少不必要冠状动脉造影 + 联邦学习多中心脓毒症早期预测 + FDA/CMS RAPID路径突破性AI器械最快2月纳入医保 |
| 2026-06-05 | 32 | [[2026-06-05\|查看]] | 产时胎心监护人机协作RCT（npj Digital Medicine，n=211，评分74）+ 眼科多智能体审议委员会准确率95%（ML4H，评分60）+ 飞利浦SmartSpeed Precise双AI MRI获FDA 510(k)（评分48） |
| 2026-06-06 | 27 | [[2026-06-06\|查看]] | MCG2Vec自监督心磁图AI（npj Digital Medicine，n=1732，评分62）+ AIDD痴呆影像鉴别系统（Neurology，n=387，评分60）+ FDA批准ArteraAI首款乳腺癌AI病理风险分层工具（评分58） |
| 2026-06-07 | 27 | [[2026-06-07\|查看]] | 飞利浦Verida获FDA 510(k)批准：全球首款AI驱动光谱CT系统（评分58）+ EyeDiff眼科生成式基础模型（npj Digital Medicine，评分45）+ Global RETFound Beta首个全球代表性视网膜FM（ARVO 2026，评分48） |
| 2026-06-08 | 22 | [[2026-06-08\|查看]] | AI素养纵向中介医学生批判性思维（npj Digital Medicine，n=372，评分63）+ RSC Bay Area全美首家落地FDA批准AI胚胎评估（评分48）+ GPT-5人口统计学偏差幻觉评测（npj Digital Medicine，评分44） |
| 2026-06-09 | 35 | [[2026-06-09\|查看]] | 宫颈细胞病理DL辅助多中心RCT（npj Digital Medicine，n=1920，评分76）+ CarDIA-AI冠心病CTA分诊RCT（n=252，评分62）+ TytoCare获FDA De Novo首款AI鼓膜分析软件（评分53） |
| 2026-06-11 | 40 | [[2026-06-11\|查看]] | 多中心骨髓涂片AML深度学习患者级诊断（arXiv，258例，评分60）+ Harvard EHR谱嵌入知识迁移（MS队列，评分53）+ AI辅助腹腔镜手术安全性RCT（NCT07186803，多伦多大学，评分50）|
| 2026-06-13 | 30 | [[2026-06-13\|查看]] | 通用LLM全面超越专用临床AI工具（Nature Medicine，MedQA/HealthBench三项评测，评分55）+ Aidoc基础模型AI获FDA清准14种急症CT分诊（评分53）+ Perimeter Claire乳腺癌术中切缘AI获FDA PMA（评分53） |
| 2026-06-14 | 33 | [[2026-06-14\|查看]] | ProViCNet前列腺癌MRI基础模型（Stanford，npj Digital Medicine，n=4401，评分75）+ 脑膜瘤H&E深度学习分子分类（Mayo Clinic，Lancet DH，评分64）+ MBD-Check术前出血障碍XAI工具前瞻验证（Lancet DH，评分63）|
| 2026-06-15 | 26 | [[2026-06-15\|查看]] | Coredio/PathAI/RecovryAI三款AI器械同日获FDA突破性认定（评分55）+ SegAnyPET全身PET通用分割FM（复旦，评分50）+ OpenAI o1急诊超越住院医生（Science，Harvard，评分45）|
| 2026-06-16 | 36 | [[2026-06-16\|查看]] | 眼科多模态推理Agent真实世界验证（68分，深圳眼科/暨南大学，Frontiers）+ Nature Cardiovascular眼科影像-心血管多组学大队列（61分，UK Biobank）+ SubtleHD CT FDA 510(k)获批（43分）|
| 2026-06-17 | 43 | [[2026-06-17\|查看]] | EPFL活动依赖自适应DBS改善帕金森病步态（Nature Medicine RCT，评分76）+ Stanford细胞衰老血浆蛋白组预测疾病（Nature Medicine，评分64）+ UPenn专家驱动生存机器多临床队列（评分56）|
| 2026-06-18 | 41 | [[2026-06-18\|查看]] | 智能手机AI自筛眼表恶性肿瘤（JAMA Ophthalmology，6个月20万人筛查，评分75）+ AI-OCT DME筛查前瞻性RCT（JAMA，香港，假阳性转诊降60%，评分74）+ MIRA首个自主医疗AI代理（Nature，DKFZ，评分58）|
| 2026-06-19 | 43 | [[2026-06-19\|查看]] | Stanford血浆蛋白组60,542人15年疾病预测（Nature Medicine，评分72）+ 通用LLM胜专科AI工具（Nature Medicine，评分55）+ ARPA-H资助首个FDA授权心血管AI Agent（评分53） |
| 2026-06-20 | 37 | [[2026-06-20\|查看]] | BrainG3N双用途分词器（Ghent/Stanford，35,309脑MRI，评分55）+ RadGrounder可扩展放射学VLM（Freiburg，MICCAI 2026，评分52）+ ACIE单中心Agentic RAG临床信息抽取（Essen，96.5%接受率，评分45） |
| 2026-06-21 | 31 | [[2026-06-21\|查看]] | ALERT-UWF RCT：AI辅助超广角视网膜紧急转诊分诊（厦门眼科，NCT07643129，评分60）+ 可穿戴ECG个性化房颤短期预测队列（arXiv，评分56）+ FDA首封AI警告信：生成式AI文件须人工审核（评分53） |
| 2026-06-22 | 27 | [[2026-06-22\|查看]] | LLM辅助再分析376例未解决儿童罕见病提升4.8%诊断率（NEJM AI，OpenAI o3，评分76）+ AI-ECG诊断促成心脏移植首例病例报告（Nature Medicine，评分56）+ EMA/FDA联合《良好AI实践原则》（评分55） |
| 2026-06-23 | 21 | [[2026-06-23\|查看]] | SmartAlert住院CBC复查智能减少RCT（Stanford/NEJM AI，n=9270，评分76）+ AIM-NASH AI临床试验终点FDA/EMA双认可里程碑（NEJM AI，评分66）+ 多国Swarm联邦学习腹腔镜阑尾切除术（NEJM AI，397例，评分63） |
| 2026-06-24 | 23 | [[2026-06-24\|查看]] | Eyenuk EyeArt获FDA追加批准多相机自主糖网筛查（眼科×FM，评分60）+ T2D随访MDP优化22154例队列（评分56）+ 美敦力Stealth AXiS获CE认证ENT手术系统（评分55） |

---

## 📅 周精选索引

| 周次 | 时间窗 | entries | 周精选 |
|:---:|---|:---:|---|
| 2026-W20 | 2026-05-11 ~ 2026-05-17 | 167 | [[周精选/2026-W20\|查看]] |
| 2026-W21 | 2026-05-18 ~ 2026-05-24 | 178 | [[周精选/2026-W21\|查看]] |
| 2026-W22 | 2026-05-25 ~ 2026-05-31 | 73 | [[周精选/2026-W22\|查看]] |
| 2026-W23 | 2026-06-01 ~ 2026-06-07 | 154 | [[周精选/2026-W23\|查看]] |
| 2026-W24 | 2026-06-08 ~ 2026-06-14 | 160 | [[周精选/2026-W24\|查看]] |
| 2026-W25 | 2026-06-15 ~ 2026-06-21 | 216 | [[周精选/2026-W25\|查看]] |

---

## 📅 月度精选索引

| 月份 | 时间窗 | entries | 月精选 |
|:---:|---|:---:|---|
| 2026-05 | 2026-05-01 ~ 2026-05-31 | 784 | [[月精选/2026-05\|查看]] |
| 2026-06-07 | 飞利浦Verida光谱CT获FDA 510(k)批准 / Philips Verida AI-Powered Spectral CT FDA Clearance | Royal Philips | 全球首款AI驱动第三代纳米面板双层探测器光谱CT系统获FDA 510(k)许可，实现常规扫描即全光谱成像，适用放射/心脏/肿瘤科，监管里程碑，评分58。 | [链接](https://www.usa.philips.com/a-w/about/news/archive/standard/news/press/2026/philips-receives-fda-510k-clearance-for-verida-the-worlds-first-ai-powered-detector-based-spectral-ct-advancing-diagnostic-precision-across-clinical-applications.html) |
| 2026-06-15 | Coredio心衰AI平台获FDA突破性认定（数字孪生+ML） / Coredio CPSE FDA Breakthrough Device | Coredio | 融合心血管物理数字孪生与AI，通过消费级智能手表实现等效心导管血流动力学评估，2026-05-28获FDA突破性认定，评分55。 | [链接](https://www.businesswire.com/news/home/20260528980762/en/FDA-Grants-Coredio-Breakthrough-Designation-for-AI-Platform-Bringing-Advanced-Heart-Failure-Assessment-Beyond-the-Hospital) |
| 2026-06-15 | PathAI PathAssist Derm获FDA突破性设备认定 / PathAI Dermatopathology AI FDA Breakthrough | PathAI | AI分析皮肤病变全切片图像辅助皮肤病理科医生诊断，解决阅片差异大问题，2026-03-03获FDA突破性认定，评分55。 | [链接](https://www.pathai.com/news/pathai-receives-u.s.-fda-breakthrough-device-designation-for-pathassist-derm-an-ai-powered-pathology-solution-to-transform-dermatopathology-workflow) |
| 2026-06-15 | OpenAI o1急诊诊断超越住院医师（Science发表）/ OpenAI o1 Outperforms Physicians at ER | Harvard Medical School / BIDMC | o1模型正确诊断率67%高于内科主治55%/50%，波士顿急诊室EHR真实病例验证，Science发表，评分45。 | [链接](https://www.science.org/doi/10.1126/science.adz4433) |
| 2026-06-07 | Global RETFound Beta：首个全球代表性视网膜基础模型 / Global RETFound Beta: First Globally Representative Retinal Foundation Model | Moorfields Eye Hospital / UCL | 203个合作伙伴、74个国家逾1亿张眼底照片训练，超越现有模型在眼科/系统性疾病检测、生物标志物提取和年龄预测，ARVO 2026发布，评分48（眼科+5加权）。 | [链接](https://www.ophthalmologytimes.com/view/arvo-2026-global-retfound-study) |
| 2026-06-07 | EyeDiff：文本驱动眼科影像生成式基础模型 / EyeDiff: Generative Foundation Model for Ophthalmic Image Synthesis | HK Polytechnic University | 提出EyeDiff，基于文本描述合成保留病灶的多模态眼科影像（42,048张/8数据集），通过少数类增强显著提升罕见眼病诊断准确率，npj Digital Medicine，评分45（眼科+5加权）。 | [链接](https://www.nature.com/articles/s41746-026-02560-2) |
| 2026-06-16 | 多模态推理Agent用于眼科决策增强：初步真实世界临床验证 / Multimodal Reasoning Agent for Ophthalmic Decision Enhancement | 深圳市眼科医院 / 暨南大学 | 结合多模态视觉分析、知识检索与诊断推理模块的ReasonAgent，在30例真实眼科病例（含3例罕见病）中治疗规划显著超越GPT-4o及眼科住院医，Frontiers in Cell and Developmental Biology发表，眼科专科AI首批真实世界临床验证证据。评分68（眼科+5加权）。 | [链接](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12325206/) |
| 2026-06-16 | 深度学习衍生表型的多组学分析揭示眼科影像与心脑血管特征的关联 / Multi-Omic Analysis of DL-Derived Ophthalmic Imaging Phenotypes | University of Manchester | 基于UK Biobank大队列，利用视网膜对抗自编码器将OCT与眼底照片编码为256维嵌入，多组学分析揭示眼科影像与心脑血管及神经系统特征的系统性关联，Nature Cardiovascular Research发表。评分61（眼科+5加权）。 | [链接](https://www.nature.com/articles/s44161-026-00815-5) |
| 2026-06-16 | 通过通才-专才协作实现医疗可泛化AI（GSCo/MedDr）/ Generalist-Specialist Collaboration for Medical AI | Shanghai AI Lab | GSCo框架将强大的通才基础模型MedDr与轻量级专才模型协同结合，在32个跨多模态医疗数据集的综合评估中超越现有最先进基础模型，显著提升下游任务迁移性能，Nature Biomedical Engineering发表。评分52。 | [链接](https://www.nature.com/articles/s41551-026-01653-3) |
| 2026-06-17 | 活动依赖自适应深部脑刺激改善帕金森病步态 / Activity-dependent adaptive DBS improves gait in Parkinson's disease | EPFL | RCT证实自适应DBS实时根据步态活动调整刺激参数，显著改善帕金森步态障碍并优于传统固定参数刺激，Nature Medicine。评分76。 | [链接](https://doi.org/10.1038/s41591-026-04432-4) |
| 2026-06-17 | 细胞衰老的血浆蛋白质组学特征预测人类疾病 / Plasma proteomic signatures of cellular aging predict human disease | Stanford University | ML分析大规模血浆蛋白质组数据建立衰老时钟模型，可预测多种年龄相关疾病风险，为早期疾病预测和干预提供新生物标志物体系，Nature Medicine。评分64。 | [链接](https://doi.org/10.1038/s41591-026-04446-y) |
| 2026-06-17 | 专家驱动生存机器：多临床队列的风险分层与可解释性提升 / Expert-Driven Survival Machines for Clinical Cohorts | University of Pennsylvania | AdaCSM混合专家增强自适应深度聚类生存框架，路由机制动态分配患者至专业化风险预测器，多临床队列验证个体化生存建模精度提升，arXiv。评分56。 | [链接](https://arxiv.org/abs/2606.14608) |
| 2026-06-21 | ALERT-UWF：AI辅助超广角视网膜图像病变紧急转诊分诊 / ALERT-UWF AI-Assisted Urgent Referral Triage of Ultra-Widefield Retinal Images | Xiamen Ophthalmology Center, Xiamen University | 前瞻性多阅读者RCT（NCT07643129），评估AI辅助超广角眼底图像紧急转诊分诊系统临床效用，眼科AI×RCT前沿。评分60（眼科+5加权）。 | [链接](https://clinicaltrials.gov/study/NCT07643129) |
| 2026-06-21 | 基于连续可穿戴ECG的个性化深度学习短期房颤预测 / Personalized Short-Term AF Prediction from Continuous Wearable ECG | Unknown (arXiv 2026) | 个性化LSTM/Transformer模型在大型可穿戴ECG数据集上通过AUROC 0.90+实现短期房颤预测，远超通用模型，推动可穿戴心脏AI个性化新范式。评分56。 | [链接](https://arxiv.org/abs/2606.10900) |
| 2026-06-21 | FDA发出首封AI相关警告信：AI生成GMP文件须人工审核 / FDA Issues First AI Warning Letter for Unreviewed AI-Generated Manufacturing Documents | FDA | 2026年4月FDA向同种疗法药物制造商发出首封涉AI警告信，确立"AI辅助、人工负责"原则，对医药AI监管具有重要先例意义。评分53。 | [链接](https://teledirectmd.com/health-guides/fda-first-ai-warning-letter-2026/) |
| 2026-06-23 | SmartAlert：ML驱动住院患者CBC不必要复查智能减少 / SmartAlert ML-Driven Clinical Decision Support for Lab Utilization | Stanford University School of Medicine | 8个急诊单元9270例住院患者RCT，ML-CDS预测稳定结果减少CBC复查，52小时内重复次数从1.82降至1.54（p<0.01），NEJM AI发表。评分76。 | [链接](https://ai.nejm.org/doi/full/10.1056/AIcs2501086) |
| 2026-06-23 | AIM-NASH：FDA与EMA联合认可首款AI病理数字工具作为NASH临床试验终点 / AIM-NASH FDA/EMA Dual Approval as AI-Enabled Clinical Trial Endpoint | Yale School of Medicine | 评述FDA与EMA首次联合认可AI病理工具为临床试验终点的里程碑意义，探讨AI辅助终点裁定对证据生成和监管框架的深远影响，NEJM AI发表。评分66。 | [链接](https://ai.nejm.org/doi/full/10.1056/AIe2600354) |
| 2026-06-23 | 隐私保护Swarm联邦学习腹腔镜阑尾切除术视频分析 / Privacy-Preserving Swarm Learning for Laparoscopic Appendectomy | TUD Dresden University of Technology | 6个国际外科中心397例腹腔镜阑尾切除术视频，去中心化弱监督深度学习+Swarm联邦学习预测病理分期，性能与集中式训练相当，NEJM AI发表。评分63。 | [链接](https://ai.nejm.org/doi/abs/10.1056/AIoa2501116) |
| 2026-06-24 | Eyenuk EyeArt眼底AI获FDA追加批准多相机自主糖网筛查 / Eyenuk EyeArt AI System FDA Multi-Camera Clearance | Eyenuk / FDA | EyeArt v2.2.0获FDA追加批准，支持Topcon NW400等多品牌相机，全球首家多相机FDA批准自主DR筛查AI，无需散瞳，眼科×FM里程碑。评分60。 | [链接](https://www.ophthalmologytimes.com/view/eyenuk-ceo-and-founder-gives-insight-into-fda-clearance-of-additional-camera-for-eyeart-ai) |
| 2026-06-24 | 基于马尔可夫决策过程的2型糖尿病随访间隔优化 / Context-Aware T2D Follow-Up Interval Optimization via MDP | University of Maryland | 构建上下文MDP模型，利用22154例T2D患者EHR数据，通过PCA聚类识别低/高风险亚群并定制最优随访间隔策略，临床决策支持大规模队列验证。评分56。 | [链接](https://arxiv.org/abs/2606.19092) |
| 2026-06-24 | 美敦力Stealth AXiS手术系统获CE认证（ENT扩展） / Medtronic Stealth AXiS Surgical System CE Mark for ENT | Medtronic | 全球首款将规划、导航与机器人技术合一的外科平台获CE认证覆盖耳鼻喉科，集成AI自动神经束成像与实时多模态影像导航，监管里程碑。评分55。 | [链接](https://news.medtronic.com/Medtronic-Receives-CE-Mark-for-Stealth-AXiS-TM-Surgical-System-for-Ear,-Nose,-and-Throat-Procedures) |

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

---
name: research-proposal-skill
description: >
  面向日本大学院申请的教授匹配型研究计划书 skill。用于：用户提供教授主页链接，
  希望先分析教授近年的研究方向与招生风险，再基于申请者背景生成 1 个可行研究题目、
  整理文献框架、确认 proposal 大纲，并最终输出 Markdown 格式研究计划书。写作阶段必须完整遵循本 skill 内置的结构、领域模板、风格与质量检查参考文件；非写作阶段遵循日本教授主页调研与题目匹配流程。适用于“研究计划书”“研究 proposal”“博士申请 proposal”“日本大学院申请研究计划”等场景。
---

# Research Proposal Skill for Japanese Graduate Admission

## Overview

使用本 skill 为日本大学院申请场景生成一套**从教授网页调研到最终研究计划书交付**的完整流程。先根据教授主页提取真实研究轨迹与招生风险，再结合申请者背景提出**恰好 1 个**可行题目，随后建立文献框架、确认 proposal 大纲，最后产出可继续编辑的 Markdown 研究计划书。

本 skill 的**写作阶段**必须完整继承 `research-proposal` 参考资料的作用，不得删减其核心写作要求、结构要求、领域适配要求、质量检查要求与输出约束。除写作阶段外，其余流程按日本教授申请场景组织执行。

## Input Contract

在开始之前，只补问缺失信息，不要一次性重复询问已给出的项目。输入与输出必须尽量贴合下表。

| 输入项 | 是否必需 | 作用 |
|---|---|---|
| 申请者姓名 | 建议提供 | 便于个性化描述与文档组织 |
| 当前院校 / 专业 / 年级或当前状态 | 必需 | 用于判断申请层级、研究训练基础与可行性 |
| 核心技能与经历优势 | 必需 | 决定题目与方法设计是否真实可行 |
| 教授主页链接 | 必需 | 作为教授研究情报提取与匹配判断的起点 |
| 输出语言（English 或 中文） | 必需 | 决定最终研究计划书的写作语言 |
| 目标字数 | 可选 | 默认约 3000 词，可按学校要求调整 |
| 已有论文 / PDF / 笔记 / 摘要 | 可选 | 可显著提升文献框架与论证质量 |
| 个人偏好的研究主题 | 可选 | 用于缩小题目搜索范围 |
| 学科领域（STEM / Humanities / Social Sciences） | 必需 | 用于调用对应结构与写作分支 |

如果用户一次提供多个教授主页链接，则默认复用同一份申请者背景；除非用户明确要求横向比较，否则按**一个教授一轮流程**执行，避免把不同教授的信息混写到同一份 proposal 中。

## Output Contract

输出不是单一一段文字，而是一组按顺序产出的中间结果与最终结果。必须按下表组织交互与交付。

| 输出层级 | 具体内容 | 是否面向最终用户 |
|---|---|---|
| 中间输出 1 | 教授研究方向、近期代表论文、研究轨迹、招生风险提示、关键信息来源链接 | 是 |
| 中间输出 2 | **1 个**建议研究题目，含匹配理由、研究空白、方法路径与可行性说明 | 是，且必须确认 |
| 中间输出 3 | 文献分类框架，至少覆盖 Background / Current State / Research Gap / Methodology 四类 | 视交互过程而定 |
| 中间输出 4 | Proposal 大纲，含章节结构与大致字数分配 | 是，且必须确认 |
| 最终输出 | Markdown 格式研究计划书 | 是 |

## Preconditions

在执行深度调研前，确保以下前提成立：

1. 可访问教授主页。
2. 用户已提供至少一个教授主页 URL。
3. 用户至少给出申请者当前背景与核心优势。
4. 输出语言与学科领域已明确。
5. 用户如有 PDF、笔记、论文列表或已选题方向，应在文献阶段纳入。

## Workflow

严格按以下顺序执行。除非用户明确要求跳过确认，否则**不得跳过题目确认**与**大纲确认**两个关口。

### Step 1: Gather Missing Inputs

先根据 **Input Contract** 检查用户是否已提供必需信息。仅补问缺失项。

优先确认以下信息：

1. 当前院校 / 专业 / 年级或当前状态。
2. 核心技能、项目经历、论文、方法能力、数据经验、实习或行业经验。
3. 教授主页链接。
4. 学科领域。
5. 输出语言。
6. 目标字数。
7. 可选材料与个人偏好主题。

如果用户主题描述过于模糊，则要求其补充研究兴趣边界，但不要在此阶段直接替用户写题目。

### Step 2: Deep Professor Intelligence Extraction

打开教授主页并主动深入点击相关页面，不要只停留在首页。重点查看但不限于以下栏目：Research、Publications、Profile、Projects、Members、News、Prospective Students、Contact。

处理日文页面时，识别常见栏目名：

- 研究内容 / 研究紹介
- 業績 / 発表論文
- メンバー
- 受験生へ / 入学希望の方へ
- 連絡先

执行以下检查与提取任务：

1. 先做**招生红线检查**。如果教授页面明确写明**不接收学生**、暂停招生或仅限校内名额，则立即告知用户，不要直接继续写研究计划书。只有当用户明确表示仍要做 speculative draft 时，才继续后续步骤。
2. 提取教授当前活跃研究方向，而不是只总结早年工作。
3. 提取至少 **2 篇**近期代表性论文，并记录**题目、发表 venue、年份**。
4. 提取可见的方法、数据集、应用场景、项目、合作、基金、实验室方向或招生偏好。
5. 为每条关键事实记录**准确来源 URL**。

绝不虚构论文、方向、实验室资源、数据集、项目、方法或来源链接。

完成后先给出**中间输出 1**：教授研究方向、近期论文、研究轨迹与招生风险提示。

### Step 3: Generate Exactly One Feasible Topic

将教授的近期研究轨迹与申请者背景进行交叉匹配，只生成**1 个具体且可行**的研究方向。该题目必须同时满足以下条件：

1. 与教授当前活跃方向一致，而非只对齐过时工作。
2. 能真实使用申请者已经具备的技能、经验或数据基础。
3. 研究范围足够聚焦，适合硕士或早期博士申请阶段。
4. 包含合理的研究空白与可执行的方法路径。
5. 不得依赖用户未具备、教授页面也未体现的关键条件。

输出**中间输出 2**时，必须同时说明：

- 题目名称
- 与教授方向的匹配点
- 与申请者优势的匹配点
- 核心研究问题
- 可行方法路径
- 为什么该题目适合当前申请阶段

然后等待用户确认。未经确认，不要进入大纲写作与全文写作。

### Step 4: Collect Literature and Build the Evidence Base

在用户确认题目后，读取 `references/LITERATURE_WORKFLOW.md`，并据此组织文献收集过程。

优先构建以下四类文献桶：

1. **Background**
2. **Current State**
3. **Research Gap**
4. **Methodology**

如有必要，可额外加入 **Related Work**。

文献来源优先级如下：

1. 用户提供的论文、PDF、摘要、笔记。
2. 高质量近期综述、系统综述、meta-analysis。
3. 领域中的基础文献与代表性研究。
4. 与方法路径直接相关的研究。

如果缺乏封闭获取文献，则明确告知局限，并优先使用开放可获取来源继续构建证据基础。不要因为文献不完美而跳过文献框架。

在此阶段输出**中间输出 3**：文献分类框架与代表性文献分组。

### Step 5: Generate the Proposal Outline

在起草大纲前，必须读取以下文件：

- `references/STRUCTURE_GUIDE.md`
- `references/DOMAIN_TEMPLATES.md`

根据用户确认后的题目、学科领域、目标字数与输出语言，生成结构化大纲。默认 proposal 结构通常包括：

- Title
- Abstract
- Introduction
- Literature Review
- Methodology
- Timeline
- Significance / Expected Contributions
- References

如果领域模板要求额外结构，则按领域模板执行。例如 Humanities 可加入 chapter-outline 逻辑；STEM 应强化方法与假设；Social Sciences 应明确 sampling、ethics 与 theory linkage。

大纲中应标出每一节的作用与大致字数分配。然后输出**中间输出 4**并等待用户确认。

### Step 6: Write the Full Proposal

这是本 skill 的核心写作阶段。开始写之前，必须读取并应用以下文件，且**不得遗漏其关键作用**：

- `references/STRUCTURE_GUIDE.md`
- `references/DOMAIN_TEMPLATES.md`
- `references/WRITING_STYLE_GUIDE.md`
- `references/QUALITY_CHECKLIST.md`

如需使用脚手架，可按输出语言选择：

- `assets/proposal_scaffold_en.md`
- `assets/proposal_scaffold_zh.md`

在写作阶段，完整继承以下约束：

1. 研究计划书默认目标长度为 **2000-4000** 词，默认约 **3000** 词；Humanities 可按需要更长。
2. 使用**连贯的学术 prose**，不得把主体内容写成堆叠式 bullet points 或编号清单。
3. 仅在真正必要时保留列表，例如研究问题、时间表里程碑、技术规格。
4. 使用审慎的 hedging 语言，避免绝对化、夸张化结论。
5. 在正文合适位置加入 **3-5 个 figure suggestions**，格式与 `WRITING_STYLE_GUIDE.md` 保持一致。
6. PhD 级 proposal 默认至少 **40 条参考文献**，并兼顾经典文献与近五年研究。
7. 不得添加 appendix；所有关键内容应置于主文结构内。
8. 按领域匹配引用风格：STEM 多用 APA，Humanities 用 MLA 或 Chicago，Social Sciences 用 APA 或 Chicago；中文输出时参考 GB/T 7714。
9. 所有主张都应由文献、教授研究轨迹或申请者真实经历支撑。
10. 申请者优势必须在方法可行性、研究准备度或题目合理性中得到明确体现。

全文应基于**已确认的大纲**一次性完成，而不是边写边重新发明结构。

### Step 7: Quality Review and File Generation

全文完成后，再次读取并执行 `references/QUALITY_CHECKLIST.md` 中的检查要求。

重点核查以下内容：

1. 结构完整且顺序合理。
2. 研究问题、文献空白、方法与时间线彼此一致。
3. 写作语体正式，过度承诺已被 hedging 修正。
4. figure suggestions 数量与分布合理。
5. 文献数量、时效性与格式符合要求。
6. 没有残留占位符、TBA、TBD 或空白字段。
7. 语言前后一致，不混用中英文叙述。
8. 没有 appendix。

最终文件命名为：

```text
proposal_{topic_slug}_{YYYY-MM-DD}.md
```

默认交付可编辑 Markdown 文件。

### Step 8: Deliver the Final Result

最终交付时：

1. 附上 Markdown 格式研究计划书。
2. 可简要说明题目、教授匹配逻辑与核心贡献。
3. 如有需要，补充转换建议，例如导出为 Word 或 PDF。

## Domain Adaptation Rules

为防止把不同学科写成同一种模板，必须按 `references/DOMAIN_TEMPLATES.md` 执行领域适配。

| 学科领域 | 默认重点 |
|---|---|
| STEM | 强化方法、实验设计、变量、验证与技术可行性 |
| Humanities | 强化理论框架、史学/文献回顾、中心论点与 chapter outline |
| Social Sciences | 强化理论关联、抽样、数据收集、分析路径与伦理说明 |

如果用户未明确学科领域，则必须先确认，不能直接套用默认模板。

## Mandatory Confirmation Gates

下列两个确认点不可跳过，除非用户明确要求“直接继续”：

1. **题目确认**：输出中间输出 2 后必须等待。
2. **大纲确认**：输出中间输出 4 后必须等待。

## Strict Constraints

始终遵守以下硬约束：

1. **No fabrication**：不得虚构教授论文、来源链接、研究方向、招生信息、实验室条件、文献、方法、数据集或申请者经历。
2. **Trajectory matching**：不得围绕教授过时研究主题构建 proposal；优先匹配近年持续方向。
3. **Applicant-grounded feasibility**：题目必须建立在申请者真实能力与经历之上。
4. **Exactly one topic**：默认只生成 **1 个**建议题目，不并列生成多个备选。
5. **Language consistency**：最终 proposal 必须完整使用用户指定语言，参考文献原始标题可保留原文。
6. **Markdown deliverable**：最终交付必须是干净、可编辑的 Markdown 文件。
7. **Writing-stage fidelity**：写作阶段不得弱化或省略 `research-proposal` 参考文件中的关键要求。

## Error Handling

### Professor Not Accepting Students

如发现教授明确不接收学生：

1. 立即告知用户。
2. 说明这是招生风险，而不是研究能力评价。
3. 等待用户决定是否仍要继续写 speculative draft。

### Insufficient Professor Information

如果教授主页信息非常少：

1. 明确说明证据不足。
2. 优先抓取 publications、news、profile、lab pages 中可验证信息。
3. 降低结论确定性，不要用猜测补足事实缺口。

### Topic Too Vague

如果用户仅给出宽泛兴趣：

1. 要求其补充研究对象、场景、方法偏好或应用方向。
2. 用教授近期轨迹帮助缩小范围。
3. 在题目确认前不要直接写整篇 proposal。

### Sparse Literature

如果相关文献稀缺：

1. 承认该领域证据基础有限。
2. 使用相邻领域、方法文献与基础综述补足论证。
3. 在 proposal 中谨慎表述新颖性与不确定性。

### Word Count Pressure

如果用户要求极短版本：

1. 优先保留 Introduction、Literature Review、Methodology、Significance。
2. 压缩背景与时间线描述，但不得删掉核心结构。
3. 仍然保持连贯 prose，而不是改写为项目符号摘要。

## Resource Map

本 skill 的资源使用方式如下：

| 文件 | 用途 |
|---|---|
| `references/LITERATURE_WORKFLOW.md` | 文献收集与分类操作流程 |
| `references/STRUCTURE_GUIDE.md` | proposal 分章节结构与长度要求 |
| `references/DOMAIN_TEMPLATES.md` | STEM / Humanities / Social Sciences 分支逻辑 |
| `references/WRITING_STYLE_GUIDE.md` | 写作风格、hedging、过渡与 figure suggestion 规范 |
| `references/QUALITY_CHECKLIST.md` | 最终质量检查清单 |
| `assets/proposal_scaffold_en.md` | 英文 proposal 脚手架 |
| `assets/proposal_scaffold_zh.md` | 中文 proposal 脚手架 |

## Success Condition

仅当以下条件同时成立时，才视为该 skill 成功完成任务：

1. 用户看到了教授研究画像与招生风险提示。
2. 用户确认了**唯一**研究题目。
3. 用户确认了 proposal 大纲。
4. 最终交付了 Markdown 格式研究计划书。
5. 写作质量、结构、领域适配与质量校验完整继承内置写作参考文件的要求。

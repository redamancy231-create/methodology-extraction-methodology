# 方法论提取方法论（Methodology Extraction Methodology）

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Status](https://img.shields.io/badge/Status-CLOSED-inactive.svg)]()
[![Version](https://img.shields.io/badge/Version-v0.1_trial-orange.svg)]()
[![Language](https://img.shields.io/badge/README-简体中文-red.svg)]()
[![Framework](https://img.shields.io/badge/Based_on-AI协作框架_v1.5.1-blue.svg)](https://github.com/redamancy231-create/ai-collaboration-framework)

[简体中文](README.md) | [正體中文](README_zh-TW.md) | [English](README_en.md)

> **定位**: 一次方法论文献提取的实验记录——不是可交付的成品，而是过程的诚实记录。
> **状态**: v0.1 trial · CLOSED · 不成熟
> **生成模型**: DeepSeek-V4-Pro (via Claude Code CLI)
> **生成日期**: 2026-06-16

---

## 这是什么

一个元层次方法论项目——从 **19 个项目**（含自有 AI 协作项目、外部开源项目、学术压力测试）中系统提取可复用的方法论模式。

它的**双重目的**：
1. **产出层**：尝试形式化一套"方法论提取框架"——如何从一组项目中识别、验证和归类跨项目的方法论模式
2. **测试层**：作为 [AI 协作项目全生命周期框架](https://github.com/redamancy231-create/ai-collaboration-framework) Protocol 3 的首次端到端试跑

## 为什么不成熟

项目自身的 G5 可追溯审计结论：**无一方法论模式满足 ≥3 个源项目的稳定组件门槛。** 16 个自有项目来自同一作者、同一时期的 AI 协作实践，3 个外部项目（NPGS/ml-quant-trading/CrossCheck）来自其他作者但由同一操作者提取——这个样本量不足以支撑泛化的方法论提取。

换句话说：我们证明了"这件事有多难"，但还没有做到"这件事该怎么做"。

## 有什么值得看

### 审查链实证（最有价值的部分）

10 轮正式审查（来自 4 个审查后端：GPT-5.5/Kimi-K2.7/Qwen3.7-Max/GLM-5），另有 1 次异后端复编码（Phase 3.5）。累计 58 项发现，全部闭合。基于 Kohli (2026-05) 的独立性分析，有效独立视角约 2-3 个。关键数据点：

- **Phase 5 双轮正交审查**：GPT-5.5 发现 17 项 + Qwen3.7-Max 发现 16 项 = **0 重叠**——在本次两轮审查及当前编码规则下未观察到重叠，提示不同模型的错误敏感性具有互补性
- **Phase 7.6 终期审查**：GPT-5.5 实用完整性评分 7.7/10
- **审查方法论价值**：整个审查链本身就是"多模型独立审查有效性"的强证据

详见 [`reviews/`](reviews/)。

### G5 可追溯审计

对 v0.1 框架的逐组件审计，结论是"所有 5 组件均未达到 ≥3 源稳定门槛"。这是项目最诚实的发现。

详见 [`synthesis/phase4_traceability_audit.md`](synthesis/phase4_traceability_audit.md)。

### 10 张公开证据卡

每张卡片记录一个源项目或外部压力测试的方法论特征提取结果。另有 10 张未公开项目的证据卡保留在本地（详见 `explorations/source_projects_summary.md` 口径说明）。

详见 [`explorations/`](explorations/)。

### 框架 v0.1（trial）

方法论提取框架的试行版本——标注了"trial"状态，每个组件都附有稳定度评估。

详见 [`framework_output/main/`](framework_output/main/)。

## 项目结构

```
├── README.md                          ← 本文件
├── CLAUDE.md                          ← 项目宪法（AI 协作指南）
├── FORKING.md                         ← Fork 指南
├── project_spec.md                    ← S1-S10 完整 Spec
├── DEV_LOG.md                         ← 开发日志
│
├── spec/                              ← 项目规范
│   ├── success_criteria.md            ← 成功标准与 Protocol 3 预登记指标
│   ├── evaluation_plan.md             ← 评估计划
│   ├── risk_register.md               ← 风险登记册
│   └── ...
│
├── explorations/                      ← 10 张公开证据卡 + 源项目汇总
│   ├── evidence_card_*.md             ← 每个源项目的方法论特征提取
│   └── phase2_completion_summary.md
│
├── synthesis/                         ← 综合与模式提取
│   ├── phase4_validated_pattern_catalog.md/.json  ← 经验证的模式目录
│   ├── phase4_traceability_audit.md   ← G5 可追溯审计
│   └── phase6_mini_extraction.md      ← 递归观察
│
├── reviews/                           ← 10 轮审查报告（核心实证）
│   ├── phase5_codex_crosscheck.md     ← GPT-5.5 审查（17 项发现）
│   ├── phase5_qwen_independent_review.md ← Qwen3.7-Max 审查（16 项发现）
│   └── ...
│
├── framework_output/main/             ← 主交付物
│   ├── 方法论提取框架_v0.1_trial.md   ← 方法论提取框架正文
│   └── 方法论提取框架_v0.1_trial.json ← 机读版
│
└── archive/                           ← 归档（复盘报告等；本地保留）
```

## 相关工作

> 2026-07-23 调查

### 想法 provenance

本项目的想法并非预先设计——它是在 2026-06-16 [AI 协作项目全生命周期框架](https://github.com/redamancy231-create/ai-collaboration-framework) Protocol 3 试跑期间，由 AI 模型（DeepSeek-V4-Pro 或同期的其他协作模型）在对话中提出的。这个想法的构成元素在学术传统中均有前驱：**系统文献综述方法论**（医学/社会科学标准方法）、**软件工程经验教训提取**（lessons learned / post-mortem analysis）、**证据分级体系**（[S]/[E]/[I] 标签来自框架自身设计）。但把这些分散的概念组合成"从多个 AI 协作项目中系统提取可复用方法论文献"——这个组合本身未在后续的系统搜索中找到直接先例。

### GitHub 搜索

对以下 9 个方向（中英双语，实际搜索使用英文关键词）进行了系统搜索，**全部零结果**：

| # | 中文 | English |
|---|------|---------|
| 1 | 方法论文献提取 + AI 协作模式 | `methodology extraction AI collaboration patterns meta` |
| 2 | 方法论文献提取 + LLM 多模型审查 | `"methodology extraction" LLM multi-model review` |
| 3 | 跨模型审查 + 独立验证 + 学术流水线 | `cross-model review independent verification pipeline academic` |
| 4 | AI 协作经验教训 + 多 agent 工作流 | `"lessons learned" AI collaboration multi-agent workflow` |
| 5 | 提示词工程模式目录 + 系统提取 | `prompt engineering patterns catalog extraction systematic` |
| 6 | LLM 协作框架 + 角色流水线 | `LLM collaboration framework role-based pipeline` |
| 7 | 多模型独立审查 + 交叉盲审 | `"multi-model" independent review blind cross` |
| 8 | AI 协作元分析 + 模式目录 | `AI collaboration meta-analysis pattern catalog empirical` |
| 9 | AI 使用经验 + 开发者工作流文档化 | `"how I use AI" developer workflow documentation systematic` |

**搜索局限**：GitHub 搜索结果受仓库 stars、活跃度和排序算法影响，低 stars 仓库的可见性有限；学术文献搜索受关键词选择影响。不排除相关工作存在但未被检索到。本次检索未发现"从多个 AI 协作项目中系统提取方法论模式"的同类项目。

已知最接近的三个项目（均来自手动发现，GitHub 搜索无法索引微型仓库）：

| 项目 | 相似度 | 差异 |
|------|--------|------|
| [sburl/CrossCheck](https://github.com/sburl/CrossCheck) | 中 | 多模型审查自修正系统，但是 **npm CLI 工具**，不做跨项目模式提取 |
| [huidev2025/CSF](https://github.com/huidev2025/CSF) | 低 | LLM 协作框架，聚焦**如何协作**，不做跨项目模式提取 |
| [rainmana/mcw-framework](https://github.com/rainmana/mcw-framework) | 低 | 人-AI 协调窗口元模型，方向不同 |

三者共同特征：单人项目、零外部贡献、<25 stars。**这个赛道目前没有社区。**

### 学术文献

本项目核心主张（多模型独立审查的价值）在 2026 年学术文献中获得了外部支持和对照：

**"九法官，两有效票"（Kohli, 2026-05）** — [*Nine Judges, Two Effective Votes: Correlated Errors Undermine LLM Evaluation Panels*](https://arxiv.org/abs/2605.29800)。核心结论：9 个前沿 LLM 组成的评审团，有效独立票数仅 ~2 票；**单一最佳评委的表现追平甚至超过整个评审团**。这为本项目的多模型审查架构提供了一个外部参照——在 Kohli 测试的分类任务上，4-5 模型可能已是有效上限（跨任务外推需谨慎），加更多模型收益递减。

**"行为纠缠"统计框架（Kuai et al., 2026-04）** — [*How Independent are Large Language Models? A Statistical Framework for Auditing Behavioral Entanglement*](https://arxiv.org/abs/2604.07650)。测试 18 个 LLM（来自 6 个模型家族），发现广泛的"行为纠缠"（共享训练数据/蒸馏/对齐管道导致的隐式依赖）。去纠缠的验证器集成可将准确率提升 4.5%。

**"当模型意见分歧时"（Nájera et al., 2026-05）** — [*When Models Disagree: Rethinking LLM Evaluation for Public Comment Analysis*](https://arxiv.org/abs/2605.29025)。将多模型分歧重新定义为**诊断信号**而非缺陷——分歧模式映射到真实的解释复杂性。本项目 Phase 5 双轮审查 33 项发现在当前编码规则下未观察到重叠，为这一理论提供了一个可能的数据点（需注意审查任务与原文公共评论分析场景的差异）。

**"人主导的 AI 共创"（Oda, 2026）** — [*Human-Led AI Co-Creation: A Practical Framework for Multi-Model Research, Convergence, and Human Authority*](https://www.academia.edu/165538962)（独立白皮书，同行评审状态未知）。提出的四角色框架（主 AI 起草 → 多模型并行审查 → 迭代跨模型对比 → 人类最终裁决）与本项目流水线几乎同构。

**关键对照**：

| 维度 | 学术前沿 | 本项目 |
|------|---------|--------|
| 多模型独立性量化 | 9→2 有效票（Kohli 2026-05） | 5 模型错误空间互补（实证，未经数学建模） |
| 分歧作为诊断信号 | 四类分歧分类法（Nájera 2026-05） | Phase 5 双轮审查零重叠（实证案例） |
| 人-AI 协作框架 | 四角色模型（Oda 2026） | 五铁律 + 角色槽位（更严格的独立性约束） |
| **跨项目模式提取** | **未检索到同类工作** | **12 项目系统提取（搜索存在已知局限，见上文）** |

### 闭合后外部验证附录

基于上述 4 篇论文的分析框架，对本项目的审查数据进行了重分析（重新分类 58 项发现、评估模型独立性、对比协作框架）。详见 [`post-hoc-external-validation.md`](post-hoc-external-validation.md)。

### 外部验证的四条修正

| 来源 | 验证了什么 | 修正了什么 |
|------|-----------|-----------|
| Kohli (2026-05) | 4-5 模型架构是最优配置 | 10 轮审查 ≈ 2-3 个有效独立视角，不应声称"10 轮独立" |
| Nájera (2026-05) | Phase 5 零重叠是"深度分歧"的预期表现 | 58 项发现可系统分为 4 类，34% 为深度分歧——≥3 后端是必要的 |
| Kuai (2026-04) | 全不同提供商的模型选择是隐式去纠缠策略 | 纠缠度虽低但非零——不能声称"完全独立" |
| Oda (2026) | 铁律体系比最接近的学术框架更严格 | Oda 的失败模式分类可注入 Phase 0 风险登记册 |

### 定位总结

本项目的核心主张（多模型独立审查有效）获得了 2026 年学术文献的外部支持和对照。但"从多个 AI 协作项目中系统提取可复用方法论文献"这个元层次动作——在 2026-07-23 对 GitHub（9 个方向）和学术文献的系统搜索中**未检索到**同类工作。搜索存在已知局限（GitHub 索引微型仓库不完整、学术搜索受关键词选择影响），因此不排除相关工作存在但未被发现。本项目受限于 n=12 同作者样本，提取出的模式尚未达到跨用户泛化的稳定门槛。

### 适用人群与使用价值

**适用人群**：已经在用 AI 做多个项目、积累了大量 CLAUDE.md / DEV_LOG / 审查报告，但感觉自己的方法论散落在各个项目里，想系统化的人。

**不适用**：只做过一两个项目的人（n 太小）、不做 AI 协作的纯代码项目、没有方法论文档的项目、想找"最佳实践模板"的人（本框架告诉你"你做了什么"，不告诉你"你应该做什么"）。

**使用价值**三点：

1. **知道自己的方法论"值多少钱"**——框架的 8 个组件是一份检查清单。跑一遍就知道你的项目在哪些维度上有方法论自觉（文档、审查、闭环）、哪些是空白
2. **把散落的碎片拼成模式**——19 个项目的方法论文档分散在各处，提取框架提供了跨项目对比的流程
3. **让方法论被外部验证**——整理成结构化形式后，可以被对比、被质疑、被学术文献交叉验证

**核心局限**：框架目前只在 19 个 AI 协作项目上运行过——其中 **16 个为作者自有项目**、**3 个为外部作者项目**（NPGS/baopinshui、ml-quant-trading/initial-d、CrossCheck/sburl）。可提取程度与项目的方法论自觉正相关：主动记录AI协作过程的项目可提取大部分方法论组件；仅保留被动代码痕迹的项目可提取内容骤降至少数几个组件——框架无法从不存在的信息中提取信息。所有项目的提取和审查由同一操作者执行。按项目类型的定性梯度见 `explorations/source_projects_summary.md`。框架的有效性是否泛化到其他作者的工作习惯和不同操作者的提取方式，**尚未验证**。

## 与父框架的关系

本项目是 [AI 协作项目全生命周期框架](https://github.com/redamancy231-create/ai-collaboration-framework) v1.5.1 的 Protocol 3 试跑对象。父框架此后已演进至更高版本。本项目是闭合时刻的历史快照，部分版本引用可能滞后。

## 关联项目

| 项目 | 关系 |
|------|------|
| [**AI 协作框架**](https://github.com/redamancy231-create/ai-collaboration-framework) | **方法论上游** — 本项目是框架 Protocol 3 的试跑对象 |
| [**claude-skills**](https://github.com/redamancy231-create/claude-skills) | **方法论文献源** — 三个 Skill 的提取结果已纳入本框架（证据卡 #11） |
| [**Independent Review Toolkit**](https://github.com/redamancy231-create/independent-review-toolkit) | **审查方法来源** — 本项目的独立审查流程使用该工具包 SOP |
| [**Prompt-TDD Methodology**](https://github.com/redamancy231-create/prompt-tdd-methodology) | **同系项目** — 对照实验方法论案例手册，共享多后端审查实证 |
| [**Methodology Handbook**](https://github.com/redamancy231-create/methodology-handbook) | **同系项目** — 50 条 AI 协作实战教训速查，Skill 设计协议的经验来源 |
| [**DOCX Pipeline**](https://github.com/redamancy231-create/docx-pipeline) | **同系项目** — Markdown → 中文 DOCX 管道（提取框架方法论源之一） |
| [**ETF Pattern Match — pybind11**](https://github.com/redamancy231-create/etf-pattern-match-pybind11) | **同系项目** — C++20/pybind11 量化加速，审查链实证源 |
| [**M&A Case Study Pipeline**](https://github.com/redamancy231-create/ma-case-study-pipeline) | **同系项目** — 8 阶段多模型学术生产流水线，证据卡源项目 |

## 相关文件

- [FORKING.md](FORKING.md) — Fork 指南（四层修改方向 + 已知局限）
- [minimal-methodology-guide.md](minimal-methodology-guide.md) — 最小方法论文档指南（面向"用AI做项目但没记录过程"的人）
- [CONTRIBUTING.md](CONTRIBUTING.md) — 贡献指南
- [CITATION.cff](CITATION.cff) — 引用信息

## 许可证

文档/数据: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

---

*"我们证明了这件事有多难，但还没有做到这件事该怎么做。"*
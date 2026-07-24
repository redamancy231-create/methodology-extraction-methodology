# 源项目汇总与口径说明

> **目的**: 提供方法论提取的完整证据基础，明确每个源项目的来源分类
> **总项目数**: 22（11 个有独立证据卡 + 11 个分析过程见 reviews/）

---

## 源项目清单

### 一、外部分析项目（12 个）

对他人开源项目或论文的独立分析。按有无独立证据卡分两组：

**有证据卡（3 个）**：

| 项目 | 类型 | 源作者 | 源仓库 |
|------|------|--------|--------|
| CrossCheck | 工具/系统（多模型 AI 编码自主循环） | sburl (Spencer Burleigh) | [sburl/CrossCheck](https://github.com/sburl/CrossCheck) |
| ml-quant-trading | 量化（ML 多因子交易系统 + arXiv 论文） | Yimin Du (initial-d) | [initial-d/ml-quant-trading](https://github.com/initial-d/ml-quant-trading) |
| NPGS | C++ 游戏/模拟（非 AI 协作项目） | baopinshui | [baopinshui/NPGS](https://github.com/baopinshui/NPGS) |

**无独立证据卡（9 个）** — 分析过程记录在 `reviews/` 审查报告中：

| 项目 | 类型 | 说明 |
|------|------|------|
| Agent Harness | AI agent 综述论文分析 | 分析 AI agent harness 综述论文的方法论 |
| claude-code-ultimate-guide | 工具指南分析 | 分析 claude-code 使用指南文档 |
| claude-md-generation | 方法论批量生成分析 | 分析 12 项目 CLAUDE.md 的生成模式 |
| Evolver | 论文+代码分析 | 分析 Evolver 论文的方法论和代码架构 |
| GitNexus | 工具分析 | 分析 GitNexus 代码知识图谱工具 |
| LIT | 论文分析 | 分析 LLM 厂商技术报告的披露完整性 |
| PilotDeck | 论文+代码分析 | 分析 PilotDeck 论文的方法论和架构 |
| PocketFlow | 架构分析 | 分析 PocketFlow 代码架构——后续启发了 prompt-tdd 对照实验 |
| Small Scale | 论文分析 | 分析 ICLR 论文 Small Scale 的方法论 |

### 二、自建公开项目（7 个）

作者自己开发并已上传 GitHub 的项目。均有独立证据卡。

| 项目 | 类型 | 仓库 |
|------|------|------|
| AI 协作项目全生命周期框架 | 元项目/方法论文档 | [ai-collaboration-framework](https://github.com/redamancy231-create/ai-collaboration-framework) |
| claude-skills | 工具/流程（Claude Code Skill 集合） | [claude-skills](https://github.com/redamancy231-create/claude-skills) |
| docx-pipeline | 工具/工程（Markdown → DOCX 管道） | [docx-pipeline](https://github.com/redamancy231-create/docx-pipeline) |
| ETF Pattern Match — pybind11 | 量化/工程（Python+C++ 混合编程） | [etf-pattern-match-pybind11](https://github.com/redamancy231-create/etf-pattern-match-pybind11) |
| Independent Review Toolkit | 工具/方法论（独立审查 SOP） | [independent-review-toolkit](https://github.com/redamancy231-create/independent-review-toolkit) |
| 中国上市公司并购重组成功案例研究 | 学术（多模型学术生产流水线） | [ma-case-study-pipeline](https://github.com/redamancy231-create/ma-case-study-pipeline) |
| Prompt-TDD Methodology | 方法论/对照实验（案例手册） | [prompt-tdd-methodology](https://github.com/redamancy231-create/prompt-tdd-methodology) |

### 三、自建未公开项目（3 个）

作者自己开发但未上传 GitHub 的项目。

| 项目 | 类型 | 有证据卡 |
|------|------|:--:|
| 形态匹配 ETF 策略 | 量化（多头轮动策略） | ✅ |
| BDC2026 | 量化竞赛 | ❌ |
| 多模型对照实验 | 方法论/对照实验 | ❌ |

---

## 方法论自觉梯度

11 个有独立证据卡的项目揭示了清晰的梯度。定性层级传达的是"有和无"的差异方向：

| 来源 | 方法论自觉 | 提取层级 | 代表 |
|------|:--------:|------|------|
| 自建（工具类） | ★★★★★ | **完整提取** — 多数组件可提取 | docx-pipeline（7/7） |
| 自建（元项目/学术类） | ★★★★★ | **主要提取** — C7 闭环有缺口 | ai-collaboration-framework（6.5/8）、ETF-pybind11、M&A 等 |
| 外部（有论文/有架构文档） | ★★★ | **部分提取** — 无 AI 协作过程记录 | ml-quant-trading（5.5/8）、CrossCheck（5.5/8） |
| 外部（纯代码，无方法论文档） | ★ | **痕迹提取** — 仅被动痕迹 | NPGS（3/8） |

> 注：梯度主要来自 C7（闭环修复）和 C8（数据溯源）。层级名称携带了"为什么"的信息。无证据卡的 11 个项目未纳入此表——其方法论文档完整度低于有证据卡的项目，提取结果分散在审查报告中。

---

## 提取的跨项目模式（Phase 2-4 合成）

| # | 模式 | 支持数 | 稳定度 |
|---|------|:-----:|:------:|
| P1 | **prompt+config 双文件机制** | 4/11 | [E] 试行 |
| P2 | **独立审查轮换**：撰稿模型不审自己的稿 | 5/11 | [E] 试行 |
| P3 | **零卷入评分官** | 3/11 | [I] 审查门禁 |
| P4 | **审查后端多样性**：≥3 个不同提供商的审查后端 | 4/11 | [E] 试行 |
| P5 | **提取者效应**：需异后端复编码 | 2/11 | [Sp] 推测 |
| P6 | **异后端审查**：不同后端发现集合近似正交 | 3/11 | [I] 审查门禁 |
| P7 | **诊断→修复闭环** | 2/11 | [Sp] 推测 |
| P8 | **术前否决位**：动笔前由独立角色做理论 kill-test | 2/11 | [Sp] 推测 |

**审计结论（G5）**：无一模式满足 ≥3 源项目稳定组件门槛。"对失败诚实"为首个达标模式。

---

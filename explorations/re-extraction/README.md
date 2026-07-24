# 异后端重提取对照实验

**目的**: 量化 P5「提取者效应」——同一框架由不同模型提取，结论差异多大。

**实验模型**: GPT-5.6-Sol (via Codex CLI) vs DeepSeek-V4-Pro（原始提取）

**日期**: 2026-07-24

---

## 实验设计

对全部 9 个有证据卡且提取模型确认为 DeepSeek-V4-Pro 的项目，由 GPT-5.6-Sol 在**不参考原始证据卡**的条件下，使用相同的 C1-C8 框架和相同的源文件独立重提取。逐组件对照差异。

每个项目的提示词内联了该项目的 README、CLAUDE.md（若有）、CONTRIBUTING 等源文件，不包含 DeepSeek 生成的分析产物。

## 九轮对照汇总

| # | 项目 | 类型 | D 等级 | G 等级 | 等级差 | G 关键发现 |
|---|------|------|:--:|:--:|:--:|------|
| 1 | NPGS | 外部 | D | C | +1 | — |
| 2 | ml-quant-trading | 外部 | C | B | +1 | — |
| 3 | CrossCheck | 外部 | C | B | +1 | Quality Gates 夜间持续失败；抽样 PR 无独立审批 |
| 4 | AI协作框架 | 自建 | A | B | **-1** | 传播表计数≠实际(6≠7)；CLI 统计口径漂移 |
| 5 | claude-skills | 自建 | — | B | = | P0→P1→P2 协议在源文件中不存在 |
| 6 | docx-pipeline | 自建 | B | B | = | 测试数三版本矛盾(17/52/73)；审查轮数 3≠5 |
| 7 | ETF-pybind11 | 自建 | B | B | = | 「32条全修复/0回归」无逐项证据；审查轮数 4≠7 |
| 8 | Independent Review Toolkit | 自建 | B | B | = | C5 适用性分歧：SOP 承担了 CLAUDE.md 功能 |
| 9 | Prompt-TDD | 自建 | B | B | = | A1 附录与事实矛盾；A2/A3 复现命令 exit 1 |

## 核心发现

### 1. 提取者不对称效应（P5 实证）

**外部 3 个项目全部抬升，自建 6 个项目 0 抬升、1 降级。** GPT-5.6-Sol 对他人项目给善意解释（"有论文就算设计意图"），对自己写的项目要求逐项核实（"50+轮不是你说了算的"）。

### 2. 组件定义漂移（9/9 复现）

C3-C8 在两个模型中对应不同内容。DeepSeek 的 C3=版本控制，GPT 的 C3=设计意图；DeepSeek 的 C4=质量保障，GPT 的 C4=开发流程——同一标签，不同操作化定义。

### 3. GPT-5.6-Sol 捕获了 DeepSeek 的自审盲区

| 项目 | DeepSeek 未发现 |
|------|------|
| CrossCheck | Quality Gates 持续失败、PR 自提自合 |
| AI框架 | 传播表计数不一致、README/CLAUDE.md 不同步 |
| docx-pipeline | 测试数三个版本、审查轮数两个版本 |
| ETF-pybind11 | 闭环核心证据（32 项/7 轮/0 回归）不在源文件中 |
| Prompt-TDD | A1 附录状态与上游事实矛盾、复现命令全部失败 |

### 4. 证据等级不对称性

DeepSeek 对自建项目最高给了 A（AI框架），GPT-5.6-Sol 对自建项目最高给了 B。GPT 对所有 6 个自建项目有 5 个评 C5（AI 协作文档）低于 DeepSeek，因为两个项目根本没有 CLAUDE.md（review-toolkit、prompt-tdd）。

## 提示词文件

每个实验的完整提示词（含内联源文件）保存在 `../prompts/re-extract_*_gpt56.md`。

---

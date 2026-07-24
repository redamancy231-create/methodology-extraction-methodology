---
project: claude-skills
type: 工具/流程（Claude Code Skill 集合）
status: v1.0.1（脱敏闭合）
extraction_date: 2026-07-24
extraction_model: DeepSeek-V4-Pro (via Claude Code CLI)
extractability: 5/6 (83%)
methodology_fragments: 8
evidence_grades: {A: 5, B: 1, C: 2}
rubric_score: 14/15
source_quality: self-owned-public
framework_version: v0.1-trial
---

# 证据卡 — claude-skills

> 提取日期: 2026-07-24 · 提取模型: DeepSeek-V4-Pro (via Claude Code CLI)
> 按方法论提取框架 v0.1 trial 的证据卡模板执行

## 项目基本信息

| 字段 | 值 |
|------|-----|
| 项目名称 | claude-skills |
| 项目类型 | 工具/流程（Claude Code Skill 集合） |
| 状态 | v1.0.1（脱敏闭合） |
| 规模 | 中（3 个 Skill + 三语 README + reference/templates/scripts） |
| 作者 | redamancy231-create |
| 仓库 | https://github.com/redamancy231-create/claude-skills |
| CLAUDE.md | ✅ 已补充（2026-07-24，按 write-claude-md 五步协议生成，~90 行） |
| 闭合记录 | project_status.md（13 行，简略） |
| CHANGELOG | ✅ v1.0.0 → v1.0.1 |
| 审查记录 | _review/（本地保留，未 tracked） |

## 准入条件检查（§1.1）

| 条件 | 结果 |
|------|:--:|
| E1: CLAUDE.md | ✅ 已补充（2026-07-24，write-claude-md 协议生成） |
| E2: 闭合记录 | ⚠️ 存在但极简（13 行） |
| E3: 产出 ≥3 文件 | ✅ |
| E4: 方法论发现 | ✅ 强——README 自述设计思路 |

**判定**: 全部准入条件满足（E1 补充后），可进入完整提取路径。

## Rubric 评分（§1.2）

| 维度 | 评分 | 理由 |
|------|:--:|------|
| 方法论密度 | 3 | 路由器模式、渐进式披露、allowed-tools、触发分级、死亡判据、共享文件所有权、中断恢复、事前否决双门协议——≥6 个可迁移片段 |
| 失败教训 | 2 | CHANGELOG 记录版本迭代，SKILL.md 含反例/教训 reference 文件 |
| 独立审查深度 | 3 | 每个 Skill ≥2 后端独立审查，项目整体 50+ 轮跨 5 后端 |
| 格式成熟度 | 3 | 三语 README + CITATION.cff + CHANGELOG + 结构化 SKILL.md frontmatter + CLAUDE.md（按自有 write-claude-md 协议生成） |
| 源项目质量 | 3 | 已被 awesome-skills 收录，框架 §9.2-§9.3 提取 |

**总分: 14/15 → 高优先级**（格式成熟度 2→3，补充 CLAUDE.md 后）

## 可提取的方法论片段

### 片段 1: 路由器模式 + 渐进式披露

**描述**: SKILL.md 仅含核心流程 + Quick Reference 路由表，详细参考件外置到 `reference/` 目录，Agent 按需读取而非全量加载。

**来源**: README.md"设计思路"章节；session-end/SKILL.md:16-24 路由表

**可迁移条件**: 适用于所有需要控制 Agent 上下文消耗的 Skill/指令设计场景。前提是 reference 文件结构清晰、路由表覆盖全场景。

**反例/限制**: 路由表不完整时 Agent 会迷路；reference 文件过时时路由表失去索引价值。不适用于极度简单（<3 场景）的 Skill。

**证据等级**: A（源文件明确记录 + 3 个 Skill 均采用此模式 + 已被 awesome-skills 收录验证）

### 片段 2: 触发分级 + 判定问句

**描述**: 每个 Skill 定义"应触发/不应触发"的明确边界，辅以一个判定问句（如"本会话是否产生了需要下一会话知道的状态变更？"），Agent 据此自主决定是否激活 Skill。防止过度触发（噪音）和漏触发（遗漏）。

**来源**: session-end/SKILL.md:37-41；write-claude-md/SKILL.md:36-40；kill-test-first/SKILL.md:28-35

**可迁移条件**: 适用于流程型和决策型 Skill。前提是触发条件可操作化（不能是"当用户需要时"这种循环定义）。

**反例/限制**: 判定问句过于模糊时 Agent 无法正确判断。非流程型 Skill（如纯知识查询类）不需要触发分级。

**证据等级**: A（3 个 Skill 均实现，每个 Skill 的判定问句均不同且适配具体场景）

### 片段 3: 共享文件所有权表

**描述**: 每个 Skill 显式声明自己写入/只读哪些文件，以及是否有其他 Skill 也是该文件的写入者。防止多 Skill 对同一文件的并发写入冲突。

**来源**: session-end/SKILL.md:27-33；write-claude-md/SKILL.md:27-31

**可迁移条件**: 适用于多个 Skill/Agent 可能操作同一项目文件的场景。前提是文件所有权边界清晰。

**反例/限制**: 当 Skill 数量增多（>10）时，手动维护所有权表不可扩展——需自动化冲突检测。单 Skill 项目不需要。

**证据等级**: B（2 个 Skill 实现了此模式，kill-test-first 因不写文件而未包含）

### 片段 4: 死亡判据

**描述**: 每个 Skill 附带可操作化的"死亡判据"——定义什么条件下本 Skill 应被视为失效。判据包含可量化阈值（如"连续 10 次使用 Next Steps 完成率 < 30%"）和升级规则。

**来源**: session-end/reference/death-criteria.md（4 条量化判据）；write-claude-md/reference/death-criteria.md；kill-test-first/reference/death-criteria.md

**可迁移条件**: 适用于需要长期维护的 Skill。前提是判据可被客观测量（不能是"当用户觉得没用时"）。

**反例/限制**: 判据测量需要人工或自动化审计——session-end 的判据 #2 需要"独立审查者或人类抽查判定"，可操作化程度受限于审计资源。一次性使用的 Skill 不需要死亡判据。

**证据等级**: A（3 个 Skill 均实现，判据可量化且有升级规则）

### 片段 5: allowed-tools 白名单

**描述**: 每个 Skill 的 YAML frontmatter 中声明 `allowed-tools`，限制 Agent 在 Skill 上下文中可调用的工具。例如 kill-test-first 不允许 Write/Edit（只读+搜索），防止决策型 Skill 越权修改文件。

**来源**: 3 个 SKILL.md 的 frontmatter `allowed-tools` 字段

**可迁移条件**: 适用于所有 Claude Code Skill。前提是 Skill 平台支持工具白名单机制。

**反例/限制**: 白名单过宽 → 形同虚设；白名单过窄 → Agent 无法完成任务。需要根据 Skill 的实际操作需求精确裁剪。

**证据等级**: A（3 个 Skill 均实现，白名单与 Skill 类型精确匹配——决策型只读、流程型可写）

### 片段 6: 中断恢复协议

**描述**: session-end Skill 定义了长会话被 auto-compact 打断后的恢复规则：已完成项通过 git diff/文件时间戳确认后跳过；不确定项重新执行（幂等）；被打断的写入先检查文件当前状态再继续。

**来源**: session-end/SKILL.md:43-48

**可迁移条件**: 适用于可能被中断的长流程 Skill（≥10 步骤）。前提是各步骤具有幂等性或可检测的完成状态。

**反例/限制**: 非幂等操作需要额外的完成检测机制。短流程（<5 步骤）不需要。

**证据等级**: C（仅 1 个 Skill 实现，从实际 auto-compact 经历中提取，未在其他 Skill 中验证）

### 片段 7: 多后端验证 + 零卷入设计

**描述**: 每个 Skill 发布前由 ≥2 个不同 LLM 后端独立审查。审查后端不得参与 Skill 的设计/编写（"零卷入"——出题模型不评自己的题）。验证状态记录在 SKILL.md frontmatter 的 `verified_by` 字段。

**来源**: README.md:13,21-23；SKILL.md frontmatter `verified_by: "GPT-5.5, DeepSeek-V4-Pro, Kimi-K2.7, Qwen3.7-Max, GLM-5.2"`

**可迁移条件**: 适用于重要 Skill 的发布前质量门。前提是有 ≥2 个可用的异后端。

**反例/限制**: 验证质量依赖于审查 prompt 的设计——需确保不同后端用不同审查角度（非同一 prompt 换模型名）。简单/临时 Skill 可跳过。

**证据等级**: A（3 个 Skill 均实现，5 后端验证，README 明确记录零卷入设计原则）

## 框架组件适用性评估

| 组件 | 可提取？ | 提取深度 | 来源 |
|------|:--:|:--:|------|
| C1 项目筛选 Checklist | ⚠️ 部分 | 触发分级+判定问句可视为轻量筛选机制 | SKILL.md 触发分级 |
| C2 提取流程标准化 | N/A | — | 非提取类项目 |
| C3 采纳决策模板 | ✅ 完整 | 三级触发 + 路由分支 + 判定问句 | 全部 3 个 SKILL.md |
| C4 跨项目模式识别 | ✅ 完整 | 路由器模式/渐进式披露/allowed-tools/死亡判据跨 3 Skill 共享 | README + SKILL.md |
| C5 独立审查 SOP | ✅ 完整 | 多后端验证 Step 5 + 零卷入设计 + verified_by 字段 | README + SKILL.md frontmatter |
| C6 多模型协作模式 | ✅ 完整 | 5 后端验证 + 每个 Skill ≥2 后端独立审查 | README:21 |
| C7 闭环修复 | ⚠️ 部分 | CHANGELOG 存在，审查记录存在（_review/），但修复过程未结构化记录 | CHANGELOG.md |
| C8 数据溯源 | N/A | — | 工具/流程项目，非数据项目 |

**可提取率**: 5/6 适用组件（83%），排除 C8 后为 5/6。

> 注：C2 和 C8 不适用——claude-skills 是 Skill 工具集，不是方法论提取或学术研究项目。

## 与其他证据卡的对比

| 维度 | claude-skills | independent-review-toolkit | docx-pipeline |
|------|:--:|:--:|:--:|
| 可提取率 | 5/6 (83%) | 6/7 (86%) | 7/7 (100%) |
| 最强模式 | 路由器+渐进式披露 | 审查 SOP 工具化 | 自动化管道 |
| C7 闭环 | ⚠️ 部分 | ⚠️ 部分 | ⚠️ 部分 |
| 审查深度 | ★★★★★ | ★★★★ | ★★★★ |

claude-skills 和 independent-review-toolkit 同属"方法论→可执行工具"的转化类项目，可提取率相近（83% vs 86%）。claude-skills 的独特增量是**死亡判据**和**中断恢复协议**——这两个模式在现有证据卡中未见。

### 片段 8: "吃自己的狗粮"——用自己生产的工具管理自己的项目

**描述**: 项目初始缺少 CLAUDE.md（E1 不通过），补充后准入条件全部满足。CLAUDE.md 按项目自身的 write-claude-md 五步协议生成，采用 CLOSED 项目差异化权重（避坑权重最高 + 重启指南）。补充 CLAUDE.md 后格式成熟度从 2→3，可提取率不变但准入路径从"降级提取"升级为"完整提取"。

**来源**: 本次提取过程中的实践（2026-07-24）

**可迁移条件**: 适用于所有"生产方法论工具但自己不消费"的项目（如 Skill 集合、审查 SOP 仓库、模板项目）。前提是工具自身适用于该项目的类型。

**反例/限制**: 不适用于工具与项目类型不匹配的场景。此片段是过程性证据而非框架组件证据——它展示的是框架应用如何反馈到被提取对象。

**证据等级**: C（单次实践观察，未经独立项目验证）

## 关键认知

1. **"无 CLAUDE.md 但有方法论"是一个可修复的临时状态**：claude-skills 初始缺少 CLAUDE.md（它生产 CLAUDE.md 但不消费），但项目自身有足够的方法论文档来支撑 CLAUDE.md 的生成。补充 CLAUDE.md 后 E1 从 ❌→✅，证明这类项目不应该是框架的永久例外——它们只是需要一次 write-claude-md 的执行。

2. **死亡判据是可迁移的元模式**：不只是"Skill 应该有死亡判据"，而是"任何长期维护的流程/工具/协议都应该有可量化、可客观判定的失效条件"。这个模式可以升级为框架组件。

3. **提取者效应警告**：提取者（DeepSeek-V4-Pro）同时也是 claude-skills 的设计/编写者之一（SKILL.md frontmatter 中 `verified_by` 列出）。这构成提取者效应的高风险场景——提取者可能对自身参与设计的模式给予过高评价。建议由异后端复编码验证本证据卡的评分。

---

*本证据卡作为扩展集（n=19）的追加提取，标注提取者效应风险。*

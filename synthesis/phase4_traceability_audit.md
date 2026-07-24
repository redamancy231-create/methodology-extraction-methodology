# Phase 4 模式→源项目可追溯性审计

> 审计对象：`synthesis/phase4_validated_pattern_catalog.md` 与 `synthesis/phase4_validated_pattern_catalog.json` 中的 P1-P6、P8。  
> 审计红线：`project_spec.md:68` S4 红线 7：5组件中任一组件无 ≥3 个项目证据支持，不得标为稳定框架组件。  
> 审计口径：这里的“源项目”指 12 个源项目，不把本项目自身的 DEV_LOG、Phase 3/4 workflow、Qwen复验证当作源项目证据。它们可作为过程证据，但不能用于满足“≥3 源项目”门槛。

## 总览

| 模式 | 当前目录强度 | 严格源项目直接证据数 | 是否满足 ≥3 | 稳定组件结论 |
|---|---:|---:|---|---|
| P1 Premise Gate | C+ | 2 | 否 | 证据不足，不得标为稳定框架组件 |
| P2 多后端审查多样性保险 | C+ | 6 | 是 | 项目数满足，但具体“两类错误分化”已被证伪；不得标为稳定组件，只能保留方向性规则 |
| P3 方法论资产提炼协议 | C+ | 4 | 是 | 项目数满足，但存在事后确认偏误；不得标为稳定组件，可作为预注册试行协议 |
| P4 证据等级意识结构性出现 | REJECTED | 不再计数 | 否 | 已拒绝，不进入框架 |
| P5 提取者效应 | B- | 2 | 否 | 证据不足，不得标为稳定框架组件；可作为高风险维度复编码门禁 |
| P6 异后端Phase后审查 | A- | 0（核心比较）；6（相关独立审查价值） | 否 | 核心证据来自本元项目而非源项目；不得以“跨项目稳定组件”标注，但可作为本项目过程规则 |
| P8 Dynamic Workflow并行执行 | Sp注记 | 0（效率测量）；3（相关workflow使用） | 否 | 工具注记，不是稳定框架组件 |

## P1：Premise Gate

**模式声称**：若审查 scope 默认为执行正确性且无显式 premise-review gate，premise-level 错误检测延迟显著长于 execution-level 错误。  
**严格计数**：2 个源项目直接支持。

直接证据：

- 形态匹配ETF策略：核心教训是 Phase 0 必须锁可证伪死亡判据，项目用 18 个版本买来“评审擅长这一步做对了吗，不擅长这件事该不该做”的教训。证据：`形态匹配ETF策略项目 CLAUDE.md:174`。
- 中国上市公司并购重组成功案例研究：playbook 明确把 Phase 0 补上“事前否决位”，并指出两个项目合起来暴露了“根本该不该做”无人事前询问的问题。证据：`并购重组案例研究项目 流水线复用包\多模型论文流水线_playbook.md:113`，`:115`，`:120`。

相关但不计入直接支持：

- 多模型对照实验：有预登记和冻结机制，属于“premise gate 正例设计”，不是“缺失 premise gate 导致错误延迟”的直接证据。证据：`多模型对照实验项目 预登记_pilot.md:63`。
- BDC2026：有 IC 快速验证和活跃边界提醒，但项目未闭合，且证据更多指向“迁移验证”而非 premise-review scope。证据：`BDC2026项目 CLAUDE.md:35`。

**审计结论**：严格源项目数为 2，不满足 ≥3。P1 不得标为稳定框架组件；可作为 C+ 级 Premise Gate 试行规则，等待第三个闭合项目验证。

## P2：多后端审查的多样性保险

**模式声称**：多后端可能覆盖更广的错误敏感性空间，但效应大小、方向、最优组合未量化。  
**严格计数**：6 个源项目支持“独立/多后端审查有增量价值”；但原先“两类错误分化”子命题被 GitNexus 反例证伪。

直接证据：

- 形态匹配ETF策略：Kimi+GLM 终期双审提出重启门槛与数据窥探等修订建议。证据：`形态匹配ETF策略项目 CLAUDE.md:26`，`形态匹配ETF策略项目 17\Kimi审阅结论_终期总结报告.md:11`。
- LIT：四轮独立审查，Codex/Qwen/Kimi/Opus 各自覆盖工程bug、数据一致性和方法有效性。证据：`LIT项目 CLAUDE.md:9`，`LIT项目 archive\cross-round-findings-matrix.md:60`。
- Agent Harness综述：ChatGPT-5.5 独立审查发现报告在论文评分、框架对照和生态声称上的可靠性问题。证据：`Agent Harness项目 analysis_report.md:305`，`Agent Harness项目 independent_review_gpt55.md:147`。
- PilotDeck分析：三轮 Codex/ChatGPT-5.5 审查逐步修正 FAISS、优先级、跨文件一致性等问题。证据：`PilotDeck项目 independent_review_report.md:10`，`PilotDeck项目 independent_review_round3_report.md:201`。
- GitNexus分析：R1/R2/R3 三轮审查分别覆盖事实、流程、决策相关性和竞争框架，R3明确称三轮视角互补。证据：`GitNexus项目 GitNexus_独立审查报告_R3.md:93`，`:96`。
- Evolver分析：DeepSeek+Qwen 两轮对核心事实高度收敛，综合评分差异仅 0.1。证据：`Evolver项目 Evolver_项目闭合记录.md:33`，`:40`。

反证/限制：

- Phase 4 已判定“两类错误分化”版本被 GitNexus 反例证伪。证据：`synthesis/phase4_validated_pattern_catalog.md:16`。
- 多后端本身不是充分条件；零卷入、多角色、多轮和审查prompt质量同样重要。证据：`synthesis/phase4_validated_pattern_catalog.md:52`，`reviews/qwen_phase4_reverify_report.md:241`。

**审计结论**：源项目数满足 ≥3，但当前模式强度仍为 C+，不得标为稳定框架组件。可写为方向性规则：“复杂概念/方法论项目应引入认知距离足够的独立审查”，但不能保留原“两类错误分化”叙事。

## P3：方法论资产提炼协议

**模式声称**：项目关闭时对失败和教训执行三级分流，仅 LEVEL 3 系统性缺陷进入方法论提炼流水线。  
**严格计数**：4 个源项目直接支持“从失败/缺陷中提炼方法论资产”。

直接证据：

- 形态匹配ETF策略：项目在投资上失败，但产出负迁移检验、事前否决位和幂等性验证等可迁移资产。证据：`形态匹配ETF策略项目 CLAUDE.md:172`，`:174`，`:177`。
- 中国上市公司并购重组成功案例研究：上一项目“诊断不落地”被转化为 Phase 9 闭环规则，且流水线复用包成为最有价值资产。证据：`并购重组案例研究项目 CLAUDE.md:65`，`并购重组案例研究项目 流水线复用包\多模型论文流水线_playbook.md:158`。
- Small Scale分析：将数据构建缺失、版本漂移、证据等级混用等缺陷转为 P0/P1 防错机制。证据：`Small Scale项目 small_scale_methodology_transfer_20260613.md:45`，`:156`，`:249`。
- Evolver分析：低质量/低可信项目仍可提取紧凑表示、信号去重等思想，但闭合记录要求完整证据限定和 [Sp] 标注后才可升级。证据：`Evolver项目 Evolver_项目闭合记录.md:42`，`:94`。

相关证据：

- GitNexus分析的 B 维度将警示模式与正向模式平级，说明“不要学什么”也是方法论资产。证据：`GitNexus项目 GitNexus_方法论提取.md:218`。

限制：

- Phase 4 已将 P3 从 A 降为 C+，理由是事后编号暴露确认偏误。证据：`synthesis/phase4_validated_pattern_catalog.md:17`。

**审计结论**：源项目数满足 ≥3，但不得标为稳定组件。建议作为“预注册试行协议”：未来项目关闭前先定义分流标准、排除清单和升级条件，再观察是否可升为稳定组件。

## P4：证据等级意识结构性出现

**模式状态**：REJECTED。  
**审计处理**：不再执行稳定组件计数。

拒绝理由：

- Phase 4 已列 6 条独立否决理由：事实错误、非独立、同作者+72小时窗口、不同分类维度、选择偏差、替代解释更优。证据：`synthesis/phase4_validated_pattern_catalog.md:60`，`:62`。

**审计结论**：已拒绝，不得写入框架稳定组件。可保留为“证据等级必须逐片段标注”的模板要求，但不能作为“自然结构性出现”的跨项目模式。

## P5：提取者效应

**模式声称**：单一后端对解释性方法论提取存在系统性倾向；DeepSeek偏膨胀，ChatGPT-5.5偏保守。  
**严格计数**：2 个源项目文档被复编码支撑该模式。

直接证据：

- Small Scale分析：Phase 3.5 对 Small Scale 做独立复编码，独有特征数从 DeepSeek 的 8 降到 Codex 的 3。证据：`synthesis/phase3_recoding_comparison.md:11`，`:30`。
- GitNexus分析：Phase 3.5 对 GitNexus 做独立复编码，发现 DeepSeek 混淆了“分析报告审查”和“方法论提取文档审查”，且独有特征数从 10 降到 3。证据：`synthesis/phase3_recoding_comparison.md:47`，`:51`，`:74`。

复验证修正：

- Qwen估计纯提取者效应约 9.4%，不是原始声称的 22%；其余分歧多来自任务规范模糊。证据：`reviews/qwen_phase4_reverify_report.md:92`，`:96`，`:102`。

**审计结论**：严格源项目数为 2，不满足 ≥3。P5 不得标为稳定框架组件。可作为“高风险维度复编码门禁”：独有特征计数、审查状态、源质量评估必须二次编码。

## P6：异后端 Phase 后审查

**模式声称**：方法论/概念归类项目中，每 Phase 产出后插入一轮异后端独立审查；异后端单轮纠偏价值高于同后端多轮。  
**严格计数**：核心比较“异后端单轮 > 同后端多轮”的直接证据来自本元项目，12 个源项目中直接计数为 0。若只统计“独立审查有价值”的相关证据，则有 6 个源项目，但它们不支持 P6 的核心比较。

核心证据（不计入源项目数）：

- Qwen复验证认为 Kimi 单轮异后端审查贡献超过 ChatGPT-5.5 三轮同后端累积贡献，并将 P6 升级至 A-。证据：`reviews/qwen_phase4_reverify_report.md:207`，`:211`，`:248`，`:460`。
- DEV_LOG 记录 HG-0、Kimi、Codex、Qwen 各轮审查时间线。证据：`DEV_LOG.md:58`，`:81`，`:97`，`:127`。

相关源项目证据（支持“独立审查有价值”，但不直接支持“Phase后异后端 > 同后端多轮”）：

- LIT：四轮独立审查覆盖不同类型缺陷。证据：`LIT项目 CLAUDE.md:9`。
- PilotDeck分析：三轮审查逐步修正事实和优先级。证据：`PilotDeck项目 independent_review_round3_report.md:12`，`:201`。
- GitNexus分析：R3明确三轮审查视角互补。证据：`GitNexus项目 GitNexus_独立审查报告_R3.md:93`。
- Evolver分析：DeepSeek+Qwen事实核查高度收敛。证据：`Evolver项目 Evolver_项目闭合记录.md:16`。
- Agent Harness综述：ChatGPT-5.5独立审查发现报告弱点。证据：`Agent Harness项目 independent_review_gpt55.md:147`。
- 形态匹配ETF策略：Kimi/GLM终期双审提出重要修订。证据：`形态匹配ETF策略项目 CLAUDE.md:26`。

**审计结论**：P6 可作为本项目过程规则和高优先 Gate，但不满足“≥3 源项目直接支撑核心比较”的稳定组件门槛。若 Phase 5 写入正文，应标注为“本项目实测强证据 + 多源项目相关证据”，而非“跨源项目已稳定验证”。

## P8：Dynamic Workflow并行执行

**模式状态**：Sp 工具注记。  
**严格计数**：对“并行 workflow 带来帕累托改善”的直接效率测量源项目数为 0。对“多个源项目使用多agent/workflow分析”的相关证据数为 3。

相关源项目证据：

- Agent Harness综述：记录 6-agent 并行工作流方法。证据：`Agent Harness项目 CLAUDE.md:48`。
- PilotDeck分析：记录 8+1 agent workflow 模式。证据：`PilotDeck项目 CLAUDE.md:68`。
- Evolver分析：闭合记录记载 workflow 完成论文分析、代码审计、6维并行、红队和方法论提取。证据：`Evolver项目 Evolver_项目闭合记录.md:14`。

限制：

- 这些项目记录的是“使用了 workflow/多agent”，不是“相对串行流程在质量、成本、时间上同时改善”的测量。
- Phase 4 已将 P8 降为工具注记，理由是 N=1、自评循环、平凡论。证据：`synthesis/phase4_validated_pattern_catalog.md:22`，`:72`。

**审计结论**：P8 不得标为稳定框架组件。仅保留为工具能力注记：拓扑独立、模板同质、可批量验证、N≥3 时可尝试并行，并必须配套异后端审查。

## 总体结论

1. 满足源项目数但仍不能稳定化：P2、P3。原因是 Phase 4 对具体命题强度给出 C+，且存在反例或确认偏误。
2. 不满足源项目数：P1、P5、P6、P8。P6虽经 Qwen 升至 A-，但核心证据来自本元项目，不满足“源项目 ≥3”红线。
3. 已拒绝：P4，不进入框架。
4. Phase 5 若要写入框架正文，应使用三类标签：`稳定组件`、`试行协议`、`工具注记/审查门禁`。按本审计，当前没有一个 P1-P6/P8 模式可无条件标为“跨源项目稳定组件”。

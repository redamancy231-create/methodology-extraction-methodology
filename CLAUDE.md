# CLAUDE.md — 方法论提取方法论 项目宪法

> **项目**: 方法论提取方法论（Methodology Extraction Methodology）
> **版本**: v1.0（项目闭合 — CLOSED）
> **生成模型**: DeepSeek-V4-Pro (via Claude Code CLI shell)
> **阅读注意**: 本文中的 `[[...]]` 为跨项目引用标记（指向同一工作区内的其他项目），在 GitHub 上不会解析为链接。项目内文件的引用使用标准相对路径。
> **生成日期**: 2026-06-16
> **最后更新**: 2026-07-24（语料扩展至22 + 分类修正 + 多轮异后端审查修复）
> **框架角色**: AI协作项目全生命周期框架 v1.5.1 的 Protocol 3（首次真实试跑）
> **闭合后维护**: 2026-07-23 语料从12扩展至19（后增至22），2026-07-24 经GPT-5.6-Sol两轮异后端审查修复19+3项发现。本 CLAUDE.md 中的 v1.5.1 引用为闭合时刻的历史快照。
> **项目规模**: M-tier（~1周，≤20 loops；已用15 loops）
> **已执行审查**: 10 轮正式审查（HG-0 Codex 7.2 / Phase2 Kimi 5.9 / Phase3 Codex 6.2 / Phase4 Qwen 5.5 / Phase5 Codex 6.1 / Phase5 Qwen 6.3 / Phase6 Kimi事实核查 / Phase7 Qwen 终期闭合 6.8 / Phase7.5 GLM-5 方法论价值 5.8 / Phase7.6 Codex 实用完整性 7.7 GO ✅）+ 1 次异后端复编码（Phase 3.5 Codex复编码）

---

## 1. 项目定义

**这是什么**：一个元层次方法论项目——从22个源项目（含自有AI协作项目、外部开源项目、学术压力测试）中系统提取方法论模式，形式化为可复用的"方法论提取框架"。初始集n=12（Phase 1-6基础），扩展至22（含2026-07-23重组+外部压力测试+追加提取）。

**双重目的**：
- **产出层**：方法论提取框架文档（.md + .json）——项目筛选checklist、提取流程标准化、采纳/不采纳决策模板、跨项目模式识别、独立审查SOP
- **测试层**：作为AI协作项目全生命周期框架 v1.5.1 的 Protocol 3 首次端到端试跑——每层框架组件接受实战检验，试跑数据写回框架成熟度评估表

**递归观察**：父框架（AI协作项目全生命周期框架）作为22个源项目之一被分析——框架既是操作手册（工具）也是提取对象（样本），形成样本内递归观察。注意：父框架 ≠ 当前项目（方法论提取方法论）；当前项目不在22个源项目清单中。递归观察不能替代独立验证。

---

## 2. 当前状态

- **版本**: v1.0（项目闭合）
- **阶段**: Phase 8 完成 → **CLOSED**
- **状态**: 闭合
- **闭合适配器**: 全部交付物产出 ✅ + 独立审查通过 ✅（Phase 7.6 Codex 7.7/10 ≥7.0）+ Retrospect 产出 ✅（3 失效 + 3 意外）

---

## 3. 证据源

### 已读（本阶段）
- [[AI协作项目全生命周期框架.md]] — 主框架文档 v1.5.1（2671行，操作手册）
- [[框架级成熟度评估表.md]] — 框架成熟度基线（~30%部分验证）
- [[v1.5.1冻结期_待执行协议清单.md]] — Protocol 3 规范 + C1-C8预登记标准
- [[methodological-review-sop.md]] — 独立审查SOP v1.0.3
- [[meta-audit-checklist.md]] — 67项元审查清单
- [[meta_methodology_extraction_todo]] — 方法论提取TODO memory
- 初始集12个源项目的 CLAUDE.md（通过 CLAUDE-md-generation 项目批量生成；当前语料已扩展至22）

### 待读（后续阶段）
- 7份已有方法论提取产物（GitNexus/PilotDeck/Small Scale/Evolver/并购重组/Agent Harness/ETF）
- 框架审查链全件（5后端跨5CLI house）
- 各项目闭合记录和终期总结

### 高风险未确认项
- 12个项目中 claude-code-ultimate-guide 无独立审查报告（轻量项目，可能跳过）
- 多模型对照实验处于搁置状态（方法论资产冻结在协议文档中）
- BDC2026 为活跃项目（非闭合），提取时需注意状态差异

---

## 4. 快速恢复

### 第一次读什么
1. 本文件（CLAUDE.md）— 项目宪法
2. `project_spec.md` — S1-S10完整Spec
3. `DEV_LOG.md` — 当前进度和最近操作
4. `spec/success_criteria.md` — 成功标准和Protocol 3预登记指标

### 常用命令
```bash
# 项目文件计数
find [项目根]/方法论提取方法论 -name "*.md" | wc -l

# 检查Dev Log最新条目
tail -30 [项目根]/方法论提取方法论/DEV_LOG.md

# 检查loop计数
grep -c "## Loop" [项目根]/方法论提取方法论/DEV_LOG.md

# 验证md/json双件配对
ls [项目根]/方法论提取方法论/framework_output/
```

---

## 5. 停止条件（S4红线）

1. 任意源项目的 CLAUDE.md 缺失或不可读 >3个 → 暂停评估
2. 框架自身 CLAUDE.md 或主文档损坏/不可读 → 立即停止
3. 独立审查评分 <5.5/10 → NO-GO，不闭合（分级：<5.5 NO-GO / 5.5-7.0 修订后GO / ≥7.0 GO）
4. 实际loops超过25（超出预算25%）→ 触发HG-1重规划
5. Phase 6递归自检超过2 loops未收敛 → 记录限制，继续前行

---

## 6. 目录地图

```
[项目根]/
├── CLAUDE.md                          ← 本文件（项目宪法）
├── project_spec.md                    ← S1-S10编译Spec
├── DEV_LOG.md                         ← Dev Log主时间线
├── spec/                              ← Spec组件
│   ├── project_status.md              ← S1 项目状态
│   ├── reference_files.md             ← S2 关键文件路径
│   ├── key_technical_details.md       ← S3 技术约定
│   ├── success_criteria.md            ← S5 成功标准 + Protocol 3 C1-C8
│   ├── evaluation_plan.md             ← S6 评估计划
│   └── risk_register.md               ← S8 风险登记
├── explorations/                      ← Phase 2: 三批探索报告
├── synthesis/                         ← Phase 3/4/6: 对比矩阵+模式+递归自检
├── framework_output/                  ← Phase 5: 主交付物
├── reviews/                           ← Phase 7: Codex审查+回应
├── archive/                           ← Phase 8: 终期总结+评估+Retrospect
├── memory/                            ← 跨项目写回
├── prompts/                           ← 关键prompt归档
└── dev-logs/                          ← Dev Log分支文档
```

---

## 7. 版本脉络

| 版本 | 日期 | 关键事件 |
|------|------|---------|
| v0.1 | 2026-06-16 | Phase 1初始化，L0 Spec定义，HG-0审批通过（Codex 7.2/10） |
| v0.2 | 2026-06-16 | Phase 2-4.5完成。4轮异后端审查。project_spec+plan同步更新。G1-G7遗留修复 |
| v0.3 | 2026-06-16 | Phase 5-6关闭。框架v0.1试行版（.md+.json经37项审查发现修正）+ Codex (6.1) + Qwen (6.3) + Kimi Phase6 + Phase 6 Mini-extraction（3观察+Kimi核查修正4项）。审查链：3后端×3Phase，37项发现，0 CRITICAL |
| v0.4 | 2026-06-16 | Phase 7 系列关闭。Phase 7 Qwen 终期闭合审查 (6.8) + Phase 7.5 GLM-5 方法论价值审查 (5.8) + Phase 7.6 Codex 实用完整性重审 (7.7 GO ✅，首个≥7.0)。5+5+8+8=26 项 Phase 7 系列发现，CRITICAL/MAJOR 全部修正。框架文档 899 行。Phase 8 就绪。 |

---

## 8. OPEN项

| ID | 状态 | 描述 |
|----|------|------|
| OPEN-1 | ✅已关闭 | 12个源项目全部提取完成（Phase 2）。BDC2026按活跃边界案例处理，降低归纳权重 |
| OPEN-2 | ✅已关闭（HG-1） | 决策：选项B Mini-extraction（1 loop）。聚焦"框架开发史有什么是12源项目没提供的独特证据"，产出为Phase 6附录非方法论片段 |
| OPEN-3 | ✅已关闭（HG-1） | 决策：选项B定制5轴终期prompt + Codex CLI主力审查。第一轮<7.0则启动第二后端(Kimi/Qwen)追加 |

---

## 9. 核心资产

- **方法论提取框架 v0.1 试行版（Phase 5 已产出）**：5组件全标试行协议——项目筛选checklist / 提取流程标准化 / 采纳决策模板 / 跨项目模式识别 / 独立审查SOP。`framework_output/main/方法论提取框架_v0.1_trial.{md,json}`。G5审计：无一组件达稳定门槛
- **7次已有提取对比矩阵（Phase 3）**：格式演进、6项共同元素、系统性缺失；完整逐格矩阵 + Codex复编码对比
- **跨项目模式目录（Phase 4）**：8模式经对抗验证——0达A/1达A-（P6）/1达B-（P5）/3达C+/1标Sp/2被拒。含Qwen复验证修正
- **递归自检报告（Phase 6，已完成）**：3项观察（均不进入模式目录），Kimi事实核查4项修正。`synthesis/phase6_mini_extraction.md`

---

## 10. 方法论转化地图

| 源项目 | 提取状态 | 对本项目的输入 |
|--------|---------|---------------|
| 形态匹配ETF | CLAUDE.md嵌入 | 18版本迭代模式、Bug教训清单、负迁移检验 |
| 并购重组案例 | Playbook v1.2 | 八阶段流水线、开卷/盲答对照、Phase 0 kill-test |
| 多模型对照实验 | 协议冻结 | 预登记实验设计、污染三层诊断、治理审计 |
| LIT | 4轮bug-hunt | 14类目评分框架、对抗式阅读checklist |
| Agent Harness | 分析报告嵌入 | 6-agent并行工作流、红队攻击清单 |
| Small Scale | 15条转化文档 | 优先级分层、证据等级L1-L4 |
| PilotDeck | 独立提取+缺口矩阵 | 最全面的提取结构、三阶段集成路线图 |
| GitNexus | 四维度A/B/C/D | 行为/警示双重视角、项目映射 |
| Evolver | 报告§VI嵌入 | 5可采纳+5反模式、闭合记录 |
| CLAUDE-md-generation | 元项目 | 批量CLAUDE.md生成流程、质量门 |
| BDC2026 | 活跃（非闭合） | Walk-Forward验证、形态匹配复用 |
| **AI协作框架自身** | **递归自检对象** | v1.0→v1.5.1开发史、5后端审查链 |

---

## 11. 跨项目关联

- [[project_ai_framework]] — 既是操作手册也是Phase 6提取对象
- [[meta_methodology_extraction_todo]] — 本项目的需求来源
- [[project_claude_md_generation]] — 提供了12个项目的CLAUDE.md快速入口
- [[feedback_md_json_pairing_analysis]] — md/json双件角色分析（本项目所有产出遵循双件规范）
- [[feedback_workflow_codex_crosscheck]] — Phase 7 Codex交叉验证的规范依据
- [[reference_codex_cli_independent_review]] — Codex CLI调用模式

---

## 12. 已知陷阱

- **"Claude" = CLI壳非后端模型**：本项目生成模型为DeepSeek-V4-Pro，所有产出header须标注
- **冻结期≠停滞**：框架v1.5.1冻结但仍可执行三协议，本项目正是Protocol 3执行
- **M-tier不是S-tier**：不能偷懒降级——Protocol 3要求真实试跑非走过场
- **递归≠无限循环**：Phase 6严格限2 loops，超限触发S4红线
- **Dev Log维护是硬要求**：每个loop结束必须记录，遗漏率<30%是Protocol 3预登记标准

---

## 13. 更新协议

### 何时更新本文件
- S1-S10任一组件变更 → 更新对应spec/文件 + 本文件版本号
- 新增OPEN项 → 追加§8
- 新增跨项目关联 → 追加§11
- 发现新陷阱 → 追加§12
- Phase完成 → 更新§2状态 + DEV_LOG.md

### 谁更新
AI自动维护（L2 Loop内），HG-1时人工确认关键变更。

---

*本文件由 DeepSeek-V4-Pro (via Claude Code CLI) 生成，遵循 [[feedback_generated_files_model_provenance]] 规范*

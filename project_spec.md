# 项目Spec（S1-S10编译）— 方法论提取方法论

> **版本**: v1.0（项目闭合 — CLOSED）
> **生成模型**: DeepSeek-V4-Pro (via Claude Code CLI shell)
> **生成日期**: 2026-06-16
> **最后更新**: 2026-06-16 20:22（Phase 8 Retrospect 完成，项目闭合）
> **框架层级**: L0 Spec — 跨任务不变量的项目宪法
> **元注**: 本 Spec 的初始版本（v0.1）和初始执行计划未经独立模型审查——这是一个已记录的方法论失误，正好印证了本项目自身正在提取的"项目启动前缺独立审查"模式。详见 §0。

---

## §0: 方法论自我记录（2026-06-16 追加）

**已发生的方法论失误**：项目初始 plan 和初始 Spec（v0.1）在 HG-0 时由用户直接批准启动，未经过异后端模型独立审查。HG-0 的 Codex CLI 审查是在 Phase 1 文件已创建后补做的（审的是已写完的 Spec 而非 plan）。这意味着：
- Phase 结构设计、loop 预算、M-tier 选择等关键决策未经过独立质疑
- 后续 Phase 2.5/3.5 的"审查→修正"循环本质上是在补救这个初始盲点
- 这是本项目提取的"Premise 质疑系统性缺失"模式（跨批共同模式#1）的活体演示

**已发生的适应性调整**：
- Phase 2 原计划 5 loops → 实际 3 个并行 Workflow 完成（1个 orchestration 周期）
- 涌现了计划外的"审查→修正"子阶段（2.5: Kimi审查修正, 3.5: Codex审查修正+异后端复编码）
- 独立审查从"Phase 7 一次"演变为"每 Phase 后一次"的持续模式（HG-0/Kimi/Codex/Codex复编码，共计4轮）
- 实际 loop 消耗约为计划的一半（并行 Workflow 大幅压缩了串行迭代）

---

## S1: 项目状态

- **项目名称**: 方法论提取方法论（Methodology Extraction Methodology）
- **当前版本**: v1.0
- **阶段**: Phase 8 完成 → **CLOSED**
- **状态**: 闭合
- **规模**: M-tier（≤20 loops；实际使用15 loops）
- **框架使用强度**: B-tier → 实际执行升级为接近 C-tier（10轮异后端审查，远超B-tier预设）
- **已执行审查**: 10轮异后端审查（HG-0 Codex / Phase2 Kimi / Phase3 Codex / Phase4 Qwen / Phase5 Codex / Phase5 Qwen / Phase6 Kimi / Phase7 Qwen / Phase7.5 GLM-5 / Phase7.6 Codex）
- **闭合触发**: 全部满足（交付物完整 + 独立审查 7.7≥7.0 + Retrospect 3失效+3意外）
- **详见**: `spec/project_status.md`

## S2: 关键文件路径

- **项目根**: `[项目根]/`
- **源项目根**: `*`（12个项目，排除`_tools`）
- **框架主文档**: `[父框架项目]/AI协作项目全生命周期框架.md`
- **框架成熟度表**: `[父框架项目]/框架级成熟度评估表.md`
- **框架协议清单**: `[父框架项目]/_protocols-and-tools/v1.5.1冻结期_待执行协议清单.md`
- **项目索引**: `CLAUDE-md-generation项目 PROJECTS_AGENT_INDEX.md`
- **详见**: `spec/reference_files.md`

## S3: 技术约定

- **双格式**: 所有正式产出 .md + .json 配对（镜像框架约定）
- **证据分类**: 使用 [S]/[E]/[I]/[J]/[Sp] 标签（按框架§9.6）
- **语言**: 方法论正文用中文；JSON字段名/代码用英文
- **生成模型**: DeepSeek-V4-Pro (via Claude Code CLI shell)
- **审查模型**: Codex CLI (ChatGPT-5.5 backend) — 用于独立审查
- **编码**: UTF-8（PYTHONIOENCODING=utf-8）
- **路径**: 正斜杠
- **详见**: `spec/key_technical_details.md`

## S4: 红线（停止条件）

1. 源项目**最小证据包不足** >3个 → 暂停评估（不仅看CLAUDE.md，看最小证据包整体）
2. 框架自身 CLAUDE.md 或主文档损坏/不可读 → 立即停止
3. 独立审查评分 **<5.5/10** → NO-GO，不闭合（分级：<5.5 NO-GO / 5.5-7.0 修订后GO / ≥7.0 GO）
4. 实际loops >25（超出预算25%）→ 触发HG-1重规划
5. Phase 6递归 >2 loops不收敛 → 记录限制继续前行；**递归自检不得反向改写Phase 4结论，不得成为新增核心组件入口（除非HG-1批准）**
6. **新增**：<8/12项目证据卡完成 → 不进入Phase 4
7. **新增**：5组件中任一组件无 ≥3个项目证据支持 → 不得标为稳定框架组件
8. **新增**：已有提取产物格式差异无法映射 → 先做中间表示，不直接综合

## S5: 成功标准

**主要**: 方法论提取框架文档（.md + .json）完成，覆盖全部5组件
**次要**: 项目评估分析（.md + .json）完成
**三级**: Retrospect报告 ≥1失效 + ≥1意外，写回框架成熟度评估表
**验证**: 独立审查（Codex CLI）**≥7.0/10**（按 Codex HG-0 M5 分级：<5.5 NO-GO / 5.5-7.0 修订后GO / ≥7.0 GO）
**详见**: `spec/success_criteria.md`

## S6: 评估计划

- **AI自评**: 每phase结束对照deliverables checklist
- **独立模型审查**: **每Phase后执行**（实际已执行4轮：HG-0 Codex / Phase2 Kimi / Phase3 Codex / Phase3.5 Codex复编码），非原计划仅在Phase 7执行一次。这是项目执行中涌现的适应性模式
- **人工审查**: HG-0（已完成）/ HG-1（Phase 4/5/7/8）/ HG-3（闭合）
- **框架指标追踪**: C1-C8全量追踪（DEV_LOG.md）
- **详见**: `spec/evaluation_plan.md`

## S7: 重启阈值

N/A（项目为活跃状态，非搁置恢复）

## S8: 风险登记

| ID | 风险 | 影响 | 概率 | 缓解 | Plan B | 实测 |
|----|------|------|------|------|--------|------|
| R01 | 12源项目太多，loop预算不足 | M | M→**L** | CLAUDE.md快速入口；分批并行Workflow | 减至8个 | **未触发** — 并行Workflow压缩了串行成本 |
| R02 | 递归自检造成无限回归 | M | L | 严格限定2 loops | 放弃递归角度 | Phase 6 待测 |
| R03 | Windows环境文件读取失败 | M | M→**L** | 绝对路径+正斜杠 | 跳过不可访问项目 | **未触发** |
| R04 | 独立审查<5.5/10 | H | L-M | 每Phase后独立审查+审查→修正循环 | 记录为Retrospect失效 | **触发但缓解** — Kimi 5.9/Phase3 Codex 6.2，均经修订后提升 |
| R05 | Dev Log维护开销超预算 | L | M | 单时间轴最小化Dev Log | 降为纯手动 | **可控** |
| **R06** | **提取者效应** — 同一模型编码+填模板，制造虚假一致性 | **H** | **H→已证实** | 异后端复编码（Phase 3.5已执行） | 关键维度强制双编码 | **Phase 3.5实测22%显著分歧率，独有特征~65% inflation** |
| **R07** | **计划未审** — 初始plan和Spec未经独立审查即执行 | **M** | **H→已发生** | 在§0中诚实记录；后续Phase前强制异后端预审 | — | **已发生**，补救措施为持续审查循环 |

**详见**: `spec/risk_register.md`

**详见**: `spec/risk_register.md`

## S9: 可复现性声明

- **项目类型**: 探索/方法论（对应框架§9.1：工程/探索档）
- **Python**: 3.12+（仅在需要脚本时使用；主要为markdown分析）
- **数据**: 所有源项目在本地磁盘可访问（Windows 工作区）
- **关键依赖**: 无，除 Claude Code CLI shell + Codex CLI 用于审查
- **随机种子**: N/A（无ML组件）
- **会话记录**: DEV_LOG.md 全程追踪

## S10: 命名约定

- **文件名**: `{主题}_{描述}.{md|json}`，下划线分隔
- **版本标签**: `v{主}.{次}` 用于交付物版本
- **目录名**: 英文小写+连字符，中文用汉字
- **日期格式**: YYYY-MM-DD 统一

---

*本文件由 DeepSeek-V4-Pro (via Claude Code CLI) 生成*

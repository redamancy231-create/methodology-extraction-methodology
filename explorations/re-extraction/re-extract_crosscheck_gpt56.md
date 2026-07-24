# CrossCheck 独立方法论特征重提取与交叉核验

## 独立性声明与口径

- 本证据卡由 GPT-5.6-Sol 独立完成，未读取或引用 DeepSeek 的既有证据卡。
- 第一层证据为提示词内嵌的原作者文件：`README.md`、`ARCHITECTURE.md`、全局级 `CLAUDE.md`、`CONTRIBUTING.md`。
- 第二层证据为 2026-07-24 对源仓库、Fork、PR、提交、Actions、文件树和仓库评估报告所做的交叉核验。
- 文档自述与仓库运行痕迹冲突时，优先采用可复核的仓库事实，并保留冲突说明。

```yaml
项目名称: CrossCheck
项目类型: 多模型 AI 编码工作流与 Shell 脚本工具集（非 npm CLI）
源作者: sburl (Spencer Burleigh)
源仓库: https://github.com/sburl/CrossCheck
分析日期: 2026-07-24
提取模型: GPT-5.6-Sol (via Codex CLI)
证据等级: B

C1_项目基础信息: ✅
C2_架构组织: ✅
C3_设计意图: ✅
C4_开发流程: ⚠️
C5_AI协作方法论文档: ⚠️
C6_独立审查: ⚠️
C7_闭环修复: ✅
C8_数据溯源: ⚠️

可提取组件数: 8/8
提取层级: 主要提取
```

## 总结性结论

CrossCheck 的核心是一套把 AI 编码规范转化为可执行约束的治理方法：在功能分支给予代理较高自由度，在提交、推送和合并边界叠加 hooks、测试、CI、异模型审查与服务端规则；先执行便宜且确定的检查，再执行昂贵的语义审查；最后通过周期性仓库评估把问题回写为脚本、测试、文档或新门禁。

该方法论在设计文档层面完整，实际仓库也存在 hooks、测试脚本、Actions 工作流和三轮仓库评估记录。但最强主张未被全部运行证据支持：抽样合并 PR 未发现独立审批，多个 PR 由提交者自行合并；2026-07-24 的夜间 Quality Gates 连续失败；若干量化比例和跨模型效果没有实验数据。因此可把 CrossCheck 视为结构化 AI 开发治理框架的强案例，但不能直接把 human-level quality、所有层均不可绕过、独立身份审查已稳定执行视为已验证结果。

## 关键交叉核验

1. **项目类型修正**：提示词称其为 npm CLI，但当前主分支没有 `package.json`；递归文件树发现 55 个脚本型文件，均为 `.sh`。更准确的类型是文档、skills、git hooks 与 Shell 脚本组成的多模型 AI 编码工作流工具集。
2. **日期口径拆分**：README 自述 `Created: 2026-01-30`，可视为内容或项目内部起始日；GitHub 源仓库实际创建于 2026-02-12，主分支首个提交为 2026-02-13。
3. **规模修正**：截至 2026-07-24，主分支为 95 个提交；PR 共 152 个，其中 7 个 open、145 个 closed、92 个已合并。作者分布为 `sburl` 134、`sburl-bot` 12、`dependabot[bot]` 6，因此约 149 PR 已过时，全部作者自提也不准确。
4. **质量基础设施存在**：仓库有 5 个 active Actions 工作流、hook 行为与安装测试脚本；截至核验时 Actions 历史运行数为 701。
5. **门禁健康度不足**：2026-07-24 最新 Security Gates 夜间运行成功，Quality Gates 夜间运行失败；本次看到的 2026-07-15 至 2026-07-24 最近记录中，Quality Gates 连续失败。最新失败项包括 Mirror Drift Check、Script Mirror Audit、Documentation Metadata；Hook Behavior Tests 成功。
6. **独立审查与实践有落差**：抽样 PR #1、#75、#133、#137、#148、#149 均未发现 review 或 approval；其中 #1、#133、#137、#149 在创建后约 42 秒、119 秒、7 秒、21 秒即合并，多为提交账号自行 merge。该样本不能代表全部 PR，但足以说明独立身份审批未被仓库历史充分证明。
7. **Fork 无源项目改写**：`redamancy231-create/CrossCheck` 与上游 `main` 比较为 identical，ahead 0、behind 0、changed files 0。Fork 作者的架构分析和 Swiss Cheese 理论对照属于仓库外二次分析。

## C1 项目基础信息：✅

- 名称、源作者、源仓库和 MIT License 均可确认。
- README 的项目起始日、GitHub 仓库创建日、首个提交日可以分别追溯，不能混写。
- README 最后标注更新为 2026-02-26；主分支最新提交为 2026-06-11；仓库最近 push 为 2026-07-10。
- 宣传语中的质量水平是目标性表述，不属于已证明的基础事实。

## C2 架构组织：✅

- `ARCHITECTURE.md` 描述 PLAN、BUILD、VERIFY、REVIEW、SHIP、IMPROVE 六阶段。
- 文档覆盖职责分离、连续验证、多层审查、自改进、hooks、GitHub protection、skills、开发流、安全边界、扩展性、性能和未来架构。
- 仓库目录与文档相互对应：`claude/`、`codex/`、`gemini/`、`git-hooks/`、`scripts/`、`skill-sources/`、`docs/`、`.github/workflows/`。
- 限制：这是规范性高层架构，不是完整的代码级依赖图。

## C3 设计意图：✅

可明确提取的设计选择包括：

1. 不依赖代理记忆规范，而把规范转成 hooks、测试、CI 和服务端规则。
2. 使用机制不同、失效相关性较低的多层防线，即 Swiss Cheese Model。
3. 功能分支宽松，主分支严格，把最强控制放在高影响边界。
4. 快速检查先行，深度审查后置。
5. Builder、Reviewer、Automation、Orchestrator 职责分离。
6. 周期性评估最近 PR，把重复问题和流程摩擦转成改进 PR。
7. 文档公开第三模型边际收益、生产 CLI 权限和 UI 视觉闭环等未决问题。

但 BUILD、VERIFY、REVIEW、SHIP 分别捕获约 60%、25%、14%、1% 问题的比例没有样本和计算方法；跨实验室审查更精确、不同训练等于不同盲点等属于设计假设，不是受控实验结论。

## C4 开发流程：⚠️

- `CONTRIBUTING.md` 明确要求分支开发、PR-only、范围单一、验证命令、风险与回滚说明、依赖顺序和约定式提交。
- 仓库确实大量使用 PR，并运行 CI 和夜间工作流。
- 主分支 95 个提交、92 个已合并 PR，与 squash 或单提交合并模式大体相容。
- 降级原因：抽样 PR 未见 approval，多由提交者自行合并；未认证访问无法读取实际 branch protection 配置；PR 作者也包含 bot 和 Dependabot。
- 结论：流程被设计并频繁使用，但所有门禁按设计持续执行未获证明。

## C5 AI 协作方法论文档：⚠️

- 存在 `CLAUDE.md`，但标题和正文明确说明它是 **Global** 工作流，并允许各项目另设项目级 `CLAUDE.md`。
- 文件包含 Autonomous First、Zero Trust、Feature Branches、Test-First、Skill-First、Clean Up、Hard Cutover 等原则，并指向 CODEX、skills 和 rules。
- 项目还有 `CODEX.md`、`CODEX-PROMPTS.md`、`QUICK-REFERENCE.md` 和各模型目录，说明 AI 协作方法是产品主体。
- 不能把全局模板误判为 CrossCheck 的项目专用代理说明，因此标记为 `⚠️`。

## C6 独立审查与质量保障：⚠️

- 文档列出 pre-commit、commit-msg、post-commit、post-checkout、pre-push、post-merge 六个 hooks。
- 仓库存在 hook 行为测试、安装测试以及质量、安全、发布、Dependabot 工作流。
- 最新安全扫描与 Hook Behavior Tests 成功，说明部分自动保障真实运行。
- 降级原因：最新 Quality Gates 非绿色，镜像一致性、脚本镜像审计和文档元数据检查失败；抽样 PR 未出现独立 review 或 approval。
- 因此自动检查与测试存在是强证据，异模型或不同身份审查构成稳定合并门禁则证据不足。

## C7 闭环修复：✅

设计文档给出 `Review → Issues Found → Fix → 再审 → Approve` 循环，以及周期性仓库评估循环。更重要的是，`docs/repo-assessment-pass-1.md` 至 `pass-3.md` 提供了实际链条：

1. Pass 1 诊断无引用脚本、PR #46 cron 风险和 PR #45 telemetry 配置健壮性问题。
2. 修复包括删除死脚本、为损坏的 Gemini JSON 增加备份与恢复，并落到 PR #51、#52。
3. 验证包括镜像检查继续通过、Pass 2 重扫未发现新危险命令漂移、Pass 3 再查高风险 shell 操作。

这构成可辨识的诊断、修复、验证闭环。但报告仍保留权限、临时目录、chmod、备份权限等待办；`docs/incidents/` 主要是模板；当前夜间 Quality Gates 的持续失败也表明并非所有问题都已闭合。

## C8 数据溯源：⚠️

- 可追溯部分：文档有 Created、Last Updated、文件引用、PR 编号、脚本名、命令和灵感来源；评估报告把发现关联到具体脚本、PR #45、#46、#51、#52 和验证命令。
- 不足部分：README 内部创建日与平台创建日口径不同；捕获率、human-level quality、跨模型收益缺少原始数据和基线；每 3 个 PR 自动评估的持续执行不能由同日三份 pass 报告单独证明；`.claude/assessment-history.txt` 为空。
- 文档头部更新时间停留在 2 月或 3 月，而仓库活动延续到 7 月，元数据新鲜度有限。

## 原作者与 Fork 作者归属对照

| 维度 | 原作者 sburl 的可确认贡献 | Fork 作者的可确认贡献 | 归属结论 |
|---|---|---|---|
| 源代码与脚本 | hooks、安装脚本、测试脚本、skills、多模型目录、Actions | Fork 无领先提交或修改文件 | 源项目实现归原作者 |
| README 方法论 | 自主循环、结构约束、分层防线、跨模型审查、主分支堡垒 | 后续分析 | 原始方法表述归原作者 |
| Swiss Cheese Model | 原 README 明确命名、解释并绘制多层防线 | 理论对照、解释或扩展 | 理论引入项目归原作者；二次比较归 Fork 作者 |
| 架构文档 | 六阶段、组件交互、数据流、安全、扩展性、未来架构 | 代码架构分析 | 原文档归原作者；分析结论归 Fork 作者 |
| AI 工作流模板 | 全局 CLAUDE、CODEX 资料、skills、rules | 无仓库内改写 | 模板归原作者，且必须标注为全局级 |
| 开发治理记录 | PR、提交、Actions、repo assessment | 无 Fork 内变更 | 一手运行痕迹归源仓库 |
| 本次证据卡 | 不适用 | Fork 背景仅用于划定归属边界 | GPT-5.6-Sol 独立重提取 |

## 可复用方法论

1. 把规范变成 hooks、CI、规则集和测试等不可忽略的执行点。
2. 以风险边界分配自由度：功能分支宽松，主分支严格。
3. 按成本排序验证：格式与秘密扫描先行，行为测试其次，语义与架构审查最后。
4. 让权限层、文本扫描、测试、模型审查和身份规则的失效模式尽量不相关。
5. 分离生产者、审查者和执行器，避免同一主体同时编写、批准和绕过门禁。
6. 要求发现关联具体文件或 PR，修复后必须重跑、复扫或回归测试。
7. 把工作流本身纳入迭代，定期检查镜像漂移、重复问题和缺失自动化。
8. 区分设计主张与运行事实：文档说应该如何，不等于仓库证明实际一直如此。

## 最终裁决

CrossCheck 最有价值的方法论组合是结构性执行、边界式信任、多层异质防线和周期性自评。架构、设计意图和闭环修复证据较强；开发流程、项目级 AI 文档、独立审查和数据溯源存在缺口或冲突。

因此本次判定为 **B 级证据、8/8 组件有痕迹、主要提取**，不提升为完整提取。若要达到 A 级，至少还需：核验实际 branch protection；全量统计 PR reviews、approvals 与合并身份；恢复夜间 Quality Gates 为持续绿色；为捕获率和跨模型收益提供可复现实验与原始数据；持续记录 assessment 触发历史和真实 incident 闭环。

## 证据索引

| 编号 | 证据 |
|---|---|
| P1 | 提示词内嵌 `README.md`：The Idea、Swiss Cheese Model、Layered Enforcement、Autonomous Loop、Core Principles、Setup |
| P2 | 提示词内嵌 `ARCHITECTURE.md`：六阶段、架构原则、组件交互、数据流、安全模型、性能与未来架构 |
| P3 | 提示词内嵌全局级 `CLAUDE.md` |
| P4 | 提示词内嵌 `CONTRIBUTING.md` |
| V1 | 2026-07-24 GitHub 源仓库元数据、主分支提交分页与递归文件树 |
| V2 | 2026-07-24 全量 PR 列表聚合及 6 个 PR 的 review 抽样 |
| V3 | 2026-07-24 Actions workflows、最近运行和失败 jobs |
| V4 | `docs/repo-assessment-pass-1.md` 至 `pass-3.md` 与 incidents 目录 |
| V5 | 上游与 `redamancy231-create/CrossCheck:main` compare，结果 identical |

## 核验限制

- 未使用认证 GitHub API，无法读取 branch protection 详细配置。
- PR 独立审查判断基于全量 PR 元数据与 6 个代表性 PR 的 review 抽样，不等于逐一审计全部 152 个 PR。
- 未在本地完整安装 CrossCheck 并执行 bootstrap、hooks 和全部工作流；运行状态依据源仓库 Actions 与测试文件。
- 本证据卡按 2026-07-24 快照成立，后续提交、PR 和工作流修复可能改变 C4、C6、C7、C8 的判定。

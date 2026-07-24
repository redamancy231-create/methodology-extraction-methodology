# ml-quant-trading 方法论特征重提取证据卡

```yaml
项目名称: ml-quant-trading
项目类型: 量化交易系统 + 学术论文
源作者: Yimin Du (initial-d)
源仓库: https://github.com/initial-d/ml-quant-trading
arXiv: arXiv:2507.07107
Fork: https://github.com/redamancy231-create/ml-quant-trading
分析日期: 2026-07-24
提取模型: GPT-5.6-Sol (via Codex CLI)
证据等级: B

C1_项目基础信息: "⚠️ 名称、作者、仓库、论文、MIT License、2025 年论文及 v0.1.0 发布均可识别；但内联材料没有首末提交日期、逐次版本时间线或完整提交记录，因此开发周期只能粗粒度追溯。"
C2_架构组织: "✅ README 同时给出五阶段数据流、默认与可选路径、模块职责、目录树，以及论文小节到代码模块和测试的映射，架构和组织可直接提取。"
C3_设计意图: "✅ 材料明确记录 validation-first、clean/fork-friendly/end-to-end 等目标，并披露简单基线、交易成本、负结果、数据限制、非目标及默认/可选模块边界，能够还原主要研究假设和设计权衡。"
C4_开发流程: "⚠️ CONTRIBUTING 规定本地测试、ruff、文档更新和 CI 门禁；GitHub Actions、tag release、外部 PR 和 Discussions 也可追溯。但没有完整 commit 时间线、明确分支命名/合并策略或 review 规则。"
C5_AI协作方法论文档: "❌ 未提供 CLAUDE.md 或等价的项目级 AI 协作规范。Fork 计划反而明确将 CLAUDE.md 视为个人工具配置，不应向上游提交；GPT 审查痕迹不能替代可复用的方法论文档。"
C6_独立审查: "✅ pytest、ruff、GitHub Actions、Docker 测试命令、论文模块到测试的映射，以及外部 PR review 共同形成明确质量保障。局限是未提供正式独立审查报告或 CI/test 运行结果。"
C7_闭环修复: "⚠️ 可见 audit 工具、PR review、文档修订和验证优先的闭环能力；Fork 的 contribution_plan v1.1 也说明计划经审查后调整。但内联材料没有给出一个具体项目缺陷从诊断、修复到复测通过的完整实例，故只能部分提取。"
C8_数据溯源: "✅ 数据源、访问方式、不再分发原始数据、按需下载、synthetic 固定种子、验证产物和 metadata.json 均有说明，论文—代码—测试也有映射。第三方数据缺少快照、版本号或哈希，仍存在外部数据漂移风险。"

可提取组件数: 7/8
提取层级: 主要提取
```

## 一、总体结论

ml-quant-trading 是一个文档化程度较高、以可复现验证为导向的研究型量化工程项目。仅凭内联材料，已经能够提取其项目身份、模块架构、研究意图、开发门禁、自动化质量保障及数据来源链路。最强证据来自原作者 README 与 CONTRIBUTING：二者不仅说明“做什么”，还说明默认流水线、可选模块、验证边界、数据限制、测试入口和贡献门槛。

本项目尚不能判为“完整提取”，主要有三项缺口：

1. 没有项目级 AI 协作方法论文档，C5 不成立。
2. Git 历史只提供概览，缺少精确开发周期、分支策略和逐 PR/commit 的过程证据。
3. 没有明确、可逐步核验的“缺陷诊断 → 代码修复 → 测试/复现验证”案例，因此 C7 只能部分成立。

因此，本证据卡给出 **B 级证据、7/8 个组件可提取、提取层级为“主要提取”**。B 级而非 A 级的原因不是项目材料贫乏，而是本次约束要求只使用内联内容：被 README 引用的 research_card、reality_check、architecture、reproducing_paper、CHANGELOG、实际测试代码、CI 日志和 Git/PR 明细均未直接展开，不能把“链接存在”视为“内容已经核验”。

## 二、逐组件详细分析

### C1 项目基础信息：⚠️ 部分完整

**原作者证据**

- 项目名称和研究主题明确：Machine Learning Enhanced Multi-Factor Quantitative Trading，并注明横截面组合优化与偏差修正。
- 作者明确为 Yimin Du，论文标识为 arXiv:2507.07107，年份为 2025。
- 源仓库、MIT License、Python 版本门槛、v0.1.0 首个公开研究基线发布均可识别。
- README 引用 CHANGELOG、release、roadmap 和论文复现文档，表明项目具有版本化和研究发布意识。
- Git 概览说明项目以单一主要作者为主，并有少量外部贡献者。

**不足与边界**

- 没有首个提交日期、最近提交日期、版本发布日期或逐版本变更条目。
- “2025 年论文 + v0.1.0 + 2026-07-24 分析日期”只能建立粗略时间锚点，不能还原完整开发周期。
- CHANGELOG 被声明存在，但其正文未内联，不能据此推断具体演进过程。

**Fork 归属**

- Fork 地址和作者身份可识别。
- PR #18 已合并、PR #27 待 review 是 Fork 贡献状态，不应改写为原作者独立完成的开发历史。

### C2 架构与组织：✅ 完整度高

**原作者证据**

README 提供了三层互相校验的架构描述：

1. **功能模块表**：tensor factors、204 个 legacy factors、Alpha101、neutralize、bias correction、augmentation、MLP/Transformer、losses、Markowitz 与 backtest。
2. **五阶段数据流**：Data → Features → Training → Portfolio → Backtest。
3. **项目目录树**：data、features、training、models、portfolio、backtest、cli，以及 configs、tests、scripts、legacy 和 docs。

架构图还区分了默认实线路径与可选/替代虚线路径：GBM augmentation 和 Transformer 并非默认 CLI 必经模块。这一点不仅说明模块连接，还记录了运行时边界。

论文复现表进一步把论文 §3.1 至 §6 映射到具体模块和测试，形成“论文章节 → 代码 → 测试”的结构化索引。由此可可靠提取以下主链：

OHLCV/合成数据 → 掩码感知因子与偏差修正 → 213 维因子张量 → 前瞻收益数据集 → MLP 或可选 Transformer → AdjMSE/IC/RankIC → 收缩协方差且禁止做空的 Markowitz → 向量化回测与 Sharpe/IC/IR/DD。

**不足与边界**

- 未展开类、函数、配置 schema 或模块依赖图，因而适合提取系统级架构，不足以重建详细代码设计。
- neutralisation 在论文映射表中没有对应测试，应视为局部测试缺口，不能由整体测试完备性替代。

**Fork 归属**

- Fork 的已知贡献是 ETF 复现和 synthetic 验证基线相关 PR；没有证据表明核心五阶段架构由 Fork 作者设计。

### C3 设计意图：✅ 可主要还原

**原作者证据**

项目明确自我定位为 clean、fork-friendly、end-to-end，并强调 validation-first。这个定位由多项具体选择支撑，而非口号：

- 默认提供 30–90 秒 synthetic 端到端 smoke test，降低首次复现成本。
- synthetic 数据使用固定种子，外部数据失败时 notebook 可回退到 synthetic panel，优先保证流程可运行。
- 公共数据验证要求 walk-forward baselines、交易成本、滑点、换手率、回撤、bootstrap 置信区间及多模型对比。
- 简单基线、公共数据失败模式和负结果与研究流水线并列记录，表明目标不是只展示最优回测。
- 对 limit-up、limit-down、停牌和掩码进行专门修正，反映 A 股横截面研究中的数据可交易性假设。
- Markowitz 使用 Ledoit-Wolf 收缩协方差和 no-short 约束，体现对估计不稳定性和组合可行性的工程权衡。
- 明确声明研究与教学用途、非投资建议、非生产就绪，并指出历史回测不等于实盘或经验证的样本外 alpha。
- legacy 目录被标记为 archival、unsupported，说明研究遗留代码与当前受支持实现之间有意隔离。

**不足与边界**

- README 提到 research_card、reality_check 和 factor handbook，但其正文未内联；不能假设其中每项论证均已核验。
- 为什么只精选 9 个 Alpha101、为什么采用特定损失函数、约束和成本参数，内联材料没有给出完整消融或决策记录。

**Fork 归属**

- contribution_plan 中免责声明增强和数据复现说明仍是 Fork 的计划项，不应倒推为原项目设计意图的来源。
- 当前 README 已有较强免责声明及中文入口，而 Fork 计划仍提出免责声明和中文 README，存在时间顺序或计划状态歧义。没有 patch/commit 证据时，不能把当前 README 相应内容归属于 Fork。

### C4 开发流程：⚠️ 有门禁，过程史不完整

**原作者证据**

CONTRIBUTING 给出可执行的开发流程：

- 安装开发依赖后运行 pytest 和 ruff check。
- 可用 Docker 构建并执行 make test。
- 新功能需要测试，行为变化需要更新文档。
- PR 前要求本地运行完整测试，并确保 CI 通过。
- GitHub Actions 在 push 和针对 main 的 PR 上执行 pytest 与 ruff。
- tag push 触发 release workflow。
- Issues、Discussions 和 newcomer tasks 提供外部协作入口。

Git 概览又证明存在 v0.1.0、外部 PR 和少量外部贡献者，因此流程不是纯粹的文档设想。

**不足与边界**

- 未说明 feature branch 命名、是否允许直接 push main、squash/rebase/merge 规则、审批人数、CODEOWNERS 或 release versioning 规范。
- 没有真实 CI 日志、失败案例、PR review 对话或 commit 序列可供核验。
- “CI 存在”可证明门禁设计，不等同于每次合并都实际通过。

**Fork 归属**

- PR #18 已合并，说明 Fork 作者至少完成过一次进入上游 review/merge 流程的贡献。
- PR #27 尚待 review，只能记为候选贡献，不能计入原项目已接受能力。
- PR #B 要先通过 issue 确认维护者偏好，体现 Fork 作者计划遵循上游沟通流程；它不是上游既有分支策略的证据。

### C5 AI 协作方法论文档：❌ 缺失

**原作者证据**

- 内联材料未提供 CLAUDE.md、AGENTS.md、AI 使用政策、提示词规范、模型选择原则、人工复核门禁、AI 生成代码标注方式或 AI 辅助实验的审计要求。

**Fork 证据**

- contribution_plan v1.1 被描述为“经 GPT-5.6-Sol 审查调整”，证明 Fork 作者使用过 AI 审查。
- 同一计划明确写明 CLAUDE.md 属于 AI 辅助工具的个人配置，不应提交上游。这是对上游边界的谨慎处理，但不是项目级 AI 协作方法论。

**判定理由**

一次 AI 审查痕迹只能证明工具使用，不能证明存在可复用、可审计的协作规范。因此 C5 必须判为缺失，且不能由 CONTRIBUTING 的一般开发规则替代。

### C6 独立审查与质量保障：✅ 质量保障成立，正式独立审查较弱

**原作者证据**

- pytest 测试套件和 ruff 静态检查被纳入本地开发与 GitHub Actions。
- Docker 与 Dev Container 提供更一致的开发/验证环境。
- 论文复现表把多数研究模块映射到测试，包括 tensor factors、Alpha101、bias、augmentation、losses、Markowitz 和 metrics。
- 公共数据验证脚本会产出 summary.md、summary.csv、summary.json、metadata.json 和 submission.md。
- 项目提供 aggregate_validation_reports 和 audit_validation_report，用于汇总与审计社区提交。
- 外部 PR 已发生，至少存在一定的人类 review 信号。

**不足与边界**

- 没有测试数量、覆盖率、通过结果、失败记录或 CI 日志。
- 没有正式第三方复现报告、独立审计报告或论文同行评审结论。
- arXiv 论文是公开研究产物，但 arXiv 标识本身不能证明已通过同行评审。
- neutralisation 在论文映射表中明确没有测试，质量保障并非无缺口。

**判定说明**

C6 的组合定义是“独立审查/质量保障”。自动化测试、lint、CI、容器化和外部 PR 足以使质量保障部分成立，故整体判为 ✅；但不能进一步声称已经完成正式独立科研审查。

### C7 闭环修复：⚠️ 有闭环基础设施，缺少完整案例

**可支持的证据**

- CONTRIBUTING 要求行为改变时同步更新文档、新功能增加测试、CI 通过后再合并，这是一套潜在修复闭环门禁。
- public_data_validation 的报告产物、聚合脚本和 audit 脚本可以支持“发现异常 → 修改 → 重新生成/审计报告”的流程。
- Fork 的 contribution_plan 已从先前版本修订为 v1.1，并注明经 GPT-5.6-Sol 审查调整，说明“审查 → 调整”确实发生过。
- PR #18 已合并，说明某项 Fork 贡献走完了提交与接受阶段。

**不能支持的推断**

- 没有具体缺陷描述、根因分析、修改 diff、回归测试名称和最终通过结果。
- contribution_plan 的修订是贡献规划闭环，不等于核心系统缺陷的“诊断 → 修复 → 验证”。
- PR #18 只被描述为 ETF 复现，不能在缺少 PR 内容时推断其修复了某一已知 bug。
- audit 脚本的存在证明能力，不证明已发生过闭环修复事件。

因此，C7 只能判为部分提取。若要升级为 ✅，至少需要一条 issue/PR/commit/test 证据链，明确展示问题、根因、修复、回归测试和验证结果。

### C8 数据溯源：✅ 较强，但未达到不可变数据归档

**原作者证据**

- 数据源表列出 Baostock、yfinance 和 Synthetic，并说明市场、访问方式与用途。
- 仓库不再分发市场数据；Baostock 与 yfinance 数据由 loader 按需下载。
- Synthetic panel 从固定种子确定性生成，适合作为零配置 smoke test 基线。
- README 给出 yfinance 与 Baostock 的调用示例、ticker 格式和时间范围示例。
- 公共数据验证输出 metadata.json，并可生成多格式摘要、成本敏感性文件和 bootstrap 区间。
- 论文小节到代码模块和测试的映射，使研究结论至少在结构层面可回指实现位置。
- 文档主动说明第三方数据限流、下载失败回退、数据质量、滑点、成本和建模假设等限制。

**不足与边界**

- 没有原始数据快照、供应商版本、下载时间戳样例、内容哈希、不可变对象存储地址或数据字典正文。
- yfinance/Baostock 是可变化的外部数据源；仅给查询参数不能保证未来得到完全相同的数据。
- 固定随机种子能保证合成生成过程的确定性，但仍需要代码版本、依赖版本和配置文件共同锁定才能保证跨环境完全复现。
- 论文结果表的具体数值、数据集切分和产物未内联，不能直接复算论文结论。

**Fork 归属**

- PR #18 的 ETF 复现可视为 Fork 对跨标的/公共数据复现能力的已接受增量，但仅能使用提示词明确给出的这一事实。
- PR #27 的 synthetic 验证基线尚未合并，不能计入上游当前数据溯源能力。
- PR #A 的免责声明与数据可复现说明仍为计划项，也不能算已落地证据。

## 三、原作者与 Fork 作者贡献对照

| 维度 | 原作者 / 上游已有证据 | Fork 作者已落地证据 | Fork 作者待定或计划 | 归属判断 |
|---|---|---|---|---|
| 项目与论文 | 项目主体、Yimin Du、arXiv:2507.07107、MIT、v0.1.0 | 无主体归属证据 | 无 | 项目与论文主体归原作者 |
| 核心架构 | Data → Features → Training → Portfolio → Backtest；213 factors；MLP/Transformer；Markowitz；backtest | 未提供核心架构修改证据 | 无 | 核心设计归原作者 |
| 测试与 CI | pytest、ruff、GitHub Actions、Docker、模块测试映射 | PR #18 经过上游合并流程 | PR #27 待 review | 上游质量体系归原作者；具体 PR 增量归 Fork |
| ETF 复现 | README/Issue 体系存在公共数据与 ETF 扩展入口 | PR #18：ETF 复现，已合并 | 无 | 已合并增量归 Fork，接受与维护归上游 |
| Synthetic 验证 | 上游已有确定性 synthetic smoke test | 未确认已合并 | PR #27：synthetic 验证基线，待 review | 不得计入上游已接受功能 |
| 免责声明 | 当前 README 已有英文和中文风险声明、Reality Check 引用 | 无可确认已合并 patch | PR #A 计划增强 | 当前内容按内联文件归上游；计划项归 Fork |
| 中文 README | 当前 README 已出现简中/繁中入口 | 无可确认已合并 patch | PR #B 计划先 issue 沟通 | 存在时间或版本歧义，不能归因给 Fork |
| AI 协作文档 | 未提供项目级文档 | contribution_plan 经 GPT 审查调整 | 明确不提交 CLAUDE.md | AI 使用痕迹归 Fork；C5 仍缺失 |
| 贡献协作 | CONTRIBUTING、Issues、Discussions、PR checklist | 已完成一次合并 PR；与维护者有 pairing 邀请 | 后续 PR 计划 | 流程框架归上游，个人计划与关系信息归 Fork |

## 四、关键证据链

### 1. 研究主张到实现

论文主题 / README 主张
→ 因子、偏差修正、模型、组合和回测模块
→ 论文小节到代码模块映射
→ 多数模块对应 pytest
→ synthetic smoke test 或 public-data validation
→ summary 与 metadata 等报告产物。

这条链在“结构和执行入口”层面完整，但缺少本次内联材料中的真实运行结果与论文数值复算，因此属于可追溯而非已复核。

### 2. 贡献到合并

CONTRIBUTING 的本地测试与 lint
→ 针对 main 的 PR
→ GitHub Actions 执行 pytest + ruff
→ review/CI 后合并
→ tag push 触发发布流程。

PR #18 的“已合并”状态为该流程提供了一条外部贡献实例，但没有 PR 明细，无法复原 review 中发生了哪些修改。

### 3. 数据到报告

Baostock / yfinance 按需下载，或固定种子 Synthetic
→ Panel
→ 因子与模型流水线
→ walk-forward、成本、滑点、换手率、回撤、bootstrap 等验证
→ summary.md/csv/json、metadata.json、submission.md
→ aggregate 与 audit 工具。

这条链具有较好的操作可追溯性，但外部市场数据未被快照化或哈希锁定，长期重现仍受供应商数据漂移影响。

## 五、证据等级说明与不越界声明

### 证据等级：B

**支持 B 级的因素**

- 材料来自项目 README、CONTRIBUTING、Fork contribution_plan 和 Git 历史概览，主体归属清楚。
- README 包含架构图、目录树、模块表、数据源、命令、论文映射和风险边界，信息密度高。
- 多项证据能交叉印证，例如 README 的测试映射与 CONTRIBUTING 的 CI 门禁相互支持。

**未达到 A 级的原因**

- 未直接读取仓库代码、测试文件、配置、CHANGELOG、被引用的 docs 正文、CI 日志、release 元数据、issue/PR 对话或 commit diff。
- Git 信息是概览而非原始历史。
- 没有实际执行测试或复现实验。
- C5 缺失，C7 无完整实例，C1/C4 的时间线与流程细节不全。

### 不越界声明

- 不把 README 中“存在某文档链接”写成“该文档内容已核验”。
- 不把自动化测试与 arXiv 发布写成正式独立同行评审。
- 不把 Fork 的待 review PR 或计划项写成上游已接受功能。
- 不把“经 GPT 审查”写成项目级 AI 协作方法论。
- 不在缺少 diff 和测试结果时声称 PR #18 完成了某个具体缺陷闭环。
- 不将当前 README 的中文入口或免责声明自动归因于 Fork，因为内联材料存在时间与版本歧义。

## 六、最终判定

该项目已具备显著的方法论外显化：架构、研究边界、复现入口、质量门禁和数据链路均能从文档中提取。它最接近“结构化、验证优先的研究工程模板”，而不是只附代码的论文仓库。但项目级 AI 协作规范缺失，过程史与缺陷闭环证据不足，且第三方市场数据尚未形成不可变归档。因此最终判定为：

- **证据等级：B**
- **可提取组件：7/8**
- **提取层级：主要提取**
- **最大优势：架构—论文—测试—验证产物之间的结构化映射**
- **最大缺口：C5 AI 协作方法论与 C7 可核验闭环案例**

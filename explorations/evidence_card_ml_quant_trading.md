# 证据卡：ml-quant-trading（外部压力测试 #2）

```yaml
项目名称: ml-quant-trading
项目类型: 量化（ML 多因子交易系统 + 学术论文）
源作者: Yimin Du (initial-d)
源仓库: https://github.com/initial-d/ml-quant-trading
Fork: https://github.com/redamancy231-create/ml-quant-trading
关联论文: arXiv:2507.07107
分析日期: 2026-07-23
提取模型: DeepSeek-V4-Pro (via Claude Code CLI)
证据等级: C（单一外部项目，有部分方法论文档但无 AI 协作记录）
压力测试目的: 检验提取框架对"有学术论文但无 AI 方法论的 OSS 项目"的适用性
```

---

## 提取方法

按方法论提取框架 v0.1 trial 的证据卡模板执行提取。与 NPGS（压力测试 #1）的对比：ml-quant-trading 有 CHANGELOG + CONTRIBUTING + arXiv 论文，方法论文档比 NPGS 多，但仍无 AI 协作的自觉记录。

---

## 可提取的维度

### 1. 项目元数据

| 维度 | 提取结果 |
|------|---------|
| 开发周期 | 2025 ~ 至今（122 upstream commits） |
| 语言 | Python 3.9+（主力，213 因子维度 + PyTorch ML + Markowitz 优化） |
| 构建 | pip install -e .[dev] + Docker + Makefile + CI（Python 3.9/3.10/3.11） |
| 代码规模 | src/mlquant/ 含 backtest/cli/data/features 五模块，15 个测试文件 |
| 许可证 | MIT |
| 学术背景 | arXiv:2507.07107（Yimin Du, 2025）——论文+代码对应 |

**提取质量**：高。

### 2. 代码组织模式

| 模式 | 证据 |
|------|------|
| 模块分层清晰 | `backtest/`（回测引擎+指标）/ `cli/`（命令行）/ `data/`（多源数据加载）/ `features/`（因子引擎）——标准量化栈分层 |
| 配置驱动 | `configs/paper.yaml` + `configs/small.yaml`——研究配置和生产配置分离 |
| 论文-代码对应 | 论文中的因子体系（204 legacy + 9 Alpha101）直接映射到 `features/` 模块 |
| 合成数据 + 公开数据双路径 | `data/synthetic.py` + `data/baostock_loader.py` + `data/yfinance_loader.py`——解决"论文使用的专有数据不可再分发"问题 |
| Docker 可复现 | `Dockerfile` + `.devcontainer/`——一键构建开发环境 |

**提取质量**：中高——结构可观察，且论文提供了设计意图的额外证据。

### 3. 版本控制模式

| 模式 | 证据 |
|------|------|
| PR-based 协作 | 外部贡献全部走 PR（#1-2 来自 Uwater1, #27-31 来自 redamancy231-create） |
| PR 合并策略 | 所有 PR 使用 merge commit（非 squash）——保留贡献者的 commit 历史 |
| commit message 规范 | 英文，语义清晰（`docs:`/`fix:`/`feat:`/`test:`） |
| 发布管理 | v0.1.0 tag + GitHub Release + CHANGELOG |

**提取质量**：中高。

### 4. 质量保障模式

| 模式 | 证据 |
|------|------|
| CI 覆盖 | GitHub Actions，Python 3.9/3.10/3.11 三版本 |
| 测试 | 15 个测试文件（pytest） |
| Lint | ruff |
| 基准测试 | `make benchmark`——可复现的性能基准 |
| 验证报告 | `make validate`——合成数据验证 + 公开数据验证 + audit report + leaderboard |

**提取质量**：中高——质量保障基础设施完整，可从 Makefile 和 CI 配置直接观察。

### 5. 方法论自我记录

| 维度 | 提取结果 |
|------|---------|
| CHANGELOG | ✅ v0.1.0 发布说明，结构清晰 |
| CONTRIBUTING | ✅ 含开发环境设置 + PR checklist |
| arXiv 论文 | ✅ 提供完整的因子设计方法论、回测框架理论、偏差修正方法 |
| CLAUDE.md | ❌ 不存在 |
| DEV_LOG | ❌ 不存在 |
| 项目复盘 | ❌ 不存在 |
| 审查记录 | ❌ 不存在 |

**提取质量**：中——有学术论文级别的正式方法论文档，但无 AI 协作过程记录。

---

## 不可提取的维度

### 6. 多模型协作模式

**提取结果**：**无。** initial-d 是独立研究者（参考 `reference_github_projects.md` 中的分析）。所有代码由一人编写，外部贡献仅限于文档和测试。

### 7. 独立审查模式

**提取结果**：**无记录。** PR review 存在（initial-d 审查了所有 incoming PR），但：
- 不知道审查的深度和标准
- 不知道是否使用了 AI 辅助审查
- 无审查报告文档

### 8. 闭环修复模式

**提取结果**：**部分可见。** commit 历史显示 bug 被修复（如 `fix: handle sparse downside sortino samples`），但修复过程不可见（无 issue 链接、无 review 记录、无验证步骤）。

### 9. 方法论自反性

**提取结果**：**无。** 项目没有像 ma-case-study-pipeline 的"起点评估分析"或方法论提取框架的"G5 审计"这样的自我批判文档。论文本身包含 limitations 讨论，但不涉及 AI 协作方法论。

---

## 提取质量评估

| 框架组件 | 可提取？ | 提取深度 | 来源 |
|---------|:------:|:------:|------|
| C1 项目元数据 | ✅ | 高 | 代码仓库 + README + arXiv |
| C2 代码组织 | ✅ | 中高 | 目录结构 + 论文（提供设计意图） |
| C3 版本控制 | ✅ | 中高 | commit 历史 + PR 记录 |
| C4 质量保障 | ✅ | 中高 | CI 配置 + Makefile + 测试目录 |
| C5 方法论文档 | ⚠️ | 中 | CHANGELOG + 论文（但无 AI 协作记录） |
| C6 多模型协作 | ❌ | — | 独立研究者项目 |
| C7 独立审查 | ❌ | — | 无审查记录 |
| C8 闭环修复 | ⚠️ | 低 | 修复存在但过程不可见 |

**可提取率**: 5.5/8 组件（69%）——显著高于 NPGS 的 37.5%。

---

## 与 NPGS 的对比

| 维度 | NPGS | ml-quant-trading |
|------|------|-----------------|
| 可提取率 | 3/8（37.5%） | 5.5/8（69%） |
| 方法论文档 | 零 | CHANGELOG + CONTRIBUTING + 学术论文 |
| 代码组织 | 可观察，动机不可知 | 可观察，论文提供了设计意图 |
| 质量保障 | 不可观察 | CI + lint + 15 测试 + benchmark |
| 协作模式 | 个人项目 | PR-based（有外部贡献者） |
| AI 协作痕迹 | 零（fork 后的工作不算） | 零（作者不使用 AI 协作工具） |

**增量发现**：有学术论文的项目比纯代码项目多提供了 ~30% 的方法论可提取性。论文充当了"被动的方法论文档"——它不是为 AI 协作写的，但恰好提供了提取框架需要的设计意图和理论背景。

---

## 压力测试结论

### 发现 1：学术论文是"准方法论文档"

ml-quant-trading 没有 CLAUDE.md，但它的 arXiv 论文在方法论提取中起到了类似作用——提供了设计意图、理论框架和局限性讨论。这意味着提取框架的 Phase 0 判别条件可以放宽：**"源项目是否有 ≥1 份方法论文档（CLAUDE.md / DEV_LOG / project_spec / academic paper / formal documentation）"**——学术论文应当被纳入合格的方法论文档类型。

### 发现 2：PR 历史是"被动的审查记录"

CONTRIBUTING.md + PR merge 模式 + commit 历史合在一起，构成了一个低分辨率但仍可读的"审查链"。它不能替代显式的审查报告，但比 NPGS 的完全空白好得多。

### 发现 3：可提取率与项目"方法论自觉"正相关

| 项目 | 方法论自觉 | 可提取率 |
|------|:--------:|:------:|
| 自有项目（ETF/M&A 等） | ★★★★★ | ~88% |
| ml-quant-trading | ★★★ | 69% |
| NPGS | ★ | 37.5% |

这个梯度说明：提取框架的价值不在于发现"全新"的模式，而在于把已有的方法论痕迹**系统化**。对高自觉项目，框架起到归纳和命名的作用；对低自觉项目，框架几乎无法运作。

---

*本证据卡作为外部压力测试 #2，不进入框架 v0.1 的正式模式目录。*

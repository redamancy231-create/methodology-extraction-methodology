# 证据卡：docx-pipeline

```yaml
项目名称: docx-pipeline
项目类型: 工具/工程（Python CLI，Markdown → DOCX 转换管道）
作者: redamancy231-create
仓库: https://github.com/redamancy231-create/docx-pipeline
分析日期: 2026-07-23
提取模型: DeepSeek-V4-Pro (via Claude Code CLI)
证据等级: B（自有项目，有完整的 AI 协作方法论文档）
```

---

## 提取方法

按方法论提取框架 v0.1 trial 的证据卡模板执行。docx-pipeline 是自有 AI 协作项目——有 CLAUDE.md + CHANGELOG + 审查链 + project_spec——属于高方法论自觉类型，预期可提取率高。

---

## 可提取的维度

### 1. 项目元数据

| 维度 | 提取结果 |
|------|---------|
| 开发周期 | 2026-07-15 ~ 至今（持续迭代，v1.1.0 → v1.2.0） |
| 语言 | Python（pip installable） |
| 构建 | pip install -e .[dev] + pytest + ruff |
| 测试 | **52 tests**，CI（Python 3.10-3.12 × Ubuntu/Windows/macOS） |
| 许可证 | MIT |
| 架构 | 双后端（Pure Python 零依赖 + Pandoc 高质量），AbstractConverter 接口 |

**提取质量**：高。

### 2. 代码组织模式

| 模式 | 证据 |
|------|------|
| 双后端策略 | `AbstractConverter` → `PandocConverter` + `PurePythonConverter`——用户按质量/依赖需求选择后端 |
| 模板驱动 | `docx_pipeline/data/templates/*.yaml`——排版样式可配置，不硬编码 |
| 渲染器分离 | Mermaid（mmdc CLI 调用）+ LaTeX 数学公式（latex2mathml → MathML → OMML 桥接）——渲染逻辑与转换逻辑分离 |
| 配置管理 | YAML 配置 + CLI 参数——用户层和开发者层分离 |

**提取质量**：高——双后端模式是显式的架构决策，有接口定义可追溯。

### 3. 版本控制模式

| 模式 | 证据 |
|------|------|
| 版本号管理 | v1.1.0 → v1.2.0，CHANGELOG 跟踪 |
| commit message 规范 | 中英混合，语义清晰（`feat:`/`fix:`/`docs:`/`chore:`） |
| 发布管理 | GitHub Release + PyPI 发布准备（badge 已移除——未实际发布到 PyPI） |

**提取质量**：中高。

### 4. 质量保障模式

| 模式 | 证据 |
|------|------|
| CI | GitHub Actions，Python 3.10/3.11/3.12 × macOS/Ubuntu/Windows——9 矩阵 |
| 测试 | 52 tests（pytest），含 benchmark 测试 |
| Lint | ruff |
| 数学渲染验证 | `_visual_check/`——目视验证数学公式渲染效果（CI 无法自动化的验证环节） |
| 截图回归 | `_screenshots/`——渲染效果的可视化回归对比 |

**提取质量**：高——双路径验证（自动化 CI + 目视检查）是有意设计。

### 5. AI 协作模式

| 模式 | 证据 |
|------|------|
| 多后端审查 | ✅ GPT-5.6-Sol 独立审查 CLAUDE.md（61/100，5 处事实错误已修正） |
| 审查链 | `_review/` + `_reviews/`——多轮审查报告完整保留 |
| prompt 保留 | `_prompts/`——审查 prompt 可追溯 |
| CLAUDE.md | ✅ 有，经独立审查 |
| project_status.md | ✅ 有（但 gitignored） |
| 审查 prompt 设计 | 内联源文件模式——将全部源文件内联到审查 prompt 中提升跨文件审查质量（参考 memory `methodology_review_prompt_inline_sources.md`） |

**提取质量**：高——CLAUDE.md 和审查链是主动记录。

### 6. 方法论自反性

| 模式 | 证据 |
|------|------|
| fork-modification-directions | ✅ 有——面向 fork 贡献者的修改路径文档 |
| 审查报告 | 多次审查报告保留，含评分和具体发现 |
| 目视验证方法论 | `_visual_check/` 的存在表明作者意识到 CI 无法覆盖渲染质量——这是对"自动化测试盲区"的自觉 |

**提取质量**：中高。

---

## 不可提取/弱提取的维度

### 7. 闭环修复模式

**提取结果**：**部分可见。** CHANGELOG 和 commit 历史显示 bug 被修复（如 `fix: remove zero-width space from hidden n-ary sub/sup elements`），math formula v1.2.0 是功能演进而非 bug 修复。但修复验证过程（谁来验证修复是否成功？目视确认还是自动化回归？）未在文档中记录。

**改进空间**：`_visual_check/` 目录虽然存在，但其检查流程和使用方式未文档化——这本身是提取到的"隐式实践"，但无法确认是否系统性地执行。

### 8. 多模型协作深度

**提取结果**：**有但较浅。** GPT-5.6-Sol 做了 CLAUDE.md 审查（61/100），但项目使用了多少模型、模型之间如何分工、是否有类似 ma-case-study-pipeline 的"角色槽位"设计——这些不可提取。审查主要是"请另一个模型审"，而非 pipeline 的多阶段模型协作。

---

## 提取质量评估

| 框架组件 | 可提取？ | 提取深度 | 来源 |
|---------|:------:|:------:|------|
| C1 项目元数据 | ✅ | 高 | README + CLAUDE.md + pyproject.toml |
| C2 代码组织 | ✅ | 高 | 源码 + 双后端接口定义 |
| C3 版本控制 | ✅ | 中高 | commit 历史 + CHANGELOG |
| C4 质量保障 | ✅ | 高 | CI 配置 + 52 tests + 目视验证 |
| C5 AI 协作 | ✅ | 中高 | CLAUDE.md + 审查链 |
| C6 方法论文档 | ✅ | 中高 | CHANGELOG + fork-directions + 审查报告 |
| C7 闭环修复 | ⚠️ | 中 | 修复存在，但验证过程不可见 |
| C8 数据溯源 | N/A | — | 不适用（工具项目非数据项目） |

**可提取率**: 7/7 适用组件——完整提取，取前 8 组件为 6.5/8——主要提取。

> 注：C8 对本项目不适用——数据溯源是学术论文类项目的方法论维度，不适用于工具类项目。排除 C8 后的可提取率为 7/7。

---

## 方法论特征提取

### 独特模式 1: 双后端架构的渐进式迁移路径

用户按质量需求选择后端——日常使用 Pandoc，离线/无依赖场景使用 Pure Python。这不是"二选一"而是"不同场景的最优解"。方法论含义：**方法论文档和工具应提供"从低质量选项到高质量选项的渐进路径"，而非强制用户迁移。**

### 独特模式 2: 自动化测试与目视检查的双轨验证

数学公式渲染的正确性无法被 CI 自动验证（需要人眼看"公式是否排版正确"）。`_visual_check/` 目录的存在表明项目意识到了这个盲区并建立了补偿机制。方法论含义：**任何质量保障体系都有盲区，应显式标注每个盲区并建立补偿检查，而非假装 CI 覆盖了一切。**

### 独特模式 3: 审查 prompt 内联源文件

审查 CLAUDE.md 时，将所有源文件内联到审查 prompt 中。这是从 ma-case-study-pipeline 继承的方法论模式（参考 `methodology_review_prompt_inline_sources.md`），在 docx-pipeline 中再次应用。方法论含义：**多文件审查时，在 prompt 中内联全部源文件可显著提升跨文件审查质量。**

---

*本证据卡标注为 B 级证据——自有项目，有完整的 AI 协作方法论文档，可进入跨项目模式合成。*

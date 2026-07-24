# 证据卡：independent-review-toolkit

```yaml
项目名称: independent-review-toolkit
项目类型: 工具/方法论（独立审查 SOP + Prompt 模板）
作者: redamancy231-create
仓库: https://github.com/redamancy231-create/independent-review-toolkit
分析日期: 2026-07-23
提取模型: DeepSeek-V4-Pro (via Claude Code CLI)
证据等级: B（自有项目，提取自 50+ 轮审查实战 + 2 轮异后端审查验证）
```

---

## 项目规模

- 版本: v2.0.1（CC BY 4.0）
- 规模: 小型——SOP（12 节）+ 2 套 prompt 模板 + 1 个 annotated example + 三语言
- 无 CLAUDE.md（和其他两个衍生项目一致——SOP 本身就是操作手册，CLAUDE.md 的功能被 SOP 覆盖）
- 审查: 2 轮 Codex GPT-5.5（R1: 16 项发现 → R2: PASS）

---

## 提取质量评估

| 组件 | 可提取？ | 深度 | 注 |
|------|:------:|:--:|------|
| C1-C3 | ✅ | 中 | 基础元数据/组织/版本控制 |
| C4 质量保障 | ✅ | 高 | SOP 源自 50+ 轮实战 → 提取后 2 轮独立审查验证 |
| C5 AI 协作 | ✅ | 中 | 审查方法论来自源框架 |
| C6 方法论文档 | ✅ | 中 | SOP + 示例 |

**可提取率**: 6/7 适用组件。

---

## 独特方法论贡献

### "方法论→可执行工具"的标准化范例

和 ai-framework 的衍生提取模式互为补充：

| | ai-framework（源） | independent-review-toolkit（衍生） |
|------|------|------|
| 形态 | 框架文档的子节 | **独立 CLI 可用的仓库** |
| 粒度 | "§9.2 独立审查" | **12 节 SOP + 2 套 prompt 模板 + 示例** |
| 目标用户 | 框架读者 | **任何想做独立审查的人** |
| 验证 | 框架级审查 | **提取后独立审查验证** |

ai-framework 和 prompt-tdd-methodology 的提取也走了同样的路径，但没有像 independent-review-toolkit 这样形成完整的"copy-paste → 5 分钟启动"的可用性。这个项目是"方法论→工具"进化路径中**最接近终点**的案例——它不再是"文档描述怎么做"，而是"复制这段 prompt 就能做"。

---

*B 级证据——自有项目，方法论价值主要在"衍生提取"模式的范例性。*

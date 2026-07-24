# S3: 技术约定

> **生成模型**: DeepSeek-V4-Pro (via Claude Code CLI shell)
> **生成日期**: 2026-06-16

## 核心约定

| 约定 | 规定 | 来源 |
|------|------|------|
| 双格式产出 | 所有正式交付物 .md + .json 配对 | [[feedback_artifact_pairing]] |
| 证据分类标签 | [S]/[E]/[I]/[J]/[Sp] 五级 | 框架§9.6 |
| 正文语言 | 中文（方法论叙述、分析、总结） | [[feedback_language]] |
| 编程语言 | JSON字段名/代码标识符用英文 | 框架约定 |
| 文件编码 | UTF-8 | [[feedback_utf8_encoding]] |
| 路径格式 | 正斜杠 `/`，绝对路径 | Windows Git Bash兼容 |
| Python版本 | 3.12.7（仅在需要脚本时） | [[reference_python_versions]] |
| 模型标注 | 所有产出header标注实际生成模型（非CLI壳名） | [[feedback_generated_files_model_provenance]] |
| 日期格式 | YYYY-MM-DD | 项目约定 |

## 生成与审查模型

| 角色 | 模型 | CLI壳 | 用途 |
|------|------|--------|------|
| 作者 | DeepSeek-V4-Pro | Claude Code | 项目执行、分析、写作 |
| 独立审查者 | ChatGPT-5.5 | Codex CLI | Phase 7独立审查（双轴独立性） |
| 备用审查者 | Qwen3.7-Max | Qwen CLI | 如需Protocol 2冷读 |

## 证据分类使用规则

在方法论提取框架中使用以下标签：

- **[S]（Speculation）**: 纯推测，无项目数据支撑
- **[E]（Example）**: 来自单个项目的孤例
- **[I]（Indication）**: 来自2个项目的初步信号
- **[J]（Judgment）**: 来自≥3个项目的模式判断，未经独立审查确认
- **[Sp]（Special）**: 特殊证据类型（如逻辑推断、外部引用）

## 框架§9.6 证据升级路径

```
[S] → [E] → [I] → [J] → 独立审查确认 → 提升可信度
```

本项目自身的证据标注实践将作为框架§9.6的试跑数据。

## 环境约束

- **OS**: Windows 11 Home China (build 26100)
- **Shell**: Git Bash (MINGW64) — 默认；PowerShell 5.1 可用
- **磁盘**: E: 为本地NVMe（铠侠1TB）
- **网络**: 不需要（所有源项目在本地磁盘）

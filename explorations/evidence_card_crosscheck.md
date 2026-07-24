# 证据卡：CrossCheck（外部压力测试 #3）

```yaml
项目名称: CrossCheck
项目类型: 工具/系统（多模型 AI 编码自主循环 + git hooks 质量门禁）
作者: sburl (Spencer Burleigh)
仓库: https://github.com/sburl/CrossCheck
Fork: https://github.com/redamancy231-create/CrossCheck
分析日期: 2026-07-23
提取模型: DeepSeek-V4-Pro (via Claude Code CLI)
证据等级: C（外部项目，有方法论文档但无 AI 协作过程记录）
```

---

## 项目规模

| 维度 | 数据 |
|------|------|
| 开发周期 | 2026-01-30 ~ 至今，149 PRs（全部作者自提） |
| 版本 | VERSION 文件追踪 |
| 许可证 | MIT |
| 文档 | README + ARCHITECTURE + ADVANCED + TROUBLESHOOTING + CODEX.md + CODEX-PROMPTS + QUICK-REFERENCE + CONTRIBUTING + SECURITY |
| CLAUDE.md | ✅（系统级全局模板，非项目级） |
| 外部贡献 | 0 PR / 0 Issue |

---

## 可提取的维度

### 1. 项目元数据 — 高

专业级开源项目——VERSION、CHANGELOG（通过 PR 历史）、完整的文档体系。

### 2. 架构/组织模式 — **极高**

| 模式 | 证据 |
|------|------|
| **6 阶段开发循环** | Plan → Build → Verify → Review → Merge → Triage——显式定义的自主循环 |
| **多模型角色分配** | "Codex writes, peer model reviews, hooks enforce"——Claude/Codex/Gemini 各有角色 |
| **瑞士奶酪模型** | 多层不相关的安全层叠加——git hooks / pre-PR check / peer review / branch protection |
| **零信任哲学** | "Zero Trust - Test everything. Nothing works until proven"——和自有项目的铁律 2/5 同源 |
| **Skills 体系** | `/submit-pr` `/commit-smart` `/codex-delegate` `/plan`——将 AI 协作的最佳实践编码为可调用的 CLI 命令 |
| **自主优先** | "Autonomous First - Fix it yourself → try Codex → try alternatives → escalate" |

### 3. 质量保障模式 — 高

| 模式 | 证据 |
|------|------|
| Git hooks 作为质量门禁 | 密码检测、时间戳验证、pre-push 检查——合规是被动的，不需要 agent "记住" |
| pre-PR 检查 | `/techdebt` + `/pre-pr-check`——提交 PR 前的自动化自检 |
| 多模型 peer review | "Codex writes → peer model reviews"——但不是"独立审查"（见下文 C7） |

### 4. 方法论文档 — 中高

| 文件 | 作用 |
|------|------|
| ARCHITECTURE.md | 6 阶段循环 + 瑞士奶酪模型的系统描述 |
| CODEX.md | Codex 代理的详细工作流 |
| CODEX-PROMPTS.md | 中间审查阶段的 prompt 模板 |
| QUICK-REFERENCE.md | Skills 速查表 |
| ADVANCED.md | 高级用法 |

有完整的方法论文档，但缺少 CLAUDE.md 级别的 AI 协作指南（其 CLAUDE.md 是系统级全局模板而非项目级）。

---

## 完全不可提取的维度

### 5. 独立审查记录

**零。** 149 个 PR 全部由作者自提——"peer review"指的是 AI 模型审查代码，而非人类审查者审查 AI 产出。没有任何独立审查报告、审查结论归档、审查发现修正记录。

### 6. AI 协作过程记录

**零。** 没有 DEV_LOG、project_spec、复盘报告。系统设计精良，但开发过程完全不可见——不知道这个系统本身是如何被开发的（是作者手写还是用 CrossCheck 自身开发的？）。

### 7. 闭环修复

**不可判断。** PR 历史显示 bug 被修复，但修复→验证过程不可见。

---

## 提取质量评估

| 组件 | 可提取？ | 深度 | 注 |
|------|:------:|:--:|------|
| C1 元数据 | ✅ | 高 | |
| C2 架构/组织 | ✅ | **极高** | 6 阶段循环 + Skills 体系——自有项目之外最丰富的架构文档 |
| C3 版本控制 | ✅ | 中 | |
| C4 质量保障 | ✅ | 高 | git hooks + pre-PR check——自动化质量门禁的完整设计 |
| C5 AI 协作设计 | ✅ | **极高** | Claude/Codex/Gemini 多模型角色分配 + Skills |
| C6 方法论文档 | ✅ | 中高 | 文档体系完整但无项目级 CLAUDE.md |
| C7 独立审查 | ❌ | — | 无审查记录 |
| C8 闭环修复 | ⚠️ | 低 | PR 历史可见但不可追溯 |

**可提取率**: 5.5/8（69%）——正好落在 ml-quant-trading 的同一档。

---

## 与自有项目的关键对比

### 相同的哲学，不同的实现

| 维度 | CrossCheck | 自有项目 |
|------|-----------|---------|
| 多模型协作 | **Skills 体系**（`/submit-pr` `/codex-delegate`）——CLI 命令化 | **角色槽位模型**（playbook + prompt+config）——文档化 |
| 独立性保障 | Git hooks 被动执行——不需要 agent "记住" | 铁律 2/3 主动执行——agent 必须自觉遵守 |
| 质量门禁 | Pre-push hook + `/pre-pr-check` | 交叉双盲审 + 答辩模拟 |
| 可审计性 | PR 历史 + commit message | **prompt+config 双文件 + 审查链归档**（更强） |
| 可迁移性 | `git clone` → 安装 hooks → 即用 | 复制 playbook → 填模板 → 分配角色（需要更多人工） |

### 梯度观更新

CrossCheck 以 69% 落在第二档，但它的失败维度和 ml-quant-trading 完全不同：

| 项目 | 强项 | 弱项 |
|------|------|------|
| ml-quant-trading | 学术论文（被动方法论文档） | 无 AI 协作记录 |
| **CrossCheck** | **架构设计 + Skills 体系**（主动方法论设计） | **无审查记录 + 无过程文档** |

ml-quant 的可提取率来自"有人替它写了方法论文档（学术论文）"。CrossCheck 的可提取率来自"作者设计了方法论（6 阶段循环 + Skills），但没记录执行过程"。**两者的 69% 来源不同。**

---

## 独特方法论贡献

### 模式 1: Skills 作为方法论的操作化

自有项目将 AI 协作方法论写成**文档**（playbook、SOP、铁律）；CrossCheck 将 AI 协作方法论写成 **CLI 命令**（`/submit-pr` `/codex-delegate` `/plan`）。

这是"方法论→工具"的另一种路径——不是从框架文档中提取独立工具，而是从一开始就把方法论设计为可调用的系统命令。自有项目在 independent-review-toolkit 中也走向了这个方向，但 CrossCheck 做得更彻底——它的整个系统就是一个可安装的 CLI。

### 模式 2: 被动合规 vs 主动自觉

CrossCheck 的核心哲学是"**git hooks make compliance the path of least resistance**"——合规不需要 agent 记住规则，hooks 在操作层面强制执行。这与自有项目的铁律 2（"agent 必须自觉遵守无人审己"）形成对比——前者是被动合规，后者是主动自觉。

两种策略都有盲区：hooks 不能强制执行"审查独立性"（agent 仍可能用同一模型自审），主动自觉依赖 agent 的记忆和诚意。理想方案可能是两者的组合。

### 模式 3: 瑞士奶酪模型作为多层质量保障的理论基础

CrossCheck 明确引用了航空安全领域的 Swiss Cheese Model 作为其多层质量保障设计的理论基础。自有项目有类似的多层设计（交叉盲审 + 设计回溯 + 答辩模拟），但没有为它命名或引用外部理论框架。CrossCheck 的做法——**给设计模式一个学术上有根基的名字**——值得借鉴。

---

*C 级证据——外部项目，方法论文档完整但缺少 AI 协作过程记录和独立审查证据。方法论设计质量很高，但设计本身的开发过程不可追溯。*

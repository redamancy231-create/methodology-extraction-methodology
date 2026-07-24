# 方法論提取方法論（Methodology Extraction Methodology）

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Status](https://img.shields.io/badge/Status-CLOSED-inactive.svg)]()
[![Version](https://img.shields.io/badge/Version-v0.1_trial-orange.svg)]()
[![Language](https://img.shields.io/badge/README-正體中文-red.svg)]()
[![Framework](https://img.shields.io/badge/Based_on-AI協作框架_v1.5.1-blue.svg)](https://github.com/redamancy231-create/ai-collaboration-framework)

[简体中文](README.md) | [正體中文](README_zh-TW.md) | [English](README_en.md)

> **定位**: 一次方法論文獻提取的實驗記錄——不是可交付的成品，而是過程的誠實記錄。
> **狀態**: v0.1 trial · CLOSED · 不成熟
> **生成模型**: DeepSeek-V4-Pro (via Claude Code CLI)
> **生成日期**: 2026-06-16

---

## 這是什麼

一個元層次方法論專案——從 **22 個源專案**中系統提取可複用的方法論模式。源專案包括作者自建專案（7 個已公開、4 個未公開）以及對他人開源專案或論文的獨立分析（11 個）。完整清單和分類見 `explorations/source_projects_summary.md`。

它的**雙重目的**：
1. **產出層**：嘗試形式化一套"方法論提取框架"——如何從一組專案中識別、驗證和歸類跨專案的方法論模式
2. **測試層**：作為 [AI 協作專案全生命週期框架](https://github.com/redamancy231-create/ai-collaboration-framework) Protocol 3 的首次端到端試跑

## 為什麼不成熟

專案自身的 G5 可追溯審計結論：**無一方法論模式滿足 ≥3 個源專案的穩定元件門檻。** 源專案共 22 個——**11 個為對他人開源專案或論文的獨立分析**（Evolver、GitNexus、PilotDeck、Small Scale、Agent Harness、claude-code-ultimate-guide、claude-md-generation、PocketFlow、NPGS、ml-quant-trading、CrossCheck）、**7 個為自建公開專案**（AI協作框架、claude-skills、docx-pipeline、ETF-pybind11、Independent Review Toolkit、M&A案例、prompt-tdd）、4 個為自建未公開專案。所有專案的提取和審查由同一操作者執行——這個樣本量不足以支撐泛化的方法論提取。

換句話說：我們證明了"這件事有多難"，但還沒有做到"這件事該怎麼做"。

## 有什麼值得看

### 審查鏈實證（最有價值的部分）

10 輪正式審查（來自 4 個審查後端：GPT-5.5/Kimi-K2.7/Qwen3.7-Max/GLM-5），另有 1 次異後端復編碼（Phase 3.5）。累計數十項發現，審查記錄見 `reviews/`。基於 Kohli (2026-05) 的獨立性分析，有效獨立視角約 2-3 個。關鍵資料點：

- **Phase 5 雙輪正交審查**：GPT-5.5 發現 17 項 + Qwen3.7-Max 發現 16 項 = **0 重疊**——在本次兩輪審查及當前編碼規則下未觀察到重疊，提示不同模型的錯誤敏感性具有互補性
- **Phase 7.6 終期審查**：GPT-5.5 實用完整性評分 7.7/10
- **審查方法論價值**：整個審查鏈本身就是"多模型獨立審查有效性"的強證據

詳見 [`reviews/`](reviews/)。

### G5 可追溯審計

對 v0.1 框架的逐元件審計，結論是"所有 5 元件均未達到 ≥3 源穩定門檻"。這是專案最誠實的發現。

詳見 [`synthesis/phase4_traceability_audit.md`](synthesis/phase4_traceability_audit.md)。

### 11 張公開證據卡

每張卡片記錄一個源專案或外部壓力測試的方法論特徵提取結果，可在 `explorations/` 目錄中查看。未公開源專案的詳細證據卡不在本倉庫中。

詳見 [`explorations/`](explorations/)。

### 框架 v0.1（trial）

方法論提取框架的試行版本——標註了"trial"狀態，每個元件都附有穩定度評估。

詳見 [`framework_output/main/`](framework_output/main/)。

## 專案結構

```
├── README.md                          ← 本檔案
├── CLAUDE.md                          ← 專案憲法（AI 協作指南）
├── FORKING.md                         ← Fork 指南
├── project_spec.md                    ← S1-S10 完整 Spec
├── DEV_LOG.md                         ← 開發日誌
│
├── spec/                              ← 專案規範
│   ├── success_criteria.md            ← 成功標準與 Protocol 3 預登記指標
│   ├── evaluation_plan.md             ← 評估計畫
│   ├── risk_register.md               ← 風險登記冊
│   └── ...
│
├── explorations/                      ← 11 張公開證據卡 + 源專案彙總
│   ├── evidence_card_*.md             ← 每個源專案的方法論特徵提取
│   └── phase2_completion_summary.md
│
├── synthesis/                         ← 綜合與模式提取
│   ├── phase4_validated_pattern_catalog.md/.json  ← 經驗證的模式目錄
│   ├── phase4_traceability_audit.md   ← G5 可追溯審計
│   └── phase6_mini_extraction.md      ← 遞迴觀察
│
├── reviews/                           ← 10 輪審查報告（核心實證）
│   ├── phase5_codex_crosscheck.md     ← GPT-5.5 審查（17 項發現）
│   ├── phase5_qwen_independent_review.md ← Qwen3.7-Max 審查（16 項發現）
│   └── ...
│
├── framework_output/main/             ← 主交付物
│   ├── 方法論提取框架_v0.1_trial.md   ← 方法論提取框架正文
│   └── 方法論提取框架_v0.1_trial.json ← 機讀版
│
└── archive/                           ← 歸檔（復盤報告等；本地保留）
```

## 相關工作

> 2026-07-23 調查

### 想法 provenance

本專案的想法並非預先設計——它是在 2026-06-16 [AI 協作專案全生命週期框架](https://github.com/redamancy231-create/ai-collaboration-framework) Protocol 3 試跑期間，由 AI 模型（DeepSeek-V4-Pro 或同期的其他協作模型）在對話中提出的。這個想法的構成元素在學術傳統中均有前驅：**系統性文獻回顧方法論**（醫學/社會科學標準方法）、**軟體工程經驗教訓提取**（lessons learned / post-mortem analysis）、**證據分級體系**（[S]/[E]/[I] 標籤來自框架自身設計）。但把這些分散的概念組合成"從多個 AI 協作專案中系統提取可複用方法論文獻"——這個組合本身未在後續的系統搜尋中找到直接先例。

### GitHub 搜尋

對以下 9 個方向（中英雙語，實際搜尋使用英文關鍵詞）進行了系統搜尋，**全部零結果**：

| # | 中文 | English |
|---|------|---------|
| 1 | 方法論文獻提取 + AI 協作模式 | `methodology extraction AI collaboration patterns meta` |
| 2 | 方法論文獻提取 + LLM 多模型審查 | `"methodology extraction" LLM multi-model review` |
| 3 | 跨模型審查 + 獨立驗證 + 學術流水線 | `cross-model review independent verification pipeline academic` |
| 4 | AI 協作經驗教訓 + 多 agent 工作流 | `"lessons learned" AI collaboration multi-agent workflow` |
| 5 | 提示詞工程模式目錄 + 系統提取 | `prompt engineering patterns catalog extraction systematic` |
| 6 | LLM 協作框架 + 角色流水線 | `LLM collaboration framework role-based pipeline` |
| 7 | 多模型獨立審查 + 交叉盲審 | `"multi-model" independent review blind cross` |
| 8 | AI 協作元分析 + 模式目錄 | `AI collaboration meta-analysis pattern catalog empirical` |
| 9 | AI 使用經驗 + 開發者工作流文件化 | `"how I use AI" developer workflow documentation systematic` |

**搜尋侷限**：GitHub 搜尋結果受儲存庫 stars、活躍度和排序演算法影響，低 stars 儲存庫的可見性有限；學術文獻搜尋受關鍵詞選擇影響。不排除相關工作存在但未被檢索到。本次檢索未發現"從多個 AI 協作專案中系統提取方法論模式"的同類專案。

已知最接近的三個專案（均來自人工發現，GitHub 搜尋無法索引微型儲存庫）：

| 專案 | 相似度 | 差異 |
|------|--------|------|
| [sburl/CrossCheck](https://github.com/sburl/CrossCheck) | 中 | 多模型審查自修正系統，但是 **npm CLI 工具**，不做跨專案模式提取 |
| [huidev2025/CSF](https://github.com/huidev2025/CSF) | 低 | LLM 協作框架，聚焦**如何協作**，不做跨專案模式提取 |
| [rainmana/mcw-framework](https://github.com/rainmana/mcw-framework) | 低 | 人-AI 協調視窗元模型，方向不同 |

三者共同特徵：單人專案、零外部貢獻、<25 stars。**這個賽道目前沒有社群。**

### 學術文獻

本專案核心主張（多模型獨立審查的價值）在 2026 年學術文獻中獲得了外部支援和對照：

**"九法官，兩有效票"（Kohli, 2026-05）** — [*Nine Judges, Two Effective Votes: Correlated Errors Undermine LLM Evaluation Panels*](https://arxiv.org/abs/2605.29800)。核心結論：9 個前沿 LLM 組成的評審團，有效獨立票數僅 ~2 票；**單一最佳評委的表現追平甚至超過整個評審團**。這為本專案的多模型審查架構提供了一個外部參照——在 Kohli 測試的分類任務上，4-5 模型可能已是有效上限（跨任務外推需謹慎），加更多模型收益遞減。

**"行為糾纏"統計框架（Kuai et al., 2026-04）** — [*How Independent are Large Language Models? A Statistical Framework for Auditing Behavioral Entanglement*](https://arxiv.org/abs/2604.07650)。測試 18 個 LLM（來自 6 個模型家族），發現廣泛的"行為糾纏"（共享訓練資料/蒸餾/對齊流程導致的隱式依賴）。去糾纏的驗證器整合可將準確率提升 4.5%。

**"當模型意見分歧時"（Nájera et al., 2026-05）** — [*When Models Disagree: Rethinking LLM Evaluation for Public Comment Analysis*](https://arxiv.org/abs/2605.29025)。將多模型分歧重新定義為**診斷訊號**而非缺陷——分歧模式對映到真實的解釋複雜性。本專案 Phase 5 雙輪審查 33 項發現在當前編碼規則下未觀察到重疊，為這一理論提供了一個可能的資料點（需注意審查任務與原文公共評論分析場景的差異）。

**"人主導的 AI 共創"（Oda, 2026）** — [*Human-Led AI Co-Creation: A Practical Framework for Multi-Model Research, Convergence, and Human Authority*](https://www.academia.edu/165538962)（獨立白皮書，同行評審狀態未知）。提出的四角色框架（主 AI 起草 → 多模型並行審查 → 迭代跨模型對比 → 人類最終裁決）與本專案流水線幾乎同構。

**關鍵對照**：

| 維度 | 學術前沿 | 本專案 |
|------|---------|--------|
| 多模型獨立性量化 | 9→2 有效票（Kohli 2026-05） | 5 模型錯誤空間互補（實證，未經數學建模） |
| 分歧作為診斷訊號 | 四類分歧分類法（Nájera 2026-05） | Phase 5 雙輪審查零重疊（實證案例） |
| 人-AI 協作框架 | 四角色模型（Oda 2026） | 五鐵律 + 角色槽位（更嚴格的獨立性約束） |
| **跨專案模式提取** | **未檢索到同類工作** | **22 專案系統提取（搜尋存在已知侷限，見上文）** |

### 閉合後外部驗證附錄

基於上述 4 篇論文的分析框架，對本專案的審查資料進行了重分析（重新分類 58 項發現、評估模型獨立性、對比協作框架）。詳見 [`post-hoc-external-validation.md`](post-hoc-external-validation.md)。

### 外部驗證的四條修正

| 來源 | 驗證了什麼 | 修正了什麼 |
|------|-----------|-----------|
| Kohli (2026-05) | 4-5 模型架構是最優配置 | 10 輪審查 ≈ 2-3 個有效獨立視角，不應聲稱"10 輪獨立" |
| Nájera (2026-05) | Phase 5 零重疊是"深度分歧"的預期表現 | 58 項發現可系統分為 4 類，34% 為深度分歧——≥3 後端是必要的 |
| Kuai (2026-04) | 全不同提供商的模型選擇是隱式去糾纏策略 | 糾纏度雖低但非零——不能聲稱"完全獨立" |
| Oda (2026) | 鐵律體系比最接近的學術框架更嚴格 | Oda 的失敗模式分類可納入 Phase 0 風險登記冊 |

### 定位總結

本專案的核心主張（多模型獨立審查有效）獲得了 2026 年學術文獻的外部支援和對照。但"從多個 AI 協作專案中系統提取可複用方法論文獻"這個元層次動作——在 2026-07-23 對 GitHub（9 個方向）和學術文獻的系統搜尋中**未檢索到**同類工作。搜尋存在已知侷限（GitHub 索引微型儲存庫不完整、學術搜尋受關鍵詞選擇影響），因此不排除相關工作存在但未被發現。本專案受限於 n=12 同作者樣本，提取出的模式尚未達到跨使用者泛化的穩定門檻。

### 適用人群與使用價值

**適用人群**：已經在用 AI 做多個專案、累積了大量 CLAUDE.md / DEV_LOG / 審查報告，但感覺自己的方法論散落在各個專案裡，想系統化的人。

**不適用**：只做過一兩個專案的人（n 太小）、不做 AI 協作的純程式碼專案、沒有方法論文件的專案、想找"最佳實踐模板"的人（本框架告訴你"你做了什麼"，不告訴你"你應該做什麼"）。

**使用價值**三點：

1. **知道自己的方法論"值多少錢"**——框架的 8 個元件是一份檢查清單。跑一遍就知道你的專案在哪些維度上有方法論自覺（文件、審查、閉環）、哪些是空白
2. **把散落的碎片拼成模式**——22 個專案的方法論文件分散在各處，提取框架提供了跨專案對比的流程
3. **讓方法論被外部驗證**——整理成結構化形式後，可以被對比、被質疑、被學術文獻交叉驗證

**核心侷限**：框架在 22 個源專案上執行過——11 個外部分析 + 7 個自建公開 + 4 個自建未公開。其中 11 個有獨立證據卡（`explorations/`），其餘 11 個的分析過程記錄在 `reviews/` 審查報告中。可提取程度與專案的方法論自覺正相關：主動記錄AI協作過程的專案可提取大部分方法論組件；僅保留被動程式碼痕跡的專案可提取內容驟降至少數幾個組件——框架無法從不存在的資訊中提取資訊。所有專案的提取和審查由同一操作者執行。完整清單和分類見 `explorations/source_projects_summary.md`。框架的有效性是否泛化到其他作者的工作習慣和不同操作者的提取方式，**尚未驗證**。

## 與父框架的關係

本專案是 [AI 協作專案全生命週期框架](https://github.com/redamancy231-create/ai-collaboration-framework) v1.5.1 的 Protocol 3 試跑對象。父框架此後已演進至更高版本。本專案是閉合時刻的歷史快照，部分版本引用可能滯後。

## 關聯專案

| 專案 | 關係 |
|------|------|
| [**AI 協作框架**](https://github.com/redamancy231-create/ai-collaboration-framework) | **方法論上游** — 本專案是框架 Protocol 3 的試跑對象 |
| [**claude-skills**](https://github.com/redamancy231-create/claude-skills) | **方法論文獻源** — 三個 Skill 的提取結果已納入本框架（證據卡 #11） |
| [**Independent Review Toolkit**](https://github.com/redamancy231-create/independent-review-toolkit) | **審查方法來源** — 本專案的獨立審查流程使用該工具包 SOP |
| [**Prompt-TDD Methodology**](https://github.com/redamancy231-create/prompt-tdd-methodology) | **同系專案** — 對照實驗方法論案例手冊，共享多後端審查實證 |
| [**Methodology Handbook**](https://github.com/redamancy231-create/methodology-handbook) | **同系專案** — 50 條 AI 協作實戰教訓速查，Skill 設計協議的經驗來源 |
| [**DOCX Pipeline**](https://github.com/redamancy231-create/docx-pipeline) | **同系專案** — Markdown → 中文 DOCX 流水線（提取框架方法論源之一） |
| [**ETF Pattern Match — pybind11**](https://github.com/redamancy231-create/etf-pattern-match-pybind11) | **同系專案** — C++20/pybind11 量化加速，審查鏈實證源 |
| [**M&A Case Study Pipeline**](https://github.com/redamancy231-create/ma-case-study-pipeline) | **同系專案** — 8 階段多模型學術生產流水線，證據卡源專案 |

## 相關檔案

- [FORKING.md](FORKING.md) — Fork 指南（四層修改方向 + 已知侷限）
- [minimal-methodology-guide.md](minimal-methodology-guide.md) — 最小方法論文件指南（面向"用AI做專案但沒記錄過程"的人）
- [CONTRIBUTING.md](CONTRIBUTING.md) — 貢獻指南
- [CITATION.cff](CITATION.cff) — 引用資訊

## 許可證

文件/資料: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

---

*"我們證明了這件事有多難，但還沒有做到這件事該怎麼做。"*
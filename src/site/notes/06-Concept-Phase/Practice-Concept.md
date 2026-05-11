---
{"dg-publish":true,"permalink":"/06-concept-phase/practice-concept/","title":"概念階段練習題","tags":["iso-21434","practice","concept-phase"],"dg-note-properties":{"title":"概念階段練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","concept","item","goals","claims","cs-concept"],"tags":["iso-21434","practice","concept-phase"],"created":"2026-05-11"}}
---


> 涵蓋：Item Definition、CS Goals、CS Claims、CS Concept。
> 共 10 題。

---

## Q1. (recall)

ISO 21434 的 Cybersecurity Concept Phase 在哪個 Clause？

> [!answer]- 解答
> **Clause 9**。
> 含：Item Definition (9.3)、Cybersecurity Goals (9.4)、Cybersecurity Claims (9.5)、Cybersecurity Concept (9.5)。

---

## Q2. (recall + 易混淆)

下列何者**最正確**描述 Cybersecurity Goal、Claim、Concept、Requirement 的差異？

A. 四者都是同義詞
B. Goal = 保護目標；Claim = 假設/轉移；Concept = 概念解決方案；Requirement = 可實作可驗證細節
C. Requirement 是最高層級
D. Claim 是技術細節

> [!answer]- 解答
> **B**。
>
> 階層：
>
> ```
> Goal (高層級保護目標)
>   ↓
> Concept (概念解決方案)
>   ↓
> Requirement (可實作可驗證)
> ```
>
> Claim 是「假設或轉移」與 Goal 並列但對 out-of-scope 風險。
> 參考 [[00-Dashboard/Exam-Traps#Trap 1\|00-Dashboard/Exam-Traps#Trap 1]]

---

## Q3. (recall)

下列哪個是合理的 Cybersecurity Goal？

A. 「TCU 應使用 AES-256-GCM」
B. 「TCU 應安全」
C. 「TCU 韌體的完整性應被保護免於未經授權的修改」
D. 「TCU 應修補所有弱點」

> [!answer]- 解答
> **C**。
>
> - A：太具體（屬於 Requirement）
> - B：太籠統，不可驗證
> - **C：正確** — 描述 Asset (韌體) + Property (完整性) + 保護對象 (未經授權修改)
> - D：不可達成
>
> 參考 [[06-Concept-Phase/02-Cybersecurity-Goals\|06-Concept-Phase/02-Cybersecurity-Goals]]

---

## Q4. (application)

下列為某 OEM 在 Item Definition 中的「Assumption」，請判斷各自屬於哪一類 CS Claim：

1. 「OBD-II 接口由車主物理保護」
2. 「LTE 網路完整性由 MNO 提供」
3. 「OEM 雲端基礎設施屬於另一個 Item 範圍」

> [!answer]- 解答
>
> | #   | 類別                | 理由                         |
> | --- | ------------------- | ---------------------------- |
> | 1   | **Assumed-context** | 假設使用情境（車主行為）成立 |
> | 2   | **Risk-transfer**   | 風險轉移給 MNO（依服務合約） |
> | 3   | **Out-of-scope**    | 範圍外（另一個 Item 處理）   |
>
> 注意：1 與 2 都需要**驗證假設成立的機制**或 fallback。
> 3 需要**確認另一個 Item 確實涵蓋此風險**。
>
> 參考 [[06-Concept-Phase/03-Cybersecurity-Claims\|06-Concept-Phase/03-Cybersecurity-Claims]]

---

## Q5. (recall)

依 ISO 21434，每個 Cybersecurity Goal 應**對應**多少個 Threat Scenario？

A. 恰好 1 個
B. 至少 1 個
C. 不需對應
D. 至少 3 個

> [!answer]- 解答
> **B**。
> 「至少 1 個」是規範要求——CS Goal 必須有 TARA 依據，否則是空談。一個 Goal 可對應多個 Threat Scenario，一個 Threat Scenario 也可對應多個 Goal。
> 參考 [[06-Concept-Phase/02-Cybersecurity-Goals\|06-Concept-Phase/02-Cybersecurity-Goals]]

---

## Q6. (application)

某 Tier-1 從 Tier-2 採購「OoC 加密 SDK」，Tier-2 文件中宣告：「假設整合者提供 FIPS 140-2 Level 3 HSM 並負責金鑰生命週期管理」。請說明這個宣告在 ISO 21434 中扮演什麼角色，以及整合者責任。

> [!answer]- 解答
>
> **角色**：這是一組 **Cybersecurity Claims**（屬於 Assumed-context 類型）。
>
> 它表示 Tier-2 的 TARA 與 CS Concept 是**基於這些假設**——若假設不成立，TARA 結果無效。
>
> **整合者（Tier-1）責任**：
>
> 1. **驗證假設**
>    - 整合的 HSM 是否真的 FIPS 140-2 L3？
>    - 自身金鑰管理流程是否符合最佳實踐？
> 2. **若不符合**：
>    - **補強**：更換 HSM 或加上補償控制
>    - **重新 TARA**：在實際情境下重新評估
>    - **接受殘餘風險**：若可接受
> 3. **更新自身 CS Claims**：
>    - 在自身 CS Concept 中明確：「我們承擔此假設驗證責任」
>    - 後續 Assessment 會檢視
> 4. **整合 CS Case**：
>    - 引用 Tier-2 部分 CS Case
>    - 補上整合層論證
>
> 參考 [[06-Concept-Phase/03-Cybersecurity-Claims\|06-Concept-Phase/03-Cybersecurity-Claims]]、[[03-Project-Dependent/05-Component-Out-of-Context\|03-Project-Dependent/05-Component-Out-of-Context]]

---

## Q7. (recall)

下列哪一項**不屬於** Item Definition 的標準內容？

A. Scope（in/out）
B. Boundaries（物理/邏輯/時間）
C. Interfaces
D. 具體加密演算法選擇

> [!answer]- 解答
> **D**。
> 加密演算法選擇屬於 **Cybersecurity Concept** 或 **CS Requirements**，不在 Item Definition。
> Item Definition 描述「**是什麼**」，不描述「**怎麼保護**」。
> 參考 [[06-Concept-Phase/01-Item-Definition\|06-Concept-Phase/01-Item-Definition]]

---

## Q8. (analysis)

某 CS Concept 提到：「採用 Defense in Depth」。請說明這個概念並舉一個 TCU 的具體例子。

> [!answer]- 解答
>
> **Defense in Depth (DiD)**：多層次防禦，不依賴單一機制。即使某層被攻破，其他層仍能延緩或阻止攻擊。
>
> **TCU 範例 — 韌體完整性 (CG-001)**：
>
> ```
> Layer 1: 硬體 Secure Boot ROM（不可改）
>    ↓ 驗證下層
> Layer 2: Bootloader 簽章驗證
>    ↓ 驗證下層
> Layer 3: Application 簽章驗證
>    ↓ 執行
> Layer 4: 執行中完整性檢查（Run-time integrity）
>    ↓
> Layer 5: 異常通報（Detection）
>    ↓
> Layer 6: 偵測到入侵 → 進入安全模式（Response）
> ```
>
> **特性**：
>
> - 多層獨立（單層失效不影響其他層）
> - 涵蓋 Prevention + Detection + Response
> - 不同層由不同元件實作（HW + SW + 雲端）
>
> 參考 [[06-Concept-Phase/04-Cybersecurity-Concept\|06-Concept-Phase/04-Cybersecurity-Concept]]

---

## Q9. (recall)

CS Concept 是哪個 Clause 的 WP？

> [!answer]- 解答
> **Clause 9 (Concept Phase)**。
> 具體在 9.5（與 CS Claims 同節）。

---

## Q10. (application + 跨章節)

請描述從 **Item Definition** 到 **CS Requirements** 的完整資訊流。

> [!answer]- 解答
>
> ```
> 1. Item Definition (Clause 9.3)
>      • Scope、Boundaries、Functions、Interfaces、Assets
>      • Operational Environment
>      • Assumptions
>          ↓
> 2. TARA (Clause 15)
>      • Asset Identification
>      • Threat Scenarios
>      • Impact Rating (SFOP)
>      • Attack Path Analysis
>      • Attack Feasibility Rating
>      • Risk Determination
>      • Risk Treatment Decision
>          ↓
> 3. Cybersecurity Goals (Clause 9.4)
>      • 對需處置的風險定義保護目標
>      • 每個 Goal 連結到 Threat Scenario
>          ↓
> 4. Cybersecurity Claims (Clause 9.5)
>      • Out-of-scope / Assumed / Transferred 風險的處置主張
>          ↓
> 5. Cybersecurity Concept (Clause 9.5)
>      • 概念解決方案（如何達成 CS Goals）
>      • Defense in Depth
>      • 保護機制（Prevention / Detection / Response）
>          ↓
> 6. (進入 Clause 10 Product Development)
>      • Cybersecurity Requirements
>      • Security Architecture
>      • Detailed Design
>      • Implementation
>          ↓
> 7. Verification (Clause 10)
> 8. Validation (Clause 11)
> ```
>
> **關鍵：每一階段都向後 traceable**，整個資訊流是 CS Case 的論證骨架。
>
> 參考 [[01-Foundations/04-Lifecycle-Overview\|01-Foundations/04-Lifecycle-Overview]]、[[06-Concept-Phase/04-Cybersecurity-Concept\|06-Concept-Phase/04-Cybersecurity-Concept]]

---

## Related Concepts

- [[06-Concept-Phase/01-Item-Definition\|06-Concept-Phase/01-Item-Definition]]
- [[06-Concept-Phase/02-Cybersecurity-Goals\|06-Concept-Phase/02-Cybersecurity-Goals]]
- [[06-Concept-Phase/03-Cybersecurity-Claims\|06-Concept-Phase/03-Cybersecurity-Claims]]
- [[06-Concept-Phase/04-Cybersecurity-Concept\|06-Concept-Phase/04-Cybersecurity-Concept]]
- [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]

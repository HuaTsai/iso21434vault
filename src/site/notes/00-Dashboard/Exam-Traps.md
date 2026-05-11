---
{"dg-publish":true,"permalink":"/00-dashboard/exam-traps/","title":"考試陷阱與易混淆觀念","tags":["iso-21434","exam-trap","moc"],"dg-note-properties":{"title":"考試陷阱與易混淆觀念","type":"exam-traps","tags":["iso-21434","exam-trap","moc"],"created":"2026-05-11"}}
---


> 命題單位最愛測的「**看似相像、實則不同**」概念整理。
> 每個陷阱以折疊式 callout 呈現，先想答案再展開。

---

## ⚠️ Trap 1：Cybersecurity Goal vs. Cybersecurity Claim vs. Cybersecurity Requirement

> [!warning]- 三者差別是什麼？
>
> - **Cybersecurity Goal**：來自 **威脅情境 + 風險評估**，是「不希望發生的事被防止」的高層級陳述。屬性導向（CIA + 補充屬性: Confidentiality/Integrity/Availability/Authenticity/Authorization/Non-repudiation/...）。
>   - 範例：「TCU 的韌體完整性應被保護免於未經授權之修改。」
> - **Cybersecurity Claim**：對某風險的**處置決策**之主張（例如：將某風險視為 out-of-scope 並轉移至營運者）。
>   - 範例：「車主將其 OBD-II 接口的物理保護視為使用者責任。」
> - **Cybersecurity Requirement**：可驗證的技術/流程要求，是 **Goal 的細化**。
>   - 範例：「韌體應使用 ECDSA-P256 + SHA-256 簽章驗證。」（汽車 ECU 主流；RSA 多用於後端伺服器）
>
> → [[06-Concept-Phase/02-Cybersecurity-Goals\|06-Concept-Phase/02-Cybersecurity-Goals]]、[[06-Concept-Phase/03-Cybersecurity-Claims\|06-Concept-Phase/03-Cybersecurity-Claims]]

---

## ⚠️ Trap 2：CAL 與 ASIL 是同一個東西嗎？

> [!warning]- 答案：**不是**
>
> | 比較項   | **CAL** (ISO 21434)                 | **ASIL** (ISO 26262)               |
> | -------- | ----------------------------------- | ---------------------------------- |
> | 全名     | Cybersecurity Assurance Level       | Automotive Safety Integrity Level  |
> | 領域     | 資安                                | 功能安全                           |
> | 推導依據 | Impact + Attack Vector              | S × E × C                          |
> | 等級數   | CAL 1–4                             | QM, ASIL A–D                       |
> | 性質     | **保證**等級（多嚴格地做開發/驗證） | **完整性**等級（功能達成的可靠度） |
> | 強制性   | **非強制**（Annex E，informative）  | 法規/標準合規常需要                |
>
> **常見錯誤**：以為 CAL 4 = ASIL D，這是錯的。兩者目的不同。
> → [[13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level\|13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level]]

---

## ⚠️ Trap 3：Attack Feasibility 分數越高 = 越容易嗎？

> [!warning]- 答案：**不是！分數越高 = 越困難**
> 這是命題單位最愛的陷阱。Attack Potential 方法中：
>
> - 總分 0–13 → **High Feasibility (容易攻擊)**
> - 總分 ≥ 25 → **Very Low Feasibility (難以攻擊)**
>
> 記憶法：「分數是**攻擊代價**，代價越高 → 越難得手」。
> → [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]

---

## ⚠️ Trap 4：Cybersecurity Plan vs. Cybersecurity Case

> [!warning]- 兩個都是 WP，差別？
>
> - **Cybersecurity Plan**：**事前計畫**，描述「將做什麼、誰做、何時做」。隨開發演進更新。
> - **Cybersecurity Case**：**證據集合**，論證「資安目標已達成」。是 **claim + evidence + argument** 的結構。
>
> 類比：Plan = 路線圖；Case = 旅行回憶錄（含照片、票根）。
> → [[03-Project-Dependent/01-Cybersecurity-Plan\|03-Project-Dependent/01-Cybersecurity-Plan]]、[[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]

---

## ⚠️ Trap 5：Cybersecurity Validation 在 Clause 11 是什麼層級？

> [!warning]- 重點：**車輛層級 (Vehicle level)**
> Clause 11 的 Validation 與 Clause 10 的 Verification 不同：
>
> - **Verification (Clause 10)**：元件/系統層級，驗證「需求是否被正確實作」。
> - **Validation (Clause 11)**：**車輛層級**，驗證「資安目標在整車情境下是否達成」。
>
> Validation 必須涵蓋滲透測試 (Penetration testing)。
> → [[08-Cybersecurity-Validation/01-Validation-Objectives\|08-Cybersecurity-Validation/01-Validation-Objectives]]

---

## ⚠️ Trap 6：Distributed Activities 中誰負責 TARA？

> [!warning]- 答案：**依 CIA 協議定義**
> Clause 7 的核心是 **CIA (Cybersecurity Interface Agreement)**：
>
> - 誰做 TARA、誰提供哪些工件、責任邊界，**都應在 CIA 中明確定義**。
> - 不可假設供應商一定會做 TARA，也不可假設 OEM 一定會做。
> - **RASIC 矩陣** 是常見表達工具。
>
> → [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]

---

## ⚠️ Trap 7：OTS / Out-of-Context Component 差別

> [!warning]- 三個術語別搞混
>
> - **OTS (Off-the-Shelf)**：已存在的成品（COTS、SOUP、開源元件）。
> - **Out-of-Context Component**：**為通用情境開發**的元件，整合時需「重新評估」其情境適用性（與 ISO 26262 的 SEooC 概念相似）。
> - **Reused component**：來自舊專案或產品線的元件，需評估資安歷史與弱點。
>
> 三者共同重點：**整合時都需重新評估 TARA**。
> → [[03-Project-Dependent/04-Reuse\|03-Project-Dependent/04-Reuse]]、[[03-Project-Dependent/05-Component-Out-of-Context\|03-Project-Dependent/05-Component-Out-of-Context]]

---

## ⚠️ Trap 8：UN R155 vs. UN R156

> [!warning]- 兩者分工
>
> - **UN R155**：Cybersecurity & **CSMS** 整體合規。
> - **UN R156**：**Software Update** & SUMS（軟體更新管理系統）。
>
> ISO 21434 與 R155 **強相關**；OTA / 韌體更新管理對應到 **R156**。
> → [[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]

---

## ⚠️ Trap 9：Cybersecurity Monitoring (Clause 8) 不只是「監看 CAN bus」

> [!warning]- 包含什麼？
> Clause 8 的 Continual Cybersecurity Activities 涵蓋：
>
> 1. **CS Monitoring**：來源含**內部**（測試、IR）+ **外部**（CVE、CERT、研究、客戶回饋、安全社群）。
> 2. **Event Assessment**：判斷是否為「資安事件」。
> 3. **Vulnerability Analysis**：分析新弱點對既有產品的影響。
> 4. **Vulnerability Management**：決定處置（修補、Workaround、接受）。
>
> 不只是 IDS/SIEM。**情報蒐集**也是 Monitoring 一環。
> → [[05-Continual-Cybersecurity/01-Cybersecurity-Monitoring\|05-Continual-Cybersecurity/01-Cybersecurity-Monitoring]]

---

## ⚠️ Trap 10：Tailoring 的合法範圍

> [!warning]- 哪些可以 Tailor？哪些不行？
>
> - **可以 Tailor**：活動的執行方式、Work Product 的格式、深度。
> - **不可 Tailor**：標準的**目標 (Objectives)** 與**結果 (Outcomes)**。
> - Tailoring 必須**文件化**並說明**理由**（rationale）。
>
> 常見陷阱：題目給你「為了節省成本，我們省略 TARA」——這是錯誤 Tailoring。
> → [[03-Project-Dependent/03-Tailoring\|03-Project-Dependent/03-Tailoring]]

---

## ⚠️ Trap 11：Penetration Testing 必須在哪個階段？

> [!warning]- 答案：**至少在 Cybersecurity Validation（Clause 11）**，但也可在 Clause 10 的 Verification 中執行
>
> - Clause 10 的 Verification 可包含元件層級滲透測試。
> - Clause 11 的 Validation **必須**在車輛層級進行，含滲透測試。
> - Clause 8 的 Continual Activities 也包含週期性安全測試。
>
> → [[08-Cybersecurity-Validation/02-Validation-Methods\|08-Cybersecurity-Validation/02-Validation-Methods]]

---

## ⚠️ Trap 12：Asset / Damage Scenario / Threat Scenario 順序

> [!warning]- 三者的因果鏈
>
> ```
> Asset (e.g. CAN訊息)
>   ↓ 屬性被破壞 (e.g. 真實性被破壞)
> Damage Scenario (e.g. 偽造煞車訊號 → 失控撞擊)
>   ↓ 攻擊者如何達成
> Threat Scenario (e.g. 攻擊者透過 OBD 注入偽造煞車 CAN 訊息)
> ```
>
> Damage Scenario **不等於** Threat Scenario。
> Damage = **後果**；Threat = **手段+後果**。
>
> → [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]

---

## ⚠️ Trap 13：Cybersecurity Case 的「Argument」結構

> [!warning]- GSN 或 Claim-Argument-Evidence (CAE)？
> ISO 21434 **未強制**特定形式，常見實作為：
>
> - **Claim**：資安目標達成的主張。
> - **Argument**：論證邏輯（推理）。
> - **Evidence**：支撐論證的證據（測試報告、TARA、Review 記錄）。
>
> 與 ISO 26262 Safety Case 相似但獨立。
> → [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]

---

## ⚠️ Trap 14：Release for Post-Development 的條件

> [!warning]- 何時可發行到後開發？
> 必須滿足：
>
> 1. Cybersecurity Case 完成（含驗證、評估報告）。
> 2. **殘餘風險已接受** (Residual risk accepted)。
> 3. 後開發工件已準備（如 IR Plan、Update Plan、EoS 條件）。
> 4. **CIA 在分散開發情境下已關閉**。
>
> 不可在 TARA 仍有 High/Very High 未處置時發行。
> → [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]

---

## ⚠️ Trap 15：Continual Activities 的「邊界」

> [!warning]- Clause 8 從什麼時候開始？到什麼時候結束？
> **從**：標準在組織內**生效之時**（不限於某個專案）。
> **到**：產品**除役 (Decommissioning)** 為止。
>
> Continual Activities 不專屬於單一專案，是**組織層級**且**跨產品**的活動。
> → [[05-Continual-Cybersecurity/01-Cybersecurity-Monitoring\|05-Continual-Cybersecurity/01-Cybersecurity-Monitoring]]

---

## Related

- [[00-Dashboard/MOC\|00-Dashboard/MOC]]
- [[00-Dashboard/Quick-Reference\|00-Dashboard/Quick-Reference]]

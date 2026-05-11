---
{"dg-publish":true,"permalink":"/08-cybersecurity-validation/practice-validation/","title":"資安驗證練習題","tags":["iso-21434","practice","validation"],"dg-note-properties":{"title":"資安驗證練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","validation","pen-test","vehicle-level"],"tags":["iso-21434","practice","validation"],"created":"2026-05-11"}}
---


> 涵蓋：Validation Objectives、Pen Test、Validation 方法。
> 共 8 題。

---

## Q1. (recall + 易混淆)

ISO 21434 Clause 11 的 Cybersecurity Validation 是在哪個**層級**進行？

A. 程式碼層級
B. 元件層級
C. 系統層級
D. **車輛層級 (Vehicle-level)**

> [!answer]- 解答
> **D**。
> Clause 11 明確規範**車輛層級**驗證。
> Clause 10 的 Verification 才是元件/系統層級。
> 參考 [[00-Dashboard/Exam-Traps#Trap 5\|00-Dashboard/Exam-Traps#Trap 5]]

---

## Q2. (recall)

ISO 21434 Clause 11 是否**規範**滲透測試？

A. 否，只是建議
B. **是，規範要求**
C. 只有 ASIL-D 系統才需要
D. 只有 CAL-4 系統才需要

> [!answer]- 解答
> **B**。
> Clause 11 明確要求 Validation 包含 Pen Test。
> 不依 ASIL/CAL 等級豁免。
> 參考 [[00-Dashboard/Exam-Traps#Trap 11\|00-Dashboard/Exam-Traps#Trap 11]]

---

## Q3. (recall)

下列何者**不適合**作為 Cybersecurity Validation 的執行者？

A. 組織內獨立 CS 團隊
B. 外部專業 Pen Test 公司
C. **該專案的開發團隊**
D. 由 OEM 與 Tier-1 共同組成的獨立 Validation 團隊

> [!answer]- 解答
> **C**。
> 開發團隊執行 Validation 違反**獨立性**——「自評」帶來盲點。
> 參考 [[08-Cybersecurity-Validation/01-Validation-Objectives\|08-Cybersecurity-Validation/01-Validation-Objectives]]

---

## Q4. (recall + 應用)

下列哪一項是 Cybersecurity Validation 的主要對應？

A. CS Plan
B. CS Requirements
C. **CS Goals + CS Claims**
D. CSMS Policies

> [!answer]- 解答
> **C**。
> Validation 直接對應**高層級的 CS Goals**（與 CS Claims 的假設驗證）。
> CS Requirements 是 Verification（Clause 10）的對象。

---

## Q5. (application)

某 OEM 計畫對新車型進行 Pen Test，下列範圍規劃中，哪一項**不可省略**？

A. Cellular 介面
B. OBD-II 介面
C. CAN 內部訊息
D. **以上都不可省略**

> [!answer]- 解答
> **D**。
> 車輛級 Validation 必須涵蓋**完整攻擊面**：
>
> - 外部：Cellular、Wi-Fi、V2X、RKE
> - 物理介面：OBD-II、USB、充電
> - 內部：CAN、Ethernet
> - 硬體：JTAG（若仍可用）
>
> 任何省略需在 Validation Plan 中**有合理理由**，且該風險需在 TARA 中**已被處置**或**被接受**。
>
> 參考 [[08-Cybersecurity-Validation/02-Validation-Methods\|08-Cybersecurity-Validation/02-Validation-Methods]]

---

## Q6. (analysis)

請說明 **Pen Test** 與 **Red Team Exercise** 的差異。

> [!answer]- 解答
>
> | 比較       | **Pen Test**           | **Red Team**                     |
> | ---------- | ---------------------- | -------------------------------- |
> | 範圍       | 技術層面               | 完整攻擊鏈（含人 + 技術 + 流程） |
> | 時程       | 短（幾週）             | 長（數月）                       |
> | 隱蔽性     | 通常公開（防守方知道） | **隱蔽**（模擬真實攻擊）         |
> | 焦點       | 找漏洞                 | 證明能否達成攻擊目標             |
> | 含社交工程 | 通常不                 | **常含**                         |
> | 含實體入侵 | 限於授權範圍           | 廣泛                             |
> | 目標       | 列出漏洞               | 評估**整體防禦成熟度**           |
> | 適用       | 所有專案               | 成熟組織高階驗證                 |
>
> **共同點**：兩者都需要授權 + Rules of Engagement + Reporting。
>
> 在 ISO 21434 中，**Pen Test 是規範要求**；Red Team 是**建議的高階方法**。
>
> 參考 [[08-Cybersecurity-Validation/02-Validation-Methods\|08-Cybersecurity-Validation/02-Validation-Methods]]

---

## Q7. (application + 跨章節)

某 OEM 完成車輛級 Pen Test，發現 1 個 High Severity 弱點（UDS Security Access 可被 timing attack 繞過）。請依 ISO 21434 說明後續流程。

> [!answer]- 解答
>
> **1. 即時處置**：
>
> - Pen Test 發現 → 立刻通報 Project CS Manager
> - 嚴重度分級確認
> - 評估是否影響其他正在開發 / 已 Release 的產品（相同 UDS 實作）
>
> **2. Validation Report 處理**：
>
> - 該 CS Goal **未通過 Validation**
> - Report 標記為 "Conditional Approve" 或 "Reject"
> - 不可進入 Release for Post-Development
>
> **3. 修補流程（Clause 10 回流）**：
>
> - 修改 UDS Security Access 實作（constant-time 比較、加入隨機延遲、強化 lockout）
> - 更新 CS Requirements（如需要）
> - 重新進行 Unit / Integration Test
> - **重做 Validation**（至少針對該 CS Goal）
>
> **4. TARA 更新**：
>
> - 該 Threat Scenario 之 Attack Feasibility 重新評估
> - 若有其他類似元件，也需重評
>
> **5. CS Case 更新**：
>
> - 加入此次發現 + 修補 + 重測證據
> - 記錄 Lessons Learned
>
> **6. 跨組織通報（若有 CIA）**：
>
> - 依 CIA 流程通知 OEM / Tier-1 對方
>
> **7. 若相同實作已在現有產品**：
>
> - 啟動 Clause 8 弱點管理 + Clause 13 Incident Response
> - 評估 OTA 修補計畫（UN R156 SUMS）
>
> **8. 重新 Validation 通過後**：
>
> - Cybersecurity Assessment
> - Release for Post-Development
>
> 參考 [[08-Cybersecurity-Validation/02-Validation-Methods\|08-Cybersecurity-Validation/02-Validation-Methods]]、[[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]、[[05-Continual-Cybersecurity/04-Vulnerability-Management\|05-Continual-Cybersecurity/04-Vulnerability-Management]]

---

## Q8. (analysis)

請設計一個簡單的 Validation Plan 涵蓋下列 CS Goal：
「CG-007：車輛位置資料的機密性應被保護免於未授權者讀取。」

> [!answer]- 解答
>
> **Validation 範例計畫**：
>
> ```yaml
> validation_for_CG-007:
>   cs_goal: "Confidentiality of vehicle location data"
>
>   attacker_models:
>     - "Network attacker (MITM on cellular)"
>     - "Local attacker (sniffing CAN/Ethernet)"
>     - "Insider (limited credentials)"
>     - "Service personnel (workshop access)"
>
>   test_cases:
>     - name: "MITM on cellular telemetry upload"
>       method: "Set up rogue base station + decode TLS"
>       pass: "TLS 1.3 prevents decryption; cert pinning blocks rogue"
>
>     - name: "CAN sniffing for location signals"
>       method: "Connect logger to internal CAN bus"
>       pass: "Location not transmitted on CAN, or SecOC + encryption applied"
>
>     - name: "Diagnostic read of stored location"
>       method: "UDS read DID for stored telemetry without authorization"
>       pass: "Read fails without proper Security Access role"
>
>     - name: "Service mode information leakage"
>       method: "Workshop tool reads internal logs"
>       pass: "Logs do not contain unencrypted location"
>
>     - name: "Flash chip off attack"
>       method: "Remove flash, dump contents"
>       pass: "Data encrypted at rest; key in HSM not extractable"
>
>     - name: "Side-channel on TLS handshake"
>       method: "DPA on private key operation"
>       pass: "First-order DPA resistant"
>
>     - name: "PII handling compliance"
>       method: "Review logs for unintended PII"
>       pass: "PII anonymised / encrypted"
>
>   environment: "HIL bench + real vehicle prototype"
>
>   duration: "4 weeks"
>
>   pass_criteria:
>     - "All test cases pass"
>     - "No information disclosure observed"
>     - "Findings (if any) classified Low severity with documented residual risk"
>
>   independent_team: true
> ```
>
> **關鍵設計原則**：
>
> - 涵蓋多種攻擊者模型
> - 涵蓋多種介面（in-transit + at-rest）
> - 包含 negative testing（嘗試各種繞過）
> - 對應 TARA 中的 Threat Scenarios
>
> 參考 [[08-Cybersecurity-Validation/01-Validation-Objectives\|08-Cybersecurity-Validation/01-Validation-Objectives]]、[[08-Cybersecurity-Validation/02-Validation-Methods\|08-Cybersecurity-Validation/02-Validation-Methods]]

---

## Related Concepts

- [[08-Cybersecurity-Validation/01-Validation-Objectives\|08-Cybersecurity-Validation/01-Validation-Objectives]]
- [[08-Cybersecurity-Validation/02-Validation-Methods\|08-Cybersecurity-Validation/02-Validation-Methods]]
- [[07-Product-Development/02-Integration-Verification\|07-Product-Development/02-Integration-Verification]]
- [[06-Concept-Phase/02-Cybersecurity-Goals\|06-Concept-Phase/02-Cybersecurity-Goals]]

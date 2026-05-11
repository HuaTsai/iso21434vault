---
{"dg-publish":true,"permalink":"/07-product-development/practice-development/","title":"產品開發練習題","tags":["iso-21434","practice","product-development"],"dg-note-properties":{"title":"產品開發練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","design","verification","weakness","hw-sw"],"tags":["iso-21434","practice","product-development"],"created":"2026-05-11"}}
---


> 涵蓋：CS Requirements、Security Architecture、Verification、Weakness Analysis、HW/SW 考量。
> 共 10 題。

---

## Q1. (recall + 易混淆)

下列關於 Verification 與 Validation 的描述，何者**正確**？

A. 兩者是同義詞
B. Verification 在 Clause 10（元件/系統層），Validation 在 Clause 11（車輛層）
C. Verification 由客戶執行，Validation 由供應商執行
D. Validation 只在元件層

> [!answer]- 解答
> **B**。
>
> - Verification = 「Are we building it right?」（需求是否正確實作）
> - Validation = 「Are we building the right thing?」（資安目標是否在實際情境下達成）
>
> 參考 [[00-Dashboard/Exam-Traps#Trap 5\|00-Dashboard/Exam-Traps#Trap 5]]、[[07-Product-Development/02-Integration-Verification\|07-Product-Development/02-Integration-Verification]]

---

## Q2. (recall)

下列哪一個**不是** Cybersecurity Requirement 的必要屬性？

A. Verifiable
B. Atomic
C. 同時為 Top Management 簽核
D. Traceable

> [!answer]- 解答
> **C**。
> CS Requirement 的核心屬性：Verifiable / Atomic / Unambiguous / Traceable / Feasible / Necessary。
> Top Management 簽核是 CSMS 層級，非單一 Requirement 屬性。

---

## Q3. (application)

某 CS Requirement 寫：「TCU 應安全儲存私鑰」。請評論並改寫。

> [!answer]- 解答
>
> **評論問題**：
>
> 1. **不可驗證**：「安全」沒有具體標準
> 2. **不夠細節**：「儲存」方式不明（HSM？加密 NVM？eFuse？）
> 3. **無 Traceability**：未指明對應 Goal
>
> **改寫**：
>
> ```
> CSR-TCU-015：
>   TCU 應將 V2X 簽章用之 ECDSA P-256 私鑰儲存於
>   HSM 內部，且該金鑰應為 non-exportable，僅允許
>   透過 HSM 內部 API 進行簽章運算。
>
>   Parent Goal: CG-005 (V2X identity confidentiality)
>   Verification: HSM 配置檢查 + 嘗試萃取測試
>   Allocated to: HSM module
> ```
>
> 改進點：
>
> - 具體儲存位置（HSM）
> - 具體保護機制（non-exportable）
> - 具體使用方式（內部 API）
> - 對應 Goal
> - 對應驗證方法
>
> 參考 [[07-Product-Development/01-Design-Requirements\|07-Product-Development/01-Design-Requirements]]

---

## Q4. (recall)

下列哪個**不屬於** Security by Design 八大原則？

A. Least Privilege
B. Defense in Depth
C. Fail Secure
D. Maximum Coupling

> [!answer]- 解答
> **D**。
> 應為 **Economy of Mechanism**（簡潔），與 Maximum Coupling 相反。
> 八大原則：Least Privilege、Defense in Depth、Fail Secure、Separation of Duties、Complete Mediation、Open Design、Psychological Acceptability、Economy of Mechanism。

---

## Q5. (recall + 易混淆)

下列何者**最正確**描述 Weakness 與 Vulnerability 在開發階段的處理？

A. 兩者都必須立即修補
B. Weakness 可記錄但不必立即修；Vulnerability（可被利用）需處置
C. Weakness 比 Vulnerability 更嚴重
D. 開發階段不需做這種分析

> [!answer]- 解答
> **B**。
> 開發階段的分析需先**判斷是否可被利用**：
>
> - 不可利用的 Weakness：記錄，後續環境變化時可能升級
> - 可利用的 Vulnerability：需處置（修補/緩解）
>
> 參考 [[07-Product-Development/03-Weakness-Vulnerability-Analysis\|07-Product-Development/03-Weakness-Vulnerability-Analysis]]、[[05-Continual-Cybersecurity/03-Vulnerability-Analysis\|05-Continual-Cybersecurity/03-Vulnerability-Analysis]]

---

## Q6. (application)

請列出**至少三種**在開發階段主動發現 Weakness 的方法。

> [!answer]- 解答
>
> 1. **Threat Modeling Review**：針對設計，使用 STRIDE 或攻擊樹
> 2. **SAST (Static Analysis)**：自動偵測程式碼缺陷
>    - 工具：Coverity、Polyspace、SonarQube
> 3. **SCA (Software Composition Analysis)**：對依賴元件做 CVE 比對
>    - 工具：Black Duck、Snyk、OWASP Dependency-Check
> 4. **Code Review (Manual)**：人工檢視關鍵區域
>    - 加密實作、認證流程、邊界檢查
> 5. **DAST (Dynamic Analysis) / Fuzz Testing**：對執行中元件做模糊測試
>    - 工具：AFL、libFuzzer、Defensics
> 6. **Memory Error Detection**：ASan、Valgrind 等執行時檢測
> 7. **Penetration Test (元件級)**：模擬攻擊測試
>
> 參考 [[07-Product-Development/03-Weakness-Vulnerability-Analysis\|07-Product-Development/03-Weakness-Vulnerability-Analysis]]

---

## Q7. (recall)

下列何者是汽車**根信任 (Root of Trust)** 的最佳實踐？

A. 韌體中 hard-coded public key
B. eFuse / OTP 中儲存 root public key hash
C. EEPROM 中儲存 root public key
D. 雲端動態下載 root public key

> [!answer]- 解答
> **B**。
> Root of Trust 需**不可篡改**。eFuse / OTP 是一次性可程式化記憶體，符合不可篡改要求。
> 通常儲存的是 **hash**（節省空間），完整 public key 在受信任的 ROM/Flash 中。
>
> 參考 [[07-Product-Development/04-HW-SW-Considerations\|07-Product-Development/04-HW-SW-Considerations]]

---

## Q8. (application)

某 ECU 在出貨前忘記關閉 JTAG 介面。在 ISO 21434 視角下：

1. 這是什麼層級的問題？
2. 後果可能是什麼？
3. 如何處理？

> [!answer]- 解答
>
> **1. 層級**：
> 涉及多層：
>
> - **HW 層**：JTAG 應在硬體層 disable（fuse blow 或啟動時設定）
> - **生產層**（Clause 12）：Provisioning 流程缺漏
> - **驗證層**（Clause 11）：Validation 未發現此缺陷
>
> **2. 後果**：
>
> - 攻擊者可透過 JTAG 直接讀取/修改韌體
> - 萃取金鑰、執行未簽章程式
> - **可能違反 Cybersecurity Goal**（韌體完整性、機密性）
> - **UN R155** 認證可能撤回
> - **召回**風險
>
> **3. 處理**：
>
> - **緊急**：
>   - 評估已出貨產品的暴露程度
>   - 啟動 Incident Response（Clause 13）
>   - 通報 OEM（CIA 流程）
> - **短期**：
>   - 韌體更新（OTA）：偵測 JTAG 連接並啟動 secure mode
>   - 設定 lockout（如連續 JTAG 嘗試 N 次後鎖定）
> - **中期**：
>   - 召回更新 fuse 設定（若可在 OTA 中操作）
>   - 或實體召回（若無法 OTA 處理）
> - **長期**：
>   - **Production Validation** 加入 JTAG 狀態檢查
>   - **Pen Test** 必測項目
>   - CSMS 流程改善
>
> **CS Case 更新**：
>
> - 記錄此事件
> - 殘餘風險評估與接受
> - Lessons Learned 寫入組織知識庫
>
> 參考 [[07-Product-Development/04-HW-SW-Considerations\|07-Product-Development/04-HW-SW-Considerations]]、[[09-Production/01-Production-Controls\|09-Production/01-Production-Controls]]、[[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]

---

## Q9. (recall)

下列關於汽車 CAN 訊息資安的描述，何者**最正確**？

A. CAN 本身已有加密，不需額外保護
B. SecOC 是 AUTOSAR 標準，提供 CMAC + Freshness Value 機制
C. CAN 訊息只能用 TLS 保護
D. SecOC 只能保護機密性，不保護完整性

> [!answer]- 解答
> **B**。
>
> - A：CAN 原始協議**無**加密與認證
> - **B：正確** — SecOC 提供完整性（CMAC）+ 抗 replay（Freshness Value）
> - C：CAN 是 broadcast 協議，不適用 TLS
> - D：SecOC 主要保護**完整性 + 真實性**，非機密性
>
> 參考 [[07-Product-Development/04-HW-SW-Considerations\|07-Product-Development/04-HW-SW-Considerations]]

---

## Q10. (analysis + 跨章節)

請說明 **Traceability Matrix** 在 ISO 21434 V-Model 中的角色與必要性。

> [!answer]- 解答
>
> **Traceability Matrix** 是 ISO 21434（與 26262）的核心 WP，貫穿 V-Model：
>
> ```
> Threat Scenario (TARA)
>      ↕
> Cybersecurity Goal
>      ↕
> Cybersecurity Concept
>      ↕
> CS Requirement
>      ↕
> Design Element
>      ↕
> Implementation
>      ↕
> Verification Test
>      ↕
> Validation Test
> ```
>
> **必要性**：
>
> 1. **完整性**：證明所有 Threat 都有對應 Goal、所有 Goal 都有實作 + 測試
> 2. **影響分析**：當某需求變更，可追蹤受影響的下游
> 3. **變更管理**：變更時知道哪些測試需重做
> 4. **CS Case 證據**：論證「所有 Goal 達成」的骨架
> 5. **稽核/Assessment**：Assessor 可快速檢視合規
> 6. **規範要求**：Clause 10 明確要求
>
> **格式**：
> 通常為矩陣表，列為元素（Threat、Goal、Req...），可雙向查詢。
> 工具：Polarion、DOORS、Codebeamer 等需求管理工具。
>
> **不可**僅以「文件之間引用」取代正式 Traceability Matrix。
>
> 參考 [[07-Product-Development/02-Integration-Verification\|07-Product-Development/02-Integration-Verification]]、[[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]

---

## Related Concepts

- [[07-Product-Development/01-Design-Requirements\|07-Product-Development/01-Design-Requirements]]
- [[07-Product-Development/02-Integration-Verification\|07-Product-Development/02-Integration-Verification]]
- [[07-Product-Development/03-Weakness-Vulnerability-Analysis\|07-Product-Development/03-Weakness-Vulnerability-Analysis]]
- [[07-Product-Development/04-HW-SW-Considerations\|07-Product-Development/04-HW-SW-Considerations]]

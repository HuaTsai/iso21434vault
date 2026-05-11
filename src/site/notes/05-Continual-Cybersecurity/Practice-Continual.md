---
{"dg-publish":true,"permalink":"/05-continual-cybersecurity/practice-continual/","title":"持續性資安活動練習題","tags":["iso-21434","practice","continual"],"dg-note-properties":{"title":"持續性資安活動練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","monitoring","event","vulnerability"],"tags":["iso-21434","practice","continual"],"created":"2026-05-11"}}
---


> 涵蓋：Monitoring、Event Assessment、Vulnerability Analysis、Vulnerability Management。
> 共 10 題。

---

## Q1. (recall)

ISO 21434 Clause 8 的活動**範圍**是什麼？

A. 只有產品在運行時
B. 只有發現安全事件時
C. 從 CSMS 在組織內生效起，至產品除役止，跨整個生命週期
D. 只在 Release 後

> [!answer]- 解答
> **C**。Clause 8 是**橫貫**活動，不限於後開發。
> 參考 [[05-Continual-Cybersecurity/01-Cybersecurity-Monitoring\|05-Continual-Cybersecurity/01-Cybersecurity-Monitoring]]、[[00-Dashboard/Exam-Traps#Trap 15\|00-Dashboard/Exam-Traps#Trap 15]]

---

## Q2. (recall + 易混淆)

下列何者**不屬於** Cybersecurity Monitoring 的資料來源？

A. 內部 IDS / SIEM
B. CVE 資料庫
C. 客戶服務回饋
D. 公司年度財務報告

> [!answer]- 解答
> **D**。
> Monitoring 包含內部（IDS、SIEM、測試、客服）+ 外部（CVE、CERT、ISAC、研究、政府公告）。
> 參考 [[05-Continual-Cybersecurity/01-Cybersecurity-Monitoring\|05-Continual-Cybersecurity/01-Cybersecurity-Monitoring]]、[[00-Dashboard/Exam-Traps#Trap 9\|00-Dashboard/Exam-Traps#Trap 9]]

---

## Q3. (recall)

請描述 Event、Vulnerability、Incident 的差別。

> [!answer]- 解答
>
> | 術語              | 定義                       | 確定性                     |
> | ----------------- | -------------------------- | -------------------------- |
> | **Event**         | 任何可能與資安相關的觀察   | 尚未確認                   |
> | **Vulnerability** | 確認的、可被利用的弱點     | 確認可利用，但尚未發生攻擊 |
> | **Incident**      | 實際發生（或正發生）的攻擊 | 已發生                     |
>
> 關係：Event → 經 Assessment → 可能分流為 Vulnerability 或 Incident。
> 參考 [[05-Continual-Cybersecurity/02-Event-Assessment\|05-Continual-Cybersecurity/02-Event-Assessment]]

---

## Q4. (recall + 易混淆)

下列何者**最正確**描述 Weakness 與 Vulnerability 的關係？

A. 兩者完全相同
B. 所有 Vulnerability 都是 Weakness，但反之不必然
C. 所有 Weakness 都是 Vulnerability
D. 兩者無關

> [!answer]- 解答
> **B**。
> Vulnerability 是「**可被利用的** Weakness」。某 weakness 雖存在但若不可被觸發/利用，則不算 vulnerability。
> 參考 [[05-Continual-Cybersecurity/03-Vulnerability-Analysis\|05-Continual-Cybersecurity/03-Vulnerability-Analysis]]、[[01-Foundations/02-Key-Terms-Definitions\|01-Foundations/02-Key-Terms-Definitions]]

---

## Q5. (application)

CSIRT 收到 Auto-ISAC 通報「某新型 CAN-bus 攻擊技術公開發表」。請說明依 Clause 8 應如何處理（前 3 步）。

> [!answer]- 解答
>
> **Step 1：Monitoring 紀錄**
>
> - 記錄來源、日期、初步描述
> - 標記為 Event candidate
>
> **Step 2：Event Assessment**
>
> - 評估是否與我們產品相關（SBOM 對應、架構檢視）
> - 判斷攻擊情境在我們系統下是否成立
> - 初步嚴重度
> - 分流：False Positive / Vulnerability / Incident / 需進一步調查
>
> **Step 3：依分流結果**
>
> - 若為 **Vulnerability** → Clause 8.5 Vulnerability Analysis
> - 若為 **Incident**（已被利用）→ Clause 13 Incident Response
> - 若 **不適用** → 關閉並文件化理由
>
> 後續可能觸發 **TARA 更新**（如攻擊面/可行性大幅變動）。
>
> 參考 [[05-Continual-Cybersecurity/01-Cybersecurity-Monitoring\|05-Continual-Cybersecurity/01-Cybersecurity-Monitoring]]、[[05-Continual-Cybersecurity/02-Event-Assessment\|05-Continual-Cybersecurity/02-Event-Assessment]]

---

## Q6. (recall)

下列哪個 Vulnerability Treatment 選項**最適合**用於「來自供應商的弱點」？

A. 自己修補就好
B. Share/Transfer（要求供應商修補 + 在 CIA 中追蹤）
C. 完全忽略
D. 立即移除整個元件

> [!answer]- 解答
> **B**。Share/Transfer 透過 CIA 機制要求供應商履行修補責任。客戶端仍需驗證修補有效性。
> 自己修補（A）可能不適用（供應商擁有源碼）；忽略（C）違反規範；移除元件（D）可能不可行。
> 參考 [[05-Continual-Cybersecurity/04-Vulnerability-Management\|05-Continual-Cybersecurity/04-Vulnerability-Management]]

---

## Q7. (analysis)

請比較 **Permanent Patch** 與 **Mitigation/Workaround** 的差異與適用情境。

> [!answer]- 解答
>
> | 比較 | **Permanent Patch**      | **Mitigation/Workaround**          |
> | ---- | ------------------------ | ---------------------------------- |
> | 範圍 | 修正根因（程式碼/設計）  | 不修根因，降低觸發/影響            |
> | 速度 | 慢（需開發、測試、部署） | 快（通常 config / firewall）       |
> | 效果 | 徹底                     | 部分                               |
> | 適用 | 長期解決                 | 緊急情境、過渡期                   |
> | 例子 | OpenSSL 升級至 3.0.13    | 雲端 firewall 擋特定 TLS handshake |
>
> **典型流程**：緊急狀況下先用 Mitigation 爭取時間，再開發 Permanent Patch。
> 兩者**都需文件化**。Mitigation 不可作為長期方案。
>
> 參考 [[05-Continual-Cybersecurity/04-Vulnerability-Management\|05-Continual-Cybersecurity/04-Vulnerability-Management]]

---

## Q8. (application + 跨章節)

某 CSIRT 處理一個 CVE，發現對某產品有影響。處置後是否一定要更新 TARA？

> [!answer]- 解答
>
> **不一定，但需評估**。判斷準則：
>
> **應更新 TARA**：
>
> - 新攻擊路徑出現（既有 TARA 未涵蓋）
> - 攻擊可行性大幅改變（如公開 PoC、自動化工具）
> - 影響先前評估為「Low」的元件升級為「High/Critical」
> - 變更影響跨多個元件或 Item
>
> **可不更新 TARA 但需紀錄**：
>
> - 既有 TARA 已涵蓋（既有 risk treatment 已生效）
> - 攻擊可行性微幅變化
> - 已透過 Vulnerability Management 處置完成
>
> 不論是否更新 TARA，**CS Case 應更新**（至少在 evidence 部分加入此次處置紀錄）。
>
> 參考 [[05-Continual-Cybersecurity/03-Vulnerability-Analysis\|05-Continual-Cybersecurity/03-Vulnerability-Analysis]]、[[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]

---

## Q9. (recall)

業界 CVD（Coordinated Vulnerability Disclosure）流程的標準 embargo 期（預設）是多久？

A. 7 天
B. 30 天
C. 90 天
D. 1 年

> [!answer]- 解答
> **C. 90 天**。
> 業界（Google Project Zero、CERT 等）共識的預設揭露窗口。視情況可協商延長或提早。
> 參考 [[05-Continual-Cybersecurity/04-Vulnerability-Management\|05-Continual-Cybersecurity/04-Vulnerability-Management]]

---

## Q10. (application + 法規)

某 OEM 完成弱點修補開發後準備 OTA 部署。除了 ISO 21434 Clause 8.6，還需符合**哪個法規流程**？

> [!answer]- 解答
>
> **UN R156 SUMS** (Software Update Management System)。
>
> R156 要求 OTA 部署需：
>
> 1. 識別受影響車型
> 2. 影響評估（safety + security + **type approval**）
> 3. 修補測試
> 4. 部署計畫（時間、批次、地區）
> 5. 使用者通知（特定情況需取得同意）
> 6. 部署過程的車輛狀態管理
> 7. 失敗回滾機制
> 8. 部署後驗證
>
> 此外，ISO 24089（軟體更新工程）為 R156 的技術依據。
>
> 流程**橫跨** ISO 21434（資安處置） + ISO 24089（更新工程） + UN R156（合規）。
>
> 參考 [[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]、[[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]

---

## Related Concepts

- [[05-Continual-Cybersecurity/01-Cybersecurity-Monitoring\|05-Continual-Cybersecurity/01-Cybersecurity-Monitoring]]
- [[05-Continual-Cybersecurity/02-Event-Assessment\|05-Continual-Cybersecurity/02-Event-Assessment]]
- [[05-Continual-Cybersecurity/03-Vulnerability-Analysis\|05-Continual-Cybersecurity/03-Vulnerability-Analysis]]
- [[05-Continual-Cybersecurity/04-Vulnerability-Management\|05-Continual-Cybersecurity/04-Vulnerability-Management]]

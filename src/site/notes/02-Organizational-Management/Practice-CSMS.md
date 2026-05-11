---
{"dg-publish":true,"permalink":"/02-organizational-management/practice-csms/","title":"CSMS 練習題","tags":["iso-21434","practice","csms"],"dg-note-properties":{"title":"CSMS 練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","csms","organizational"],"tags":["iso-21434","practice","csms"],"created":"2026-05-11"}}
---


> 涵蓋：CSMS、文化、管理系統整合、工具管理、資訊共享、稽核。
> 共 10 題。

---

## Q1. (recall)

CSMS 是哪一個 Clause 的核心？

> [!answer]- 解答
> **Clause 5**：Organizational cybersecurity management。

---

## Q2. (recall + 易混淆)

下列哪一項是 CSMS 與 ISMS (ISO 27001) 的**主要差異**？

A. CSMS 包含 ISMS
B. CSMS 聚焦**車輛產品**資安；ISMS 聚焦**組織 IT** 資訊安全
C. 兩者對象相同，僅標準不同
D. CSMS 不包含管理流程，只含技術

> [!answer]- 解答
> **B**。
> CSMS 是產品（車輛/E/E）資安；ISMS 是組織 IT 資訊安全。兩者**互補可整合**，但對象不同。
> 參考 [[02-Organizational-Management/03-Management-Systems\|02-Organizational-Management/03-Management-Systems]]

---

## Q3. (recall)

UN R155 CSMS 認證的有效期是多久？

> [!answer]- 解答
> **3 年**。期間仍需執行內部稽核（至少年度）。

---

## Q4. (application)

某公司新導入 ISO 21434，CSMS 才剛建立 6 個月。在準備 UN R155 認證稽核時，下列何者**最重要**？

A. 提交最新的 CSMS 政策文件即可
B. 展示「政策 + 執行紀錄 + 持續改善證據」
C. 只需 Top Management 簽核就好
D. 等政策運行 3 年後再申請

> [!answer]- 解答
> **B**。
> 認證稽核重視 **PDCA 證據**：
>
> - 政策（Plan）
> - 執行紀錄（Do）
> - 量測/檢討（Check）
> - 改善行動（Act）
>
> 6 個月雖短，但若有完整證據鏈仍可通過初次稽核。Top Mgmt 簽核**必要但不充分**。

---

## Q5. (recall)

下列哪個**不是** CSMS 必要的 Work Product？

A. Organizational Cybersecurity Policy
B. Competence Management Plan
C. **ASIL Decomposition Record**
D. Tool Approval Records

> [!answer]- 解答
> **C. ASIL Decomposition Record**。
> ASIL 屬於 ISO 26262，不在 ISO 21434 範圍。資安的對應等級是 **CAL**（且非強制）。
> 參考 [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]、[[00-Dashboard/Exam-Traps#Trap 2\|00-Dashboard/Exam-Traps#Trap 2]]

---

## Q6. (application + 分析)

請說明 **CSMS Audit** 與 **Cybersecurity Assessment** 的差異，並各舉一例情境。

> [!answer]- 解答
>
> | 比較 | CSMS Audit | Cybersecurity Assessment |
> |---|---|---|
> | 層級 | 組織 | 專案 |
> | 焦點 | 流程是否被遵循 | 專案結果是否充分 |
> | Clause | 5 | 6.4.10 |
> | 頻率 | 至少年度 | 重大階段（Release 前）|
>
> **CSMS Audit 範例**：稽核員檢視「公司 TARA 流程是否在所有近期專案被執行」。發現某專案未做 TARA → Major NC。
>
> **Cybersecurity Assessment 範例**：評估員針對 TCU-2026 專案，檢視 TARA 完整性、CS Goals 合理性、Verification/Validation 結果、殘餘風險接受程度 → 給出「同意/拒絕」Release 建議。
>
> 參考 [[02-Organizational-Management/06-Audit-and-Assessment\|02-Organizational-Management/06-Audit-and-Assessment]]

---

## Q7. (analysis)

某 OEM 想將下列幾個管理系統整合成 IMS（Integrated Management System）：ISMS、QMS、CSMS、Safety Mgmt。請列出可整合與**不可整合**的部分。

> [!answer]- 解答
> **可共享**：
>
> - 文件控制流程
> - 變更管理機制
> - 內部稽核**流程**（非稽核員專業）
> - 培訓平台（基礎設施）
> - CAPA（Corrective and Preventive Action）系統
> - Top Management 承諾
>
> **不可共享（需獨立）**：
>
> - 風險評估方法（TARA、HARA、FMEA、ISMS 風險評估各自獨立）
> - 領域專業內容（CS、Safety、Quality 各自方法論）
> - 稽核員的**領域知識**
> - KPI 指標（各自獨立）
> - Item Definition 雖共享，但 CS 與 Safety 的評估**獨立**
>
> 結論：基礎設施可整合，但**領域專業必須保留**。
>
> 參考 [[02-Organizational-Management/03-Management-Systems\|02-Organizational-Management/03-Management-Systems]]

---

## Q8. (application)

公司有一台新型 TARA 工具想引入使用，依 ISO 21434，下列何者**必須**完成？

A. 只要 IT 部門批准即可
B. 評估工具能力、可信度、可重現性，並建立 Tool Approval Record
C. 直接使用，等問題出現再評估
D. 只在 ASIL D 專案使用前才需評估

> [!answer]- 解答
> **B**。
> Clause 5.4.6 要求工具評估與批准紀錄。所有用於資安活動的工具都需評估，不限 ASIL 等級（ASIL 是 26262 概念）。
>
> 參考 [[02-Organizational-Management/04-Tool-Management\|02-Organizational-Management/04-Tool-Management]]

---

## Q9. (recall + 應用)

ISO 21434 要求組織參與「資訊共享」，下列何者**最完整**描述其範圍？

A. 只需接收 CVE 通報
B. 只需參加 Auto-ISAC
C. 包含 Inbound（外部情報）+ Outbound（對外分享），含 CERT、ISAC、CVE、研究、客戶回饋等
D. 只需內部跨專案分享

> [!answer]- 解答
> **C**。
> 資訊共享是雙向且多來源的。包含：
>
> - Inbound：CERT、ISAC、CVE 資料庫、供應商通報、學術研究、客戶回饋、政府公告
> - Outbound：依 TLP 分類，向 ISAC、社群、CVE 揭露
>
> 同時組織也需建立 **VDP** 接收外部研究者通報。
>
> 參考 [[02-Organizational-Management/05-Information-Sharing\|02-Organizational-Management/05-Information-Sharing]]

---

## Q10. (analysis)

公司年度 CSMS 內部稽核時，稽核員是同一個專案的 CS Engineer。發現 1 個 Major NC，但因稽核員與被稽核活動有關，無法客觀判斷。請依 ISO 21434 評論並提出改善建議。

> [!answer]- 解答
> **問題**：違反**獨立性要求**（Clause 5.4.7）。稽核員不可為被稽核活動的負責人或執行者。
>
> **影響**：
>
> 1. 稽核結果可信度降低
> 2. 認證機構可能不接受此次稽核
> 3. UN R155 認證可能受影響
>
> **改善建議**：
>
> 1. **立即**：由另一獨立人員重新稽核同一範圍
> 2. **短期**：建立稽核員池，跨專案輪調避免衝突
> 3. **中期**：考慮聘請外部稽核員或專業稽核服務
> 4. **長期**：將獨立性檢查納入 CSMS 流程，每次稽核前確認
>
> 此外，該稽核員發現的 Major NC 仍應評估真實性（不因獨立性問題而忽略），但需獨立驗證。
>
> 參考 [[02-Organizational-Management/06-Audit-and-Assessment\|02-Organizational-Management/06-Audit-and-Assessment]]

---

## Related Concepts

- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]
- [[02-Organizational-Management/02-Cybersecurity-Culture\|02-Organizational-Management/02-Cybersecurity-Culture]]
- [[02-Organizational-Management/03-Management-Systems\|02-Organizational-Management/03-Management-Systems]]
- [[02-Organizational-Management/04-Tool-Management\|02-Organizational-Management/04-Tool-Management]]
- [[02-Organizational-Management/05-Information-Sharing\|02-Organizational-Management/05-Information-Sharing]]
- [[02-Organizational-Management/06-Audit-and-Assessment\|02-Organizational-Management/06-Audit-and-Assessment]]

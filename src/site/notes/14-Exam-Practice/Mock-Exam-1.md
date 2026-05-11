---
{"dg-publish":true,"permalink":"/14-exam-practice/mock-exam-1/","title":"模擬試題 1：基礎觀念 + 生命週期","tags":["iso-21434","mock-exam"],"dg-note-properties":{"title":"模擬試題 1：基礎觀念 + 生命週期","type":"mock-exam","source_pdf":"內部彙整","keywords":["mock-exam","foundations","lifecycle"],"tags":["iso-21434","mock-exam"],"created":"2026-05-11"}}
---


> 20 題綜合模擬。建議計時 30 分鐘完成後再核對。

---

## 一、單選題

### Q1

ISO/SAE 21434:2021 是哪一年發布？

A. 2018 B. 2020 C. 2021 D. 2023

> [!answer]-
> **C. 2021**（2021 年 8 月聯合發布）

---

### Q2

ISO 21434 的主體規範性 Clause 範圍為何？

A. 1-15 B. 5-15 C. 9-15 D. 全部 Clause

> [!answer]-
> **B. 5-15**。Clause 1-3 為範圍/參考/術語，Clause 4 為一般考量，Annex 多為 informative。

---

### Q3

下列哪個術語**不在** ISO 21434 範圍？

A. CSMS B. TARA C. HARA D. CIA

> [!answer]-
> **C. HARA**（Hazard Analysis and Risk Assessment）是 ISO 26262 概念。

---

### Q4

某 OEM 與 Tier-1 開發新車型，誰負責簽署 CIA？

A. 只有 Project Manager
B. 雙方資安專業人員 + 適當層級主管
C. 法務部門即可
D. 不需簽署

> [!answer]-
> **B**。CIA 是工程文件，需 CS 專業參與，加上適當層級權威。

---

### Q5

UN R155 CSMS 認證有效期？

A. 1 年 B. 2 年 C. 3 年 D. 5 年

> [!answer]-
> **C. 3 年**

---

### Q6

Cybersecurity Validation（Clause 11）的層級為何？

A. 元件層 B. 系統層 C. 車輛層 (Vehicle-level) D. 程式碼層

> [!answer]-
> **C. Vehicle-level**

---

### Q7

下列何者**最正確**？

A. CAL 4 = ASIL D
B. CAL 與 ASIL 是兩個獨立等級系統
C. ASIL 包含 CAL
D. CAL 取代 ASIL

> [!answer]-
> **B**。CAL（21434 Annex E）與 ASIL（26262）獨立。

---

### Q8

某 Threat Scenario 的 Attack Potential 總分為 **18**，對應 Feasibility 為？

A. High B. Medium C. Low D. Very Low

> [!answer]-
> **B. Medium**。
> 0-13: High / 14-19: Medium / 20-24: Low / ≥25: Very Low
> 18 落於 14-19 → Medium

---

### Q9

ISO 21434 的 Tailoring 規則中，下列**不可**裁適的是？

A. WP 格式
B. 活動的執行方式
C. 活動深度
D. 標準的 Objectives

> [!answer]-
> **D**。Objectives 不可裁適——必須達成。

---

### Q10

Damage Scenario 是從誰的角度描述？

A. 攻擊者 B. Road User C. 開發者 D. 監管機構

> [!answer]-
> **B. Road User**

---

## 二、複選題（多選）

### Q11. (複選)

下列哪些屬於 ISO 21434 的 SFOP 衝擊類別？

A. Safety B. Financial C. Operational D. Privacy E. Performance

> [!answer]-
> **A, B, C, D**。
> **SFOP** = Safety, Financial, Operational, Privacy。
> E. Performance 不在 SFOP 中。

---

### Q12. (複選)

下列哪些是 Risk Treatment 的合法選項？

A. Avoid B. Reduce C. Share/Transfer D. Retain E. Ignore

> [!answer]-
> **A, B, C, D**。
> 「Ignore」**不是**合法處置——所有風險都需被有意識地決策（即使 Retain 也需文件化）。

---

### Q13. (複選)

下列哪些是 Cybersecurity Plan 的**必要**內容？

A. 活動清單與時程
B. 角色與責任 (RASIC)
C. Tailoring 決策
D. 適用 Clause
E. 具體加密演算法選擇

> [!answer]-
> **A, B, C, D**。E 屬於設計階段。

---

## 三、申論題

### Q14

請列出 TARA 八步驟並各以一句話描述其目的。

> [!answer]-
>
> 1. **Asset Identification**：識別「有價值」需保護的對象
> 2. **Threat Scenario Identification**：識別「如何威脅」這些 asset
> 3. **Impact Rating**：評估若被威脅實現的「後果嚴重度」(SFOP)
> 4. **Attack Path Analysis**：分析「攻擊者要走哪些步驟」實現威脅
> 5. **Attack Feasibility Rating**：評估「最容易那條 path」的可行性
> 6. **Risk Value Determination**：結合 Impact × Feasibility 得「風險值」
> 7. **Risk Treatment Decision**：決定處置策略（Avoid/Reduce/Share/Retain）
> 8. **持續監控與更新**：TARA 是 living document

---

### Q15

請說明 Cybersecurity Plan 與 Cybersecurity Case 的差異與關係。

> [!answer]-
>
> | 比較 | CS Plan                 | CS Case                     |
> | ---- | ----------------------- | --------------------------- |
> | 時序 | **事前計畫**            | **事後 / 進行中累積證據**   |
> | 內容 | 將做什麼、誰做、何時做  | 已做什麼 + 達成證據         |
> | 結構 | 活動清單、RASIC、時程   | Claim - Argument - Evidence |
> | 階段 | Clause 6 制定，持續更新 | Clause 6 持續累積至 Release |
>
> **關係**：CS Plan **規範** CS Case 將如何被論證。執行 Plan 過程中**累積**證據填入 Case。
>
> 兩者都是 Living Document，且都會被 Cybersecurity Assessment 檢視。

---

### Q16

ISO 21434 Clause 8 的「持續性活動」涵蓋什麼？這些活動的生命週期範圍為何？

> [!answer]-
>
> **涵蓋四個子活動**：
>
> 1. **Cybersecurity Monitoring**（8.3）：內外部情報蒐集
> 2. **Event Assessment**（8.4）：Triage，判斷是否為事件/弱點
> 3. **Vulnerability Analysis**（8.5）：對弱點深度分析
> 4. **Vulnerability Management**（8.6）：決定處置並追蹤完成
>
> **生命週期範圍**：
>
> - **從**：CSMS 在組織內生效之時
> - **到**：產品**除役**（Decommissioning）為止
>
> 是**橫貫**活動，**不專屬**任何單一階段或專案。

---

### Q17

請說明 Release for Post-Development（Clause 6.4.11）的必要條件。

> [!answer]-
>
> 必須**全部**滿足：
>
> 1. **Cybersecurity Case 完成**
> 2. **Cybersecurity Validation 通過**（Clause 11）
> 3. **Cybersecurity Assessment 通過**（獨立評估）
> 4. **所有 TARA 風險已處置或明確接受**
>    - 未處置的 High/Very High 風險 → **不可** Release
> 5. **殘餘風險已被適當層級接受 + 文件化**
> 6. **後開發工件已準備**：
>    - Incident Response Plan
>    - Update Management Plan
>    - EoS Plan（初稿）
>    - Operational Monitoring Plan
> 7. **CIA 已關閉所有 open items**（分散開發情境）
> 8. **法規文件齊備**（如 UN R155 對應）
>
> 通過後責任**移轉**至 Operations & Maintenance 團隊。

---

### Q18

請說明為什麼「ISO 21434 + UN R155」 與「ISO 24089 + UN R156」是**並列**而非從屬關係。

> [!answer]-
>
> 兩組標準/法規處理**不同主題**：
>
> | 組                      | 主題                | 範圍                                    |
> | ----------------------- | ------------------- | --------------------------------------- |
> | **ISO 21434 + UN R155** | 整體資安 + CSMS     | 全生命週期、所有資安活動                |
> | **ISO 24089 + UN R156** | 軟體更新工程 + SUMS | 專注**軟體更新流程**（含 OTA + 非 OTA） |
>
> **不是從屬**：
>
> - 一個產品可能符合 R155 但不需 R156（無更新功能）
> - 一個產品可能符合 R156 但屬於 R155 範圍外（如 non-vehicle）
>
> **重疊處**：
>
> - OTA 更新的資安面（R155 + R156 都涉及）
> - 變更管理 → CS Case 更新
>
> 認證**分別**進行：R155 CSMS 認證 + R156 SUMS 認證。

---

### Q19

某 Tier-1 在開發過程中發現一個產品「先前評估為 Low Risk」的元件，因新的攻擊技術公開而升級為 **High Risk**。請依 ISO 21434 說明應如何處理。

> [!answer]-
>
> **步驟**：
>
> 1. **觸發 Clause 8 流程**：
>    - Monitoring 蒐集到此新技術
>    - Event Assessment → Vulnerability Analysis
> 2. **TARA 更新**（Clause 15）：
>    - 重評該 Threat Scenario 的 Attack Feasibility
>    - 重新計算 Risk Value
> 3. **Risk Treatment 重評**：
>    - Low Risk 時可能 Retain
>    - High Risk 時通常需 Reduce
> 4. **CS Case 更新**：
>    - 加入此次重評紀錄
>    - 加入修補措施證據
> 5. **若已 Release**：
>    - 啟動 Clause 13 弱點管理
>    - OTA 修補（依 UN R156 SUMS）
>    - 通知客戶、監管機構（視嚴重度）
> 6. **跨組織通報**（依 CIA）：
>    - 通知 OEM
>    - 評估其他類似元件
> 7. **CSMS 紀錄**：
>    - Lessons Learned
>    - 更新 Monitoring 過程（為何先前未發現）

---

### Q20

請說明 Cybersecurity Monitoring（Clause 8.3）的資料來源（至少 5 種）。

> [!answer]-
>
> **Internal 來源**：
>
> 1. 內部 IDS / SIEM
> 2. 客戶服務回饋 / 保固紀錄
> 3. 內部 Pen Test / Bug Bounty 結果
> 4. Incident Response 紀錄
> 5. 開發過程的 SAST / DAST 發現
>
> **External 來源**：6. CVE 資料庫（MITRE、NIST NVD）7. CERT 通告（CERT-EU、JPCERT 等）8. ISAC（如 Auto-ISAC）9. 學術研究（Black Hat、DEF CON）10. 供應商安全公告 11. 政府 / 監管警示（NHTSA、ENISA、UN）12. 公開的競爭者召回 / 公告
>
> **關鍵**：不只技術監控（IDS），還含**情報蒐集**。

---

## Related Concepts

- [[00-Dashboard/MOC\|00-Dashboard/MOC]]
- [[00-Dashboard/Quick-Reference\|00-Dashboard/Quick-Reference]]
- [[00-Dashboard/Exam-Traps\|00-Dashboard/Exam-Traps]]
- 各章節練習題

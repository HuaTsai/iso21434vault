---
{"dg-publish":true,"permalink":"/04-distributed-cs-activities/practice-distributed/","title":"分散式資安活動練習題","tags":["iso-21434","practice","distributed"],"dg-note-properties":{"title":"分散式資安活動練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","cia","supplier","distributed"],"tags":["iso-21434","practice","distributed"],"created":"2026-05-11"}}
---


> 涵蓋：客戶/供應商互動、CIA、供應商能力評估。
> 共 8 題。

---

## Q1. (recall)

ISO 21434 Clause 7 的核心 WP 是什麼？

> [!answer]- 解答
> **Cybersecurity Interface Agreement (CIA)**。
> 它定義雙方的責任、共享 WP、介面流程。

---

## Q2. (recall + 易混淆)

下列何者**正確**？

A. CIA 只是法務合約，不需工程介入
B. CIA 由 Project Manager 簽字即可
C. CIA 是工程文件，需資安專業 + 適當層級簽署，內容含 RASIC、共享 WP、事件介面等
D. CIA 與供應商能力評估無關

> [!answer]- 解答
> **C**。
> CIA 是**工程文件**（不僅是法務），需 CS 專業參與，包含具體技術介面。
> 參考 [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]

---

## Q3. (recall)

依 ISO 21434，「客戶」與「供應商」這兩個名詞應如何理解？

> [!answer]- 解答
> **相對概念**。
>
> - Tier-1 對 Tier-2 而言是客戶；
> - Tier-1 對 OEM 而言是供應商。
>
> 同一組織在不同關係中扮演不同角色。CIA 需在每一對「客戶-供應商」關係中分別簽訂。

---

## Q4. (application)

某 OEM 正在準備一個新車型開發，想評估三家潛在 Tier-1 供應商。下列哪個時機最適合納入資安要求？

A. 簽約後再談
B. RFQ 階段就納入
C. 進入開發後才談
D. Validation 前才談

> [!answer]- 解答
> **B**。
> RFQ 階段就應包含資安要求，作為供應商評選的維度之一。**事後**才談會造成價格、時程衝突。
> 參考 [[04-Distributed-CS-Activities/03-Supplier-Capability\|04-Distributed-CS-Activities/03-Supplier-Capability]]

---

## Q5. (recall)

下列哪些**不能**直接證明供應商有產品資安能力？

A. UN R155 CSMS 認證
B. ISO 27001 認證
C. 過去 ISO 21434 專案經驗
D. TARA 流程文件

> [!answer]- 解答
> **B. ISO 27001**。
> 27001 是 **IT 資訊安全**，不是**車輛產品**資安。
> 其他選項：
>
> - A：UN R155 是直接相關（但仍需專案級評估）
> - C：過去經驗是強證據
> - D：直接展示能力
>
> 參考 [[04-Distributed-CS-Activities/03-Supplier-Capability\|04-Distributed-CS-Activities/03-Supplier-Capability]]、[[02-Organizational-Management/03-Management-Systems\|02-Organizational-Management/03-Management-Systems]]

---

## Q6. (analysis)

某 Tier-1 完成 TCU 開發並交付至 OEM。一個月後，Tier-1 的 CSIRT 收到外部研究者通報：TCU 韌體中發現可被遠端利用的 buffer overflow。請依 ISO 21434 + 良好 CIA 實務說明 Tier-1 應如何處理？

> [!answer]- 解答
>
> **依 CIA 約定流程處理**（假設標準 CIA）：
>
> 1. **內部驗證**（< 24 小時）
>    - CSIRT 確認弱點真實性
>    - 評估嚴重度（CVSS）與影響範圍
> 2. **通報 OEM**（依 CIA SLA，通常 P1: 1 hr / P2: 4 hr）
>    - 透過 CIA 約定的安全通報管道（PGP email / hotline）
>    - 提供初步技術細節、影響範圍、緩解建議
> 3. **啟動 Joint Incident Response**
>    - 依 CIA 約定的聯合 IR Team 運作
>    - 雙方共同擬定處置計畫
> 4. **TARA 更新**
>    - 評估此弱點對 TARA 的影響（攻擊路徑、攻擊可行性可能變化）
>    - 必要時更新 CS Case
> 5. **修補開發**
>    - Tier-1 開發修補
>    - 雙方協調 OTA 部署計畫（涉及 UN R156 SUMS）
> 6. **協調揭露**
>    - 與研究者協調 CVD 流程（通常 90 天揭露窗口）
>    - 與 OEM 協調對外公告時機
> 7. **Lessons Learned**
>    - 更新內部流程
>    - 評估其他類似元件是否有相似弱點
> 8. **CSMS 紀錄**
>    - 事件、處置、結果寫入 CSMS 紀錄（Clause 8）
>
> **關鍵原則**：
>
> - 不可單方面對外揭露
> - 不可拖延 OEM 通報
> - 不可只修補不更新 CS Case
>
> 參考 [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]、[[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]

---

## Q7. (recall + 易混淆)

下列關於 CIA 與 DIA 的描述，何者**正確**？

A. CIA 是 DIA 的子集
B. CIA (ISO 21434) 與 DIA (ISO 26262) 是並列概念，可整合為 IDIA
C. CIA 包含 DIA
D. DIA 已過時，全部用 CIA 取代

> [!answer]- 解答
> **B**。
>
> - CIA = Cybersecurity Interface Agreement（資安）
> - DIA = Development Interface Agreement（功能安全）
> - 兩者**獨立但可整合**為 IDIA（Integrated DIA），避免雙文件
>
> 參考 [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]

---

## Q8. (application + 分析)

某 OEM 與 Tier-1 簽訂 CIA 時，發現雙方對「誰負責 TARA」有歧見：

- Tier-1 認為：「我們負責元件層級 TARA，OEM 負責車輛層級」
- OEM 認為：「TARA 是 Tier-1 全責」

請依 ISO 21434 評論並提出解決方案。

> [!answer]- 解答
>
> **正確觀點：Tier-1 的描述更接近實務**，但**雙方都需明確界定**。
>
> **依 ISO 21434 + 業界實務**：
>
> - **元件層級 TARA**：Tier-1 主責（最了解元件內部）
> - **車輛層級 TARA**：OEM 主責（最了解整車情境與其他 ECU 互動）
> - **介面層級 TARA**：通常 OEM 主導，Tier-1 配合
>
> **解決方案**：
>
> 1. 在 CIA 中**明確切分** TARA 範圍：
>
>    ```
>    Tier-1 負責：
>      - TCU 內部威脅情境
>      - TCU 介面（CAN/Ethernet/Cellular）的元件視角
>      - HSM 整合層
>
>    OEM 負責：
>      - 車輛級 Asset 識別
>      - 車輛級 Threat Scenarios（含跨 ECU）
>      - 車輛級 Impact Rating（含 SFOP）
>      - 整合所有 ECU TARA 為車輛級 TARA
>    ```
>
> 2. **交付介面**：
>    - Tier-1 提供 TCU TARA Report 給 OEM
>    - OEM 在車輛級 TARA 中**引用** + **檢視**
> 3. **共同 Review**：
>    - 雙方對齊 Threat Scenarios（避免遺漏或重複）
> 4. **變更觸發**：
>    - 任一方 TARA 變更 → 通知對方 → 影響評估
> 5. **責任最終仲裁**：
>    - 若仍有歧見，由 OEM 作為**車輛級總負責**裁決（OEM 擁有 UN R155 認證責任）
>
> **保守原則**：CIA 不明確時，**雙方都應假設自己負責**——避免責任真空。
>
> 參考 [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]、[[00-Dashboard/Exam-Traps#Trap 6\|00-Dashboard/Exam-Traps#Trap 6]]

---

## Related Concepts

- [[04-Distributed-CS-Activities/01-Customer-Supplier-Interaction\|04-Distributed-CS-Activities/01-Customer-Supplier-Interaction]]
- [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]
- [[04-Distributed-CS-Activities/03-Supplier-Capability\|04-Distributed-CS-Activities/03-Supplier-Capability]]

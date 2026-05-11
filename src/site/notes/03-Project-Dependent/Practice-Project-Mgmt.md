---
{"dg-publish":true,"permalink":"/03-project-dependent/practice-project-mgmt/","title":"專案層級資安管理練習題","tags":["iso-21434","practice","project-dependent"],"dg-note-properties":{"title":"專案層級資安管理練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","cs-plan","tailoring","reuse","case","assessment","release"],"tags":["iso-21434","practice","project-dependent"],"created":"2026-05-11"}}
---


> 涵蓋：CS Plan、RASIC、Tailoring、Reuse/OTS/OoC、CS Case/Assessment、Release。
> 共 12 題。

---

## Q1. (recall + 易混淆)

下列何者**最正確**描述 Cybersecurity Plan 與 Cybersecurity Case 的差異？

A. 兩者是同義詞
B. **CS Plan 是事前計畫**；**CS Case 是事後證據與論證**
C. CS Plan 由 Tier-1 製作；CS Case 由 OEM 製作
D. CS Plan 在 Release 後不再更新；CS Case 從 Release 才開始

> [!answer]- 解答
> **B**。
>
> - CS Plan = **施工藍圖**（將做什麼）
> - CS Case = **完工報告**（已做什麼 + 達成證據）
>
> 兩者都是 **living document**，會持續更新。
> 參考 [[03-Project-Dependent/01-Cybersecurity-Plan\|03-Project-Dependent/01-Cybersecurity-Plan]]、[[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]、[[00-Dashboard/Exam-Traps#Trap 4\|00-Dashboard/Exam-Traps#Trap 4]]

---

## Q2. (recall)

在 RASIC 矩陣中，下列哪一個是**必須唯一**的？

A. R (Responsible)
B. **A (Accountable)**
C. S (Supporting)
D. I (Informed)

> [!answer]- 解答
> **B. Accountable**。
> 每個活動只能有一個 Accountable，否則責任不清。R / S / I / C 可以多人。

---

## Q3. (recall)

下列哪一項**屬於**合理 Tailoring？

A. 為了趕進度，省略 TARA 活動
B. 因為是 ASIL D 系統，跳過資安驗證
C. 在 Reuse 情境下，TARA 採差異分析（Delta TARA）取代完整重做
D. 將獨立 Cybersecurity Assessment 改由開發團隊執行

> [!answer]- 解答
> **C**。
>
> - A：裁適 Objective，不可
> - B：HARA ≠ TARA，無關
> - **C：可裁適**——調整執行方式但 Objective 仍達成
> - D：違反獨立性
>
> 參考 [[03-Project-Dependent/03-Tailoring\|03-Project-Dependent/03-Tailoring]]、[[00-Dashboard/Exam-Traps#Trap 10\|00-Dashboard/Exam-Traps#Trap 10]]

---

## Q4. (recall)

ISO 21434 中對 Tailoring **不可**裁適的是什麼？

> [!answer]- 解答
> **標準的 Objectives 與 Outcomes**。
> 可以調整：
>
> - 活動的執行方式 (How)
> - 深度 (Depth)
> - WP 格式
>   不可以裁掉：
> - 標準要達成的目標
> - 規範性 "shall" 條款要求的結果

---

## Q5. (application + 分析)

某 Tier-1 從 Tier-2 採購一份「AUTOSAR Crypto Stack（Out-of-Context 元件）」。Tier-2 提供：SDK、Assumed Context 文件、其 TARA Report。請說明 Tier-1 接下來必須做的事。

> [!answer]- 解答
>
> **Tier-1 整合者責任**：
>
> 1. **驗證 Assumed Context 是否符合實際情境**
>    - HSM 規格是否相符？
>    - 攻擊者模型是否相符？
>    - 整合介面是否相符？
> 2. **處理 Gap**
>    - Tier-2 假設「攻擊者無物理存取」，但 Tier-1 產品有 OBD 接口 → Gap
>    - 補強整合層防護（如 OBD 訊息驗證、安全閘道）
> 3. **在實際情境下重做 / 補做 TARA**
>    - Tier-2 的 TARA 是基於假設情境，Tier-1 需以整合後的真實情境執行 TARA
> 4. **整合層 V&V**
>    - 驗證 SDK 整合後行為符合 CSR
> 5. **更新自身 CS Case**
>    - 引用 Tier-2 部分 Case + 整合層論證
>    - 文件化 OoC 假設驗證證據
> 6. **建立持續監控機制**
>    - 監控 Tier-2 是否發布 SDK 安全更新
>
> 參考 [[03-Project-Dependent/05-Component-Out-of-Context\|03-Project-Dependent/05-Component-Out-of-Context]]

---

## Q6. (recall)

下列哪一項**不是** Cybersecurity Case 結構的核心要素？

A. Claim
B. Argument
C. Evidence
D. **Action Plan**

> [!answer]- 解答
> **D. Action Plan**。
> Action Plan 屬於 Cybersecurity Plan。CS Case 的核心是 **Claim-Argument-Evidence (CAE)** 或 GSN。

---

## Q7. (recall + 應用)

某專案的 TARA 結果有 2 個 High Risk 與 1 個 Medium Risk。下列哪一種狀況**可以**進入 Release for Post-Development？

A. 2 個 High Risk 暫未處置，計畫 Release 後 OTA 補上
B. 2 個 High Risk 已 Reduce 到 Low；Medium 已被適當層級接受作為殘餘風險
C. 1 個 High Risk 被 Project Manager 接受作為殘餘風險
D. 全部跳過處置，反正 Release 後可監控

> [!answer]- 解答
> **B**。
>
> - A：未處置的 High Risk 不可 Release
> - **B：正確**——High 已 reduce，Medium 接受有理由（殘餘風險文件化 + 適當層級簽核）
> - C：接受層級不足（High Risk 通常需 VP/CTO 層級接受）
> - D：違反 Clause 6.4.11
>
> 參考 [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]、[[00-Dashboard/Exam-Traps#Trap 14\|00-Dashboard/Exam-Traps#Trap 14]]

---

## Q8. (recall)

Cybersecurity Assessment 由誰執行？

A. Project CS Manager
B. Project Manager
C. **獨立評估員（不可為專案執行者）**
D. 客戶代表

> [!answer]- 解答
> **C**。
> 獨立性是規範性要求。可以是組織內部獨立人員或外部第三方。
> 參考 [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]、[[02-Organizational-Management/06-Audit-and-Assessment\|02-Organizational-Management/06-Audit-and-Assessment]]

---

## Q9. (application)

公司收購一家小公司，其產品線採用「無 TARA、但有完整 SBOM 與滲透測試報告」的開發方式。在準備將其產品整合至 ISO 21434 合規體系時，下列**最優先**做什麼？

A. 立即停止販售該產品
B. 為其產品執行完整 TARA + 撰寫 CS Case + 建立後續監控
C. 將 SBOM 與滲透測試報告改名為「CS Case」
D. 只需 OEM 簽核就符合

> [!answer]- 解答
> **B**。
>
> 收購而來的產品線**等同 Reuse**，需：
>
> 1. 執行完整 TARA（情境可能與原開發者不同）
> 2. 利用既有 SBOM + 滲透測試結果作為**部分證據**
> 3. 撰寫整合後的 CS Case
> 4. 建立後續 Clause 8 監控 + Clause 13 維運機制
> 5. 評估殘餘風險並取得適當層級接受
>
> SBOM 與 Pen Test 是**證據**，**不等於** CS Case（缺 Claim 與 Argument 結構）。
>
> 參考 [[03-Project-Dependent/04-Reuse\|03-Project-Dependent/04-Reuse]]

---

## Q10. (analysis)

下表為某專案的 RASIC，請找出**至少兩個錯誤**：

| 活動       | PM  | CS Mgr | Engineer | Tester |
| ---------- | :-: | :----: | :------: | :----: |
| TARA 執行  |  A  |   A    |    R     |   I    |
| Pen Test   |  C  |   I    |    A     |   R    |
| Validation |  I  |   I    |    A     |   A    |

> [!answer]- 解答
>
> **錯誤清單**：
>
> 1. **TARA 執行：兩個 A**（PM + CS Mgr）—— Accountable 必須唯一
> 2. **Pen Test：Engineer 是 A** —— Pen Test 應由 CS Mgr 或 Test Lead 為 A，且 R 通常是獨立測試人員
> 3. **Validation：Engineer 與 Tester 都是 A** —— 違反唯一性，且 Validation 為車輛級活動，A 應為 CS Mgr
>
> **正確版本（建議）**：
>
> | 活動       | PM  | CS Mgr | Engineer | Tester |
> | ---------- | :-: | :----: | :------: | :----: |
> | TARA 執行  |  I  | **A**  |  **R**   |   I    |
> | Pen Test   |  I  | **A**  |    C     | **R**  |
> | Validation |  I  | **A**  |    S     | **R**  |
>
> 參考 [[03-Project-Dependent/02-Responsibilities-Roles\|03-Project-Dependent/02-Responsibilities-Roles]]

---

## Q11. (application)

某 OEM 計畫對已 Release 的 TCU 進行 OTA 更新（修補一個新發現的 CVE）。下列哪一項**最重要**？

A. 直接更新就好，已經 Release 了
B. 更新 CS Case，重新評估殘餘風險，必要時更新 TARA
C. 只通知 Project Manager，不需動 CS Case
D. 等下一次 Major Release 時再一起處理

> [!answer]- 解答
> **B**。
>
> CS Case 是 **Living Document**。任何重大變更（含 OTA 修補）都應：
>
> 1. 評估變更對 CS Case 的影響
> 2. 必要時更新 TARA（新弱點可能改變攻擊面）
> 3. 重新評估殘餘風險
> 4. 文件化變更決策
>
> 此外屬 UN R156 SUMS 範疇，需依 SUMS 流程執行。
>
> 參考 [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]、[[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]

---

## Q12. (分析 + 跨章節)

請說明 **CS Plan**、**CS Case**、**CS Assessment Report**、**TARA Report** 四者的關係（哪個產生哪個、彼此依賴）。

> [!answer]- 解答
>
> **時序與依賴**：
>
> ```
> 1. Cybersecurity Plan（事前）
>    ├── 規劃活動、責任、時程、工具
>    └── 規範後續所有活動
>           ↓
> 2. TARA Report（依 CS Plan 執行）
>    ├── 識別威脅、風險、處置
>    └── 提供 CS Goals 依據
>           ↓
> 3. Cybersecurity Case（持續累積）
>    ├── 收集 TARA + V&V + 過程證據
>    └── 論證 CS Goals 達成
>           ↓
> 4. Cybersecurity Assessment Report（獨立評估）
>    ├── 評估 CS Case 是否成立
>    └── 提供 Release 建議
> ```
>
> **依賴關係**：
>
> - CS Plan **規範**所有後續活動
> - TARA Report **是** CS Case 的核心證據之一
> - CS Case **被** Assessment Report 評估
> - Assessment **可拒絕** Release，即使 CS Case 看似完整
>
> 四者構成 **Plan → Execute → Document → Assess → Release** 的完整閉環。
>
> 參考 [[03-Project-Dependent/01-Cybersecurity-Plan\|03-Project-Dependent/01-Cybersecurity-Plan]]、[[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]、[[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]

---

## Related Concepts

- [[03-Project-Dependent/01-Cybersecurity-Plan\|03-Project-Dependent/01-Cybersecurity-Plan]]
- [[03-Project-Dependent/02-Responsibilities-Roles\|03-Project-Dependent/02-Responsibilities-Roles]]
- [[03-Project-Dependent/03-Tailoring\|03-Project-Dependent/03-Tailoring]]
- [[03-Project-Dependent/04-Reuse\|03-Project-Dependent/04-Reuse]]
- [[03-Project-Dependent/05-Component-Out-of-Context\|03-Project-Dependent/05-Component-Out-of-Context]]
- [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]
- [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]

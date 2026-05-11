---
{"dg-publish":true,"permalink":"/01-foundations/practice-foundations/","title":"基礎觀念練習題","tags":["iso-21434","practice","foundations"],"dg-note-properties":{"title":"基礎觀念練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","foundations","overview","terms"],"tags":["iso-21434","practice","foundations"],"created":"2026-05-11"}}
---


> 涵蓋：標準骨架、術語、Cybersecurity vs Safety、Lifecycle、UN R155/R156。
> 共 12 題（含 8+ 題基本 + 應用 + 分析）。

---

## Q1. (recall)

ISO/SAE 21434 的主體規範性 Clause 為哪幾條？

> [!answer]- 解答
> **Clause 5 ~ Clause 15**。Clause 1-3 為範圍/參考/術語，Clause 4 為一般考量。Annex A-H 多為 informative（資訊性）。

---

## Q2. (recall)

請列出 ISO 21434 的三個層級活動。

> [!answer]- 解答
>
> 1. **Organizational level**（Clause 5 — CSMS）
> 2. **Project-dependent level**（Clause 6）
> 3. **Distributed activities**（Clause 7）
>
> 此外 Clause 8（Continual）與 Clause 15（TARA）橫貫所有層級。

---

## Q3. (recall + 易混淆)

下列關於 Damage Scenario 與 Threat Scenario 的敘述何者**正確**？

A. 兩者是同義詞
B. Damage Scenario 描述攻擊者的具體攻擊步驟
C. Damage Scenario 描述對 road user 的不利後果，Threat Scenario 描述如何達成這個後果
D. Threat Scenario 一定來自 Annex 5

> [!answer]- 解答
> **C**。
>
> - Damage Scenario = **後果**（站在 road user 角度的不利結果）
> - Threat Scenario = **手段+目標**（如何破壞資產的資安屬性以實現 Damage）
>
> 參考 [[01-Foundations/02-Key-Terms-Definitions\|01-Foundations/02-Key-Terms-Definitions]] §3-§4 及 [[00-Dashboard/Exam-Traps#Trap 12\|00-Dashboard/Exam-Traps#Trap 12]]

---

## Q4. (recall)

ISO 21434 中下列哪個是「對 road user 不希望發生的後果」？

A. Threat Scenario
B. Damage Scenario
C. Attack Path
D. Cybersecurity Event

> [!answer]- 解答
> **B. Damage Scenario**。
> 定義中明確提及 "adverse consequence involving a vehicle ... affecting a road user"。

---

## Q5. (application)

某 Tier-1 供應商開發 TCU，OEM 要求合規 ISO 21434。下列哪一項**不是** ISO 21434 直接要求供應商產出的 WP？

A. Cybersecurity Interface Agreement
B. TARA Report (依 CIA 範圍)
C. ASIL 等級分配文件
D. Cybersecurity Plan

> [!answer]- 解答
> **C. ASIL 等級分配文件**。
> ASIL 是 **ISO 26262**（功能安全）的 WP，**ISO 21434 不要求供應商產出此文件**（但兩者在 co-engineering 中可能共享輸入，如 Item Definition）。Cybersecurity 的對應等級是 **CAL**（informative）。
>
> 參考 [[01-Foundations/03-Cybersecurity-vs-Safety\|01-Foundations/03-Cybersecurity-vs-Safety]]、[[00-Dashboard/Exam-Traps#Trap 2\|00-Dashboard/Exam-Traps#Trap 2]]

---

## Q6. (recall)

UN R155 與 ISO 21434 的關係，下列何者**最正確**？

A. UN R155 強制使用 ISO 21434 作為實作標準
B. ISO 21434 是 UN R155 合規最常被接受的技術依據，但 R155 不強制
C. ISO 21434 與 UN R155 是同一份文件
D. ISO 21434 是法律強制；UN R155 是建議

> [!answer]- 解答
> **B**。
> UN R155 是法規（強制，視適用地區），但**不指定**具體技術標準。ISO 21434 是事實上的合規依據（OEM 可選擇其他標準證明合規）。

---

## Q7. (recall)

UN R155 與 UN R156 的差別？

> [!answer]- 解答
>
> - **R155**：Cybersecurity Management System + 車型資安認證（整體資安）
> - **R156**：Software Update Management System + 車型軟體更新認證（OTA 流程）
>
> 兩者**並列**（非包含關係）。R155 對應 ISO 21434，R156 對應 ISO 24089。
> 參考 [[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]、[[00-Dashboard/Exam-Traps#Trap 8\|00-Dashboard/Exam-Traps#Trap 8]]

---

## Q8. (recall)

UN R155 的 CSMS 認證有效期為多少年？

A. 1 年
B. 2 年
C. 3 年
D. 5 年

> [!answer]- 解答
> **C. 3 年**。
> 之後需重新認證（含每年內部稽核）。

---

## Q9. (application)

當 ISO 26262 的安全要求與 ISO 21434 的資安要求**直接衝突**時，依 ISO 21434 Clause 4 的建議，應如何處理？

> [!answer]- 解答
>
> 1. **Safety considerations shall take precedence**（安全優先）。
> 2. 在不損害 Safety 的前提下，最大化 Security。
> 3. **文件化** trade-off 決策（理由、影響、批准者）。
>
> 注意：這不是「資安可以被忽略」，而是衝突無解時的優先級。
> 參考 [[01-Foundations/03-Cybersecurity-vs-Safety\|01-Foundations/03-Cybersecurity-vs-Safety]]

---

## Q10. (analysis)

下列 ISO 21434 條文中，"**shall**"、"**should**"、"**may**" 的差別為何？這對證照考試與實務各有什麼意涵？

> [!answer]- 解答
> **條文用詞分級**：
>
> | 用詞   | 強制性   | 含意                     |
> | ------ | -------- | ------------------------ |
> | shall  | **必須** | 不執行 = 不合規          |
> | should | **建議** | 可不執行，但需有合理理由 |
> | may    | **允許** | 自由選擇                 |
> | can    | 能力陳述 | 描述可能性，非要求       |
>
> **考試意涵**：
>
> - 命題單位常用 should/may 取代 shall 設陷阱（例：「ISO 21434 規定**必須**執行 X」——實際上只是 should）。
> - 仔細閱讀題目用詞。
>
> **實務意涵**：
>
> - Tailoring 時，should 比 shall 容易裁適（仍需理由）。
> - 認證稽核時，shall 條款被嚴格檢視。

---

## Q11. (analysis)

請說明 TARA 在 ISO 21434 生命週期中應在哪些時機執行或更新？

> [!answer]- 解答
> TARA **非一次性**活動，應於以下時機執行/更新：
>
> 1. **Item Definition 完成後**（首次完整 TARA — Clause 9）
> 2. **架構/設計重大變更時**（攻擊路徑可能改變 — Clause 10）
> 3. **新弱點/威脅出現時**（Clause 8 持續監控觸發）
> 4. **變體 (Variant) / 重用情境**（情境改變需重新評估 — Clause 6）
> 5. **後開發階段定期 review**（Clause 13）
> 6. **事件回應後**（如有 Lessons Learned — Clause 13）
>
> 參考 [[01-Foundations/04-Lifecycle-Overview\|01-Foundations/04-Lifecycle-Overview]]、[[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]

---

## Q12. (application + 跨章節)

公司 X 開發完成某 ECU，TARA 結果尚有兩個 **High Risk** 項目尚未處置完成，但專案延遲嚴重，能否進入 Production (Clause 12)？依 ISO 21434 應如何回應？

> [!answer]- 解答
> **不可進入 Production**。理由：
>
> 1. ISO 21434 要求進入 **Release for Post-Development** 前需滿足：
>    - Cybersecurity Case 完成
>    - **殘餘風險已被適當層級接受**（不是「未處置」，是「處置完成或接受」）
>    - 後開發工件已準備
> 2. High Risk **未處置** ≠ 殘餘風險被接受。
> 3. 合規回應：
>    - **方案 A**：完成風險處置（Reduce/Avoid/Transfer）後再 Release。
>    - **方案 B**：經適當層級書面接受**作為殘餘風險**（含理由、補償措施、監控計畫），但需符合組織政策（通常 High/Very High 不允許僅以「接受」處置）。
>    - **方案 C**：縮小 Item 範圍，將該功能移除（Avoid）。
> 4. 過程需有**文件化決策**與**簽核紀錄**，未來會出現在 Cybersecurity Case 中。
>
> 參考 [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]、[[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]

---

## Related Concepts

- [[01-Foundations/01-Standard-Overview\|01-Foundations/01-Standard-Overview]]
- [[01-Foundations/02-Key-Terms-Definitions\|01-Foundations/02-Key-Terms-Definitions]]
- [[01-Foundations/03-Cybersecurity-vs-Safety\|01-Foundations/03-Cybersecurity-vs-Safety]]
- [[01-Foundations/04-Lifecycle-Overview\|01-Foundations/04-Lifecycle-Overview]]
- [[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]
- [[00-Dashboard/Exam-Traps\|00-Dashboard/Exam-Traps]]

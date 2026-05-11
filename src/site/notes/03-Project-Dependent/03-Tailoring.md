---
{"dg-publish":true,"permalink":"/03-project-dependent/03-tailoring/","title":"裁適 (Tailoring)","tags":["iso-21434","concept-note","project-dependent","tailoring"],"dg-note-properties":{"title":"裁適 (Tailoring)","source_pdf":"內部彙整 (ISO 21434 Clause 6.4.4)","part":"Clause 6","keywords":["tailoring","adaptation","justification"],"tags":["iso-21434","concept-note","project-dependent","tailoring"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> adaptation of cybersecurity activities to suit the project's specific characteristics.

簡言之：「**依專案特性調整**資安活動的執行方式」。

---

## 可以 Tailor 什麼？

```
✓ 可裁適：
  • 活動的執行**方式**（How）
  • Work Product 的**格式**
  • 活動的**深度**（簡化／加強）
  • 工具選擇
  • 並行/串行的執行順序
  • 重複活動的頻率

✗ 不可裁適：
  • 標準的**目標 (Objectives)**
  • 標準的**結果 (Outcomes)**
  • 規範性 "shall" 條款的存在
  • 安全相關的最低要求
```

> [!important]
> **規則總結**：可改「How」與「Depth」，但**不可改「What/Why」**。

---

## Tailoring 的合理情境

### 情境 1：高重用率

專案 90% 重用上一代產品。

- **可 Tailor**：TARA 主要做差異分析，不重做全部
- **不可 Tailor**：仍需有 TARA 結果與決策紀錄

### 情境 2：OTS 元件大量使用

HSM、加密庫等大量使用 OTS。

- **可 Tailor**：將 OTS 的歷史驗證作為輸入，減少重複測試
- **不可 Tailor**：整合層測試仍需執行

### 情境 3：低風險專案

無外部連線、無 OTA、無 PII。

- **可 Tailor**：簡化某些 WP（如 IR Plan 較簡）
- **不可 Tailor**：仍需 TARA 證明確實低風險

### 情境 4：學術/實驗性專案

不會量產。

- **可 Tailor**：減少正式 CS Case 的篇幅
- **不可 Tailor**：標準的目標仍需達成

---

## Tailoring 流程

```
1. 識別欲裁適的活動
   ↓
2. 對照標準確認可裁適範圍
   ↓
3. 撰寫 Tailoring Justification（理由）
   ↓
4. 風險評估：裁適是否引入新風險？
   ↓
5. 批准（CS Manager + 適當層級）
   ↓
6. 寫入 CS Plan
   ↓
7. 執行
   ↓
8. 後續 Assessment 檢視合理性
```

---

## Tailoring Justification 範本

```yaml
tailoring_decision:
  id: TAIL-001
  activity: "Independent TARA review per design change"
  baseline_standard: "ISO 21434 Clause 9.4.4 + Clause 15"

  proposed_tailoring: >
    Combine minor design changes (no impact on attack paths)
    into quarterly TARA review, instead of per-change TARA.

  rationale: >
    Per change analysis showed that 80% of SW changes do not
    alter attack surface or attack paths. Quarterly batching
    reduces administrative load while maintaining coverage.

  risk_analysis:
    - "Risk: New threat may emerge between reviews"
      mitigation: "Clause 8 monitoring still active; emergency TARA trigger documented"

  evidence_of_compliance:
    - "Quarterly TARA review reports"
    - "Emergency trigger criteria documented"

  approval:
    by: "Project CS Manager"
    date: 2026-05-11

  scope: "Applicable only to TCU-2026 project"
```

---

## 常見錯誤 Tailoring

> [!warning] 命題單位最愛測這些
>
> ❌ **錯誤 1**："為了趕進度，省略 TARA"
>
> - 違反規則：Objective 被裁掉
> - 正確做法：簡化 TARA 深度（如重用前代 TARA + 差異分析）
>
> ❌ **錯誤 2**："因為是 ASIL D 系統，所以不需要做 TARA（已經有 HARA）"
>
> - 違反規則：HARA ≠ TARA，目的不同
>
> ❌ **錯誤 3**："Validation 改由開發團隊執行，省外部測試成本"
>
> - 違反規則：獨立性被裁掉
>
> ❌ **錯誤 4**："OTS 元件已被廣泛使用，跳過 TARA"
>
> - 違反規則：OTS 在新情境下仍需重新評估

---

## Tailoring 必要紀錄

每個 Tailoring 決策的**最低紀錄**：

1. **識別**：哪一個活動 / WP / 條款
2. **裁適內容**：原本怎麼做 → 改為怎麼做
3. **理由**：為什麼裁適合理
4. **風險評估**：是否引入新風險 + 緩解
5. **批准**：誰批准 + 日期
6. **適用範圍**：此 Tailoring 適用範圍

---

## Tailoring 的稽核與評估

> [!important]
> Cybersecurity Assessment 會**特別檢視** Tailoring 決策：
>
> - 理由是否合理？
> - 風險評估是否完整？
> - 是否導致無法達成 Objectives？
>
> 不合理的 Tailoring **可能導致 Release 被拒**。

---

## 證照考點

> [!important] 高頻考點
>
> 1. Tailoring **可以**調整「How / Depth / Format」
> 2. Tailoring **不可以**裁掉「Objectives / Outcomes」
> 3. 每個 Tailoring 必須有**書面理由 (rationale)**
> 4. Tailoring 紀錄寫入 **CS Plan**
> 5. 不可以為了「節省成本/時間」而省略整個活動
> 6. **OTS / Reuse** 不代表自動可裁適 TARA
> 7. Tailoring 會在 **Cybersecurity Assessment** 中被檢視

---

## Related Notes

- [[03-Project-Dependent/01-Cybersecurity-Plan\|03-Project-Dependent/01-Cybersecurity-Plan]]
- [[03-Project-Dependent/04-Reuse\|03-Project-Dependent/04-Reuse]]
- [[03-Project-Dependent/05-Component-Out-of-Context\|03-Project-Dependent/05-Component-Out-of-Context]]
- [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]
- [[00-Dashboard/Exam-Traps#Trap 10\|00-Dashboard/Exam-Traps#Trap 10]]

## Practice

- [[03-Project-Dependent/Practice-Project-Mgmt\|03-Project-Dependent/Practice-Project-Mgmt]]

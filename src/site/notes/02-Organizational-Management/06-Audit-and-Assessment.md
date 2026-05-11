---
{"dg-publish":true,"permalink":"/02-organizational-management/06-audit-and-assessment/","title":"稽核與資安評估","tags":["iso-21434","concept-note","csms","audit"],"dg-note-properties":{"title":"稽核與資安評估","source_pdf":"內部彙整 (ISO 21434 Clause 5.4.7 + 6.4.10)","part":"Clause 5 + 6","keywords":["audit","assessment","independence","csms-audit","cs-assessment"],"tags":["iso-21434","concept-note","csms","audit"],"created":"2026-05-11"}}
---


## 兩種重要的「檢視」活動

| 活動                         | 層級 | 焦點                       | 對應 Clause   |
| ---------------------------- | ---- | -------------------------- | ------------- |
| **CSMS Audit**               | 組織 | CSMS 流程是否被遵循？      | Clause 5      |
| **Cybersecurity Assessment** | 專案 | 此專案的資安成果是否充分？ | Clause 6.4.10 |

> [!warning] 易混淆
> 兩者**不同層級、不同目的**。Audit 看「制度」，Assessment 看「結果」。

---

## CSMS Audit (組織稽核)

### 目的

驗證組織的 CSMS 是否：

1. 符合 ISO 21434 Clause 5 要求
2. 被實際遵循（而非紙上談兵）
3. 持續改善

### 頻率

- **至少年度**
- 重大變更後（如組織重組、收購）

### 獨立性要求

- 稽核員**不可**為被稽核活動的負責人或執行者
- 可由內部獨立部門或外部第三方執行

### 流程

```
1. 規劃（Audit Plan）
   ↓
2. 開立會議（Opening Meeting）
   ↓
3. 證據蒐集（文件、面談、觀察）
   ↓
4. 不符合 (NC) 識別
   ↓
5. 結束會議（Closing Meeting）
   ↓
6. 稽核報告
   ↓
7. 改善追蹤（CAPA）
```

### 稽核發現分級

| 等級            | 描述                   | 處理                    |
| --------------- | ---------------------- | ----------------------- |
| **Critical NC** | 嚴重不符合（影響合規） | 立即改善 + 認證可能撤回 |
| **Major NC**    | 重大不符合             | 30 日內改善             |
| **Minor NC**    | 輕微不符合             | 下次稽核前改善          |
| **Observation** | 觀察建議               | 自行決定                |

---

## Cybersecurity Assessment (專案評估)

### 目的

獨立評估**特定專案**的資安成果：

- TARA 是否充分？
- CS Goals 是否合理？
- 風險處置是否適當？
- Cybersecurity Case 是否成立？

### 何時執行

- **發佈至後開發階段前**（必要）
- 重大設計變更後
- 客戶要求時

### 獨立性

- 評估人**不可**為該專案的直接執行者
- 通常由組織內獨立 CS Officer 或外部專家執行

### 輸出：Cybersecurity Assessment Report

```yaml
cs_assessment_report:
  project: "TCU-2026"
  date: 2026-05-01
  assessor: "Independent CS Officer (Bob Smith)"
  assessment_basis:
    - "Cybersecurity Plan v2.3"
    - "TARA Report v3.1"
    - "Verification Report v1.0"
    - "Validation Report v1.0"

  findings:
    - id: F-001
      severity: Major
      description: "CSR-005 (DPA countermeasure) verification incomplete"
      recommendation: "Complete DPA test before release"

    - id: F-002
      severity: Minor
      description: "Lesson learned from F-1234 incident not propagated"

  recommendation: "REJECT release until F-001 resolved"
  next_review: "Upon resolution of F-001"
```

---

## 稽核員/評估員技能要求

| 技能                   | CSMS 稽核員 | CS 評估員  |
| ---------------------- | :---------: | :--------: |
| ISO 21434 條文         |   Expert    |   Expert   |
| 稽核技巧（ISO 19011）  |   Expert    |    Adv     |
| TARA / Risk Mgmt       |    Inter    | **Expert** |
| 安全技術（加密、滲透） |    Basic    |    Adv     |
| 領域知識（汽車 E/E）   |     Adv     |    Adv     |
| 獨立性與公正性         |  **必要**   |  **必要**  |

---

## 外部 vs 內部稽核

| 比較項 | 內部稽核         | 外部稽核 (3rd Party)       |
| ------ | ---------------- | -------------------------- |
| 執行者 | 組織內部獨立人員 | 認證機構 (TÜV、DEKRA、SGS) |
| 頻率   | 年度（至少）     | 3 年（UN R155 認證）       |
| 目的   | 持續改善         | 法規/標準合規認證          |
| 結果   | 內部改善建議     | 認證證書 + 公開狀態        |

---

## 持續改善 (Continual Improvement)

稽核 + 評估的結果必須驅動改善：

```
       ┌──────────────────┐
       │   Findings        │
       │ (NC / Issues)    │
       └────────┬─────────┘
                │
                ↓
       ┌──────────────────┐
       │ Root Cause Analysis│
       └────────┬─────────┘
                ↓
       ┌──────────────────┐
       │ Corrective Action │
       │ (CAPA)           │
       └────────┬─────────┘
                ↓
       ┌──────────────────┐
       │ Effectiveness    │
       │ Verification     │
       └────────┬─────────┘
                ↓
       ┌──────────────────┐
       │ Lessons Learned  │
       │ (組織知識更新)    │
       └──────────────────┘
```

---

## 證照考點

> [!important] 高頻考點
>
> 1. **CSMS Audit ≠ Cybersecurity Assessment**
>    - Audit：組織層級、流程
>    - Assessment：專案層級、結果
> 2. **獨立性**：稽核員/評估員不可為執行者
> 3. **CSMS Audit 頻率**：至少年度
> 4. **Assessment 時機**：發佈至後開發前必要
> 5. **UN R155 CSMS 認證**：3 年一次，由外部認證機構
> 6. **Cybersecurity Assessment Report** 是必要 WP

---

## Related Notes

- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]
- [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]
- [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]

## Practice

- [[02-Organizational-Management/Practice-CSMS\|02-Organizational-Management/Practice-CSMS]]

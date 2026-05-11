---
{"dg-publish":true,"permalink":"/03-project-dependent/06-case-and-assessment/","title":"資安案例 (Cybersecurity Case) 與評估","tags":["iso-21434","concept-note","project-dependent","case","assessment"],"dg-note-properties":{"title":"資安案例 (Cybersecurity Case) 與評估","source_pdf":"內部彙整 (ISO 21434 Clause 6.4.7 + 6.4.8)","part":"Clause 6","keywords":["cs-case","cs-assessment","evidence","argument"],"tags":["iso-21434","concept-note","project-dependent","case","assessment"],"created":"2026-05-11"}}
---


## 兩個關鍵 WP

| WP                                  | 由誰製作                        | 用途               |
| ----------------------------------- | ------------------------------- | ------------------ |
| **Cybersecurity Case**              | **執行者**（CS Manager + Team） | 論證資安目標達成   |
| **Cybersecurity Assessment Report** | **獨立評估員**                  | 評估 Case 是否成立 |

> [!important]
> 兩者**配對存在**：Case 是「主張+證據」，Assessment 是「第三方確認」。

---

## Cybersecurity Case 結構

> [!quote] 定義 (Clause 3)
> structured argument, supported by evidence, providing a compelling, comprehensible and valid case that cybersecurity goals are satisfied.

```
┌───────────────────────────────────────┐
│        Top Claim                      │
│ "TCU 達成所有資安目標"                  │
└────────────────┬──────────────────────┘
                 │ Argument
       ┌─────────┴─────────┐
       │                   │
   Sub-claim 1         Sub-claim 2
   "CG-001 達成"       "CG-002 達成"
       │                   │
   ┌───┴───┐           ┌───┴───┐
 Evidence Evidence   Evidence Evidence
 (Pen test)(TARA)   (Verif)  (Review)
```

### 常見論證框架

| 框架     | 全名                        | 特色                                 |
| -------- | --------------------------- | ------------------------------------ |
| **CAE**  | Claim - Argument - Evidence | 直觀，易讀                           |
| **GSN**  | Goal Structuring Notation   | 圖形化，標準化（多用於 Safety Case） |
| **混合** | CAE + GSN                   | 結合兩者優點                         |

ISO 21434 **不強制**特定框架。

---

## CS Case 內容應包含

```yaml
cs_case:
  metadata:
    item: "TCU-2026"
    version: 1.0
    release_date: 2027-07-01

  scope:
    item_definition_ref: "..."
    applicable_phases: [Concept, Development, Validation]

  top_claim:
    statement: "TCU achieves all cybersecurity goals throughout its operational lifecycle"

  cybersecurity_goals:
    - id: CG-001
      claim: "Firmware integrity is protected against unauthorized modification"
      arguments:
        - "Secure boot enforced (CSR-001, CSR-002)"
        - "Signed update only (CSR-005)"
      evidence:
        - "Verification Report Section 4.2"
        - "Pen Test Report PT-2027-018"
        - "Review Record RR-Arch-005"

  residual_risks:
    - id: RR-001
      description: "Side-channel attack on RSA signing"
      level: "Low"
      treatment: "Retain + monitor"
      acceptor: "VP Engineering (signed 2027-06-15)"

  ots_components:
    - "OpenSSL 3.0.12 (see SBOM v2.1)"
    - "AUTOSAR BSW (Vector, see OoC ref)"

  reused_components:
    - "Gateway SW v1.5 (reused from project G2, Delta TARA done)"

  assumptions:
    - "Vehicle OEM provides physically secured OBD port (CS Claim CL-002)"

  references:
    - "CS Plan v2.3"
    - "TARA Report v3.1"
    - "Verification Report v1.0"
    - "Validation Report v1.0"
```

---

## 證據 (Evidence) 來源

| 證據類型          | 範例                                     |
| ----------------- | ---------------------------------------- |
| **分析**          | TARA Report、Threat Model、Attack Tree   |
| **設計**          | 架構文件、Design Review Record           |
| **驗證**          | Verification Report、SAST 報告、單元測試 |
| **驗證 (車輛級)** | Validation Report、Pen Test Report       |
| **流程**          | CS Plan、Audit Records                   |
| **變更管理**      | Change Request、Impact Analysis          |
| **持續活動**      | Monitoring Records、Incident Reports     |

---

## Cybersecurity Assessment

> [!quote] 定義 (Clause 6.4.8)
> independent judgement of the cybersecurity engineering performed for the item or component.

### 評估目的

```
1. CS Case 是否成立？
2. Argument 是否合理？
3. Evidence 是否充分？
4. Residual Risk 是否合理被接受？
5. Tailoring 是否合理？
6. 是否符合 Clause 5-15 要求？
```

### 評估員資格

| 要求       | 說明                           |
| ---------- | ------------------------------ |
| **獨立性** | 不可為專案執行者               |
| **能力**   | 21434 條文、TARA、滲透測試基本 |
| **權威**   | 有「拒絕 Release」的權力       |
| **位階**   | 通常向 Top Management 報告     |

---

## Assessment Report 結構

```yaml
cs_assessment_report:
  metadata:
    project: "TCU-2026"
    assessor: "Bob Smith (Independent CS Officer)"
    assessment_date_range: 2027-06-01 to 2027-06-25
    cs_case_version_reviewed: 1.0

  methodology:
    - Document review
    - Sample-based evidence verification
    - Interview with CS team, architects, testers
    - Independent verification of selected TARA scenarios

  findings:
    - id: F-001
      severity: Major
      description: "CSR-005 (DPA countermeasure) test data missing"
      recommendation: "Re-execute DPA test or remove CSR-005 (and update TARA)"

    - id: F-002
      severity: Observation
      description: "CS Case mixes evidence and conclusion structure"
      recommendation: "Restructure for next release"

  overall_assessment:
    cs_case_completeness: "Partial — F-001 blocking"
    residual_risk_acceptance: "Acceptable for non-blocking risks"
    tailoring_assessment: "Reasonable"

  recommendation: "REJECT release until F-001 resolved"

  next_assessment: "Upon F-001 resolution"
```

---

## 評估結果可能

| 結果                    | 後續行動                            |
| ----------------------- | ----------------------------------- |
| **Approve**             | 可進入 Release for Post-Development |
| **Conditional Approve** | 完成指定改善後 Release              |
| **Reject**              | 不可 Release，需修正後重評          |
| **Withdraw**            | 評估範圍嚴重不足，重做              |

---

## CS Case 是 Living Document

```
Initial CS Case (Release 1.0)
        │
新威脅出現 / 新弱點 / OTA 更新
        │
        ↓
Updated CS Case (Release 1.1)
        │
        ↓
…直至 EoS
```

> [!tip]
> CS Case 在後開發階段持續更新，每次 OTA 都可能需要更新。

---

## 證照考點

> [!important] 高頻考點
>
> 1. **CS Case ≠ CS Plan**：Plan = 計畫；Case = 證據+論證
> 2. CS Case 結構：**Claim - Argument - Evidence**
> 3. CS Case 是 **Living Document**
> 4. Assessment 由**獨立**人員執行
> 5. Assessment 有「**拒絕 Release**」權力
> 6. Assessment Report 是必要 WP
> 7. ISO 21434 **不強制**特定論證框架（GSN/CAE 皆可）
> 8. **殘餘風險**需被適當層級接受並在 CS Case 中記錄

---

## Related Notes

- [[03-Project-Dependent/01-Cybersecurity-Plan\|03-Project-Dependent/01-Cybersecurity-Plan]]
- [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]
- [[02-Organizational-Management/06-Audit-and-Assessment\|02-Organizational-Management/06-Audit-and-Assessment]]
- [[00-Dashboard/Exam-Traps#Trap 4\|00-Dashboard/Exam-Traps#Trap 4]]
- [[00-Dashboard/Exam-Traps#Trap 13\|00-Dashboard/Exam-Traps#Trap 13]]

## Practice

- [[03-Project-Dependent/Practice-Project-Mgmt\|03-Project-Dependent/Practice-Project-Mgmt]]

---
{"dg-publish":true,"permalink":"/08-cybersecurity-validation/01-validation-objectives/","title":"資安驗證 (Cybersecurity Validation) 目標與策略","tags":["iso-21434","concept-note","validation"],"dg-note-properties":{"title":"資安驗證 (Cybersecurity Validation) 目標與策略","source_pdf":"內部彙整 (ISO 21434 Clause 11)","part":"Clause 11","keywords":["validation","vehicle-level","objectives","strategy"],"tags":["iso-21434","concept-note","validation"],"created":"2026-05-11"}}
---


## 為什麼需要獨立的 Validation？

> [!important]
> Clause 10 的 Verification 確認「**需求被正確實作**」。
> 但 Clause 11 的 Validation 問的是另一個問題：「**整車情境下，CS Goals 真的被達成嗎**？」

範例：

- 每個元件單獨測試都過了（Verification ✓）
- 但整車情境下，多個元件互動可能產生新的攻擊路徑（Validation ✗）

---

## Validation 的核心特徵

```
1. 車輛層級 (Vehicle-level)
   • 整車情境，非單一元件
   • 含跨 ECU 互動

2. 從攻擊者視角
   • 真實攻擊面
   • 真實攻擊技術

3. 對應 CS Goals
   • 每個 CS Goal 至少一個 Validation 活動
   • 直接證明 Goal 達成

4. 通常含滲透測試 (Penetration Testing)
   • Clause 11 列為「適當方法」之一
   • R155 type approval 實務上普遍期待
   • 若不執行需在 CS Case 中提出明確 justification
```

---

## Validation Objectives

```yaml
validation_objectives:
  - "Verify that all CS Goals are achieved at vehicle level"
  - "Verify that CS Claims hold in operational environment"
  - "Identify residual cybersecurity risks at vehicle level"
  - "Provide evidence for Cybersecurity Case (top-level claim)"
```

---

## Validation 範圍

```
        ┌────────────────────────────────┐
        │      Vehicle-level Validation   │
        │                                 │
        │  • 整車測試平台 (HIL 或實車)     │
        │  • 多 ECU 互動                  │
        │  • 攻擊面完整                    │
        │  • 真實環境條件                  │
        │                                 │
        └────────────────────────────────┘
                      ↑
                      │ 整合
                      │
        ┌────────────────────────────────┐
        │  Component Verification (10)   │
        │  各元件已通過驗證                │
        └────────────────────────────────┘
```

---

## Validation Plan

```yaml
cs_validation_plan:
  scope: "Complete vehicle (EV Platform G3)"

  test_environment:
    primary: "HIL bench with all ECUs"
    secondary: "Real vehicle prototype (Sprint Eval)"

  test_team:
    internal: "OEM CS Validation Team"
    external: "Specialised pen test vendor"
    independence: "Independent of development team"

  cs_goals_to_validate:
    - id: CG-001
      goal: "Firmware integrity"
      validation_methods:
        - "OTA tampering test (vehicle-level)"
        - "Boot chain pen test"
      pass_criteria: "Tampered firmware rejected; no escalation possible"

    - id: CG-002
      goal: "Cellular comms confidentiality"
      validation_methods:
        - "MITM proxy attack"
        - "Cert pinning bypass test"
      pass_criteria: "All MITM attempts fail; logs reflect detection"

    - id: CG-003
      goal: "Diagnostic access control"
      validation_methods:
        - "UDS Security Access brute force"
        - "Session hijack attempt"
      pass_criteria: "No bypass possible; lockout works"

  attacker_models:
    - "Network attacker (Internet, Cellular)"
    - "Local attacker (parking lot, OBD)"
    - "Physical attacker (workshop tools)"
    - "Insider (limited credentials)"

  out_of_scope:
    - "Backend cloud (separate validation)"
    - "User mobile app (separate item)"

  schedule:
    start: 2027-03-01
    end: 2027-05-30
    re_test_for_findings: 2027-06-15
```

---

## Validation 必須涵蓋

```
☑ 所有 CS Goals
☑ 所有 CS Claims（驗證假設成立）
☑ 攻擊面完整（含跨 ECU）
☑ 真實情境條件（如環境溫度、振動、不同 SoC）
☑ Attack scenarios from TARA
☑ Pen Test
☑ Negative testing（嘗試破壞）
```

---

## Validation vs Verification 對照

| 比較   | Verification         | Validation                 |
| ------ | -------------------- | -------------------------- |
| Clause | 10.4.2               | **11**                     |
| 層級   | 元件/系統            | **車輛**                   |
| 視角   | 需求對應             | 攻擊者                     |
| 範圍   | In-bound（需求清單） | Out-of-bound（攻擊面完整） |
| 對應   | CS Requirement       | CS Goal                    |
| 工具   | SAST、UT、IT         | Pen Test、實車測試         |
| 結果   | Verification Report  | **Validation Report**      |

→ [[00-Dashboard/Exam-Traps#Trap 5\|00-Dashboard/Exam-Traps#Trap 5]]

---

## Independence Requirement

> [!important]
> Validation 通常**要求獨立性**：
>
> - 不應由開發團隊執行
> - 可由組織內獨立 CS Team 或外部專家
>
> **理由**：避免「自評」帶來的盲點。

---

## Validation Report

```yaml
cs_validation_report:
  metadata:
    item: "TCU-2026 in EV Platform G3 vehicle"
    version: 1.0
    date: 2027-05-30

  scope:
    cs_goals_tested: [CG-001 to CG-012]
    attacker_models: ["Network", "Local", "Physical", "Insider"]

  results:
    cs_goal: CG-001
      validation_passed: true
      evidence:
        - "OTA tampering test: 50 attempts, all rejected"
        - "Boot chain pen test: no bypass found"
      residual_risk: "Low (theoretical attack on root cert, not feasible)"

    cs_goal: CG-002
      validation_passed: true
      with_findings: 1
      finding: "TLS downgrade attempt logged but not blocked actively"
      remediation: "Software update to actively reject TLS < 1.3"
      severity: Medium

    cs_goal: CG-003
      validation_passed: false  # ⚠
      finding: "UDS Security Access timing attack possible (sub-ms)"
      severity: High
      remediation_required: true
      target_remediation: "Before final release"

  pen_test_summary:
    duration: 8 weeks
    findings:
      critical: 0
      high: 1
      medium: 3
      low: 7

  recommendation: "CONDITIONAL APPROVE — fix CG-003 finding before Release"
```

---

## 與 Release for Post-Development 的關係

```
Validation Pass
   ↓
Cybersecurity Assessment
   ↓
Release for Post-Development（Clause 6.4.9）
   ↓
Production (12) + Operations (13)
```

Validation **失敗 → 不可 Release**。

→ [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]

---

## 證照考點

> [!important] 高頻考點
>
> 1. Validation 是**車輛層級**
> 2. Validation **通常需包含滲透測試**（Clause 11 列為適當方法，R155 type approval 普遍期待；不執行需 justification）
> 3. Validation **獨立性**要求（不可由開發團隊）
> 4. Validation 對應 **CS Goals**（不是 Requirements）
> 5. Validation 失敗 → 不可 Release
> 6. Validation Report 是必要 WP
> 7. CS Claims **也需** validation

---

## Related Notes

- [[08-Cybersecurity-Validation/02-Validation-Methods\|08-Cybersecurity-Validation/02-Validation-Methods]]
- [[07-Product-Development/02-Integration-Verification\|07-Product-Development/02-Integration-Verification]]
- [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]
- [[06-Concept-Phase/02-Cybersecurity-Goals\|06-Concept-Phase/02-Cybersecurity-Goals]]
- [[00-Dashboard/Exam-Traps#Trap 5\|00-Dashboard/Exam-Traps#Trap 5]]
- [[00-Dashboard/Exam-Traps#Trap 11\|00-Dashboard/Exam-Traps#Trap 11]]

## Practice

- [[08-Cybersecurity-Validation/Practice-Validation\|08-Cybersecurity-Validation/Practice-Validation]]

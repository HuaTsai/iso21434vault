---
{"dg-publish":true,"permalink":"/03-project-dependent/07-release-for-post-development/","title":"發行至後開發階段 (Release for Post-Development)","tags":["iso-21434","concept-note","project-dependent","release"],"dg-note-properties":{"title":"發行至後開發階段 (Release for Post-Development)","source_pdf":"內部彙整 (ISO 21434 Clause 6.4.11)","part":"Clause 6","keywords":["release","post-development","gate","criteria"],"tags":["iso-21434","concept-note","project-dependent","release"],"created":"2026-05-11"}}
---


## 是什麼？

「**正式宣告**：該 item/元件可進入後開發階段（Production + Operations）」的**閘門 (Gate)**。

> [!important]
> 這是 Clause 6 與 Clause 12-13 之間的**關鍵交接點**。
> 一旦 Release，後續維護責任轉移至 Operations & Maintenance 團隊。

---

## Release 前的必要條件 (Pre-conditions)

```
✓ Cybersecurity Case 完成
✓ Cybersecurity Validation 通過（Clause 11）
✓ Cybersecurity Assessment 通過（Clause 6.4.10）
✓ 所有 TARA 風險已「處置」或「明確接受」
✓ 殘餘風險被適當層級接受 + 文件化
✓ 後開發工件已準備：
    • Incident Response Plan
    • Update Management Plan
    • EoS Plan
    • Operational Monitoring Plan
✓ 若為分散開發，CIA 已關閉所有 open items
✓ 必要法規文件已備齊（如 UN R155/R156 應對）
```

---

## Release Gate 檢查清單

```yaml
release_gate_checklist:
  cybersecurity_case:
    completed: true
    version_baselined: "v1.0"
    sign_off_by: "Project CS Manager + Independent Assessor"

  validation:
    cs_validation_passed: true
    pen_test_executed: true
    pen_test_findings_resolved: true

  assessment:
    cs_assessment_completed: true
    findings_resolution: "All Major findings closed; Observations tracked"
    final_recommendation: "Approve"

  tara:
    all_risks_treated_or_accepted: true
    high_risk_count: 0
    very_high_risk_count: 0
    medium_risk_accepted_with_rationale: 3

  residual_risk:
    documented: true
    accepted_by_role: "VP Engineering"
    acceptance_date: 2027-06-25

  post_development_artifacts:
    incident_response_plan: ready
    update_management_plan: ready
    eos_plan: drafted
    monitoring_plan: ready

  distributed:
    cia_closed: true
    supplier_handover_complete: true

  regulatory:
    un_r155_documentation: ready
    un_r156_documentation: ready # if applicable
    type_approval_supporting: ready

  decision: "RELEASE APPROVED"
  approved_by: "Top Management (CTO)"
  release_date: 2027-07-01
```

---

## Release 後的責任移轉

```
開發團隊 (Clause 9-11)
       ↓
   Release Gate
       ↓
       ├── Production 團隊（Clause 12）
       │   接手生產資安、Provisioning
       │
       └── Operations 團隊（Clause 13）
           接手 IR、Update、Monitoring
```

**移交必要資訊**：

- CS Case 副本
- TARA Report
- 殘餘風險清單
- 已知弱點清單
- 監控指標定義
- IR Playbook

---

## 常見 Release Gate 失敗案例

> [!warning]

### 案例 1：未處置 High Risk

- **狀況**：TARA 結果有 1 個 High Risk 標記為「將在 OTA 補上」。
- **問題**：High Risk 不可在未處置狀態下 Release。
- **解法**：在 Release 前完成 reduce 措施，或經適當層級**明確接受作為殘餘風險**。

### 案例 2：Validation 未完成滲透測試

- **狀況**：因進度壓力，Pen Test 排在 Release 後。
- **問題**：違反 Clause 11 要求。
- **解法**：延後 Release 或縮減範圍至已驗證部分。

### 案例 3：殘餘風險接受層級不足

- **狀況**：殘餘風險由 Project Manager 簽核。
- **問題**：High/Very High 殘餘風險應由更高層級接受（通常 VP/CTO）。
- **解法**：升級簽核層級。

### 案例 4：後開發工件未準備

- **狀況**：IR Plan 還是草稿，沒人正式負責。
- **問題**：Operations 階段無法執行 Clause 13 要求。
- **解法**：完成 IR Plan 並指派負責人後再 Release。

### 案例 5：CIA 仍有 Open Items

- **狀況**：與 Tier-1 仍有 5 個未關閉的資安界面議題。
- **問題**：分散責任不清，Release 後恐爭議。
- **解法**：在 Release 前全部關閉。

---

## Release 後的「資安生命」尚未結束

> [!important]
> **Release ≠ 結案**。
> Release 後仍需：
>
> - 持續監控（Clause 8）
> - 事件回應（Clause 13）
> - 弱點管理（Clause 8）
> - 軟體更新（Clause 13 + UN R156）
> - 直至 **EoS**（Clause 14）

---

## 證照考點

> [!important] 高頻考點
>
> 1. Release for Post-Development **必須**通過 Assessment
> 2. **未處置的 High/Very High Risk** → 不可 Release
> 3. **殘餘風險**必須被**適當層級**接受
> 4. **後開發工件**（IR Plan 等）必須在 Release 前準備
> 5. **CIA** 必須關閉所有 open items
> 6. Release 後責任**移轉**至 Operations 團隊
> 7. **Release ≠ 結案**——Clause 8 與 13 持續

---

## Related Notes

- [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]
- [[08-Cybersecurity-Validation/01-Validation-Objectives\|08-Cybersecurity-Validation/01-Validation-Objectives]]
- [[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]
- [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]
- [[00-Dashboard/Exam-Traps#Trap 14\|00-Dashboard/Exam-Traps#Trap 14]]

## Practice

- [[03-Project-Dependent/Practice-Project-Mgmt\|03-Project-Dependent/Practice-Project-Mgmt]]

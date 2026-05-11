---
{"dg-publish":true,"permalink":"/06-concept-phase/03-cybersecurity-claims/","title":"資安主張 (Cybersecurity Claims)","tags":["iso-21434","concept-note","concept-phase","cs-claims"],"dg-note-properties":{"title":"資安主張 (Cybersecurity Claims)","source_pdf":"內部彙整 (ISO 21434 Clause 9.4 — 與 Cybersecurity Goals 同節)","part":"Clause 9","keywords":["cs-claims","assumptions","out-of-scope","transfer"],"tags":["iso-21434","concept-note","concept-phase","cs-claims"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> statement specifying the cybersecurity-related assumption or sharing of risk.

簡言之：「**我們對某風險的處置主張**」——通常用於：

1. **假設**某條件成立（環境/使用者責任）
2. **轉移**某風險至其他方
3. 將某風險**排除**於 Item 範圍外

---

## CS Goal vs CS Claim 對照

| 比較 | **CS Goal**                    | **CS Claim**                        |
| ---- | ------------------------------ | ----------------------------------- |
| 目的 | 保護 Asset/Property            | 假設或轉移風險                      |
| 範圍 | In-scope 風險的處置目標        | Out-of-scope / Assumed-context 風險 |
| 後續 | 對應 CS Concept + Requirements | 對應**驗證假設成立**的證據          |
| 例子 | 「韌體完整性受保護」           | 「OBD 物理保護由車主負責」          |

> [!warning] 易混淆
> CS Goal 與 CS Claim **不是同一個東西**。
> Goal = 「我們會保護」；Claim = 「假設別人會保護」或「不在我們範圍」。
>
> 參考 [[00-Dashboard/Exam-Traps#Trap 1\|00-Dashboard/Exam-Traps#Trap 1]]

---

## CS Claim 的三種主要情境

### 1. Assumed-Context Claim（假設條件）

```yaml
cs_claim:
  id: CL-TCU-001
  type: assumed-context
  statement: >
    The OBD-II port is assumed to be physically inaccessible
    to unauthorized parties during normal vehicle operation.

  rationale: >
    OEM design places OBD-II behind a secured panel in
    Premium variants. Mass-market variants rely on vehicle owner.

  related_threats:
    - "T-OBD-001: Physical attack via OBD diagnostic port"

  validity_conditions:
    - "Vehicle is parked and locked"
    - "Owner adheres to security guidance"

  if_invalidated:
    - "Need additional protection: OBD authentication"
    - "Trigger TARA update"
```

### 2. Risk-Transfer Claim（轉移風險）

```yaml
cs_claim:
  id: CL-TCU-002
  type: risk-transfer
  statement: >
    Cellular network protection (transport layer integrity)
    is assumed to be provided by Mobile Network Operator.

  rationale: >
    LTE/5G includes integrity protection at radio layer.
    Additional TLS at app layer for defense-in-depth.

  responsibility_holder: "Mobile Network Operator (per service agreement)"

  defense_in_depth:
    - "TLS 1.3 at application layer (not relying solely on MNO)"
```

### 3. Out-of-Scope Claim（範圍外）

```yaml
cs_claim:
  id: CL-TCU-003
  type: out-of-scope
  statement: >
    Cybersecurity of OEM backend cloud infrastructure is
    out of scope for this Item (TCU); covered by separate
    Item "OEM Cloud Platform".

  rationale: "Item separation per Project Scope Document"

  reference_to_other_item: "ITEM-CLOUD-2026-001"
```

---

## CS Claim 的「品質」標準

| 品質         | 描述                             |
| ------------ | -------------------------------- |
| **明確**     | 假設/轉移條件清楚                |
| **可驗證**   | 假設成立的證據可取得             |
| **合理**     | 在情境下確實合理                 |
| **追蹤**     | 對應 Threat Scenario 或 OoC 假設 |
| **失效處理** | 若假設不成立怎麼辦？             |

---

## CS Claim 與 OoC 元件的關係

> [!tip]
> OoC 元件的「Assumed Context」就是一組 CS Claims：
>
> ```
> OoC 開發者宣告：
>   CL-OOC-001: 「假設整合者提供 HSM」
>   CL-OOC-002: 「假設攻擊者無實體存取」
>
> 整合者責任：
>   驗證 CL-OOC-001、CL-OOC-002 在實際情境下成立
>   或補上整合層防護
> ```
>
> 參考 [[03-Project-Dependent/05-Component-Out-of-Context\|03-Project-Dependent/05-Component-Out-of-Context]]

---

## CS Claim 在 CS Case 中的角色

```
Top Claim: "All CS Goals achieved + All CS Claims valid"
   ↓
For each CS Claim:
   Sub-claim: "CL-XXX is valid"
   Argument: Why valid in this context
   Evidence:
     - Operational data showing assumption holds
     - Service agreement (for risk-transfer)
     - Item separation document (for out-of-scope)
```

---

## CS Claim 失效時的處理

如果 Claim 失效（如假設不成立、轉移對象不履行）：

```
1. 重新 TARA（該風險可能變高）
2. 修改處置策略：
   ├── 改為 In-scope Reduce
   ├── 補上技術防護
   └── 重新協商責任
3. 更新 CS Case
4. 通知相關方
```

---

## CS Claim 的審慎使用

> [!warning] 不當的 Claim
>
> ❌ **錯誤 1**：「假設攻擊者不存在」
>
> - 不合理假設
>
> ❌ **錯誤 2**：「假設使用者會做正確設定」
>
> - 使用者責任假設**需明確且可驗證**
>
> ❌ **錯誤 3**：「假設供應商會安全」
>
> - 無 CIA 支撐的轉移是空話
>
> ❌ **錯誤 4**：用 Claim 來「逃避」應做的工作
>
> - Assessment 會檢視 Claim 的合理性
>
> ✅ **好的 Claim 特徵**：
>
> - 有明確失效條件
> - 有驗證機制
> - 有對應的 fallback

---

## 證照考點

> [!important] 高頻考點
>
> 1. CS Claim 與 CS Goal **不同**
> 2. CS Claim 三類：**Assumed-context / Risk-transfer / Out-of-scope**
> 3. CS Claim **不可**用來迴避應做的工作
> 4. CS Claim 需有**失效處理**機制
> 5. OoC 元件的 Assumed Context **就是** CS Claims
> 6. CS Claim **進入 CS Case**，被 Assessment 檢視
> 7. CS Claim 是 Cybersecurity Concept 的一部分

---

## Related Notes

- [[06-Concept-Phase/02-Cybersecurity-Goals\|06-Concept-Phase/02-Cybersecurity-Goals]]
- [[06-Concept-Phase/04-Cybersecurity-Concept\|06-Concept-Phase/04-Cybersecurity-Concept]]
- [[03-Project-Dependent/05-Component-Out-of-Context\|03-Project-Dependent/05-Component-Out-of-Context]]
- [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]
- [[00-Dashboard/Exam-Traps#Trap 1\|00-Dashboard/Exam-Traps#Trap 1]]

## Practice

- [[06-Concept-Phase/Practice-Concept\|06-Concept-Phase/Practice-Concept]]

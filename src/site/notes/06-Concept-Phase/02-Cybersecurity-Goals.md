---
{"dg-publish":true,"permalink":"/06-concept-phase/02-cybersecurity-goals/","title":"資安目標 (Cybersecurity Goals)","tags":["iso-21434","concept-note","concept-phase","cs-goals"],"dg-note-properties":{"title":"資安目標 (Cybersecurity Goals)","source_pdf":"內部彙整 (ISO 21434 Clause 9.4)","part":"Clause 9","keywords":["cs-goals","goals","properties"],"tags":["iso-21434","concept-note","concept-phase","cs-goals"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> concept-level cybersecurity requirement associated with one or more threat scenarios.

簡言之：「**保護資安屬性免於威脅情境**的高層級陳述」。

---

## CS Goal 的格式

```
CS Goal = 對某 Asset 的某 Property 的保護
```

範例：

- 「**TCU 韌體的完整性** 應被保護免於未經授權的修改。」
- 「**蜂巢通訊的機密性** 應被保護免於竊聽。」
- 「**eCall 服務的可用性** 應被保護免於阻斷服務攻擊。」

---

## 資安屬性 (Cybersecurity Properties)

ISO 21434 採用擴展的 **CIA + AAA** 模型：

| 屬性                | 中文       | 例子         |
| ------------------- | ---------- | ------------ |
| **Confidentiality** | 機密性     | 加密通訊內容 |
| **Integrity**       | 完整性     | 韌體簽章     |
| **Availability**    | 可用性     | 抗 DoS       |
| **Authenticity**    | 真實性     | 訊息來源驗證 |
| **Authorization**   | 授權       | 角色權限控制 |
| **Non-repudiation** | 不可否認性 | Log 不可竄改 |
| (Auditability)      | 可稽核性   | 完整 log     |

> [!tip]
> CIA 是經典三屬性；其他屬性在汽車情境下也很重要（如 Authenticity 對 V2X、SecOC）。

---

## CS Goal 從哪裡來？

```
TARA 結果（威脅情境 + 風險）
        ↓
對於需處置的風險，定義保護目標
        ↓
Cybersecurity Goal
```

每個 CS Goal 必須**對應至少一個 Threat Scenario**。

---

## CS Goal 的結構建議

```yaml
cs_goal:
  id: CG-TCU-001
  statement: "The integrity of TCU firmware shall be protected
    against unauthorized modification."

  rationale: "Address threat scenarios TS-001, TS-005"

  threat_scenarios:
    - TS-001: "Remote firmware tampering via OTA"
    - TS-005: "Physical firmware tampering via JTAG"

  affected_asset: "TCU Firmware Image"

  cybersecurity_property: "Integrity"

  attack_potential_required: "Beyond Layman + Standard equipment" # 防護到的水準

  cal_recommendation: CAL-3 # (Annex E, informative)

  treatment_intent: "Reduce"

  notes:
    - "Achieved by: secure boot + signed updates + HSM-backed signature verification"
    - "Constraint: must support post-quantum signature in future"
```

---

## CS Goal vs Threat Scenario vs Damage

```
Damage Scenario (what we don't want)
   ↑
   ↑ 防止
   ↑
CS Goal (what we want to protect)
   ↑
   ↑ 對應
   ↑
Threat Scenario (how attacker could cause damage)
```

> [!important]
> **CS Goal 不是「具體技術解決方案」**，是高層級目標。
> 細節由 Cybersecurity Concept + CS Requirements 提供。

---

## CS Goal 的「品質」標準

| 品質       | 描述                               |
| ---------- | ---------------------------------- |
| **可追溯** | 對應至少一個 Threat Scenario       |
| **明確**   | 識別 Asset + Property + 保護程度   |
| **可驗證** | 後續可以設計 Validation 確認達成   |
| **可達成** | 技術與成本可行                     |
| **獨立**   | 不重複（多個 Goal 不應描述同一事） |
| **非實作** | 不指定「用 AES-256」這種細節       |

---

## CS Goal 的常見錯誤

> [!warning] ❌ 錯誤範例
>
> **錯誤 1**：「TCU 應使用 AES-256-GCM 加密」
>
> - 太具體（屬於 CS Requirement，非 Goal）
>
> **錯誤 2**：「TCU 應安全」
>
> - 太籠統，不可驗證
>
> **錯誤 3**：「防止所有攻擊」
>
> - 不可達成
>
> **錯誤 4**：「韌體應簽章」
>
> - 描述了「方法」而非「目標」
>
> ✅ **正確改寫**：
>
> - 「TCU 韌體的完整性應被保護，使攻擊者無法在攻擊潛能 < Moderate 條件下成功修改。」

---

## 多 CS Goal 的關係

一個 Threat Scenario 可能對應多個 CS Goal：

```
TS-001: "Remote firmware tampering"
   ↓
   ├── CG-001: "Integrity of firmware in transit"
   ├── CG-002: "Integrity of firmware at rest"
   └── CG-003: "Authenticity of update source"
```

一個 CS Goal 也可能對應多個 Threat Scenario：

```
CG-001: "Integrity of firmware"
   ↑
   ├── TS-001: "OTA tampering"
   ├── TS-005: "JTAG tampering"
   └── TS-008: "Supply chain tampering"
```

---

## CS Goal 在 CS Case 中的角色

```
Top Claim: "All CS Goals achieved"
   ↓
For each CS Goal:
   Claim: "CG-XXX achieved"
   Argument: Why
   Evidence: Test, review, analysis
```

→ [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]

---

## 證照考點

> [!important] 高頻考點
>
> 1. CS Goal 是**概念層級**（concept-level），非實作細節
> 2. 必須**對應至少一個 Threat Scenario**
> 3. 描述「Asset + Property + 保護程度」
> 4. **不指定具體技術**（屬於 CS Requirement）
> 5. CS Goal **vs** CS Requirement：Goal 是高層級，Requirement 是可實作可驗證的細化
> 6. CS Goal 是 CS Case 的**核心 Claim**

---

## Related Notes

- [[06-Concept-Phase/01-Item-Definition\|06-Concept-Phase/01-Item-Definition]]
- [[06-Concept-Phase/03-Cybersecurity-Claims\|06-Concept-Phase/03-Cybersecurity-Claims]]
- [[06-Concept-Phase/04-Cybersecurity-Concept\|06-Concept-Phase/04-Cybersecurity-Concept]]
- [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]
- [[00-Dashboard/Exam-Traps#Trap 1\|00-Dashboard/Exam-Traps#Trap 1]]

## Practice

- [[06-Concept-Phase/Practice-Concept\|06-Concept-Phase/Practice-Concept]]

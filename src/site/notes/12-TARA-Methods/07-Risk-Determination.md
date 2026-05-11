---
{"dg-publish":true,"permalink":"/12-tara-methods/07-risk-determination/","title":"風險值判定 (Risk Value Determination)","tags":["iso-21434","concept-note","tara","risk-determination"],"dg-note-properties":{"title":"風險值判定 (Risk Value Determination)","source_pdf":"內部彙整 (ISO 21434 Clause 15.8)","part":"Clause 15.8","keywords":["risk","risk-matrix","risk-value"],"tags":["iso-21434","concept-note","tara","risk-determination"],"created":"2026-05-11"}}
---


## 基本公式

```
Risk = f(Impact, Attack Feasibility)
```

> [!important]
> 注意：ISO 21434 採用 **Risk = f(Impact, Feasibility)** 兩維度推導（**非乘法**，標準未指定算式），不是 ISO 26262 的 **S × E × C**。

---

## 標準風險矩陣

ISO 21434 Clause 15.8 (Risk value determination) 規範以 Impact 與 Feasibility 兩維度推導風險值（標準未指定具體算式）。下列為業界常用的 4×4 矩陣（**標準本體未強制特定矩陣**；Annex F 是 Impact 評等指引，Annex G 是 Feasibility 評等指引）：

```
                      Attack Feasibility →
                Very Low   Low    Medium   High
Impact ↓     ┌────────┬────────┬───────┬────────┐
Severe       │   2    │   3    │   4   │   5    │
             ├────────┼────────┼───────┼────────┤
Major        │   1    │   2    │   3   │   4    │
             ├────────┼────────┼───────┼────────┤
Moderate     │   1    │   1    │   2   │   3    │
             ├────────┼────────┼───────┼────────┤
Negligible   │   1    │   1    │   1   │   2    │
             └────────┴────────┴───────┴────────┘
```

風險值 1-5（**1 = 最低，5 = 最高**）

> [!tip]
> 部分組織使用 1-25 矩陣（5 × 5），原理相同。

---

## 風險等級對應

| 風險值 | 等級                  | 行動                 |
| ------ | --------------------- | -------------------- |
| 5      | **Very High**         | 必須處置             |
| 4      | **High**              | 必須處置             |
| 3      | **Medium**            | 應處置或接受並文件化 |
| 2      | Low                   | 通常接受             |
| 1      | Negligible / Very Low | 通常接受             |

---

## 範例計算

### 範例 1：偽造煞車訊息

```
Threat: TS-005 (Spoofed brake CAN message)
Impact:
  Safety: Severe
  Financial: Moderate
  Operational: Major
  Privacy: Negligible
  → Overall: Severe

Attack Feasibility:
  Total score: 12 → High (容易)

Risk Value: 5 (Very High)
Required Action: 必須處置（如 SecOC）
```

### 範例 2：HSM 旁通道金鑰萃取

```
Threat: TS-022 (DPA on HSM)
Impact:
  Safety: Major (key 洩漏可影響多車)
  Financial: Severe
  Operational: Major
  Privacy: Major
  → Overall: Severe

Attack Feasibility:
  Total score: 55 → Very Low

Risk Value: 2 (Low)
Required Action: 通常接受（成本不對等）
```

### 範例 3：HMI 視覺干擾

```
Threat: TS-099 (Inject visual artifacts on HMI)
Impact:
  Safety: Negligible
  Financial: Negligible
  Operational: Moderate (annoying)
  Privacy: Negligible
  → Overall: Moderate

Attack Feasibility:
  Total score: 8 → High

Risk Value: 3 (Medium)
Required Action: 評估是否處置
```

---

## 風險矩陣的可變化性

> [!warning]
> ISO 21434 **未強制**特定風險矩陣。Annex F (Impact rating) 與 Annex G (Attack feasibility rating) 皆為 **informative**（資訊性）。
> 組織可**自訂矩陣**，但需在 CSMS 中**一致使用**並文件化。

常見變體：

- **5 × 5**（細粒度）
- **4 × 4**（最常見）
- **3 × 3**（粗粒度，小組織）
- **加權**（不同 Impact 面向有不同權重）

---

## 處置決策的基本原則（Risk Treatment 預告）

```
Risk Value 5 (Very High) → Reduce 或 Avoid
   └── 通常組織政策禁止「保留」

Risk Value 4 (High) → Reduce 為主
   └── 可特例 Retain（需高層級接受 + 補償措施）

Risk Value 3 (Medium) → 評估後決定
   └── Reduce / Transfer / Retain 都可能

Risk Value 1-2 (Low) → 通常 Retain
   └── 文件化即可
```

→ 詳見 [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]

---

## 殘餘風險 (Residual Risk)

```
Initial Risk (處置前)
       ↓
   風險處置
       ↓
Residual Risk (處置後仍存在)
       ↓
   需被適當層級接受
       ↓
   文件化於 CS Case
```

範例：

```
Initial Risk: 5 (Very High)
  → 加入 SecOC + Anti-replay
Residual Risk: 2 (Low)
  → 仍可能被多專家攻破，但成本不對等
  → 接受 + 持續監控
```

---

## 風險判定的紀錄要求

```yaml
risk_record:
  id: RR-TCU-005
  threat_scenario_ref: TS-005
  attack_path_ref: AP-005-A # 最容易那條

  impact:
    safety: Severe
    financial: Moderate
    operational: Major
    privacy: Negligible
    overall: Severe

  feasibility:
    method: "Attack Potential"
    parameters:
      time: 1
      expertise: 3
      knowledge: 3
      window: 1
      equipment: 4
    total: 12
    level: High

  risk_value: 5 # Very High
  risk_level: "Very High"

  initial_decision: "Must Reduce"

  reviewer: "CS Engineer Lead"
  reviewed_date: 2026-09-15
```

---

## 證照考點

> [!important] 高頻考點
>
> 1. 公式：**Risk = f(Impact, Feasibility)**
> 2. 矩陣最高值 = **Severe + High Feasibility = 5**
> 3. 風險值 5 = **Very High**，必須處置
> 4. **標準未強制特定矩陣**；Annex F (Impact) 與 Annex G (Feasibility) 為 informative
> 5. **殘餘風險**需被接受並文件化
> 6. **不是** S × E × C（那是 ISO 26262 HARA）
> 7. 跨組織的矩陣可能不同——需在 CIA 中對齊

---

## Related Notes

- [[12-TARA-Methods/04-Impact-Rating\|12-TARA-Methods/04-Impact-Rating]]
- [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]
- [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]
- [[00-Dashboard/Quick-Reference#五、風險值矩陣 (Risk Matrix)\|00-Dashboard/Quick-Reference#五、風險值矩陣 (Risk Matrix)]]

## Practice

- [[12-TARA-Methods/Practice-TARA\|12-TARA-Methods/Practice-TARA]]

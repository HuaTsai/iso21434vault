---
{"dg-publish":true,"permalink":"/01-foundations/03-cybersecurity-vs-safety/","title":"資安 (Cybersecurity) vs 功能安全 (Functional Safety)","tags":["iso-21434","concept-note","foundations","comparison"],"dg-note-properties":{"title":"資安 (Cybersecurity) vs 功能安全 (Functional Safety)","source_pdf":"內部彙整 (ISO 21434 vs ISO 26262)","part":"Clause 4 + General","keywords":["cybersecurity","safety","iso-26262","comparison"],"tags":["iso-21434","concept-note","foundations","comparison"],"created":"2026-05-11"}}
---


## 核心對照

| 比較項     | **Cybersecurity (ISO 21434)**                    | **Functional Safety (ISO 26262)**    |
| ---------- | ------------------------------------------------ | ------------------------------------ |
| 防範對象   | **惡意攻擊者**（intentional）                    | **隨機/系統性故障**（unintentional） |
| 焦點       | 對抗**人為威脅**                                 | 對抗**故障/錯誤**                    |
| 風險評估   | **TARA**（Threat-based）                         | **HARA**（Hazard-based）             |
| 等級       | **CAL**（保證等級）                              | **ASIL**（完整性等級）               |
| 等級推導   | Impact × Attack Feasibility                      | S × E × C                            |
| 衝擊面向   | **SFOP**（Safety/Financial/Operational/Privacy） | **Safety only**                      |
| 時間特性   | 持續演變（新攻擊不斷出現）                       | 統計穩定（隨機故障率）               |
| 後開發階段 | **重要**（更新、IR、EoS）                        | 相對輕（事件回應、變更）             |
| 主要 WP    | CS Case、TARA、CIA                               | Safety Case、HARA、DIA               |

---

## 為什麼必須並行？

```
              ┌─────────────┐
              │   Vehicle   │
              └──────┬──────┘
                     │
        ┌────────────┴────────────┐
        │                         │
   ┌────▼────┐               ┌────▼────┐
   │  Safety │ ←─ 互相影響 ──→ │ Security │
   │ ISO 26262│               │ ISO 21434│
   └─────────┘               └─────────┘
```

> [!important] 兩者互相影響
>
> - **資安失敗 → 安全危害**：攻擊者注入煞車 CAN 訊號 = Safety 危害。
> - **安全機制 → 資安弱點**：Limp-home 模式可能成為攻擊面。
> - **權衡 (Trade-off)**：強化資安（如加簽章驗證）可能拖慢安全反應時間。

---

## 共享與獨立的工件

```
┌───────────────────────────────────────────┐
│            Shared / Coordinated            │
│  • Item Definition (用語可能不同但對應同一物)│
│  • System Architecture (共用)              │
│  • V-Model 時序對齊                        │
│  • 整合測試（HIL）共享平台                  │
└───────────────────────────────────────────┘

┌──────────────────┐        ┌──────────────────┐
│   Safety Only    │        │ Security Only    │
│  • HARA          │        │  • TARA          │
│  • Safety Goals  │        │  • CS Goals      │
│  • Safety Case   │        │  • CS Case       │
│  • ASIL          │        │  • CAL           │
│  • DIA           │        │  • CIA           │
└──────────────────┘        └──────────────────┘
```

---

## 風險評估方法對照

### HARA (ISO 26262)

```
Hazard 識別
   ↓
評估 S × E × C
   ↓
ASIL 推導 (QM, A, B, C, D)
   ↓
Safety Goal
```

### TARA (ISO 21434)

```
Asset 識別
   ↓
Threat Scenario + Damage Scenario
   ↓
評估 Impact (SFOP) × Attack Feasibility
   ↓
Risk Value
   ↓
Risk Treatment + CS Goal
```

---

## 關鍵差異：時間特性

> [!tip]
> **Safety 故障率**：基於統計（如 FIT），可量化、相對穩定。
> **Security 威脅**：演變快速——昨日安全，今日可能因新攻擊技術而不安全。
> → 因此 ISO 21434 強調 **Clause 8 持續監控**，這在 ISO 26262 中相對輕。

---

## 工程組織常見模型

| 模型                  | 描述                         | 優點     | 缺點             |
| --------------------- | ---------------------------- | -------- | ---------------- |
| **完全分離**          | 兩個獨立團隊、獨立 WP        | 專業分工 | 重複工、整合風險 |
| **嵌入式 (Embedded)** | 資安工程師嵌入 Safety 團隊   | 對齊好   | 資安專業可能不足 |
| **協同 (Joint)** ⭐   | 兩團隊共用部分流程、共享工件 | 平衡     | 需明確 RACI      |

⭐ ISO 21434 建議模型。

---

## Co-engineering 介面點

```
Concept Phase:
  Item Definition (共用) ←─→ 安全 + 資安各自評估
                                  ↓
                          可能影響 Item 邊界

Product Development:
  Safety Architecture ↔ Security Architecture
  (例：MAC 機制要不要做硬體加速？)

Validation:
  HIL/Vehicle Test 平台共用，但測試案例不同

Operations:
  事件回應 (IR) 可能交叉觸發：
    Safety incident → 是否為資安事件？(誤動作 vs 攻擊)
    Cyber incident → 是否影響安全？
```

---

## 衝突解決優先順序

> [!warning] 經典考點
> 當資安要求與安全要求衝突時，**優先級**通常為：
>
> 1. **Safety 優先**（保護人命）
> 2. 在不損害 Safety 的前提下，最大化 Security
> 3. 文件化權衡決策（trade-off rationale）
>
> 但這不代表「安全可以忽略資安」——而是當**直接衝突無解**時的優先級。

範例：

- 緊急煞車訊號是否需要 MAC 驗證？
  - **資安觀點**：是，防止偽造。
  - **安全觀點**：MAC 驗證會增加延遲，可能違反 FTTI。
  - **解決**：硬體加速 MAC + 預先計算 + 超時降級到安全模式。

---

## ISO 21434 對 ISO 26262 的明確引用

> [!note] Clause 4 概要（非 verbatim）
> ISO 21434 Clause 4 要求**與 ISO 26262 協調**，並考量資安活動對 safety 的影響。
>
> **業界共識**：當 cybersecurity 與 safety 需求衝突時，safety 優先處置——但這是業界實務原則，**ISO 21434 Clause 4 本身並未以 "shall" 明文規定 "safety precedence"**。決策需文件化於 CS Case 並由適當層級接受。

---

## Related Notes

- [[01-Foundations/01-Standard-Overview\|01-Foundations/01-Standard-Overview]]
- [[01-Foundations/02-Key-Terms-Definitions\|01-Foundations/02-Key-Terms-Definitions]]
- [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]
- [[13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level\|13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level]]

## Practice

- [[01-Foundations/Practice-Foundations\|01-Foundations/Practice-Foundations]]

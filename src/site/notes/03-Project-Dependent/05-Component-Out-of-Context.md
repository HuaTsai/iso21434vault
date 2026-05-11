---
{"dg-publish":true,"permalink":"/03-project-dependent/05-component-out-of-context/","title":"脈絡外元件 (Out-of-Context Component)","tags":["iso-21434","concept-note","project-dependent","out-of-context"],"dg-note-properties":{"title":"脈絡外元件 (Out-of-Context Component)","source_pdf":"內部彙整 (ISO 21434 Clause 6.4.5)","part":"Clause 6","keywords":["out-of-context","ooc","platform","assumed-context"],"tags":["iso-21434","concept-note","project-dependent","out-of-context"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> component developed in a generic manner, not for a specific item, with **assumed context** about its usage and operational environment.

簡言之：「**為通用情境**開發，由整合者帶入**特定情境**的元件」。

---

## 典型範例

| 類型         | 範例                            | 假設情境                                      |
| ------------ | ------------------------------- | --------------------------------------------- |
| **平台軟體** | Tier-2 開發的 BSP / AUTOSAR BSW | 「將跑在 Cortex-M7、有 HSM、有 CAN/Ethernet」 |
| **晶片**     | 通用 SoC                        | 「將被用於 ASIL-B 以上汽車控制」              |
| **加密庫**   | 為汽車設計的加密 SDK            | 「將與符合 21434 的 HSM 一起使用」            |
| **通用模組** | OTA 客戶端通用框架              | 「將與 OEM 後端整合，TLS 由整合者實作」       |
| **參考設計** | TCU 參考板                      | 「將整合至車輛、由 OEM 提供天線」             |

---

## 與 ISO 26262 的 SEooC 關係

```
ISO 26262  → SEooC (Safety Element out of Context)
ISO 21434  → Out-of-Context Component
```

**概念相近**：都是「先開發、後決定情境」。
**重點都在**：開發者需文件化「**假設情境**」，整合者需**驗證**這些假設成立。

---

## 開發者（Tier-2）的責任

```
1. 定義「Assumed Context」
   ├── 預期的使用情境
   ├── 預期的攻擊者能力
   ├── 預期的整合介面
   └── 預期的環境（HSM、安全週邊）
   ↓
2. 在假設情境下執行 TARA
   ↓
3. 提供 OoC 元件 + 文件：
   ├── 假設情境清單
   ├── TARA 結果（基於假設）
   ├── 已知限制
   ├── 整合要求
   └── 已知威脅與緩解
```

---

## 整合者（OEM / Tier-1）的責任

```
1. 取得 OoC 元件 + 假設情境文件
   ↓
2. 驗證「實際情境」是否符合「假設情境」
   ├── 介面相符？
   ├── 環境相符？
   ├── 攻擊者模型相符？
   └── 限制可接受？
   ↓
3. 處理「差異」：
   ├── 補上缺失的整合層防護
   ├── 調整其他元件
   └── 接受殘餘風險（若可）
   ↓
4. 整合後再做一次 TARA（含 OoC 元件）
   ↓
5. 整合層 V&V
```

> [!warning]
> **常見錯誤**：直接信任 OoC 元件的 TARA 而不驗證假設。
> 例：OoC 假設「攻擊者無物理存取」，但整合產品暴露 OBD 接口。

---

## OoC vs Reuse vs OTS

| 比較     | **Out-of-Context** | **Reuse**         | **OTS**            |
| -------- | ------------------ | ----------------- | ------------------ |
| 開發目的 | **通用**（待整合） | 為**舊專案**開發  | 為**廣泛市場**開發 |
| 預期情境 | 由開發者**假設**   | 由舊專案決定      | 由供應商市場決定   |
| 整合責任 | 驗證**假設情境**   | Delta 分析        | 評估**整合風險**   |
| 範例     | 平台 BSP           | 前代 Gateway 軟體 | OpenSSL            |

> [!tip] 三者交集
> 一個元件可能**同時是**多種：例如「**OoC 的開源**參考設計」= OoC + OTS。

---

## OoC 元件的 CS Case 處理

OoC 元件**自帶**一份「**部分 CS Case**」（基於假設）。
整合者的 CS Case 必須：

1. **引用** OoC 元件的部分 CS Case
2. **論證**假設情境成立的證據
3. 補上**整合層**的論證

---

## 範例：HSM SDK 作為 OoC

```yaml
ooc_hsm_sdk:
  component: "Generic Automotive HSM SDK v3.2"
  vendor: "Tier-2 Inc."

  assumed_context:
    - "HSM hardware compliant with FIPS 140-2 Level 3"
    - "Used in vehicle E/E system with bounded compute resources"
    - "Integrator provides secure key provisioning at manufacturing"
    - "Attacker model: Level 4 (Expert, time-bound, equipment-bound)"
    - "No physical tampering during normal vehicle operation"

  delivered_artifacts:
    - SDK source/binary
    - Assumed context document
    - TARA Report (based on assumed context)
    - Integration Guide
    - Known limitations:
        - "Side-channel resistance limited to first-order DPA"
        - "Random source must be supplied by HSM hardware"

  integrator_responsibilities:
    - "Verify HSM hardware meets assumption"
    - "Implement secure key provisioning at production"
    - "Validate attacker model fits actual use case"
    - "Re-run TARA in actual integration context"
    - "Add side-channel countermeasures if higher resistance needed"
```

---

## 證照考點

> [!important] 高頻考點
>
> 1. **Out-of-Context** = 通用開發 + 假設情境
> 2. 開發者必須**文件化假設情境**
> 3. 整合者必須**驗證假設情境**
> 4. **整合者責任**：補足整合層 + 重做 TARA
> 5. 與 ISO 26262 的 **SEooC** 概念相近但獨立
> 6. OoC ≠ Reuse ≠ OTS（但可能重疊）

---

## Related Notes

- [[03-Project-Dependent/04-Reuse\|03-Project-Dependent/04-Reuse]]
- [[03-Project-Dependent/03-Tailoring\|03-Project-Dependent/03-Tailoring]]
- [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]
- [[00-Dashboard/Exam-Traps#Trap 7\|00-Dashboard/Exam-Traps#Trap 7]]

## Practice

- [[03-Project-Dependent/Practice-Project-Mgmt\|03-Project-Dependent/Practice-Project-Mgmt]]

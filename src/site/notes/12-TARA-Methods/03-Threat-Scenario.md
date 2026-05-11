---
{"dg-publish":true,"permalink":"/12-tara-methods/03-threat-scenario/","title":"威脅情境 (Threat Scenario)","tags":["iso-21434","concept-note","tara","threat-scenario"],"dg-note-properties":{"title":"威脅情境 (Threat Scenario)","source_pdf":"內部彙整 (ISO 21434 Clause 15.4)","part":"Clause 15.4","keywords":["threat-scenario","damage-scenario","stride","threat-modeling"],"tags":["iso-21434","concept-note","tara","threat-scenario"],"created":"2026-05-11"}}
---


## 兩個關鍵概念

### Damage Scenario（損害情境）

> [!quote]
> adverse consequence involving a vehicle or vehicle function and affecting a **road user**.

**特徵**：

- 站在 **road user** 角度
- 描述「**不希望發生的結果**」
- **不**描述「如何達成」

範例：

- 「車輛在高速公路失控撞擊」
- 「車主隱私資料被外洩」
- 「車輛被遠端鎖死無法啟動」

### Threat Scenario（威脅情境）

> [!quote]
> potential cause of compromise of cybersecurity properties of one or more assets in order to realize a damage scenario.

**特徵**：

- 描述「**手段 + 對象**」
- 連結 Asset + Property + Damage

範例：

- 「攻擊者透過 OBD 注入偽造煞車 CAN 訊息，導致車輛在高速行駛失控」
- 「攻擊者破解雲端帳號取得車主位置資料」
- 「攻擊者向 TCU 注入惡意 OTA 韌體導致 TCU 不可用」

---

## 兩者關係

```
                ┌──────────────────────┐
                │ Damage Scenario       │ ← Road User 視角
                │ "車輛失控撞擊"         │   後果
                └──────────┬───────────┘
                           │ 由以下手段達成
                           ↓
                ┌──────────────────────┐
                │ Threat Scenario       │ ← 攻擊者視角
                │ "OBD 注入偽煞車訊號"   │   過程
                └──────────────────────┘
                           ↑
                ┌──────────────────────┐
                │   Affected Asset      │
                │  "Brake CAN message"  │
                └──────────────────────┘
                           ↑
                ┌──────────────────────┐
                │   Compromised Property │
                │   "Authenticity"      │
                └──────────────────────┘
```

> [!warning] 易混淆
> **Damage ≠ Threat**。
> 命題單位最愛測這個（參考 [[00-Dashboard/Exam-Traps#Trap 12\|00-Dashboard/Exam-Traps#Trap 12]]）。

---

## Threat Scenario 結構

> [!important] Clause 15.4.2 要求
> ISO 21434 Threat Scenario 定義（Clause 3.1.32）：「**potential cause of compromise of cybersecurity properties of one or more assets in order to realize a damage scenario**」
>
> 關鍵：threat scenario **必須鏈結** damage scenario，否則只是「孤兒威脅」，無法評估 impact。

```
Threat Scenario = Threat × Asset × Property → Damage Scenario
                = (攻擊行為) × (被攻擊資產) × (被破壞屬性) → (對 road user / 系統的後果)

範例：
  Threat：注入訊息
  Asset：CAN 煞車訊號
  Property：真實性 (Authenticity)
  → Damage Scenario：高速行駛中誤煞車，導致追撞 / 失控
  → 完整描述：「攻擊者注入偽造煞車訊息（破壞真實性），導致高速失控撞擊」
```

---

## 識別 Threat Scenario 的方法

### 方法 1：STRIDE

| 縮寫（威脅類別）           | 中文     | 破壞的屬性      | 範例                   |
| -------------------------- | -------- | --------------- | ---------------------- |
| **S**poofing               | 假冒     | Authenticity    | 假冒 OEM 後端伺服器    |
| **T**ampering              | 竄改     | Integrity       | 修改韌體               |
| **R**epudiation            | 否認     | Non-repudiation | 否認自己發過某訊息     |
| **I**nformation Disclosure | 資訊洩漏 | Confidentiality | 萃取金鑰               |
| **D**enial of Service      | 阻斷服務 | Availability    | 癱瘓 CAN               |
| **E**levation of Privilege | 提權     | Authorization   | bypass Security Access |

> [!note]
> 左欄是**威脅行為**（攻擊類別），右欄是**被破壞的資安屬性**。例如 Repudiation 這個威脅破壞的是 Non-repudiation 屬性 — 兩者用詞相似但概念相反。

> [!tip]
> STRIDE 是業界**最常用**的方法，每個 asset/property 對照六類，可系統化發現威脅。

### 方法 2：UN R155 Annex 5 威脅清單

七大類 + 69 條具體威脅。對照清單檢視是否適用於自己系統。

### 方法 3：Attack Tree

從攻擊目標倒推，建構樹狀分解。

### 方法 4：Historical Threat Intel

從 CVE / Auto-ISAC / 過去事件學習。

### 方法 5：Brainstorming + Devil's Advocate

跨團隊腦力激盪 + 「攻擊者思維」演練。

> [!important]
> **多方法併用** + **跨團隊參與**，可降低遺漏。

---

## Threat Scenario 範本

```yaml
threat_scenario:
  id: TS-TCU-007
  name: "Remote firmware tampering via compromised OTA channel"

  damage_scenario_ref: DS-007
  damage_description: >
    Vehicle behavior unpredictably modified, potentially causing
    crash or denial of service.

  affected_assets:
    - id: A-001 (TCU Firmware)
    - id: A-005 (OTA delivery channel)

  compromised_properties:
    - "Integrity (firmware tampered)"
    - "Authenticity (source not verified)"

  stride_category: "Tampering + Spoofing"

  high_level_attack:
    - "Compromise OTA server credentials"
    - "Replace firmware in package"
    - "Re-sign with stolen key or bypass signature check"
    - "Push to fleet"

  preconditions:
    - "OTA server has internet exposure"
    - "Vehicle accepts updates from OTA server"

  attacker_motivation: "Mass disruption / extortion / sabotage"

  related_un_r155_threats:
    - "T2: Communication channel threats"
    - "T3: Update procedure threats"

  damage_categories:
    - safety: Severe (worst case crash)
    - financial: Major (recall + compensation)
    - operational: Severe (fleet-wide impact)
    - privacy: Major (also exposes data)
```

---

## Damage Scenario 範本

```yaml
damage_scenario:
  id: DS-007
  name: "Multiple vehicles affected by malicious firmware update"

  road_user_perspective: >
    Drivers experience uncommanded acceleration / braking,
    potentially causing crashes. Some vehicles bricked.

  affected_user_groups:
    - "Drivers of affected vehicles"
    - "Passengers"
    - "Other road users (collision risk)"
    - "Vehicle owners (asset value loss)"

  worst_case_scenario: "Fatal crash"

  reasonable_scenario: "Service disruption, panic, minor accidents"

  scope:
    geographical: "Region or country-wide if cloud campaign"
    fleet_size_affected: "Up to total fleet"
    duration: "Until OTA recovery deployed"
```

---

## Threat Scenario 與 Damage Scenario 的多對多關係

```
              Damage Scenarios
               ↑    ↑    ↑
               │    │    │
            ┌──┴────┴────┴──┐
            │ Threat        │
            │ Scenarios     │
            └───────────────┘

一個 Threat 可能對應多個 Damage：
  "OTA 攻擊" → 可能造成「失控」、「數據洩漏」、「服務中斷」

一個 Damage 可能來自多個 Threat：
  "失控" 可能來自 OTA、CAN 注入、診斷濫用等
```

---

## Damage Scenario 與 ISO 26262 Hazard 的關係

```
ISO 26262：Hazard
   └── 從車輛安全角度

ISO 21434：Damage Scenario
   └── 廣義 road user 後果（含 Safety + Financial + Operational + Privacy）
```

兩者可能**重疊**（如「失控撞擊」是 Hazard 也是 Damage），但 Damage Scenario **範圍更廣**。

---

## 證照考點

> [!important] 高頻考點
>
> 1. **Damage Scenario ≠ Threat Scenario**
> 2. Damage 從 **road user 角度**
> 3. Threat 包含 **攻擊手段 + 受影響資產 + 受破壞屬性**
> 4. **STRIDE** 是業界標準識別方法
> 5. **UN R155 Annex 5** 提供 69 條威脅參考
> 6. 多對多關係（一 Threat 多 Damage、一 Damage 多 Threat）
> 7. 識別需**多方法併用**

---

## Related Notes

- [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]
- [[12-TARA-Methods/02-Asset-Identification\|12-TARA-Methods/02-Asset-Identification]]
- [[12-TARA-Methods/04-Impact-Rating\|12-TARA-Methods/04-Impact-Rating]]
- [[13-Annexes-Tools/03-STRIDE-DREAD\|13-Annexes-Tools/03-STRIDE-DREAD]]
- [[00-Dashboard/Exam-Traps#Trap 12\|00-Dashboard/Exam-Traps#Trap 12]]

## Practice

- [[12-TARA-Methods/Practice-TARA\|12-TARA-Methods/Practice-TARA]]

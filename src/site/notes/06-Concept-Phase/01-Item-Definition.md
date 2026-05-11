---
{"dg-publish":true,"permalink":"/06-concept-phase/01-item-definition/","title":"標的定義 (Item Definition)","tags":["iso-21434","concept-note","concept-phase","item"],"dg-note-properties":{"title":"標的定義 (Item Definition)","source_pdf":"內部彙整 (ISO 21434 Clause 9.3)","part":"Clause 9","keywords":["item-definition","scope","boundary","interface"],"tags":["iso-21434","concept-note","concept-phase","item"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> Item is a component or set of components that implements a function at the vehicle level.
>
> Item Definition 描述 item 的**範圍、功能、邊界、介面、依賴與操作環境**。

ISO 21434 的 Item Definition 與 ISO 26262 概念**相近但獨立**——可以共用一份文件，或分別撰寫。

---

## 為什麼是「Concept Phase 的起點」？

```
沒有清楚的 Item Definition
       ↓
不知道要保護什麼（Assets 識別不全）
       ↓
TARA 不完整
       ↓
CS Goals 遺漏
       ↓
產品開發資安缺口
```

> [!important]
> Item Definition 是**所有後續資安活動的基礎**。

---

## Item Definition 必含內容

```yaml
item_definition:
  metadata:
    item_name: "Telematics Control Unit (TCU)"
    item_id: "TCU-2026-001"
    version: 1.0
    project: "EV Platform G3"

  description: >
    4G/5G connected TCU providing remote services,
    emergency call (eCall), and V2X capability.

  scope:
    in_scope:
      - "TCU ECU hardware"
      - "TCU firmware (bootloader + app)"
      - "Internal HSM"
      - "Antenna controller"
    out_of_scope:
      - "External antenna (physical)"
      - "Cellular network infrastructure"
      - "OEM backend service (separate item)"

  boundaries:
    physical:
      - "ECU PCB + enclosure"
      - "Connector pins"
    logical:
      - "CAN bus (2 channels)"
      - "Ethernet (100BASE-T1)"
      - "Cellular modem interface"
      - "OTA update interface"
      - "Diagnostic (UDS over DoIP)"
    temporal:
      - "Active: Ignition ON to Ignition OFF + 30 min"
      - "Standby: Wake on RF event"

  functions:
    - id: F-001
      name: "Emergency Call (eCall)"
      description: "Detect crash + transmit position to PSAP"
      criticality: high

    - id: F-002
      name: "OTA Software Update"
      description: "Receive + install firmware updates"
      criticality: high

    - id: F-003
      name: "Remote Diagnostics"
      description: "Allow OEM cloud to query DTC and parameters"
      criticality: medium

    - id: F-004
      name: "Telematics Streaming"
      description: "Periodic vehicle data upload"
      criticality: low

  assets: # 高層級識別，TARA 會細化
    data:
      - "Vehicle location data (real-time + historical)"
      - "Vehicle identifier (VIN)"
      - "User PII (paired device IDs)"
      - "Firmware images"
    keys:
      - "TLS client certificate + private key"
      - "Code signing public key (root of trust)"
      - "V2X PKI material"
      - "SecOC keys for CAN"
    functions:
      - "Emergency call dispatch"
      - "OTA firmware installation"

  interfaces:
    - id: IF-001
      name: "Cellular (5G/LTE)"
      direction: bidirectional
      protocol: "TLS 1.3 over IP"
      criticality: high
      attack_exposure: high
    - id: IF-002
      name: "CAN bus (Powertrain)"
      direction: bidirectional
      protocol: "CAN 2.0B + SecOC"
      criticality: high
      attack_exposure: medium
    - id: IF-003
      name: "Diagnostic (UDS over DoIP)"
      direction: bidirectional
      protocol: "ISO 14229 + Security Access"
      criticality: medium
      attack_exposure: high

  operational_environment:
    physical:
      - "Vehicle interior, behind dashboard"
      - "Temperature: -40 to +85 C"
      - "Vibration: per ISO 16750"
    operational:
      - "Normal driving"
      - "Parked (key off)"
      - "Service mode"
      - "End-of-line production"
      - "OTA update"

  assumptions:
    - "Vehicle is parked during major firmware update"
    - "OBD-II port physically secured by vehicle owner"
    - "Cellular network may be untrusted (attacker may MITM)"
    - "Diagnostic tools require authentication"

  dependencies:
    upstream:
      - "Gateway ECU (CAN traffic filtering)"
      - "Vehicle power management"
    downstream:
      - "Body Control Module (door lock commands)"
      - "Powertrain (limited control via secure channel)"

  related_items:
    - "Gateway ECU (separate item, separate TARA)"
    - "Infotainment Head Unit (separate item)"
```

---

## 範圍切割的考量

```
        車輛
         │
    ┌────┴────┐
    │         │
   Item A   Item B
  (TCU)   (Gateway)
    │         │
   ECUs    ECUs
```

> [!tip] 如何決定 Item 邊界
>
> - **太小**：失去整體視角，無法評估跨元件攻擊
> - **太大**：分析過於龐雜，不可行
> - **適中**：在「**車輛級可辨識功能單元**」切割
>
> 常見作法：以 ECU 或 ECU 群（執行同一功能）為 Item。

---

## Item Definition 與 TARA 的關係

```
Item Definition
   ↓
   ├── Assets 識別（TARA Step 1）
   ├── Interfaces 識別（攻擊面）
   ├── Operational Environment（攻擊者能達到的位置）
   └── Functions 識別（受保護的對象）
        ↓
       TARA
```

Item Definition **沒做好** → TARA 一定有缺失。

---

## Item Definition 與 Cybersecurity Goals 的關係

```
Item Definition 描述「什麼」
   ↓
TARA 找出「威脅」
   ↓
Cybersecurity Goals 描述「希望保護什麼」
   ↓
（回到 Item Definition：CS Goals 是 item 的屬性）
```

---

## Item Definition 是 Living Document

當以下情況發生時需更新：

- 設計變更（新增/移除介面、功能）
- 新依賴（整合新 ECU）
- 新操作模式（新增服務模式）
- 新威脅情境發現（可能需擴展 in-scope）

---

## 與 ISO 26262 Item Definition 的整合

```
策略 A：分別撰寫
  - 26262 Item Def (focus on hazards)
  - 21434 Item Def (focus on assets/threats)

策略 B：共用一份（推薦）
  - 共用 metadata、scope、boundaries
  - 各自附錄（26262 hazard analysis input vs 21434 asset list）
```

---

## 證照考點

> [!important] 高頻考點
>
> 1. Item Definition 是 Concept Phase **起點**
> 2. 必含：scope、boundaries（物理/邏輯/時間）、functions、assets、interfaces、environment、assumptions
> 3. 可與 ISO 26262 Item Definition **整合或分立**
> 4. Item Definition 是 **Living Document**
> 5. **沒做好 Item Definition → TARA 必有缺失**
> 6. assumptions 部分常被忽略但**極重要**（後續成為 CS Claims）

---

## Related Notes

- [[06-Concept-Phase/02-Cybersecurity-Goals\|06-Concept-Phase/02-Cybersecurity-Goals]]
- [[06-Concept-Phase/03-Cybersecurity-Claims\|06-Concept-Phase/03-Cybersecurity-Claims]]
- [[06-Concept-Phase/04-Cybersecurity-Concept\|06-Concept-Phase/04-Cybersecurity-Concept]]
- [[12-TARA-Methods/02-Asset-Identification\|12-TARA-Methods/02-Asset-Identification]]
- [[01-Foundations/02-Key-Terms-Definitions\|01-Foundations/02-Key-Terms-Definitions]]

## Practice

- [[06-Concept-Phase/Practice-Concept\|06-Concept-Phase/Practice-Concept]]

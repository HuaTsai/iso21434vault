---
{"dg-publish":true,"permalink":"/01-foundations/04-lifecycle-overview/","title":"資安工程生命週期總覽","tags":["iso-21434","concept-note","foundations","lifecycle"],"dg-note-properties":{"title":"資安工程生命週期總覽","source_pdf":"內部彙整 (ISO/SAE 21434:2021 Clause 6 + V-Model)","part":"Clause 6 + 跨章節","keywords":["lifecycle","v-model","workflow","work-products"],"tags":["iso-21434","concept-note","foundations","lifecycle"],"created":"2026-05-11"}}
---


## V-Model 視角

```
                     ┌─────────────────────┐
                     │  Concept Phase (9)  │
                     │  • Item Definition  │
                     │  • CS Goals         │
                     │  • CS Concept       │
                     └──────────┬──────────┘
                                │
        ┌───────────────────────┴───────────────────────┐
        ↓                                               ↑
┌───────────────┐                              ┌────────────────┐
│ Product Dev   │                              │ CS Validation  │
│ (Clause 10)   │                              │ (Clause 11)    │
│ • Design      │                              │ • Vehicle-level│
│ • Architecture│ ────── Verification ────→    │   validation   │
│ • Integration │                              │   (含 Pen Test │
│               │                              │   等方法)       │
│               │                              │ • Goal achieved│
└───────┬───────┘                              └────────┬───────┘
        ↓                                               ↑
   (Software/Hardware Unit Implementation & Test)
                                │
                                ↓
                     ┌─────────────────────┐
                     │ Production (12)     │
                     │ • Provisioning      │
                     │ • Build security    │
                     └──────────┬──────────┘
                                ↓
                     ┌─────────────────────┐
                     │ Ops & Maint (13)    │
                     │ • Incident Response │
                     │ • Updates (OTA)     │
                     └──────────┬──────────┘
                                ↓
                     ┌─────────────────────┐
                     │ EoS (14)            │
                     │ • Notify users      │
                     │ • Stop patches      │
                     └──────────┬──────────┘
                                ↓
                     ┌─────────────────────┐
                     │ Decommissioning (14)│
                     │ • Wipe data/keys    │
                     └─────────────────────┘
```

橫貫所有階段：

```
  • Clause 5：CSMS (Organizational)
  • Clause 6：Cybersecurity Plan, Tailoring, Case, Assessment
  • Clause 7：Distributed Activities (CIA)
  • Clause 8：Continual Monitoring & Vulnerability Mgmt
  • Clause 15：TARA（在每個關鍵階段執行/更新）
```

---

## 各階段重點與 Work Products

### Phase 0：組織就緒（Clause 5 — CSMS）

| 活動           | WP                         |
| -------------- | -------------------------- |
| 建立 CS Policy | Organizational CS Policy   |
| 角色與責任     | RASIC 矩陣                 |
| 能力管理       | Competence Management Plan |
| 文化建立       | CS Culture Documentation   |
| 工具評估       | Tool Approval Records      |
| 內部稽核       | CS Audit Reports           |

→ [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]

---

### Phase 1：專案啟動（Clause 6）

| 活動           | WP                        |
| -------------- | ------------------------- |
| 制定 CS Plan   | **Cybersecurity Plan** ⭐ |
| Tailoring 決策 | Tailoring Justification   |
| 角色指派       | Project RASIC             |
| OTS/Reuse 決策 | Reuse Analysis Report     |

→ [[03-Project-Dependent/01-Cybersecurity-Plan\|03-Project-Dependent/01-Cybersecurity-Plan]]

---

### Phase 2：分散式安排（Clause 7）

若有供應商參與：

| 活動           | WP                                       |
| -------------- | ---------------------------------------- |
| 供應商能力評估 | Supplier Capability Assessment           |
| RFQ 含 CS 條款 | RFQ Document                             |
| 簽訂 CIA       | **Cybersecurity Interface Agreement** ⭐ |

→ [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]

---

### Phase 3：概念階段（Clause 9）

```
Item Definition
    ↓
TARA (Clause 15) ← 第一次完整 TARA
    ↓
Cybersecurity Goals
    ↓
Cybersecurity Claims (out-of-scope 風險)
    ↓
Cybersecurity Concept (functional)
```

| WP                           | 說明              |
| ---------------------------- | ----------------- |
| Item Definition              | item 範圍與介面   |
| TARA Report                  | 完整威脅分析      |
| **Cybersecurity Goals** ⭐   | 高層級資安目標    |
| Cybersecurity Claims         | 假設/轉移風險陳述 |
| **Cybersecurity Concept** ⭐ | 概念解決方案      |

→ [[06-Concept-Phase/01-Item-Definition\|06-Concept-Phase/01-Item-Definition]]

---

### Phase 4：產品開發（Clause 10）

```
Cybersecurity Requirements
    ↓
Architecture Design
    ↓
Detailed Design (HW + SW)
    ↓
Implementation
    ↓
Integration & Verification
```

| WP                              | 階段 |
| ------------------------------- | ---- |
| CS Requirements Specification   | 設計 |
| Architecture Documentation      | 設計 |
| Verification Report             | 驗證 |
| Weakness/Vulnerability Analysis | 持續 |

→ [[07-Product-Development/01-Design-Requirements\|07-Product-Development/01-Design-Requirements]]

---

### Phase 5：資安驗證（Clause 11）

> 在**車輛層級**驗證資安目標達成。

| WP                                     | 重點           |
| -------------------------------------- | -------------- |
| **Cybersecurity Validation Report** ⭐ | 含滲透測試結果 |

→ [[08-Cybersecurity-Validation/01-Validation-Objectives\|08-Cybersecurity-Validation/01-Validation-Objectives]]

---

### Phase 6：生產（Clause 12）

| 活動                           | WP                      |
| ------------------------------ | ----------------------- |
| Provisioning（金鑰、憑證植入） | Production CS Controls  |
| 製程資安（防偽冒、防竄改）     | Production Audit Record |

→ [[09-Production/01-Production-Controls\|09-Production/01-Production-Controls]]

---

### Phase 7：營運與維護（Clause 13）

| 活動               | WP                            |
| ------------------ | ----------------------------- |
| 事件回應           | **Incident Response Plan** ⭐ |
| 更新管理（含 OTA） | Update Management Process     |
| 持續監控           | Monitoring Reports            |

→ [[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]

---

### Phase 8：終止支援與除役（Clause 14）

| 活動         | WP                        |
| ------------ | ------------------------- |
| 通知 EoS     | EoS Communication Records |
| 除役程序     | Decommissioning Procedure |
| 資料清除驗證 | Wipe Verification Report  |

→ [[11-EndOfSupport-Decommission/01-End-of-Support\|11-EndOfSupport-Decommission/01-End-of-Support]]

---

## 持續性活動（Clause 8）— 橫貫整個生命週期

```
┌─────────────────────────────────────┐
│ Monitoring （內外部情報蒐集）          │
│   ↓                                  │
│ Event Assessment （是否為資安事件？）   │
│   ↓                                  │
│ Vulnerability Analysis （影響範圍）    │
│   ↓                                  │
│ Vulnerability Management （處置）      │
└─────────────────────────────────────┘
```

→ [[05-Continual-Cybersecurity/01-Cybersecurity-Monitoring\|05-Continual-Cybersecurity/01-Cybersecurity-Monitoring]]

---

## TARA 介入點（Clause 15）

> [!important]
> TARA **不是一次性**活動。應在以下時機執行或更新：
>
> 1. **Item Definition 完成後**（首次完整 TARA）
> 2. **架構/設計變更時**（影響攻擊路徑）
> 3. **新弱點/威脅出現時**（Clause 8 觸發）
> 4. **變體 (Variant) / 重用情境**
> 5. **後開發階段定期 review**

---

## 階段間「Release Gate」

每個重大階段轉換需通過 Cybersecurity Gate：

| Gate                     | 通過條件                                        |
| ------------------------ | ----------------------------------------------- |
| Concept → Development    | TARA 完成、CS Goals 凍結、CS Plan 批准          |
| Development → Validation | Verification 完成、無 High/Very High 未處置風險 |
| Validation → Production  | CS Validation Report 通過、Case 簽核            |
| Production → Operations  | **Release for Post-Development** 完成           |

→ [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]

---

## Related Notes

- [[01-Foundations/01-Standard-Overview\|01-Foundations/01-Standard-Overview]]
- [[03-Project-Dependent/01-Cybersecurity-Plan\|03-Project-Dependent/01-Cybersecurity-Plan]]
- [[06-Concept-Phase/04-Cybersecurity-Concept\|06-Concept-Phase/04-Cybersecurity-Concept]]
- [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]
- [[00-Dashboard/Quick-Reference\|00-Dashboard/Quick-Reference]]

## Practice

- [[01-Foundations/Practice-Foundations\|01-Foundations/Practice-Foundations]]

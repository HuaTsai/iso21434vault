---
{"dg-publish":true,"permalink":"/04-distributed-cs-activities/02-cybersecurity-interface-agreement/","title":"資安界面協議 (CIA / Cybersecurity Interface Agreement)","tags":["iso-21434","concept-note","distributed","cia"],"dg-note-properties":{"title":"資安界面協議 (CIA / Cybersecurity Interface Agreement)","source_pdf":"內部彙整 (ISO 21434 Clause 7.4.3)","part":"Clause 7","keywords":["cia","interface-agreement","rasic","distributed"],"tags":["iso-21434","concept-note","distributed","cia"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義（業界通用釋義，非 Clause 3 verbatim）
> agreement between customer and supplier specifying the cybersecurity-related interactions, responsibilities, work products and information to be shared.

簡言之：**「跨組織資安合作合約」**。

---

## CIA vs DIA（ISO 26262 對應）

| 比較 | **CIA** (ISO 21434)               | **DIA** (ISO 26262)             |
| ---- | --------------------------------- | ------------------------------- |
| 全名 | Cybersecurity Interface Agreement | Development Interface Agreement |
| 領域 | 資安                              | 功能安全                        |
| 結構 | 相近（RASIC + WP + 時程）         | 相近                            |
| 整合 | 可整合為單一 IDIA（含 CIA + DIA） | —                               |

**業界實務**：常將 CIA + DIA 整合為 **IDIA (Integrated Development Interface Agreement)**，避免雙份文件。

---

## CIA 必含內容（最小集）

| 項目             | 說明                              |
| ---------------- | --------------------------------- |
| **雙方識別**     | 法人實體、聯絡窗口                |
| **適用範圍**     | 哪個 Item、哪個 ECU、哪個合約     |
| **RASIC 矩陣**   | 每個資安活動的責任分配            |
| **共享 WP 清單** | 哪一方提供哪些 WP、交付時程、格式 |
| **TARA 責任**    | 誰做、誰 review、誰維護           |
| **變更管理**     | 變更通知流程、影響評估、批准      |
| **事件回應介面** | 通報流程、SLA、聯合 IR            |
| **弱點管理**     | 弱點通報、修補責任                |
| **稽核權**       | 客戶能否稽核供應商                |
| **後開發**       | 維護年限、EoS 通知                |
| **訊息保密**     | NDA、TLP 分類                     |
| **爭議解決**     | 衝突解決流程                      |

---

## CIA 詳細 RASIC 範例

```
雙方：OEM-X (Customer) ↔ Tier-1-Y (Supplier)
Item：Telematics Control Unit (TCU)
```

| 活動 / 角色                |   OEM   |      Tier-1      |
| -------------------------- | :-----: | :--------------: |
| Item Definition (車輛級)   | **A/R** |        C         |
| Item Definition (TCU 範圍) |    C    |     **A/R**      |
| TARA (TCU 層級)            |    C    |     **A/R**      |
| TARA (車輛級)              | **A/R** |        C         |
| CS Goals 對齊              |  **A**  |        R         |
| 架構設計 (TCU)             |    I    |     **A/R**      |
| 韌體開發                   |    I    |     **A/R**      |
| Unit Verification          |    I    |     **A/R**      |
| Integration Verification   |    C    |     **A/R**      |
| Vehicle-level Validation   | **A/R** |        S         |
| Pen Test (TCU)             |    C    |     **A/R**      |
| Pen Test (整車)            | **A/R** |        S         |
| CS Case (TCU)              |    C    |     **A/R**      |
| CS Case (整車)             | **A/R** |        C         |
| Cybersecurity Assessment   |    A    | C (供應商側自評) |
| Incident Response (TCU)    |    C    |      **R**       |
| Incident Response (車輛)   |  **A**  |        S         |
| OTA Update Mgmt            | **A/R** | S (提供更新封包) |

---

## 共享 WP 清單範例

```yaml
shared_work_products:
  - wp_id: WP-001
    name: "Item Definition (TCU scope)"
    provider: Tier-1
    consumer: OEM
    delivery: "Project Kick-off + 4 weeks"
    format: "Doc + ARxml"
    version_control: "PLM system shared link"

  - wp_id: WP-002
    name: "TARA Report (TCU)"
    provider: Tier-1
    consumer: OEM
    delivery: "After Item Definition"
    format: "Excel + Medini export"
    review_required: true
    review_sla: "10 working days"

  - wp_id: WP-003
    name: "Verification Report"
    provider: Tier-1
    consumer: OEM
    delivery: "Pre-V&V Gate"
    format: "PDF"

  - wp_id: WP-004
    name: "Vehicle-level Validation Report"
    provider: OEM
    consumer: Tier-1
    delivery: "Post-Validation"
    format: "PDF"
```

---

## CIA 中的事件回應介面

```yaml
incident_response_interface:
  reporting_channel:
    primary: "secure@oem-x.com (PGP key on company website)"
    backup: "Hotline +1-xxx-xxx-xxxx (24/7)"

  reporting_sla:
    P1_critical: "1 hour"
    P2_high: "4 hours"
    P3_medium: "24 hours"
    P4_low: "5 business days"

  classification:
    framework: "Joint severity matrix (Annex A of CIA)"

  joint_response_team:
    oem_lead: "John Smith, OEM CSIRT Lead"
    tier1_lead: "Alice Wang, Tier-1 Security Lead"

  evidence_preservation:
    - "Logs preserved 90 days"
    - "Vehicle data preserved per CIA Annex B"

  external_communication:
    - "No party shall publicly disclose without joint approval"
    - "Coordinated disclosure to regulators"
```

---

## CIA 的版本管理

CIA 是 **Living Document**：

- 每次組織結構變動需 review
- 每次重大設計變更需 review
- 每年至少 review 一次
- 新發現的弱點/事件可能觸發更新

---

## 簽署層級

| 層級       | 範例                         |
| ---------- | ---------------------------- |
| **執行層** | 雙方 Project CS Manager 簽字 |
| **管理層** | 雙方 CS Officer / VP 簽字    |
| **法務層** | 法務批准（涉及合約義務）     |

> [!warning]
> CIA **不可**僅由 PM 簽字。需有資安專業批准 + 適當層級權威。

---

## CIA 缺失的後果

> [!warning]
> 沒有 CIA / CIA 不完整時的常見問題：
>
> 1. **責任真空**：某活動雙方都以為對方做
> 2. **WP 不一致**：格式、深度不對接
> 3. **事件處理混亂**：發現弱點不知通知誰
> 4. **稽核失敗**：UN R155 認證時無法展示供應鏈管理
> 5. **法律爭議**：事件後責任認定困難

---

## 證照考點

> [!important] 高頻考點
>
> 1. CIA **必須**在分散開發中存在
> 2. CIA 內容**最小集**：雙方識別、RASIC、共享 WP、變更/事件介面
> 3. CIA **不僅是法務文件**，是工程文件
> 4. CIA 是 **Living Document**
> 5. CIA 應在 **Release for Post-Development** 前所有議題關閉
> 6. CIA 與 26262 的 **DIA** 可整合（IDIA）
> 7. 通用準則：「**CIA 未明確 = 雙方都應假設自己負責**」（保守原則）

---

## Related Notes

- [[04-Distributed-CS-Activities/01-Customer-Supplier-Interaction\|04-Distributed-CS-Activities/01-Customer-Supplier-Interaction]]
- [[04-Distributed-CS-Activities/03-Supplier-Capability\|04-Distributed-CS-Activities/03-Supplier-Capability]]
- [[03-Project-Dependent/02-Responsibilities-Roles\|03-Project-Dependent/02-Responsibilities-Roles]]
- [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]
- [[00-Dashboard/Exam-Traps#Trap 6\|00-Dashboard/Exam-Traps#Trap 6]]

## Practice

- [[04-Distributed-CS-Activities/Practice-Distributed\|04-Distributed-CS-Activities/Practice-Distributed]]

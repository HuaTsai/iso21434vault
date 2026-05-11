---
{"dg-publish":true,"permalink":"/04-distributed-cs-activities/01-customer-supplier-interaction/","title":"客戶與供應商互動","tags":["iso-21434","concept-note","distributed"],"dg-note-properties":{"title":"客戶與供應商互動","source_pdf":"內部彙整 (ISO 21434 Clause 7)","part":"Clause 7","keywords":["customer","supplier","oem-tier1","distributed"],"tags":["iso-21434","concept-note","distributed"],"created":"2026-05-11"}}
---


## 為什麼需要 Clause 7？

汽車產業**沒有**一個 OEM 單獨開發整車軟體。
典型供應鏈：

```
Tier-3 (晶片/材料)
   ↓
Tier-2 (元件/平台軟體)
   ↓
Tier-1 (系統/ECU)
   ↓
OEM (整車)
```

每一層都可能擁有部分資安活動。**沒有清晰界面 → 風險被遺漏或重複**。

---

## Clause 7 的核心訴求

```
1. 識別「供應商-客戶」介面
2. 明確雙方資安責任（RASIC）
3. 簽訂 Cybersecurity Interface Agreement (CIA)
4. 評估供應商資安能力
5. 在 RFQ 階段納入資安要求
6. 持續監控供應商
```

---

## 「客戶」與「供應商」的相對性

> [!important]
> ISO 21434 中「客戶/供應商」是**相對概念**：
>
> ```
> 對 Tier-2 而言：Tier-1 是客戶
> 對 Tier-1 而言：OEM 是客戶
> 對 OEM 而言：Tier-1 是供應商
> ```
>
> 同一個組織在不同關係中可能扮演不同角色。

---

## 典型供應鏈情境

### 情境 A：完全外包

```
OEM ── 規格與整合 ──┐
                      │
            ┌─────────┴────────┐
            │                  │
        Tier-1A           Tier-1B
       (Powertrain)      (Infotainment)
            │                  │
        Tier-2A            Tier-2B
        (HSM)              (RTOS)
```

**重點**：每一層都需 CIA。

### 情境 B：OEM 自製 + 採購

```
OEM 開發部分元件 + 採購其他元件
   ↓
僅採購部分需 CIA
   ↓
自製部分由 OEM 內部 Clause 6 管理
```

### 情境 C：供應商間互動

```
Tier-1A 整合 Tier-2 (HSM)
   ↓
Tier-1A 與 Tier-1B 之間有資料交換
   ↓
Tier-1A 與 Tier-1B 之間也需 CIA（或由 OEM 協調）
```

---

## 介面類型

| 介面         | 說明           | 範例                            |
| ------------ | -------------- | ------------------------------- |
| **資訊介面** | 共享資料       | TARA 結果、Threat Intel         |
| **WP 介面**  | 交付工件       | CS Concept、Verification Report |
| **流程介面** | 共同活動       | Joint Review、Joint Pen Test    |
| **責任介面** | 誰負責什麼     | RASIC 跨組織                    |
| **變更介面** | 變更通知與評估 | 設計變更通知流程                |
| **事件介面** | 事件通報       | Tier-1 發現弱點如何通知 OEM     |

---

## 客戶端（OEM 或上游）的責任

```
☑ 在 RFQ 中包含資安要求
☑ 評估供應商資安能力
☑ 提供 Item 情境與 TARA 假設給供應商
☑ 接收並整合供應商交付的 WP
☑ 持續監控供應商
☑ 處理跨組織事件
☑ 在 CSMS 中追蹤所有供應商
```

---

## 供應商端的責任

```
☑ 展示資安能力（含 CSMS 對應）
☑ 遵守 CIA 約定
☑ 交付約定 WP
☑ 通報自身發現的弱點 / 變更
☑ 配合稽核
☑ 對其下游再簽 CIA（Subsubcontracting）
```

---

## 證照考點

> [!important]
>
> 1. **客戶/供應商** 是相對概念
> 2. 介面責任由 **CIA** 定義（→ [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]）
> 3. RFQ 階段就應包含資安要求
> 4. 供應商能力評估是**事前**活動
> 5. 跨組織事件回應需事先約定（不能臨時想）

---

## Related Notes

- [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]
- [[04-Distributed-CS-Activities/03-Supplier-Capability\|04-Distributed-CS-Activities/03-Supplier-Capability]]
- [[03-Project-Dependent/02-Responsibilities-Roles\|03-Project-Dependent/02-Responsibilities-Roles]]

## Practice

- [[04-Distributed-CS-Activities/Practice-Distributed\|04-Distributed-CS-Activities/Practice-Distributed]]

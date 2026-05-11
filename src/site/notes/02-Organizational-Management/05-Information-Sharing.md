---
{"dg-publish":true,"permalink":"/02-organizational-management/05-information-sharing/","title":"資訊共享 (Information Sharing)","tags":["iso-21434","concept-note","csms","information-sharing"],"dg-note-properties":{"title":"資訊共享 (Information Sharing)","source_pdf":"內部彙整 (ISO 21434 Clause 5.4.5)","part":"Clause 5","keywords":["information-sharing","isac","threat-intelligence","disclosure"],"tags":["iso-21434","concept-note","csms","information-sharing"],"created":"2026-05-11"}}
---


## 為什麼資訊共享是規範性要求？

> [!important]
> 汽車資安威脅**演變迅速**，單一組織難以全面掌握。
> ISO 21434 Clause 5 要求組織**主動參與**資訊共享，包含：
>
> - 接收外部威脅情報
> - 分享自身發現的威脅/弱點（在不揭露機密前提下）

---

## 資訊共享的兩個方向

```
        ┌──────────────────┐
        │   組織內部        │
        └──────┬───────────┘
               │
       ┌───────┴────────┐
       │                │
   ┌───▼───┐        ┌───▼────┐
   │ Inbound │      │ Outbound│
   │ 接收外部 │      │ 對外分享 │
   └─────────┘      └─────────┘
```

---

## Inbound 來源

| 來源類型          | 範例                         | 內容                   |
| ----------------- | ---------------------------- | ---------------------- |
| **ISAC**          | Auto-ISAC                    | 汽車業專屬威脅情報共享 |
| **CERT/CSIRT**    | CERT-EU、JPCERT、TWNCERT     | 國家級資安事件回應     |
| **CVE 資料庫**    | NVD、MITRE                   | 已公開弱點             |
| **供應商通報**    | HSM、軟體元件供應商          | 元件層級弱點           |
| **學術研究**      | 學術論文、Black Hat、DEF CON | 新型攻擊技術           |
| **客戶/車主回饋** | 客服回報                     | 異常行為通報           |
| **政府公告**      | NHTSA、TÜV、ENISA            | 法規/警示              |
| **Bug Bounty**    | 自家或第三方平台             | 研究者發現             |

---

## Outbound 共享

```
組織發現新威脅/弱點
        ↓
評估「能否」+「應否」分享
        ↓
┌──────────────────────────┐
│ 機密程度分類：              │
│   • Confidential (不分享)   │
│   • TLP:RED (僅特定對象)   │
│   • TLP:AMBER (受限分享)    │
│   • TLP:GREEN (社群分享)    │
│   • TLP:WHITE (公開)        │
└──────────────────────────┘
        ↓
依分類執行分享流程
```

> **TLP (Traffic Light Protocol)** 是業界標準分享分級。

---

## ISAC：汽車產業專屬

### Auto-ISAC（Automotive Information Sharing and Analysis Center）

- 2015 成立，OEM 與 Tier-1 主導
- 提供威脅情報、Best Practices、Incident Coordination
- 會員需簽 NDA + 共享協議

### 區域 ISAC

- 美國：Auto-ISAC
- 歐洲：AutoISAC（與美國互通）
- 日本：J-Auto-ISAC（J-ISAC 的車用分支）

---

## 弱點揭露 (Vulnerability Disclosure)

### Coordinated Vulnerability Disclosure (CVD)

```
研究者發現弱點
    ↓
通報組織（透過 VDP - Vulnerability Disclosure Program）
    ↓
組織確認 + 評估
    ↓
組織修補
    ↓
協調揭露時間（通常 90 天）
    ↓
公開 CVE / 通告
```

> [!important]
> ISO 21434 + UN R155 期望 OEM 建立 **VDP**：
>
> - 公開窗口（security.txt、安全聯絡信箱）
> - SLA（回應時限）
> - 安全港 (Safe Harbor)：不對善意研究者提告

---

## 內部資訊共享機制

組織內部也需有共享流程：

```
專案 A 發現新威脅
    ↓
通報 CS Manager
    ↓
評估是否影響其他專案
    ↓
跨專案通報（內部入口、會議）
    ↓
更新 Lessons Learned 資料庫
    ↓
（若需要）更新組織政策、培訓教材
```

---

## 紀錄要求

**Information Sharing Records** 應含：

- 共享日期
- 對象（in/out）
- 內容摘要
- 機密分類
- 批准者
- 追蹤狀態

---

## 法律與隱私考量

> [!warning]
> 共享前必須確認：
>
> - 不違反 NDA / 客戶合約
> - 不揭露 PII / 商業機密
> - 不違反出口管制（如加密技術）
> - 不違反當地隱私法（GDPR、CCPA、PIPL）
> - 不主動揭露未公開弱點細節（在修補前）

---

## 證照考點

> [!important]
>
> - 資訊共享是 **Clause 5 規範性要求**（不是可選）
> - 包含 **Inbound + Outbound** 兩個方向
> - **ISAC** 是業界主要平台
> - **VDP** 與 **CVD** 是揭露的最佳實踐
> - **TLP** 是分類分享的常用標準
> - 共享紀錄是必要 WP

---

## Related Notes

- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]
- [[05-Continual-Cybersecurity/01-Cybersecurity-Monitoring\|05-Continual-Cybersecurity/01-Cybersecurity-Monitoring]]
- [[05-Continual-Cybersecurity/03-Vulnerability-Analysis\|05-Continual-Cybersecurity/03-Vulnerability-Analysis]]

## Practice

- [[02-Organizational-Management/Practice-CSMS\|02-Organizational-Management/Practice-CSMS]]

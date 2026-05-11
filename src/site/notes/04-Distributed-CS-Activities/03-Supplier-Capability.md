---
{"dg-publish":true,"permalink":"/04-distributed-cs-activities/03-supplier-capability/","title":"供應商能力評估","tags":["iso-21434","concept-note","distributed","supplier"],"dg-note-properties":{"title":"供應商能力評估","source_pdf":"內部彙整 (ISO 21434 Clause 7.4.2)","part":"Clause 7","keywords":["supplier-capability","rfq","evaluation","audit"],"tags":["iso-21434","concept-note","distributed","supplier"],"created":"2026-05-11"}}
---


## 為什麼需要評估供應商？

> [!important]
> 「**你不會把資安工作交給沒能力的人做**」
>
> Clause 7.4.2 要求客戶在採購前評估供應商的資安能力，確保：
>
> 1. 供應商能履行 CIA
> 2. 供應商有適當的 CSMS
> 3. 供應商有持續維護能力（含後開發）

---

## 評估流程

```
1. RFQ 階段：要求供應商提供資安能力證據
   ↓
2. 文件審查：CSMS 文件、認證、歷史紀錄
   ↓
3. 現場稽核（重要供應商）
   ↓
4. 試辦（Pilot）或小規模專案先試水
   ↓
5. 評估報告 + 決策
   ↓
6. 簽訂 CIA + 採購合約
   ↓
7. 持續監控（重評估）
```

---

## RFQ 階段的資安要求

> [!tip]
> ISO 21434 + UN R155 要求 OEM 在 **RFQ** 階段就納入資安要求。
> 不是等供應商選定後才談——那就太晚。

### RFQ 應包含

```yaml
rfq_cybersecurity_section:
  general_capability:
    - "Compliance with ISO/SAE 21434"
    - "CSMS evidence (UN R155 alignment)"
    - "Cybersecurity team structure"
    - "Past incident response examples"

  project_specific:
    - "TARA capability for proposed item"
    - "Pen test capability"
    - "Cryptographic implementation experience"
    - "HSM integration experience"

  contractual:
    - "Willingness to sign CIA"
    - "Audit rights"
    - "Disclosure obligations"
    - "Supply chain transparency (SBOM)"

  cost:
    - "Cybersecurity activities separately costed"
    - "Maintenance / patch SLA pricing"
```

---

## 供應商能力評估維度

```
┌─────────────────────────────────────┐
│ 1. Process Maturity                 │
│    • CSMS 流程文件化                  │
│    • 過去專案 ISO 21434 應用經驗      │
├─────────────────────────────────────┤
│ 2. Technical Capability             │
│    • TARA 執行能力                   │
│    • 安全設計能力                    │
│    • 滲透測試能力                    │
│    • 加密 / HSM 整合經驗             │
├─────────────────────────────────────┤
│ 3. Organizational                   │
│    • CS 團隊規模 + 資質              │
│    • Top Mgmt 承諾                   │
│    • 培訓計畫                        │
├─────────────────────────────────────┤
│ 4. Track Record                     │
│    • 過去事件如何處理                 │
│    • 客戶推薦                        │
│    • CVE 暴露歷史                    │
├─────────────────────────────────────┤
│ 5. Sustainability                   │
│    • 後開發支援承諾                   │
│    • EoS 政策                        │
│    • 持續監控能力                    │
└─────────────────────────────────────┘
```

---

## 評估方法

| 方法               | 適用                      | 成本       |
| ------------------ | ------------------------- | ---------- |
| **問卷 (RFI/RFQ)** | 初步篩選                  | 低         |
| **文件審查**       | 中型供應商                | 中         |
| **電話/視訊面談**  | 釐清問題                  | 低-中      |
| **現場稽核**       | 關鍵供應商                | 高         |
| **試辦專案**       | 戰略供應商                | 很高       |
| **第三方評估**     | 不熟悉供應商              | 中-高      |
| **既有認證**       | TISAX、ISO 27001、UN R155 | 低（已有） |

---

## 認證作為證據（注意限制）

| 認證                      | 可作為              | 不可取代     |
| ------------------------- | ------------------- | ------------ |
| **UN R155 CSMS**          | CSMS 存在的初步證據 | 專案層級評估 |
| **TISAX**                 | 資訊安全管理        | 產品資安能力 |
| **ISO 27001**             | IT 資訊安全         | 車輛產品資安 |
| **ISO 9001 / IATF 16949** | 品質管理            | 資安專業     |
| **Common Criteria**       | 特定產品/元件評估   | 整體流程     |

> [!warning]
> **任何認證都只是「部分證據」**——仍需結合 RFQ 回應與實地檢視。

---

## 評估報告範本

```yaml
supplier_evaluation:
  supplier: "Tier-1-Y Inc."
  evaluator: "OEM Supplier Cybersecurity Team"
  date: 2026-05-11
  proposed_item: "TCU for EV Platform G3"

  capability_scores: # 1-5 scale
    process_maturity: 4
    technical_capability: 4
    organizational: 5
    track_record: 3 # 1 prior CVE in 2023, well handled
    sustainability: 4

  certifications:
    - ISO 9001: valid
    - IATF 16949: valid
    - UN R155 CSMS: valid (2024-09)
    - ISO 27001: valid

  findings:
    strengths:
      - "Strong TARA process"
      - "Dedicated CSIRT 24/7"
      - "Active in Auto-ISAC"
    concerns:
      - "Pen test mostly outsourced"
      - "Long term EoS policy unclear"

  recommendations:
    - "Require Pen test capability buildup before contract"
    - "Negotiate explicit EoS terms in CIA"

  decision: "Conditional Approve"
  conditions:
    - "Sign CIA with Pen test capability commitment"
    - "Re-assess in 12 months"
```

---

## 持續監控供應商

```
合約簽訂後 → 不是結束，是開始

監控項目：
├── CSMS 狀態（年度確認）
├── 安全事件通報
├── 供應商 CVE 暴露
├── 交付品質（WP 完整性）
├── 變更管理遵循
└── 後開發承諾履行
```

---

## 供應商重評估時機

- 重大組織變動（收購、分拆）
- 重大資安事件
- 認證到期 / 撤銷
- 新專案啟動（情境變化）
- 至少**每 3 年**全面重評估

---

## 證照考點

> [!important] 高頻考點
>
> 1. 供應商能力評估在 **RFQ 階段就要做**
> 2. 評估維度：Process、Technical、Organizational、Track Record、Sustainability
> 3. 認證**只是部分證據**，不取代評估
> 4. 評估結果**寫入 CIA**
> 5. 供應商需**持續監控**（不只是一次性評估）
> 6. 重大變更觸發**重評估**

---

## Related Notes

- [[04-Distributed-CS-Activities/01-Customer-Supplier-Interaction\|04-Distributed-CS-Activities/01-Customer-Supplier-Interaction]]
- [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]
- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]

## Practice

- [[04-Distributed-CS-Activities/Practice-Distributed\|04-Distributed-CS-Activities/Practice-Distributed]]

---
{"dg-publish":true,"permalink":"/10-operations-maintenance/02-updates/","title":"更新管理（含 OTA）","tags":["iso-21434","concept-note","operations","updates","ota"],"dg-note-properties":{"title":"更新管理（含 OTA）","source_pdf":"內部彙整 (ISO 21434 Clause 13 + UN R156 / ISO 24089)","part":"Clause 13","keywords":["updates","ota","sums","un-r156","iso-24089"],"tags":["iso-21434","concept-note","operations","updates","ota"],"created":"2026-05-11"}}
---


## ISO 21434 + UN R156 + ISO 24089 的三角關係

```
ISO 21434 (Clause 13)
   └── 描述：更新如何與資安整合

ISO 24089 (詳細工程標準)
   └── 描述：軟體更新工程方法

UN R156 (法規)
   └── 描述：SUMS 與車型認證
```

> [!warning]
> ISO 21434 **本身不深入**更新工程細節。**ISO 24089** 是專屬技術依據。
> 但 21434 要求更新的**資安面**與整體 CSMS 整合。

---

## OTA 更新生命週期

```
Trigger
   ↓
   ├── Bug fix
   ├── Security patch
   ├── Feature update
   └── Recall
        ↓
Update Package Preparation
   ├── 開發
   ├── 測試（功能 + 資安）
   ├── 影響分析（safety、security、type approval）
   └── 簽章
        ↓
Distribution Planning
   ├── 目標車型 / 區域
   ├── 分批計畫
   ├── 時間窗口
   └── Rollback Plan
        ↓
Deployment
   ├── 通知使用者（必要時）
   ├── 下載
   ├── 安裝（適當時機）
   └── 驗證
        ↓
Post-Update Monitoring
   ├── 失敗率
   ├── 異常通報
   └── 必要時 rollback
```

---

## 更新的資安要求 (Clause 13 視角)

```
1. 更新封包真實性
   ├── 簽章驗證 (ECDSA / RSA)
   └── 簽章金鑰於 HSM

2. 更新封包完整性
   ├── 雜湊驗證
   └── 全程加密傳輸 (TLS)

3. 抗 Rollback
   ├── Anti-rollback counter (eFuse / monotonic)
   └── 拒絕降級到含弱點的舊版

4. 更新中車輛安全
   ├── 不在駕駛中更新關鍵元件
   ├── 失敗回滾
   └── 雙 partition（A/B）

5. 更新後驗證
   ├── 開機簽章驗證
   ├── 自我測試
   └── 異常通報

6. 變更追蹤
   ├── 每車版本紀錄
   ├── 雲端 SBOM 同步
   └── Type approval 維持
```

---

## A/B Partition 更新模式

```
┌──────────────────┐
│  Partition A     │  ← Active
│  (FW v2.3.0)     │
├──────────────────┤
│  Partition B     │  ← Inactive
│  (FW v2.4.0      │
│   downloaded)    │
└──────────────────┘
        ↓
   驗證 + 簽章 OK
        ↓
   切換 active 至 B
        ↓
   重新開機到 B
        ↓
   驗證新版正常運作
        ↓
   舊版 (A) 保留作為 rollback
```

**優點**：

- 失敗可立即 rollback
- 更新中車輛仍能運作
- 風險降低

---

## 更新與 TARA 的關係

每次重大更新需評估：

```
Update Package
   ↓
Impact Analysis：
├── 引入新弱點？
├── 改變攻擊面？
├── 影響其他元件？
└── 影響 type approval？
   ↓
若有影響 → 更新 TARA
   ↓
更新 CS Case
   ↓
（若必要）通知 UN R155 / R156 監管機構
```

---

## UN R156 SUMS 要點

```yaml
sums_compliance:
  required_processes:
    - "識別所有可更新的車輛軟體"
    - "軟體版本對應車輛狀態"
    - "變更影響評估"
    - "更新前後合規維持（type approval）"
    - "使用者通知（重要更新）"
    - "失敗回滾機制"

  per_update:
    - "Pre-update vehicle compatibility check"
    - "Documentation per update"
    - "Customer notification (if functional change)"
    - "Records of who got what update"

  certification:
    - "SUMS Certification (3 years)"
    - "Vehicle Type Approval (per type)"
```

---

## ISO 24089 結構（與 21434 對應）

```
ISO 24089 結構 → 與 21434 對應

CSMS-like 管理 (Part 2)
   ├── 與 ISO 21434 Clause 5 整合

Project-level (Part 3-4)
   ├── 與 Clause 6 整合

Update Engineering (Part 5-8)
   ├── 概念、開發、驗證、生產

Operations (Part 9)
   ├── 與 Clause 13 整合
```

---

## 更新類型

| 類型                    | 範例       | 是否需資安 review |
| ----------------------- | ---------- | ----------------- |
| Critical Security Patch | 修補 CVE   | ✓ 全流程          |
| Functional Update       | 新功能、UI | ✓ 影響評估        |
| Calibration Update      | 參數調整   | 視影響            |
| Map Update              | 導航地圖   | 通常輕量          |
| Recall                  | 重大修補   | ✓ 全流程 + 監管   |

---

## 證照考點

> [!important]
>
> 1. **ISO 21434 + UN R156 + ISO 24089** 三角關係
> 2. **A/B Partition** 是業界 OTA 最佳實踐
> 3. **Anti-rollback** 防止降級攻擊
> 4. 重大更新需更新 **TARA + CS Case**
> 5. **SUMS Certification** 有效期 3 年
> 6. 更新需考慮 **type approval 維持**
> 7. 更新失敗需有 **rollback 機制**

---

## Related Notes

- [[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]
- [[05-Continual-Cybersecurity/04-Vulnerability-Management\|05-Continual-Cybersecurity/04-Vulnerability-Management]]
- [[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]

## Practice

- [[10-Operations-Maintenance/Practice-Operations\|10-Operations-Maintenance/Practice-Operations]]

---
{"dg-publish":true,"permalink":"/12-tara-methods/01-tara-overview/","title":"TARA (Threat Analysis and Risk Assessment) 流程總覽","tags":["iso-21434","concept-note","tara","methodology"],"dg-note-properties":{"title":"TARA (Threat Analysis and Risk Assessment) 流程總覽","source_pdf":"內部彙整 (ISO 21434 Clause 15)","part":"Clause 15","keywords":["tara","threat-analysis","risk-assessment","methodology"],"tags":["iso-21434","concept-note","tara","methodology"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> **Systematic** approach to identify and **assess** cybersecurity-related **risks**.

簡言之：「**找出威脅** + **評估風險** + **決定處置**」的系統化方法。

> [!important]
> TARA 是 ISO 21434 中**最被考的**章節之一。八步驟需牢記。

---

## 為什麼 TARA 是核心？

```
TARA 結果
   ├── 決定 Cybersecurity Goals
   ├── 決定 Cybersecurity Concept
   ├── 決定 CS Requirements
   ├── 決定 CAL（保證等級）
   ├── 影響架構設計
   └── 影響 Validation 範圍

→ TARA 不對，後續全錯
```

---

## TARA 八步驟（**必背**）

```
1. Asset Identification           (Clause 15.3) ← 資產識別
   ↓
2. Threat Scenario Identification (Clause 15.4) ← 威脅情境識別
   ↓
3. Impact Rating                  (Clause 15.5) ← 衝擊評等 (SFOP)
   ↓
4. Attack Path Analysis           (Clause 15.6) ← 攻擊路徑分析
   ↓
5. Attack Feasibility Rating      (Clause 15.7) ← 攻擊可行性評等
   ↓
6. Risk Value Determination       (Clause 15.8) ← 風險值判定
   ↓
7. Risk Treatment Decision        (Clause 15.9) ← 風險處置決策
   ↓
8. (持續監控 + 更新)              ← 非顯式步驟，但實務必要（屬 Clause 8 Continual activities）
```

> [!tip] 記憶法
> **A**sset → **T**hreat → **I**mpact → **A**ttack Path → **F**easibility → **R**isk → **T**reatment
>
> 縮寫：「**ATIA-FRT**」或記成：
> 「**找資產 → 想威脅 → 看後果 → 畫路徑 → 算難度 → 算風險 → 決定處置**」

---

## 各步驟對應筆記

| 步驟 | 中文       | 對應筆記                                         |
| ---- | ---------- | ------------------------------------------------ |
| 1    | 資產識別   | [[12-TARA-Methods/02-Asset-Identification\|12-TARA-Methods/02-Asset-Identification]]      |
| 2    | 威脅情境   | [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]           |
| 3    | 衝擊評等   | [[12-TARA-Methods/04-Impact-Rating\|12-TARA-Methods/04-Impact-Rating]]             |
| 4    | 攻擊路徑   | [[12-TARA-Methods/05-Attack-Path-Analysis\|12-TARA-Methods/05-Attack-Path-Analysis]]      |
| 5    | 可行性評等 | [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]] |
| 6    | 風險判定   | [[12-TARA-Methods/07-Risk-Determination\|12-TARA-Methods/07-Risk-Determination]]        |
| 7    | 風險處置   | [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]            |

---

## TARA 輸入

```
Item Definition         ← Concept Phase 提供
   ├── Scope, Boundaries
   ├── Functions, Assets
   ├── Interfaces
   └── Operational Environment

業界威脅情報       ← Clause 8 Monitoring
   ├── CVE
   ├── Auto-ISAC alerts
   └── 歷史事件

組織政策            ← CSMS
   ├── 風險容忍度
   ├── 處置政策
   └── CAL 對應規則
```

---

## TARA 輸出

```
TARA Report 含：
├── Asset 清單
├── Threat Scenarios 清單
├── Damage Scenarios 清單
├── Impact Rating（SFOP）
├── Attack Paths 清單
├── Attack Feasibility Rating
├── Risk Value 矩陣
├── Risk Treatment 決策
├── 殘餘風險
└── 對 CS Goals / Requirements 的影響
```

---

## TARA 工具

| 工具                        | 廠商               | 特色                        |
| --------------------------- | ------------------ | --------------------------- |
| **Medini Analyze**          | ANSYS              | 業界廣泛使用，含 26262 整合 |
| **PREEvision**              | Vector             | E/E 架構整合                |
| **ITEM ToolKit**            | ITEM               | TARA + FMEA                 |
| **ThreatModeler**           | ThreatModeler Inc. | 雲端、跨產業                |
| **MS Threat Modeling Tool** | Microsoft          | 免費、STRIDE                |
| **OWASP Threat Dragon**     | OWASP              | 開源                        |
| 自製 Excel                  | —                  | 小型專案常用                |

---

## TARA 在生命週期中的時機

```
Item Definition 完成 ────────→ 首次完整 TARA
                                    ↓
Architecture 變更 ─────────────→ TARA 更新（focus changed areas）
                                    ↓
Verification 發現新攻擊路徑 ────→ TARA 更新
                                    ↓
Clause 8 新威脅出現 ────────────→ TARA 更新
                                    ↓
事件發生 ─────────────────→ TARA 更新
                                    ↓
Reuse / 新車型 ────────────────→ Delta TARA
                                    ↓
EoS ───────────────────────→ TARA 凍結
```

---

## TARA 報告範本（high-level）

```yaml
tara_report:
  metadata:
    item: "TCU-2026"
    version: 3.1
    date: 2026-09-15
    performed_by: "CS Engineer Team"
    reviewed_by: "Project CS Manager"
    approved_by: "VP Engineering"

  item_reference: "Item Definition v1.5"

  step_1_assets:
    - id: A-001
      name: "TCU Firmware"
      properties: [Integrity, Authenticity]
    # ...

  step_2_threats:
    - id: TS-001
      asset: A-001
      threat: "Remote firmware tampering"
      damage_scenario: "Vehicle compromised remotely"
    # ...

  step_3_impact:
    - id: TS-001
      sfop:
        safety: Severe
        financial: Major
        operational: Severe
        privacy: Major
      overall: Severe

  step_4_attack_paths:
    - id: AP-001
      threat: TS-001
      path:
        - "Compromise OTA server"
        - "Sign malicious firmware"
        - "Push to fleet"

  step_5_feasibility:
    - id: AP-001
      elapsed_time: 13
      expertise: 6
      knowledge: 3
      window: 4
      equipment: 4
      total: 30
      rating: Low

  step_6_risk:
    - id: TS-001
      impact: Severe
      feasibility: Low
      risk_value: 3
      level: Medium

  step_7_treatment:
    - id: TS-001
      decision: Reduce
      goals_addressed: ["CG-001", "CG-005"]
      controls:
        - "Code signing"
        - "Anti-rollback"
      residual_risk: Low

  summary:
    total_threats: 47
    risk_distribution:
      very_high: 0
      high: 2
      medium: 15
      low: 30
    treatments:
      reduce: 17
      avoid: 1
      transfer: 4
      retain: 25
```

---

## TARA 的常見錯誤

> [!warning]
>
> 1. **跳過 Item Definition 直接做**：基礎不全
> 2. **Asset 識別不全**：威脅就找不到
> 3. **Damage 與 Threat 混淆**
> 4. **Impact 只考慮 Safety**：忘記 FOP
> 5. **Attack Feasibility 分數方向錯**：高分=難，低分=易
> 6. **Risk Treatment 沒文件化理由**
> 7. **不更新 TARA**：當作一次性工作

---

## 證照考點

> [!important] 高頻考點
>
> 1. **八步驟順序**（必背）
> 2. TARA 是 **Clause 15**
> 3. TARA 是**橫貫方法**，不專屬某階段
> 4. **Damage Scenario ≠ Threat Scenario**
> 5. TARA 結果驅動 **CS Goals + Concept + Requirements**
> 6. TARA 是 **Living Document**
> 7. TARA 是 CS Case 的核心證據

---

## 官方範例：Annex H（headlamp system）

> [!tip]
> ISO 21434 **Annex H** (informative) 提供完整 TARA 應用範例：「Examples of application of TARA methods – **headlamp system**」。
>
> 涵蓋從 Item Definition、Asset Identification 一路到 Risk Treatment Decision 的具體寫法，是備考時練手最佳對照範本。
> 配合 Annex F (Impact rating)、Annex G (Attack feasibility rating) 一起讀效果最佳。

---

## Related Notes

- [[12-TARA-Methods/02-Asset-Identification\|12-TARA-Methods/02-Asset-Identification]]
- [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]
- [[12-TARA-Methods/04-Impact-Rating\|12-TARA-Methods/04-Impact-Rating]]
- [[12-TARA-Methods/05-Attack-Path-Analysis\|12-TARA-Methods/05-Attack-Path-Analysis]]
- [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]
- [[12-TARA-Methods/07-Risk-Determination\|12-TARA-Methods/07-Risk-Determination]]
- [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]
- [[00-Dashboard/Quick-Reference#二、TARA 八步驟（Clause 15）\|00-Dashboard/Quick-Reference#二、TARA 八步驟（Clause 15）]]

## Practice

- [[12-TARA-Methods/Practice-TARA\|12-TARA-Methods/Practice-TARA]]

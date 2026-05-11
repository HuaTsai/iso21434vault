---
{"dg-publish":true,"permalink":"/12-tara-methods/04-impact-rating/","title":"衝擊評等 (Impact Rating)","tags":["iso-21434","concept-note","tara","impact-rating"],"dg-note-properties":{"title":"衝擊評等 (Impact Rating)","source_pdf":"內部彙整 (ISO 21434 Clause 15.5 + Annex F)","part":"Clause 15.5","keywords":["impact","sfop","safety","financial","operational","privacy"],"tags":["iso-21434","concept-note","tara","impact-rating"],"created":"2026-05-11"}}
---


## SFOP 四大衝擊類別

> [!important]
> ISO 21434 採用 **SFOP** 模型（含 4 個獨立評估面）：

| 縮寫  | 中文             | 範例                     |
| ----- | ---------------- | ------------------------ |
| **S** | Safety 安全      | 人員傷亡、實體傷害       |
| **F** | Financial 財務   | 召回、賠償、車輛價值     |
| **O** | Operational 營運 | 功能不可用、效能降級     |
| **P** | Privacy 隱私     | PII 洩漏、追蹤、商業機密 |

每個面**獨立評等**，最後取「**最嚴重的**」作為 Overall Impact。

---

## 四個等級

ISO 21434 Annex F 建議四級：

| 等級 | 英文       | 中文   | 程度                |
| ---- | ---------- | ------ | ------------------- |
| 1    | Negligible | 可忽略 | 幾乎無影響          |
| 2    | Moderate   | 中等   | 中度影響、可恢復    |
| 3    | Major      | 重大   | 嚴重影響、難恢復    |
| 4    | Severe     | 極嚴重 | 最高等級、致命/災難 |

---

## 各面向的評等準則

### Safety 安全

| 等級       | 描述                         |
| ---------- | ---------------------------- |
| Severe     | 致命傷害、生命危險           |
| Major      | 重傷（永久殘疾、需長期治療） |
| Moderate   | 輕傷、短期治療可恢復         |
| Negligible | 無人身傷害                   |

**對應 ISO 26262 嚴重度 (S0-S3)**：

```
Severe  ≈ S3
Major   ≈ S2
Moderate ≈ S1
Negligible ≈ S0
```

### Financial 財務

| 等級       | 描述                         |
| ---------- | ---------------------------- |
| Severe     | 災難性損失（公司存續威脅）   |
| Major      | 重大召回（百萬美元級）       |
| Moderate   | 顯著但可承受（單一事件處理） |
| Negligible | 微小財務影響                 |

> [!tip]
> 金額閾值由**組織自行定義**，無國際統一標準。
> 可參考公司營收 % 或絕對金額。

### Operational 營運

| 等級       | 描述                             |
| ---------- | -------------------------------- |
| Severe     | 主功能完全失效（如車輛無法啟動） |
| Major      | 重要功能失效（如導航失效）       |
| Moderate   | 次要功能失效或降級               |
| Negligible | 不影響使用                       |

### Privacy 隱私

| 等級       | 描述                          |
| ---------- | ----------------------------- |
| Severe     | 大量 PII 洩漏、可造成身分盜用 |
| Major      | 中量 PII 洩漏                 |
| Moderate   | 少量 PII、可匿名化            |
| Negligible | 無 PII 涉及                   |

---

## Overall Impact 計算

```
Overall Impact = max(S, F, O, P)
```

範例：

| 情境         | S          | F          | O          | P          | Overall      |
| ------------ | ---------- | ---------- | ---------- | ---------- | ------------ |
| 偽造煞車訊號 | Severe     | Major      | Major      | Negligible | **Severe**   |
| 韌體被反組譯 | Negligible | Moderate   | Negligible | Negligible | **Moderate** |
| GPS 位置外洩 | Negligible | Moderate   | Negligible | **Major**  | **Major**    |
| 廣告插入 UI  | Negligible | Negligible | Moderate   | Negligible | **Moderate** |

---

## 評等的客觀化挑戰

> [!warning]
> Impact 評等容易**主觀化**，需建立組織級準則：
>
> 1. **量化準則**：金額、傷害程度有明確 anchor
> 2. **跨團隊 review**：避免單人偏見
> 3. **歷史 calibration**：與業界事件對標
> 4. **保守原則**：不確定時往**較嚴重**估
> 5. **文件化理由**：每個評等需有 rationale

---

## 與 Safety HARA 的對接

```
TARA Impact - Safety 面
   ↑↓
ISO 26262 HARA 嚴重度 (S0-S3)
```

可以**共用評估**——避免重複工：

- 同一個 Damage Scenario 在兩標準下評估
- 結果應一致（若不一致 → 需協調）

---

## Impact Rating 範本

```yaml
impact_rating:
  threat_scenario_id: TS-TCU-007
  damage_scenario_id: DS-007

  ratings:
    safety:
      level: Severe
      rationale: "Mass uncommanded braking on highway could cause multiple fatal crashes"

    financial:
      level: Major
      rationale: >
        Estimated $500M+ in recall + lawsuits + brand damage
        (based on similar industry events)

    operational:
      level: Severe
      rationale: "All affected vehicles become unsafe to drive until OTA recovery"

    privacy:
      level: Major
      rationale: "Telemetry data may be exfiltrated as side-channel of attack"

  overall_impact: Severe # max of above

  cross_reference:
    iso_26262_severity: "S3 (life-threatening)"

  reviewed_by: "CS Engineer + Safety Engineer + Legal Counsel"
```

---

## 證照考點

> [!important] 高頻考點
>
> 1. **SFOP** 四大類別（背熟縮寫）
> 2. 各面**獨立評估**，最後取最高
> 3. 四個等級：Negligible / Moderate / Major / Severe
> 4. Safety 面可與 ISO 26262 對接（S0-S3）
> 5. Impact 評等需**文件化理由**
> 6. 金額閾值組織自定，無國際標準
> 7. Privacy 含**身分盜用 + 追蹤 + 商業機密**

---

## Related Notes

- [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]
- [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]
- [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]
- [[12-TARA-Methods/07-Risk-Determination\|12-TARA-Methods/07-Risk-Determination]]

## Practice

- [[12-TARA-Methods/Practice-TARA\|12-TARA-Methods/Practice-TARA]]

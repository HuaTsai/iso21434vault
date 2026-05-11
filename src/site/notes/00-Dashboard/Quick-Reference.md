---
{"dg-publish":true,"permalink":"/00-dashboard/quick-reference/","title":"ISO 21434 速查表","tags":["iso-21434","quick-ref","moc"],"dg-note-properties":{"title":"ISO 21434 速查表","type":"quick-ref","tags":["iso-21434","quick-ref","moc"],"created":"2026-05-11"}}
---


> 一頁速覽全標準。每個小節結尾以 `→ [[...]]` 指向深度筆記。

---

## 一、標準骨架 (15 個 Clauses + Annex)

| Clause    | 中文名稱                                         | 內容焦點                                 |
| --------- | ------------------------------------------------ | ---------------------------------------- |
| 1–3       | 範圍、參考、術語                                 | 定義、術語、標準範圍                     |
| 4         | General considerations                           | 通用考量、依據與目的                     |
| 5         | Organizational cybersecurity management          | **CSMS**、文化、能力、稽核               |
| 6         | Project-dependent cybersecurity management       | **CS Plan**、Tailoring、Case             |
| 7         | Distributed cybersecurity activities             | **CIA**、供應商管理                      |
| 8         | Continual cybersecurity activities               | 監控、事件評估、弱點管理                 |
| 9         | Concept                                          | Item 定義、CS Goal、CS Claim、CS Concept |
| 10        | Product development                              | 設計、整合、驗證、弱點分析               |
| 11        | Cybersecurity validation                         | **車輛層級**驗證 (含滲透測試)            |
| 12        | Production                                       | 生產資安控制、Provisioning               |
| 13        | Operations and maintenance                       | 事件回應、更新（含 OTA）                 |
| 14        | End of cybersecurity support and decommissioning | EoS、除役                                |
| 15        | Threat analysis and risk assessment methods      | **TARA 八步驟方法**                      |
| Annex A–H | 範例、CAL 表、攻擊可行性參數                     | 工具與表格                               |

→ [[01-Foundations/01-Standard-Overview\|01-Foundations/01-Standard-Overview]]

---

## 二、TARA 八步驟（Clause 15）

```
1. Asset Identification         → 資產識別
2. Threat Scenario Identification → 威脅情境識別
3. Impact Rating                → 衝擊評等 (SFOP)
4. Attack Path Analysis         → 攻擊路徑分析
5. Attack Feasibility Rating    → 攻擊可行性評等
6. Risk Value Determination     → 風險值判定
7. Risk Treatment Decision      → 風險處置決策
8. (持續監控與更新)
```

→ [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]

---

## 三、SFOP 衝擊類別

| 簡寫  | 名稱             | 範例                     |
| ----- | ---------------- | ------------------------ |
| **S** | Safety 安全      | 致命/重傷、人員受傷      |
| **F** | Financial 財務   | 召回成本、車輛價值損失   |
| **O** | Operational 營運 | 功能無法使用、效能降級   |
| **P** | Privacy 隱私     | PII 洩漏、車主行為被追蹤 |

四個等級：`Negligible → Moderate → Major → Severe`

→ [[12-TARA-Methods/04-Impact-Rating\|12-TARA-Methods/04-Impact-Rating]]

---

## 四、Attack Feasibility 五大參數（Annex G）

> 採 **Attack Potential** 方法（最常考），其他兩種方法：CVSS、Attack Vector。

| 參數                               | 0 分 (容易)   | ~ 高分 (困難)              |
| ---------------------------------- | ------------- | -------------------------- |
| **Elapsed Time** 流逝時間          | < 1 day (0)   | > 6 months (19)            |
| **Specialist Expertise** 專家能力  | Layman (0)    | Multiple Experts (8)       |
| **Knowledge of Item** 標的知識     | Public (0)    | Strictly confidential (11) |
| **Window of Opportunity** 機會窗口 | Unlimited (0) | Difficult (10)             |
| **Equipment** 設備                 | Standard (0)  | Multiple bespoke (9)       |

**總分對應**（**易混淆考點**：分數越**高** = 可行性越**低**）：

| Total Score | Attack Feasibility |
| ----------- | ------------------ |
| 0–13        | High (容易)        |
| 14–19       | Medium             |
| 20–24       | Low                |
| ≥ 25        | Very Low           |

→ [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]

---

## 五、風險值矩陣 (Risk Matrix)

```
              Attack Feasibility →
Impact ↓     Very Low   Low    Med    High
Severe         2         3      4      5
Major          1         2      3      4
Moderate       1         1      2      3
Negligible     1         1      1      2
```

風險值 1–5（或 1–25 等變體，視組織定義）。

→ [[12-TARA-Methods/07-Risk-Determination\|12-TARA-Methods/07-Risk-Determination]]

---

## 六、風險處置 4 種選項

| 選項                    | 含意                  | 範例                    |
| ----------------------- | --------------------- | ----------------------- |
| **Avoid** 避免          | 移除功能/設計變更     | 不提供遠端解鎖          |
| **Reduce** 降低         | 加入資安控制          | 加入訊息驗證 (SecOC)    |
| **Share/Transfer** 轉移 | 保險、供應商承擔      | 委由 Tier-1 處理 + 合約 |
| **Retain** 保留         | 接受殘餘風險 + 文件化 | 殘餘風險紀錄與監控      |

→ [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]

---

## 七、CAL：Cybersecurity Assurance Level（Annex E）

> CAL ≠ ASIL。CAL 是「**保證等級**」非「整合等級」，描述開發/驗證的嚴謹度。

```
CAL 推導 = f(Impact, Attack Vector)
等級：CAL 1 → CAL 2 → CAL 3 → CAL 4 (最嚴格)
```

→ [[13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level\|13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level]]

---

## 八、Cybersecurity Concept 四要素

```
Item Definition
   ↓
Cybersecurity Goals (對應 Threat Scenario)
   ↓
Cybersecurity Claims (含 Assumed-out-of-scope)
   ↓
Cybersecurity Concept (功能性 + 約束)
```

→ [[06-Concept-Phase/04-Cybersecurity-Concept\|06-Concept-Phase/04-Cybersecurity-Concept]]

---

## 九、Work Products 速記（高頻考點）

| Work Product                                | 哪個階段  | 中文            |
| ------------------------------------------- | --------- | --------------- |
| Organizational cybersecurity policies       | Clause 5  | 組織資安政策    |
| **Cybersecurity Plan**                      | Clause 6  | 資安計畫 ⭐     |
| **Cybersecurity Case**                      | Clause 6  | 資安案例 ⭐     |
| Cybersecurity Assessment Report             | Clause 6  | 資安評估報告    |
| **CIA (Cybersecurity Interface Agreement)** | Clause 7  | 資安界面協議 ⭐ |
| **TARA Report**                             | Clause 15 | TARA 報告 ⭐    |
| Cybersecurity Goals / Claims / Concept      | Clause 9  | 概念階段三件套  |
| Validation Report                           | Clause 11 | 驗證報告        |
| Incident Response Plan                      | Clause 13 | 事件回應計畫    |

⭐ = 高頻考題

→ [[03-Project-Dependent/01-Cybersecurity-Plan\|03-Project-Dependent/01-Cybersecurity-Plan]]、[[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]

---

## 十、與 UN R155 / R156 / ISO 24089 / ISO 26262 對照

| 對應主題   | ISO 21434       | UN R155            | UN R156 / ISO 24089  | ISO 26262   |
| ---------- | --------------- | ------------------ | -------------------- | ----------- |
| 管理系統   | Clause 5 (CSMS) | §7.2 CSMS          | —                    | Part 2      |
| 風險評估   | Clause 15 TARA  | Annex 5 (威脅清單) | —                    | Part 3 HARA |
| 概念設計   | Clause 9        | —                  | —                    | Part 3      |
| 產品開發   | Clause 10       | §7.3               | —                    | Part 4–6    |
| 驗證       | Clause 11       | §7.3               | —                    | Part 4      |
| 生產       | Clause 12       | —                  | —                    | Part 7      |
| 營運       | Clause 13       | §7.4               | —                    | Part 7      |
| EoS / 除役 | Clause 14       | —                  | —                    | —           |
| 軟體更新   | —（不在範圍）   | —                  | **R156 + ISO 24089** | —           |

→ [[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]、[[13-Annexes-Tools/02-Mapping-to-UN-R155\|13-Annexes-Tools/02-Mapping-to-UN-R155]]

---

## 十一、常用縮寫

| 縮寫 | 全名                                       |
| ---- | ------------------------------------------ |
| CSMS | Cybersecurity Management System            |
| CS   | Cybersecurity                              |
| CIA  | Cybersecurity Interface Agreement          |
| TARA | Threat Analysis and Risk Assessment        |
| CAL  | Cybersecurity Assurance Level              |
| SFOP | Safety / Financial / Operational / Privacy |
| OTS  | Off-the-Shelf                              |
| EoS  | End of Cybersecurity Support               |
| VAS  | Vulnerability Assessment Statement         |
| WP   | Work Product                               |
| RFQ  | Request For Quotation                      |

→ [[01-Foundations/02-Key-Terms-Definitions\|01-Foundations/02-Key-Terms-Definitions]]

---

## Related

- [[00-Dashboard/MOC\|00-Dashboard/MOC]]
- [[00-Dashboard/Exam-Traps\|00-Dashboard/Exam-Traps]]

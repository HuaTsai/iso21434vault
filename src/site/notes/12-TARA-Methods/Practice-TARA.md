---
{"dg-publish":true,"permalink":"/12-tara-methods/practice-tara/","title":"TARA 練習題","tags":["iso-21434","practice","tara"],"dg-note-properties":{"title":"TARA 練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","tara","asset","threat","impact","feasibility","risk","treatment"],"tags":["iso-21434","practice","tara"],"created":"2026-05-11"}}
---


> 涵蓋：八步驟、SFOP、Attack Feasibility、Risk Matrix、Treatment、CAL。
> **共 15 題**（高頻考點，題數較多）。

---

## Q1. (recall + 必背)

請依正確順序列出 TARA 八步驟。

> [!answer]- 解答
>
> 1. **Asset Identification** 資產識別
> 2. **Threat Scenario Identification** 威脅情境識別
> 3. **Impact Rating** 衝擊評等
> 4. **Attack Path Analysis** 攻擊路徑分析
> 5. **Attack Feasibility Rating** 攻擊可行性評等
> 6. **Risk Value Determination** 風險值判定
> 7. **Risk Treatment Decision** 風險處置決策
> 8. (持續監控與更新)
>
> 記憶：「找資產 → 想威脅 → 看後果 → 畫路徑 → 算難度 → 算風險 → 決定處置」
>
> 參考 [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]

---

## Q2. (recall + 易混淆)

下列何者**最正確**描述 SFOP？

A. Safety / Function / Operational / Performance
B. Safety / Financial / Operational / Privacy
C. Severity / Frequency / Operational / Probability
D. Spoofing / Forgery / Output / Process

> [!answer]- 解答
> **B**。**S**afety / **F**inancial / **O**perational / **P**rivacy
> 是 ISO 21434 衝擊評等的四個面向，每面獨立評估，取最高為 Overall。
> 參考 [[12-TARA-Methods/04-Impact-Rating\|12-TARA-Methods/04-Impact-Rating]]

---

## Q3. (recall + 易混淆 — **必考**)

某 Attack Path 評估，Attack Potential 各參數總分為 **30**。對應的 Attack Feasibility 等級為何？

A. Very High
B. High
C. Low
D. Very Low

> [!answer]- 解答
> **D. Very Low**。
>
> 對應表：
>
> | Total Score | Attack Feasibility |
> |---|---|
> | 0–13 | High |
> | 14–19 | Medium |
> | 20–24 | Low |
> | ≥ 25 | Very Low |
>
> **分數越高 = 攻擊越困難 = Feasibility 越低**。
> 30 分屬於 ≥ 25 區間，所以 Very Low。
>
> 這是 ISO 21434 **最容易考錯的點**——很多人直覺覺得 30 分高 = High Feasibility，**錯！**
>
> 參考 [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]、[[00-Dashboard/Exam-Traps#Trap 3\|00-Dashboard/Exam-Traps#Trap 3]]

---

## Q4. (recall)

ISO 21434 Annex G 提供的三種 Attack Feasibility 評估方法為何？

> [!answer]- 解答
>
> 1. **Attack Potential-based**（業界最常用，源自 Common Criteria）
> 2. **CVSS-based**（適用已知 CVE）
> 3. **Attack Vector-based**（簡化方法）
>
> 三選一，但**全公司一致**使用。
> 參考 [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]

---

## Q5. (application — SFOP 評估)

某威脅情境：「攻擊者透過 OBD 注入煞車 CAN 訊息，導致高速行駛失控」。請評估各 SFOP 面向。

> [!answer]- 解答
>
> ```yaml
> impact_rating:
>   safety: Severe # 高速失控可致命
>   financial: Major # 召回 + 賠償 + 品牌
>   operational: Severe # 車輛無法安全駕駛
>   privacy: Negligible # 不涉及 PII
>
>   overall: Severe # max
> ```
>
> 注意：
>
> - **Safety 為 Severe** 是主要驅動
> - **Operational 也為 Severe**（功能完全失效）
> - Privacy 可被忽略
> - Financial 嚴重但不到 Severe（除非全車隊）
>
> Overall = Severe（任一面 Severe 即 Severe）
>
> 參考 [[12-TARA-Methods/04-Impact-Rating\|12-TARA-Methods/04-Impact-Rating]]

---

## Q6. (recall + 易混淆 — **超重要**)

下列何者**正確**描述 CAL 與 ASIL 的關係？

A. CAL 4 等同 ASIL D
B. CAL 是 ISO 21434 的資安保證等級，與 ASIL（ISO 26262 功能安全完整性等級）獨立
C. CAL 包含 ASIL
D. CAL 強制使用

> [!answer]- 解答
> **B**。
>
> | 比較   | **CAL**                | **ASIL**       |
> | ------ | ---------------------- | -------------- |
> | 標準   | ISO 21434 (Annex E)    | ISO 26262      |
> | 領域   | 資安                   | 功能安全       |
> | 等級   | 1-4                    | QM, A-D        |
> | 推導   | Impact + Attack Vector | S × E × C      |
> | 強制性 | **非強制**             | 通常為標準要求 |
>
> **CAL 是 informative**（Annex E）。
> **不可**將兩者畫等號或混用。
>
> 參考 [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]、[[13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level\|13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level]]、[[00-Dashboard/Exam-Traps#Trap 2\|00-Dashboard/Exam-Traps#Trap 2]]

---

## Q7. (recall)

ISO 21434 風險處置的四大選項為何？

> [!answer]- 解答
>
> **Avoid（避免）** / **Reduce（降低）** / **Share or Transfer（轉移）** / **Retain（保留 / 接受）**
>
> | 選項           | 適用                                        |
> | -------------- | ------------------------------------------- |
> | Avoid          | 移除功能/設計變更                           |
> | Reduce         | 加入資安控制（最常見）                      |
> | Share/Transfer | 給供應商/保險（需驗證對方）                 |
> | Retain         | 接受作為殘餘風險（需文件化 + 適當層級簽核） |
>
> 參考 [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]

---

## Q8. (application)

某 Threat Scenario 的 Risk Value 為 5 (Very High)，但開發團隊認為「修補成本過高」，建議直接 Retain。請評論。

> [!answer]- 解答
>
> **錯誤**——Risk Value 5 通常**不可直接 Retain**。
>
> **問題**：
>
> 1. 組織政策通常禁止 Retain Very High Risk
> 2. 「修補成本過高」**不是充分理由**
> 3. 即使要 Retain，需 VP/CTO 層級接受（不是開發團隊）
> 4. Cybersecurity Assessment 會拒絕
> 5. **不可 Release** 至 Post-Development
>
> **正確做法**：
>
> 1. 嘗試 **Reduce**：加入資安控制降低 feasibility 或 impact
> 2. 若 Reduce 不可行，考慮 **Avoid**：移除功能
> 3. 若仍要 Retain（極少數情況）：
>    - 詳細風險評估
>    - 補償措施（如監控、限制使用情境）
>    - 高層級書面接受（CTO 或更高）
>    - 完整文件化於 CS Case
>    - 持續監控觸發升級條件
>
> **不可**：
>
> - 為趕進度 Retain
> - 由 Project Manager 私自接受
>
> 參考 [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]、[[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]

---

## Q9. (recall + 易混淆 — 必考)

下列何者**正確**描述 Damage Scenario 與 Threat Scenario？

A. 兩者是同義詞
B. Damage Scenario 描述攻擊步驟；Threat Scenario 描述後果
C. Damage Scenario 描述對 road user 的不利後果；Threat Scenario 描述如何達成這個後果
D. Threat Scenario 必須來自 Annex 5

> [!answer]- 解答
> **C**。
>
> ```
> Damage Scenario：「車輛在高速公路失控撞擊」（後果）
>          ↑
>          │ 由以下手段達成
>          │
> Threat Scenario：「攻擊者透過 OBD 注入偽煞車 CAN 訊息」（過程）
> ```
>
> 參考 [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]、[[00-Dashboard/Exam-Traps#Trap 12\|00-Dashboard/Exam-Traps#Trap 12]]

---

## Q10. (application — Attack Potential 計算)

依下列參數計算 Attack Potential 總分與 Feasibility：

- Elapsed Time：< 1 day (0)
- Specialist Expertise：Proficient (3)
- Knowledge of Item：Restricted (3)
- Window of Opportunity：Easy (1)
- Equipment：Specialized (4)

> [!answer]- 解答
>
> **總分 = 0 + 3 + 3 + 1 + 4 = 11**
>
> 對應 Feasibility：
>
> - 0-13 → **High** (容易)
>
> **結論：Attack Feasibility = High**
>
> 此情境可能是「使用商業 CAN tool 從 OBD 注入偽 CAN 訊息」——熟手在數小時內就能完成。
>
> 參考 [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]

---

## Q11. (application — Risk Matrix)

依下列計算最終 Risk Value：

- Impact: Major
- Attack Feasibility: Medium

> [!answer]- 解答
>
> 對照矩陣：
>
> ```
>                Very Low  Low    Medium   High
> Severe         2         3      4        5
> Major          1         2      3        4
> Moderate       1         1      2        3
> Negligible     1         1      1        2
> ```
>
> Major × Medium = **3**
>
> **Risk Value = 3 (Medium)**
>
> 此風險通常需評估後決定處置（不一定要 Reduce，但需文件化）。
>
> 參考 [[12-TARA-Methods/07-Risk-Determination\|12-TARA-Methods/07-Risk-Determination]]

---

## Q12. (analysis)

請說明為什麼一個 Threat Scenario 的 Attack Feasibility 應採用「**最容易**」的那條 Attack Path，而不是平均或最難的那條。

> [!answer]- 解答
>
> **理由：保守原則 + 攻擊者選擇權**
>
> 1. **攻擊者選擇權**：
>    - 攻擊者**不會選最難的路**
>    - 一定會選成本最低、最快、最容易的路
>    - 評估「最容易」反映**真實攻擊情境**
> 2. **保守原則**：
>    - 低估容易度 → 低估風險 → 防護不足
>    - 高估容易度 → 過度防護（成本高但不致命）
>    - 兩權相害取其輕：寧可過度防護
> 3. **多路徑時**：
>    - 識別所有路徑
>    - 評估每條的 feasibility
>    - 取 **max(feasibility)** = 最容易那條
> 4. **防禦含意**：
>    - 想降低風險 → 必須降低「最容易那條」的 feasibility
>    - 若多條都同樣容易 → 需多管齊下
> 5. **與 Risk Treatment 連動**：
>    - 處置後若該路徑被堵住，第二容易的路徑成為新的「最容易」
>    - 需重評
>
> 參考 [[12-TARA-Methods/05-Attack-Path-Analysis\|12-TARA-Methods/05-Attack-Path-Analysis]]、[[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]

---

## Q13. (application — 整合題)

某 OEM 開發 TCU 時識別出威脅情境：「攻擊者透過 Cellular MITM 取得車輛位置即時資料」。請完整執行 TARA Step 3-7 的決策。

> [!answer]- 解答
>
> **Step 3：Impact Rating (SFOP)**
>
> ```
> Safety: Negligible (不直接影響行車安全)
> Financial: Moderate (品牌損害、客戶流失)
> Operational: Negligible (功能仍可用)
> Privacy: Major (位置追蹤、跟監風險)
> → Overall: Major
> ```
>
> **Step 4：Attack Path Analysis**
>
> ```
> 路徑 A：Rogue base station + 沒有 TLS
>   - 不適用（已有 TLS 1.3）
> 路徑 B：TLS Cert validation bypass
>   - 需找 CA 或實作弱點
> 路徑 C：Hijack DNS + cert pinning bypass
>   - 需 device 無 cert pinning
> 路徑 D：Compromise OEM CA
>   - 極困難
> ```
>
> **Step 5：Feasibility (路徑 B 為例)**
>
> ```
> Time: 4 (< 1 month)
> Expertise: 6 (Expert)
> Knowledge: 3 (Restricted)
> Window: 4 (Moderate)
> Equipment: 4 (Specialized)
> Total: 21 → Low Feasibility
> ```
>
> **Step 6：Risk Determination**
>
> ```
> Impact: Major × Feasibility: Low
> Risk Value: 2 (Low)
> ```
>
> **Step 7：Risk Treatment**
>
> ```
> Risk Value 2 通常可 Retain，但 Privacy Major 需謹慎：
>
> 決策：Reduce (額外控制)
>   • 已實作：TLS 1.3 + Cert pinning + Per-device cert (mTLS)
>   • 補強：Perfect Forward Secrecy、 連線異常通報
>   • Privacy 額外：位置資料加密 at rest、最小化收集、匿名化
>
> 接受者：CS Manager + Privacy Officer
> 殘餘風險：1 (Very Low) — 接受
> 持續監控：TLS 弱點 CVE 追蹤、加密演算法演進
> ```
>
> 對應 CS Goal：
>
> - **CG-XXX**：車輛位置資料的機密性應被保護免於蜂巢通訊中的中間人攻擊。
>
> 參考所有 [[12-TARA-Methods/02-Asset-Identification\|12-TARA-Methods/02-Asset-Identification]] 至 [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]

---

## Q14. (recall)

CAL 由哪兩個因素推導？

A. Impact + Attack Feasibility
B. Impact + Attack Vector
C. S × E × C
D. CVSS Score

> [!answer]- 解答
> **B**。
> CAL（Annex E）由 **Impact** 與 **Attack Vector** 推導。
> 注意：是 Attack Vector（網路/實體等向量），**不是** Attack Feasibility。
>
> 參考 [[13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level\|13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level]]

---

## Q15. (analysis + 跨章節)

請說明 TARA 結果如何驅動下游所有 Cybersecurity 活動。

> [!answer]- 解答
>
> ```
> TARA Step 1-2: Assets + Threats
>    ↓
>    → 識別需保護的 Asset/Property
>
> TARA Step 3: Impact
>    ↓
>    → 決定 SFOP 衝擊
>    → 影響 CAL 推導
>    → 影響後續 Validation 嚴格度
>
> TARA Step 4-5: Attack Path + Feasibility
>    ↓
>    → 識別攻擊面
>    → 影響架構設計（Trust Boundary）
>    → 影響 Pen Test 範圍
>
> TARA Step 6: Risk Value
>    ↓
>    → 排序處置優先級
>    → 影響資源分配
>
> TARA Step 7: Treatment Decision
>    ↓
>    → 產生 Cybersecurity Goals（Reduce / Avoid 情境）
>    → 產生 Cybersecurity Claims（Transfer / Out-of-scope 情境）
>    → 接受的 Retain → 殘餘風險紀錄
>
> Cybersecurity Goals
>    ↓
>    → Cybersecurity Concept（如何達成）
>    → Cybersecurity Requirements（可實作）
>    → Architecture Design
>    → Implementation
>    → Verification（驗證 Requirements）
>    → Validation（驗證 Goals 在車輛級達成）
>    → Cybersecurity Case（論證 Goals 達成）
>    → Assessment（評估 Case 是否成立）
>    → Release for Post-Development
>
> Post-Development：
>    → Production Controls
>    → Operations + Incident Response
>    → Updates + Vulnerability Management
>    → EoS + Decommissioning
>
> 同時 Clause 8 Continual Monitoring：
>    → 觸發 TARA 重新評估（閉環）
> ```
>
> **核心啟示**：TARA 是「**車輛資安整體生命週期**」的引擎。錯誤的 TARA → 後續所有活動都受影響。
>
> 因此 TARA **必須**：
>
> - 完整（不遺漏 Asset / Threat）
> - 準確（評等正確）
> - 持續更新（隨情境變化）
> - 文件化（可追溯）
>
> 參考 [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]、[[01-Foundations/04-Lifecycle-Overview\|01-Foundations/04-Lifecycle-Overview]]

---

## Related Concepts

- [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]
- [[12-TARA-Methods/02-Asset-Identification\|12-TARA-Methods/02-Asset-Identification]]
- [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]
- [[12-TARA-Methods/04-Impact-Rating\|12-TARA-Methods/04-Impact-Rating]]
- [[12-TARA-Methods/05-Attack-Path-Analysis\|12-TARA-Methods/05-Attack-Path-Analysis]]
- [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]
- [[12-TARA-Methods/07-Risk-Determination\|12-TARA-Methods/07-Risk-Determination]]
- [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]

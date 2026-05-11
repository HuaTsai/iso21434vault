---
{"dg-publish":true,"permalink":"/01-foundations/02-key-terms-definitions/","title":"關鍵術語與定義 (Clause 3)","tags":["iso-21434","concept-note","foundations","terminology"],"dg-note-properties":{"title":"關鍵術語與定義 (Clause 3)","source_pdf":"內部彙整 (ISO/SAE 21434:2021 Clause 3)","part":"Clause 3","keywords":["terms","definitions","vocabulary"],"tags":["iso-21434","concept-note","foundations","terminology"],"created":"2026-05-11"}}
---


> ISO 21434 的 Clause 3 是**規範性術語**，與 ISO 26262 Part 1 同等重要。
> 考試會直接測「下列哪個定義最符合 ISO 21434 對 XXX 的定義」。

---

## 1. 核心：資安 (Cybersecurity)

> [!quote] 定義
> **Cybersecurity**: condition in which assets are sufficiently protected against threat scenarios to items of road vehicles, their functions and their electrical or electronic components.

關鍵字：

- **assets**：被保護對象
- **sufficient**：相對概念（依風險決定）
- **threat scenarios**：威脅情境
- **items / functions / E/E components**：範圍三層

---

## 2. Asset（資產）

> [!quote] 定義
> object that has value, or contributes to value.

**特徵**：

- 可以是 **資料**（韌體、金鑰、PII）、**功能**（煞車控制）、**通訊**（CAN 訊號）。
- 評估其 **資安屬性 (cybersecurity properties)**：CIA + Authenticity + Non-repudiation + Authorization。

---

## 3. 威脅情境 (Threat Scenario)

> [!quote] 定義
> potential cause of compromise of cybersecurity properties of one or more assets in order to realize a damage scenario.

**結構**：

```
Threat Scenario = (Asset + 破壞屬性) + 達成方式
```

→ 對應 [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]

---

## 4. Damage Scenario（損害情境）

> [!quote] 定義
> adverse consequence involving a vehicle or vehicle function and affecting a road user.

**關鍵**：站在 **road user (道路使用者)** 角度描述「不希望發生的後果」。

- 例：「煞車失靈導致車輛撞擊」是 Damage Scenario。
- 例：「攻擊者注入偽造煞車 CAN 訊號」是 Threat Scenario（不是 Damage）。

> [!warning] 易混淆陷阱
> **Damage = 結果；Threat = 過程**。命題單位最愛測這個。

---

## 5. Item（標的）

> [!quote] 定義
> component or set of components that implements a function at the vehicle level, to which ISO 21434 is applied.

**重點**：

- 與 ISO 26262 的 Item **概念相同**，但獨立評估。
- 通常是「車輛級可辨識的功能單元」：TCU、ADAS 控制器、Gateway。

---

## 6. Component（元件）

> [!quote] 定義
> part that is logically and technically separable.

階層：

```
Vehicle → Item → System → Component → HW/SW Unit
```

---

## 7. CSMS — Cybersecurity Management System

> [!quote] 定義
> systematic risk-based approach defining organizational processes, responsibilities and governance to treat risk associated with cyber threats.

**關鍵字**：

- **systematic** + **risk-based**
- 組織級而非專案級

→ [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]

---

## 8. Cybersecurity Case

> [!quote] 定義
> structured argument, supported by evidence, providing a compelling, comprehensible and valid case that cybersecurity goals are satisfied.

**結構三要素**：

1. **Structured argument**：論證邏輯
2. **Evidence**：證據（測試、TARA、Review）
3. **Claim**：要證明的事（資安目標達成）

→ [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]

---

## 9. Cybersecurity Goal

> [!quote] 定義
> concept-level cybersecurity requirement associated with one or more threat scenarios.

**特徵**：

- **概念層級**（high-level）
- 對應 **威脅情境**
- 表達為「資安屬性的保護目標」

→ [[06-Concept-Phase/02-Cybersecurity-Goals\|06-Concept-Phase/02-Cybersecurity-Goals]]

---

## 10. Cybersecurity Claim

> [!quote] 定義
> statement specifying the cybersecurity-related assumption or sharing of risk.

**用途**：當你**不在 item 範圍內**處理某風險時，明確聲明：

- 「這個風險假設由 OEM 處理（不是 Tier-1）」
- 「這個風險由使用者承擔（如 OBD 物理保護）」

→ [[06-Concept-Phase/03-Cybersecurity-Claims\|06-Concept-Phase/03-Cybersecurity-Claims]]

---

## 11. CIA — Cybersecurity Interface Agreement

> [!quote] 定義
> agreement between customer and supplier specifying the cybersecurity-related interactions, responsibilities and work products.

**內容必包含**：

- 雙方角色 (RASIC)
- 共享 Work Product
- 介面點（哪些活動需要哪一方參與）
- 變更管理

→ [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]

---

## 12. TARA — Threat Analysis and Risk Assessment

> [!quote] 定義
> systematic approach to identify and assess cybersecurity-related risks.

**八步驟**：見 [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]

---

## 13. CAL — Cybersecurity Assurance Level

> [!quote] 定義
> level that specifies rigor of cybersecurity activities and provides assurance that residual cybersecurity risk is acceptable.

**等級**：CAL 1 ~ CAL 4（4 最嚴格）
**屬性**：**informative**（Annex E）

→ [[13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level\|13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level]]

---

## 14. Attack Path / Attack Feasibility

| 術語                   | 定義                                                                          |
| ---------------------- | ----------------------------------------------------------------------------- |
| **Attack Path**        | sequence of deliberate actions to realize a threat scenario                   |
| **Attack Feasibility** | attribute that describes the ease of successfully carrying out an attack path |

→ [[12-TARA-Methods/05-Attack-Path-Analysis\|12-TARA-Methods/05-Attack-Path-Analysis]]、[[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]

---

## 15. Vulnerability / Weakness

| 術語              | 定義                                                                | 差別                           |
| ----------------- | ------------------------------------------------------------------- | ------------------------------ |
| **Weakness**      | flaw, defect or pre-condition that can develop into a vulnerability | **潛在**問題（尚未確認可利用） |
| **Vulnerability** | weakness that **can be exploited** as part of an attack path        | **可利用**的弱點               |

> [!warning] 易混淆
> Weakness ⊃ Vulnerability。所有 Vulnerability 都是 Weakness，但反之不必然。

→ [[05-Continual-Cybersecurity/03-Vulnerability-Analysis\|05-Continual-Cybersecurity/03-Vulnerability-Analysis]]

---

## 16. Cybersecurity Incident vs. Event

| 術語                       | 定義                                                                              |
| -------------------------- | --------------------------------------------------------------------------------- |
| **Cybersecurity Event**    | identifiable occurrence in a system that has potential cybersecurity implications |
| **Cybersecurity Incident** | event that affects the cybersecurity of an item or component                      |

**關係**：Event 是廣義發生；經過評估後若確認影響資安，升級為 Incident。

→ [[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]

---

## 17. Item Definition / Operational Environment

| 術語                        | 重點                                      |
| --------------------------- | ----------------------------------------- |
| **Item Definition**         | 描述 item 的範圍、邊界、功能、介面、依賴  |
| **Operational Environment** | item 運行的環境條件（含實體、邏輯、時間） |

→ [[06-Concept-Phase/01-Item-Definition\|06-Concept-Phase/01-Item-Definition]]

---

## 18. Residual Risk（殘餘風險）

> [!quote] 定義
> remaining cybersecurity risk after risk treatment.

- 必須被**明確接受 (accepted)** 並文件化。
- 接受人需有適當權責層級。
- 構成 Cybersecurity Case 的一部分。

→ [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]

---

## 19. EoS — End of Cybersecurity Support

> [!quote] 定義
> point in time after which cybersecurity support for a product is no longer provided.

關鍵：

- 必須**事先**通知相關方（如車主、OEM）。
- 不等於車輛除役；EoS 後車輛仍可運作但**不再修補弱點**。

→ [[11-EndOfSupport-Decommission/01-End-of-Support\|11-EndOfSupport-Decommission/01-End-of-Support]]

---

## 20. Decommissioning（除役）

> [!quote] 定義
> permanent retirement of a cybersecurity-relevant component or item.

特徵：

- 含**資料清除**（金鑰、PII、訓練資料）。
- 含**憑證撤銷** (V2X PKI)。
- 不可逆。

→ [[11-EndOfSupport-Decommission/02-Decommissioning\|11-EndOfSupport-Decommission/02-Decommissioning]]

---

## 速記表

| 縮寫    | 全名                                                                           | 中文               |
| ------- | ------------------------------------------------------------------------------ | ------------------ |
| CSMS    | Cybersecurity Management System                                                | 資安管理系統       |
| CS      | Cybersecurity                                                                  | 資安               |
| CIA     | Cybersecurity Interface Agreement                                              | 資安界面協議       |
| CIA-AAA | Confidentiality/Integrity/Availability/Authenticity/Authorization/Auditability | 資安屬性           |
| TARA    | Threat Analysis and Risk Assessment                                            | 威脅分析與風險評估 |
| CAL     | Cybersecurity Assurance Level                                                  | 資安保證等級       |
| SFOP    | Safety / Financial / Operational / Privacy                                     | 衝擊類別           |
| OTS     | Off-The-Shelf                                                                  | 既有元件           |
| RFQ     | Request For Quotation                                                          | 詢價單             |
| WP      | Work Product                                                                   | 工作產物           |
| EoS     | End of Cybersecurity Support                                                   | 終止資安支援       |
| RASIC   | Responsible/Accountable/Supporting/Informed/Consulted                          | 角色矩陣           |

---

## Related Notes

- [[01-Foundations/01-Standard-Overview\|01-Foundations/01-Standard-Overview]]
- [[01-Foundations/03-Cybersecurity-vs-Safety\|01-Foundations/03-Cybersecurity-vs-Safety]]
- [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]

## Practice

- [[01-Foundations/Practice-Foundations\|01-Foundations/Practice-Foundations]]

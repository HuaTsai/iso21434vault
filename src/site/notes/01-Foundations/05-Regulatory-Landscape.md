---
{"dg-publish":true,"permalink":"/01-foundations/05-regulatory-landscape/","title":"法規地景：UN R155 / R156 / WP.29","tags":["iso-21434","concept-note","foundations","un-r155","un-r156"],"dg-note-properties":{"title":"法規地景：UN R155 / R156 / WP.29","source_pdf":"內部彙整 (UNECE WP.29 + ISO 21434 對應)","part":"外部法規對應","keywords":["un-r155","un-r156","wp29","regulation","type-approval"],"tags":["iso-21434","concept-note","foundations","un-r155","un-r156"],"created":"2026-05-11"}}
---


> ISO 21434 是**技術標準**，UN R155/R156 是**法規**。
> 兩者關係：21434 是 R155 合規最常被接受的**技術依據**。

---

## UNECE WP.29 框架

```
UNECE (United Nations Economic Commission for Europe)
   └── WP.29 (World Forum for Harmonization of Vehicle Regulations)
            ├── GRVA (Automated/Autonomous & Connected Vehicles)
            │      └── 制定 R155, R156, R157 (ALKS)
            └── 各國採用（EU、日本、韓國、英國...）
```

**重要時間點**：

- 2020-06：WP.29 通過 R155 與 R156。
- 2022-07：**EU 全新車型**強制 R155 + R156。
- 2024-07：**所有新生產車輛**（含既有車型）強制 R155 + R156。

> [!warning]
> **美國、加拿大、中國不直接適用** UN R155，但有類似法規（如中國 GB/T、美國 NHTSA 指引）。

---

## UN R155：CSMS 與車型資安認證

### 法規結構

```
UN R155 (官方目次)
├── Section 5：Approval（車型認證）
├── Section 6：Certificate of Compliance for CSMS（CSMS 證書）
├── Section 7：Specifications（核心要求）
│     ├── 7.2 CSMS 要求（OEM 流程）
│     └── 7.3 Vehicle type 要求（車型資安）
├── Annex 1：Information document（型認申報資料）
├── Annex 2：Communication（核發/拒發通知）
├── Annex 3：Arrangement of approval mark（認證標誌格式）
├── Annex 4：Model of Certificate of Compliance for CSMS（CSMS 證書範本）
└── Annex 5：List of threats and corresponding mitigations（威脅與緩解 ⭐ 高頻考點）
```

> [!note]
> 核心**要求**寫在 **Section 6/7**，Annex 多為**範本/通訊格式/威脅清單**。
> 常見誤解：把「CSMS 認證要求」當成 Annex 1，實際在 §7.2。

### 兩種認證

| 認證類型                  | 對象     | 內容                    |
| ------------------------- | -------- | ----------------------- |
| **CSMS Certification**    | OEM 整體 | 一次性、有效期 **3 年** |
| **Vehicle Type Approval** | 每款車型 | 每款新車需個別認證      |

### 與 ISO 21434 對應

| UN R155 要求       | ISO 21434 對應             |
| ------------------ | -------------------------- |
| §7.2 CSMS 流程建立 | **Clause 5** CSMS          |
| §7.2 風險評估      | **Clause 15** TARA         |
| §7.3 開發階段資安  | **Clause 9-11**            |
| §7.3 供應商管理    | **Clause 7** Distributed   |
| §7.3 滲透測試      | **Clause 11** Validation   |
| §7.4 後生產階段    | **Clause 13** Ops & Maint  |
| Annex 5 威脅清單   | TARA Threat Scenarios 參考 |

> [!important]
> **常見考點**：UN R155 **不要求**特定技術或工具，只要求「有 CSMS + 能管理風險」。ISO 21434 是最被廣泛接受的**證明方式**。

---

## UN R155 Annex 5 威脅清單（重點）

七大類威脅（共 69 條）：

| 類別 | 主題                      | 範例                 |
| ---- | ------------------------- | -------------------- |
| 1    | Back-end servers          | OEM 雲端被入侵       |
| 2    | Communication channels    | 車-雲、V2X 攔截/竄改 |
| 3    | Update procedures         | 偽造 OTA 韌體        |
| 4    | Unintended human actions  | 員工誤操作、社交工程 |
| 5    | External connectivity     | OBD、USB、Wi-Fi 攻擊 |
| 6    | Vehicle data/code         | 韌體萃取、私鑰提取   |
| 7    | Potential vulnerabilities | 未修補弱點           |

每條威脅對應一組**緩解措施 (mitigations)**。TARA 結果應**對應**這些威脅或說明為何不適用。

---

## UN R156：軟體更新與 SUMS

### 法規結構

```
UN R156 (官方目次)
├── Section 5：Approval（車型認證）
├── Section 6：Certificate of Compliance for SUMS（SUMS 證書）
├── Section 7：Specifications
│     ├── 7.1 SUMS 要求（OEM 軟體更新管理流程）
│     └── 7.2 Vehicle type 要求（軟體更新的型認）
├── Annex 1：Information document
├── Annex 2：Communication
├── Annex 3：Arrangement of approval mark
└── Annex 4：Model of Certificate of Compliance for SUMS
```

> [!note]
> 與 R155 一致：核心**要求**在 **Section 6/7**，Annex 為**範本/通訊格式**。

### 核心概念：**SUMS** (Software Update Management System)

```
SUMS 要求
├── 識別所有可更新的車輛軟體
├── 軟體版本對應車輛狀態
├── 變更影響評估（safety + security + type approval）
├── 更新前後的合規維持
└── 使用者通知（重要更新）
```

### OTA 更新需處理

1. 更新**真實性與完整性**（簽章驗證）
2. 更新**過程**中車輛狀態（不可在駕駛中關鍵更新）
3. 更新**失敗回滾**
4. 更新**前**取得使用者同意（特定情況）
5. 更新**後**驗證車輛功能

> [!warning]
> **R156 不是 R155 的子集**！兩者**並列**：
>
> - R155：整體 CSMS（含資安）
> - R156：軟體更新管理（不限資安，也含功能更新合規）

---

## 對比表

| 比較項         | **UN R155**     | **UN R156**                              |
| -------------- | --------------- | ---------------------------------------- |
| 主題           | CSMS + 車型資安 | 軟體更新管理 (SUMS)                      |
| 認證對象       | OEM CSMS + 車型 | OEM SUMS + 車型                          |
| 有效期         | 3 年（CSMS）    | 3 年（SUMS）                             |
| 觸發 ISO 21434 | **強相關**      | 部分相關（OTA 安全）                     |
| 觸發 ISO 24089 | —               | **強相關**（ISO 24089 是 R156 技術依據） |

---

## ISO 24089：軟體更新的 21434 兄弟

```
ISO/SAE 21434 ←→ UN R155
ISO 24089     ←→ UN R156
```

**ISO 24089:2023** Road vehicles — Software update engineering

- 與 21434 相同的結構（V-Model、CSMS-like 管理系統）。
- 專注**軟體更新**全週期。
- 21434 與 24089 共享部分 WP（CS Case 可含更新議題）。

---

## 其他相關法規/標準

| 標準/法規                       | 領域               | 與 21434 關係                         |
| ------------------------------- | ------------------ | ------------------------------------- |
| ISO 26262                       | 功能安全           | 並列、共享 Item                       |
| ISO 21448 (SOTIF)               | 預期功能安全       | 並列、有重疊（攻擊導致 SOTIF 議題）   |
| IEC 62443                       | 工控資安           | 21434 借鑑來源                        |
| ISO/IEC 27001                   | 資訊安全管理       | 互補（IT vs OT）                      |
| NIST SP 800-30                  | 風險評估           | 方法論來源                            |
| Common Criteria (ISO/IEC 15408) | 評估準則           | 21434 Annex G (Attack Potential) 參考 |
| Auto-ISAC Best Practices        | 業界共識           | 21434 文化參考                        |
| TISAX                           | 汽車供應鏈資訊安全 | 互補（企業 IT 面）                    |
| UN R157 (ALKS)                  | 自駕系統           | 並列                                  |

---

## 證照考試重點

> [!important] 高頻考點
>
> 1. R155 強制日期（**2022-07** 新車型 / **2024-07** 所有新車）
> 2. R155 與 R156 的**並列**關係（不是包含）
> 3. CSMS 認證**有效期 3 年**
> 4. ISO 21434 與 R155 的**對應關係**（不是法律強制，但是事實標準）
> 5. Annex 5 七大威脅類別
> 6. 認證類型：CSMS（公司層級）+ Type Approval（車型層級）

---

## Related Notes

- [[01-Foundations/01-Standard-Overview\|01-Foundations/01-Standard-Overview]]
- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]
- [[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]
- [[13-Annexes-Tools/02-Mapping-to-UN-R155\|13-Annexes-Tools/02-Mapping-to-UN-R155]]

## Practice

- [[01-Foundations/Practice-Foundations\|01-Foundations/Practice-Foundations]]

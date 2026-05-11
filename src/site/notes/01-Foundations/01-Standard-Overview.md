---
{"dg-publish":true,"permalink":"/01-foundations/01-standard-overview/","title":"ISO/SAE 21434 標準總覽","tags":["iso-21434","concept-note","foundations"],"dg-note-properties":{"title":"ISO/SAE 21434 標準總覽","source_pdf":"內部彙整 (ISO/SAE 21434:2021)","part":"Clause 1-4 + 全標準骨架","keywords":["iso-21434","overview","scope","lifecycle","csms"],"tags":["iso-21434","concept-note","foundations"],"created":"2026-05-11"}}
---


## 標準身分

| 項目 | 內容                                                                        |
| ---- | --------------------------------------------------------------------------- |
| 全名 | **ISO/SAE 21434:2021 — Road vehicles — Cybersecurity engineering**          |
| 發行 | 2021 年 8 月（ISO 與 SAE 聯合制定）                                         |
| 取代 | SAE J3061（指引性質）→ 21434 為**正式國際標準**                             |
| 範圍 | **電/電子 (E/E)** 系統的道路車輛資安工程                                    |
| 不含 | 純機械、車載娛樂內容、車隊管理 IT 雲端                                      |
| 關係 | 與 ISO 26262（功能安全）、UN R155（CSMS 法規）、UN R156（軟體更新）緊密相關 |

> [!important]
> ISO 21434 **不規範具體技術**（如要用 AES-256），而是規範**流程與工程方法**。

---

## 標準骨架

```
+--- Clause 1-3：範圍、規範性參考、術語
|
+--- Clause 4：一般性考量（context、cybersecurity engineering 的依據）
|
+--- Clause 5：組織層級 CS 管理（CSMS）          ┐
+--- Clause 6：專案層級 CS 管理                   │ 管理面
+--- Clause 7：分散式 CS 活動 (Distributed)        │
+--- Clause 8：持續性 CS 活動 (Continual)           ┘
|
+--- Clause 9：Concept 概念階段                   ┐
+--- Clause 10：Product Development 產品開發        │ 工程
+--- Clause 11：Cybersecurity Validation 驗證       │ 生命
+--- Clause 12：Production 生產                     │ 週期
+--- Clause 13：Operations and Maintenance 營運     │
+--- Clause 14：End of Support / Decommissioning   ┘
|
+--- Clause 15：TARA 方法（橫向方法論）
|
+--- Annex A-H：範例、CAL 表、攻擊可行性參數、Mapping
```

---

## 三個層次的活動

```
┌──────────────────────────────────────────┐
│ 組織層級 (Organizational)  ← Clause 5     │
│  CSMS、政策、能力、文化、稽核              │
├──────────────────────────────────────────┤
│ 專案層級 (Project)         ← Clause 6     │
│  CS Plan、Tailoring、Case、Assessment     │
├──────────────────────────────────────────┤
│ 跨組織協作 (Distributed)   ← Clause 7     │
│  CIA、供應商管理、能力評估                 │
└──────────────────────────────────────────┘

橫貫所有層級：
   Clause 8 (Continual)：監控、事件、弱點管理
   Clause 15 (TARA)：威脅分析方法
```

---

## 工程生命週期 (V-Model 視角)

```
                       Concept (9)
                          │
                 ┌────────┴────────┐
                 ↓                 ↑
        Product Dev (10)    CS Validation (11)
                 │                 ↑
                 └─→ Verification ─┘
                          │
                       Production (12)
                          │
                       Operations & Maintenance (13)
                          │
                       End of Support (14)
                          │
                       Decommissioning (14)
```

> [!tip]
> ISO 21434 的 V-Model 與 ISO 26262 對應，但**獨立進行**——資安工程與功能安全工程**並行**，於介面點交互（共享 Item 定義、共享部分 WP）。

---

## 標準的根本精神

ISO 21434 圍繞三個核心理念：

1. **Risk-based**：所有活動以風險（TARA 結果）驅動。
2. **Lifecycle-wide**：從概念到除役全週期。
3. **Distributed**：承認車輛由多方協作開發，需明確界面。

---

## 與其他標準的關係

| 標準                  | 關係類型         | 接點                                 |
| --------------------- | ---------------- | ------------------------------------ |
| **ISO 26262**         | 並列（功能安全） | 共享 Item 定義；安全 vs 資安互相影響 |
| **ISO 21448 (SOTIF)** | 並列             | 與資安在「非預期行為」上重疊         |
| **UN R155**           | 法規對應         | 21434 是 R155 合規的事實技術依據     |
| **UN R156**           | 法規對應         | 軟體更新（OTA）流程                  |
| **IEC 62443**         | 借鑑來源         | 工業控制資安方法的車用化             |
| **ISO/IEC 27001**     | 互補             | 21434 偏產品、27001 偏 IT            |

---

## 強制性說明

> [!warning]
> ISO 21434 條文用詞**嚴格分級**：
>
> - **shall**：強制要求（不做就不合規）
> - **should**：建議（可不做但需理由）
> - **may**：允許（自由選擇）
> - **can**：能力陳述（描述可能性，非要求）
>
> Annex 多為 **informative**（資訊性），如 CAL、TARA 具體分數表。
> Clause 5–15 主體多為 **normative**（規範性）。

---

## 證照考點重點

考題常測：

1. **Clause 編號 ↔ 主題**（背骨架）
2. **Work Product** 是哪個 Clause 產出
3. **TARA 八步驟**順序
4. **WP 與其他 Clause 的依賴**（如 CIA 影響哪些活動）
5. **CAL** 與 ASIL 區別
6. 條文用詞（shall vs should）

---

## Related Notes

- [[01-Foundations/02-Key-Terms-Definitions\|01-Foundations/02-Key-Terms-Definitions]]
- [[01-Foundations/03-Cybersecurity-vs-Safety\|01-Foundations/03-Cybersecurity-vs-Safety]]
- [[01-Foundations/04-Lifecycle-Overview\|01-Foundations/04-Lifecycle-Overview]]
- [[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]
- [[00-Dashboard/Quick-Reference\|00-Dashboard/Quick-Reference]]

## Practice

- [[01-Foundations/Practice-Foundations\|01-Foundations/Practice-Foundations]]

---
{"dg-publish":true,"permalink":"/readme/","title":"ISO/SAE 21434:2021 證照學習 Vault","tags":["gardenEntry"],"dg-note-properties":{"title":"ISO/SAE 21434:2021 證照學習 Vault","created":"2026-05-11"}}
---


# ISO/SAE 21434:2021 證照學習筆記

> **Road vehicles — Cybersecurity engineering** 證照準備完整筆記。
> 涵蓋 Clause 4-15 + Annex + TARA + 練習題 + 模擬試題。

---

## 從這裡開始

1. **[[00-Dashboard/MOC\|學習地圖 (MOC)]]** — 完整章節索引與學習路徑
2. **[[00-Dashboard/Quick-Reference\|速查表]]** — 一頁速覽全標準
3. **[[00-Dashboard/Exam-Traps\|考試陷阱]]** — 15 個易混淆觀念
4. **[[00-Dashboard/Weak-Areas\|個人弱點區]]** — 動態紀錄錯題

---

## 章節結構

| 編號     | 主題                          | 對應 Clause            | 檔案數 |
| -------- | ----------------------------- | ---------------------- | ------ |
| **00**   | Dashboard（入口）             | —                      | 4      |
| **01**   | Foundations 基礎              | Clause 1-4 + 法規      | 6      |
| **02**   | Organizational Mgmt           | Clause 5 (CSMS)        | 7      |
| **03**   | Project-Dependent             | Clause 6               | 8      |
| **04**   | Distributed Activities        | Clause 7 (CIA)         | 4      |
| **05**   | Continual Activities          | Clause 8               | 5      |
| **06**   | Concept Phase                 | Clause 9               | 5      |
| **07**   | Product Development           | Clause 10              | 5      |
| **08**   | Validation                    | Clause 11              | 3      |
| **09**   | Production                    | Clause 12              | 3      |
| **10**   | Operations & Maintenance      | Clause 13              | 3      |
| **11**   | End of Support / Decommission | Clause 14              | 3      |
| **12**   | TARA Methods                  | **Clause 15 (⭐核心)** | 9      |
| **13**   | Annexes & Tools               | Annex E + 業界方法     | 4      |
| **14**   | Exam Practice                 | 綜合模擬               | 3      |
| **總計** |                               |                        | **72** |

---

## 建議學習順序

```
Week 1：基礎 + 治理
  └─ 01-Foundations → 02-Organizational → 03-Project-Dependent

Week 2：分散開發 + 持續資安
  └─ 04-Distributed → 05-Continual

Week 3：開發生命週期
  └─ 06-Concept → 07-Development → 08-Validation

Week 4：後開發 + TARA 深化
  └─ 09-Production → 10-Operations → 11-EoS → 12-TARA (★)

Week 5：補強 + 模擬題
  └─ 13-Annexes → 14-Exam-Practice → 重看 Exam-Traps
```

---

## 練習題分布

每個資料夾內含對應 **Practice-XXX.md**，共：

- 9 個章節練習題（每題集 6-15 題）
- 3 個跨章節模擬試題（Mock-Exam-1/2/3）
- 約 **120+ 題**

題型分布：

- Recall（記憶）：~60%
- Application（應用）：~25%
- Analysis（分析）：~15%

所有答案採 `> [!answer]-` 折疊式 callout，可先想再展開。

---

## 高頻考試重點（⭐⭐⭐）

1. **Clause 編號 ↔ 主題**對應（背骨架）
2. **TARA 八步驟**順序
3. **CAL vs ASIL** 區別（最大陷阱）
4. **Attack Feasibility 分數方向**（分數高=困難，最易考錯）
5. **Damage Scenario vs Threat Scenario**
6. **CS Goal vs Claim vs Concept vs Requirement**
7. **Verification vs Validation** 層級
8. **Risk Treatment** 四選項（Avoid/Reduce/Share/Retain）
9. **SFOP** 四大衝擊類別
10. **UN R155 vs R156** 並列關係

---

## 標籤系統

```
領域：#iso-21434, #automotive-cybersecurity
階段：#concept, #development, #validation, #production, #operations
方法：#tara, #stride, #attack-tree
治理：#csms, #cs-plan, #audit
法規：#un-r155, #un-r156
類型：#concept-note, #practice, #mock-exam, #moc, #quick-ref
```

---

## 使用建議

1. **背骨架**：先讀 [[00-Dashboard/Quick-Reference\|00-Dashboard/Quick-Reference]] 速覽全標準
2. **深入概念**：依 MOC 順序讀各章節筆記
3. **作題驗證**：每讀完一章做對應 Practice
4. **錯題回顧**：寫入 [[00-Dashboard/Weak-Areas\|00-Dashboard/Weak-Areas]]
5. **考前衝刺**：14-Exam-Practice 模擬題 + Exam-Traps 重看

---

## 資料來源

- 內部彙整：基於 `automotive-automotive-cybersecurity` skill 的 ISO 21434 內容
- 模型既有知識（ISO/SAE 21434:2021、UN R155、UN R156、ISO 26262 對應）
- 業界實務（STRIDE、Attack Tree、Pen Test 方法）

注意：本筆記為**準備考試用**的整理版本，**不取代**原文標準。
應試前建議搭配原版 ISO/SAE 21434:2021 與當地認證單位之教材。

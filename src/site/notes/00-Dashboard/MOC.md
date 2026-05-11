---
{"dg-publish":true,"permalink":"/00-dashboard/moc/","title":"ISO/SAE 21434 學習地圖 (MOC)","tags":["moc","iso-21434","automotive-cybersecurity"],"dg-note-properties":{"title":"ISO/SAE 21434 學習地圖 (MOC)","type":"moc","tags":["moc","iso-21434","automotive-cybersecurity"],"created":"2026-05-11"}}
---


> 本站為 **ISO/SAE 21434:2021 Road vehicles — Cybersecurity engineering** 證照準備筆記。
> 涵蓋 Clause 4 ~ Clause 15 與主要 Annex，搭配 TARA 方法、UN R155/R156 對應、練習題。

---

## 學習路徑建議 (Recommended Path)

```
Week 1: Foundations + 組織治理
  └─ 01-Foundations → 02-Organizational-Management → 03-Project-Dependent

Week 2: 分散式開發 + 持續資安
  └─ 04-Distributed-CS-Activities → 05-Continual-Cybersecurity

Week 3: 開發生命週期 (Concept → Validation)
  └─ 06-Concept-Phase → 07-Product-Development → 08-Cybersecurity-Validation

Week 4: 後開發階段 + TARA 深化
  └─ 09-Production → 10-Operations-Maintenance → 11-EndOfSupport → 12-TARA-Methods

Week 5: Annex + 練習題衝刺
  └─ 13-Annexes-Tools → 14-Exam-Practice → 00-Dashboard/Quick-Reference
```

---

## 主題地圖 (Topic Map)

### 01-Foundations｜基礎觀念

- [[01-Foundations/01-Standard-Overview\|ISO 21434 標準總覽]]
- [[01-Foundations/02-Key-Terms-Definitions\|關鍵術語與定義 (Clause 3)]]
- [[01-Foundations/03-Cybersecurity-vs-Safety\|資安 vs. 功能安全 (Cybersecurity vs Safety)]]
- [[01-Foundations/04-Lifecycle-Overview\|資安工程生命週期總覽 (Clause 6 框架)]]
- [[01-Foundations/05-Regulatory-Landscape\|法規地景 UN R155/R156/WP.29]]

### 02-Organizational-Management｜組織層級資安管理 (Clause 5)

- [[02-Organizational-Management/01-CSMS-Overview\|CSMS 網路安全管理系統總覽]]
- [[02-Organizational-Management/02-Cybersecurity-Culture\|資安文化與能力管理]]
- [[02-Organizational-Management/03-Management-Systems\|管理系統（資訊安全、品質、組織政策）]]
- [[02-Organizational-Management/04-Tool-Management\|工具管理與工具評估]]
- [[02-Organizational-Management/05-Information-Sharing\|資訊共享 (Information Sharing)]]
- [[02-Organizational-Management/06-Audit-and-Assessment\|稽核與資安評估]]

### 03-Project-Dependent｜專案層級資安管理 (Clause 6)

- [[03-Project-Dependent/01-Cybersecurity-Plan\|資安計畫 (Cybersecurity Plan)]]
- [[03-Project-Dependent/02-Responsibilities-Roles\|角色與責任分配 (RASIC)]]
- [[03-Project-Dependent/03-Tailoring\|裁適 (Tailoring)]]
- [[03-Project-Dependent/04-Reuse\|重用 (Reuse) 與 OTS 元件]]
- [[03-Project-Dependent/05-Component-Out-of-Context\|脈絡外元件 (Out-of-Context Component)]]
- [[03-Project-Dependent/06-Case-and-Assessment\|資安案例與評估報告 (Cybersecurity Case / Assessment)]]
- [[03-Project-Dependent/07-Release-for-Post-Development\|發行至後開發階段 (Release for Post-Development)]]

### 04-Distributed-CS-Activities｜分散式資安活動 (Clause 7)

- [[04-Distributed-CS-Activities/01-Customer-Supplier-Interaction\|客戶與供應商互動]]
- [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|資安界面協議 (CIA)]]
- [[04-Distributed-CS-Activities/03-Supplier-Capability\|供應商能力評估 (RFQ + Capability)]]

### 05-Continual-Cybersecurity｜持續性資安活動 (Clause 8)

- [[05-Continual-Cybersecurity/01-Cybersecurity-Monitoring\|資安監控 (CS Monitoring)]]
- [[05-Continual-Cybersecurity/02-Event-Assessment\|資安事件評估]]
- [[05-Continual-Cybersecurity/03-Vulnerability-Analysis\|弱點分析]]
- [[05-Continual-Cybersecurity/04-Vulnerability-Management\|弱點管理]]

### 06-Concept-Phase｜概念階段 (Clause 9)

- [[06-Concept-Phase/01-Item-Definition\|Item 定義]]
- [[06-Concept-Phase/02-Cybersecurity-Goals\|資安目標 (Cybersecurity Goals)]]
- [[06-Concept-Phase/03-Cybersecurity-Claims\|資安主張 (Cybersecurity Claims)]]
- [[06-Concept-Phase/04-Cybersecurity-Concept\|資安概念 (Cybersecurity Concept)]]

### 07-Product-Development｜產品開發 (Clause 10)

- [[07-Product-Development/01-Design-Requirements\|設計階段：資安需求與架構]]
- [[07-Product-Development/02-Integration-Verification\|整合與驗證 (Integration & Verification)]]
- [[07-Product-Development/03-Weakness-Vulnerability-Analysis\|弱點與漏洞分析（開發階段）]]
- [[07-Product-Development/04-HW-SW-Considerations\|HW/SW/介面 資安考量]]

### 08-Cybersecurity-Validation｜資安驗證 (Clause 11)

- [[08-Cybersecurity-Validation/01-Validation-Objectives\|驗證目標與策略]]
- [[08-Cybersecurity-Validation/02-Validation-Methods\|驗證方法（滲透測試/Fuzz/模糊測試）]]

### 09-Production｜生產 (Clause 12)

- [[09-Production/01-Production-Controls\|生產資安控制]]
- [[09-Production/02-Provisioning\|金鑰/憑證植入 (Provisioning)]]

### 10-Operations-Maintenance｜營運與維護 (Clause 13)

- [[10-Operations-Maintenance/01-Incident-Response\|資安事件回應]]
- [[10-Operations-Maintenance/02-Updates\|更新管理（含 OTA）]]

### 11-EndOfSupport-Decommission｜終止支援與除役 (Clause 14)

- [[11-EndOfSupport-Decommission/01-End-of-Support\|終止支援 (EoS) 通知與條件]]
- [[11-EndOfSupport-Decommission/02-Decommissioning\|除役 (Decommissioning)]]

### 12-TARA-Methods｜TARA 方法 (Clause 15 + Annex)

- [[12-TARA-Methods/01-TARA-Overview\|TARA 流程總覽]]
- [[12-TARA-Methods/02-Asset-Identification\|資產識別]]
- [[12-TARA-Methods/03-Threat-Scenario\|威脅情境 (Threat Scenario)]]
- [[12-TARA-Methods/04-Impact-Rating\|衝擊評等 (SFOP)]]
- [[12-TARA-Methods/05-Attack-Path-Analysis\|攻擊路徑分析 (Attack Path)]]
- [[12-TARA-Methods/06-Attack-Feasibility-Rating\|攻擊可行性評等 (Attack Feasibility)]]
- [[12-TARA-Methods/07-Risk-Determination\|風險判定 (Risk Determination)]]
- [[12-TARA-Methods/08-Risk-Treatment\|風險處置 (Risk Treatment) + CAL]]

### 13-Annexes-Tools｜附錄與工具

- [[13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level\|CAL：資安保證等級]]
- [[13-Annexes-Tools/02-Mapping-to-UN-R155\|對應 UN R155 表]]
- [[13-Annexes-Tools/03-STRIDE-DREAD\|STRIDE / DREAD 補充]]
- [[13-Annexes-Tools/04-Attack-Trees\|攻擊樹 (Attack Trees)]]

### 14-Exam-Practice｜練習題（依章節）

- 每個主資料夾內含對應 `Practice-*.md`，本資料夾為 **綜合模擬題**。
- [[14-Exam-Practice/Mock-Exam-1\|模擬試題 1：基礎觀念 + Lifecycle]]
- [[14-Exam-Practice/Mock-Exam-2\|模擬試題 2：TARA + Risk Treatment]]
- [[14-Exam-Practice/Mock-Exam-3\|模擬試題 3：跨章節情境題]]

---

## 學習工具 (Study Tools)

- 🗺️ [[00-Dashboard/Quick-Reference\|Quick Reference 速查表]] — 一頁速覽全標準
- ⚠️ [[00-Dashboard/Exam-Traps\|常見考試陷阱]] — 易混淆觀念整理

---

## 標籤索引 (Tag Index)

### 規則 (Tagging Rules)

- 一律 **英文小寫 + kebab-case**
- 層級：`top → domain → detail → technique → note-type`
- 細節標籤需附上 parent domain tag

### 主要標籤

- 領域：`#iso-21434`, `#cybersecurity`, `#automotive`
- 階段：`#concept`, `#development`, `#validation`, `#production`, `#operations`, `#post-development`
- 方法：`#tara`, `#stride`, `#attack-tree`, `#risk-assessment`
- 治理：`#csms`, `#cs-plan`, `#audit`, `#tailoring`
- 對應：`#un-r155`, `#un-r156`, `#unece-wp29`
- 風險：`#impact-rating`, `#attack-feasibility`, `#cal`, `#risk-treatment`
- 筆記類型：`#concept-note`, `#practice`, `#moc`, `#quick-ref`

---

## 非核心主題政策 (Non-core Topics)

下列主題在 ISO 21434 中**非考試核心**，僅做背景理解，不深入：

- 詳細加密演算法數學推導（AES/RSA/ECC 內部運算）
- 具體攻擊技術細節（屬於滲透測試訓練範疇）
- 特定 OEM 內部流程（不在標準範圍內）

---

## Related

- [[00-Dashboard/Quick-Reference\|00-Dashboard/Quick-Reference]]
- [[00-Dashboard/Exam-Traps\|00-Dashboard/Exam-Traps]]
- [[01-Foundations/01-Standard-Overview\|01-Foundations/01-Standard-Overview]]

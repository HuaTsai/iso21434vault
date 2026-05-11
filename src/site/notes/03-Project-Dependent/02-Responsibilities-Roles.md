---
{"dg-publish":true,"permalink":"/03-project-dependent/02-responsibilities-roles/","title":"角色與責任分配 (RASIC)","tags":["iso-21434","concept-note","project-dependent","roles"],"dg-note-properties":{"title":"角色與責任分配 (RASIC)","source_pdf":"內部彙整 (ISO 21434 Clause 6.4.3)","part":"Clause 6","keywords":["rasic","raci","roles","responsibilities"],"tags":["iso-21434","concept-note","project-dependent","roles"],"created":"2026-05-11"}}
---


## 為什麼需要明確角色？

> [!important]
> 資安活動跨多個團隊（CS、Safety、Architect、Tester、PM）。
> 不明確的責任 → **遺漏**、**重複工**、**互推**。
>
> ISO 21434 要求：每個資安活動都有**明確負責人**。

---

## RASIC vs RACI

業界常見兩種模型：

### RASIC

```
R - Responsible：實際執行者
A - Accountable：最終負責人（一個！）
S - Supporting：支援者
I - Informed：被告知
C - Consulted：諮詢對象
```

### RACI（簡化版）

```
R - Responsible
A - Accountable
C - Consulted
I - Informed
```

> [!warning] 重要規則
> **每個活動只能有一個 A (Accountable)**。
> 多個 R 可以，但 A 必須唯一，否則責任不清。

---

## ISO 21434 預期的核心角色

```
組織層級 (Organizational, Clause 5)
├── Top Management
├── CS Manager / CS Officer  ← 組織整體
└── Internal Auditor

專案層級 (Project, Clause 6)
├── Project Manager
├── Project CS Manager      ← 專案資安總管
├── CS Engineer / Analyst
├── Security Architect
├── Verification Engineer
├── Validation Engineer
├── Independent Assessor    ← 獨立評估
└── Project Safety Manager  ← 跨領域協作

分散式 (Distributed, Clause 7)
├── Customer-side CS Mgr
└── Supplier-side CS Mgr

後開發 (Post-development, Clause 13)
├── Incident Response Lead
├── Vulnerability Mgr
└── Update Mgr / OTA Mgr
```

---

## 角色 vs 職稱

> [!tip]
> ISO 21434 描述**角色 (role)**，而非**職稱 (title)**。
> 一個人可擔任多角色；多個人可分擔一個角色。

範例：

- 小公司：Project CS Manager 同時兼 CS Engineer
- 大公司：CS Engineer 由 5 人組成的團隊

---

## 完整 RASIC 範本（產品開發）

| 活動 / 角色             | PM  | CS Mgr  | Architect | CS Eng | Test  | Safety | Mgmt  | Indep Assessor |
| ----------------------- | :-: | :-----: | :-------: | :----: | :---: | :----: | :---: | :------------: |
| **Item Definition**     |  A  |    C    |     R     |   S    |   I   |   C    |   I   |       I        |
| **TARA 執行**           |  I  |  **A**  |     C     | **R**  |   I   |   C    |   I   |       I        |
| **CS Goals 凍結**       |  C  |  **A**  |     C     |   R    |   I   |   C    |   I   |       I        |
| **架構設計**            |  I  |    A    |   **R**   |   S    |   I   |   C    |   I   |       I        |
| **CS Requirements**     |  I  |    A    |     S     | **R**  |   I   |   C    |   I   |       I        |
| **Verification**        |  I  |    A    |     C     |   S    | **R** |   I    |   I   |       I        |
| **Penetration Test**    |  I  |    A    |     C     |   C    | **R** |   I    |   I   |       I        |
| **Validation (車輛級)** |  C  |  **A**  |     I     |   S    | **R** |   C    |   I   |       I        |
| **CS Case 編製**        |  C  | **R/A** |     S     |   S    |   S   |   C    |   I   |       C        |
| **CS Assessment**       |  I  |    I    |     I     |   I    |   I   |   I    |   I   |    **R/A**     |
| **Release 決策**        |  C  |    C    |     I     |   I    |   I   |   C    | **A** |       C        |

> A = Accountable (only one), R = Responsible (executor)

---

## 關鍵衝突點

### Architect vs Engineer

- **Architect**：設計層面 → R/A 在設計工件
- **Engineer**：實作層面 → R/A 在實作工件
- **介面**：兩者需頻繁協作；Architect 通常 Consulted 於 Engineer 的工作

### CS Manager vs Project Manager

- **PM**：專案整體（時程、預算、scope）
- **CS Mgr**：資安專業面
- **衝突解法**：PM 通常為「資源 A」，CS Mgr 為「資安成果 A」

### CS Manager vs Safety Manager

- 兩者**互不從屬**
- 衝突時：依組織政策 + 在 Plan 中明定優先級（Safety 通常優先）

---

## 獨立性 (Independence) 要求

某些角色 ISO 21434 **明確要求獨立性**：

| 角色                     | 與誰獨立             | 為何         |
| ------------------------ | -------------------- | ------------ |
| **Independent Assessor** | 與專案執行者         | 評估的客觀性 |
| **Internal Auditor**     | 與被稽核活動         | 稽核的客觀性 |
| **CS Validation**        | 部分情況下與開發團隊 | 驗證的客觀性 |

> [!warning]
> 「獨立」**不必然指外部人員**——可以是組織內部、不同部門。但**不可在向同一主管報告**的範圍內。

---

## RASIC 表的版控

CS Plan 中的 RASIC 表：

- 隨組織變動更新（人員異動、角色重組）
- 版本化（與 CS Plan 連動）
- 任何角色變動需 CS Mgr 批准

---

## 證照考點

> [!important] 高頻考點
>
> 1. **每個活動只能有一個 A**
> 2. RASIC 與 RACI **不同**（多了 S = Supporting）
> 3. **Project CS Manager** 是 Clause 6 的核心角色
> 4. **獨立性**：Assessor、Auditor 必須與被檢視活動獨立
> 5. ISO 21434 描述「角色」非「職稱」——一人可多角色
> 6. RASIC 應寫入 **CS Plan**（不是另一份文件）

---

## Related Notes

- [[03-Project-Dependent/01-Cybersecurity-Plan\|03-Project-Dependent/01-Cybersecurity-Plan]]
- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]
- [[02-Organizational-Management/06-Audit-and-Assessment\|02-Organizational-Management/06-Audit-and-Assessment]]
- [[04-Distributed-CS-Activities/01-Customer-Supplier-Interaction\|04-Distributed-CS-Activities/01-Customer-Supplier-Interaction]]

## Practice

- [[03-Project-Dependent/Practice-Project-Mgmt\|03-Project-Dependent/Practice-Project-Mgmt]]

---
{"dg-publish":true,"permalink":"/03-project-dependent/01-cybersecurity-plan/","title":"資安計畫 (Cybersecurity Plan)","tags":["iso-21434","concept-note","project-dependent","cs-plan"],"dg-note-properties":{"title":"資安計畫 (Cybersecurity Plan)","source_pdf":"內部彙整 (ISO 21434 Clause 6.4.2)","part":"Clause 6","keywords":["cs-plan","cybersecurity-plan","project","planning"],"tags":["iso-21434","concept-note","project-dependent","cs-plan"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> document that describes the cybersecurity activities, their order, dependencies, planned timing, responsibilities and tools to be used.

簡言之：**「資安活動的施工藍圖」**。

---

## CS Plan 的 5W1H 內容

```
What  — 要執行哪些資安活動
Who   — 誰負責（含 RASIC）
When  — 何時執行（時程、依賴）
Where — 在哪個階段／文件中產出
Why   — 活動的目的與依據
How   — 用什麼方法、工具
```

---

## 必含項目（Mandatory Content）

| 項目                        | 範例                                   |
| --------------------------- | -------------------------------------- |
| 專案範圍                    | TCU、適用車型、地理區                  |
| 適用 Clause                 | Clause 9-13 + 適用條件                 |
| **活動清單**                | TARA、Design Review、Pen Test...       |
| **時程與依賴**              | Gantt + Milestone                      |
| **角色與責任 (RASIC)**      | Project CS Manager、Engineer、Reviewer |
| **Tailoring 決策**          | 哪些活動被裁適 + 理由                  |
| **工具清單**                | Medini、Burp、Fuzz tool...             |
| **Work Product 清單**       | 將產出哪些 WP + 對誰交付               |
| **與其他 Plan 的關係**      | Safety Plan、QM Plan                   |
| **變更管理**                | 何時 review、誰批准變更                |
| **Cybersecurity Case 結構** | 預計如何論證                           |

---

## CS Plan 範本骨架

```yaml
cybersecurity_plan:
  metadata:
    project_id: "TCU-2026"
    version: 2.3
    date: 2026-05-11
    approved_by: "Project CS Manager"

  scope:
    item: "Telematics Control Unit (TCU)"
    vehicle_program: "EV Platform G3"
    market: ["EU", "US", "JP"]
    applicable_regulations: ["UN R155", "UN R156"]

  applicable_clauses:
    clause_5: included # 引用組織 CSMS
    clause_6: included
    clause_7: included # 含 Tier-1 供應商
    clause_8: included
    clause_9: included
    clause_10: included
    clause_11: included
    clause_12: included
    clause_13: included
    clause_14: future # 後續更新
    clause_15: included

  tailoring:
    - activity: "Repeated TARA after minor SW change"
      decision: "Combined into quarterly TARA review"
      rationale: "Minor SW changes do not alter attack paths"
      approver: "CS Manager"

  responsibilities:
    project_cs_manager:
      - "Overall CS execution"
      - "Coordinate with Safety Manager"
    cs_engineer:
      - "TARA execution"
      - "Verification support"
    architect:
      - "Security architecture design"
    independent_assessor:
      - "Cybersecurity Assessment"

  timeline:
    item_definition: 2026-06-01
    tara_v1: 2026-07-15
    cs_goals_freeze: 2026-08-01
    architecture_review: 2026-10-01
    verification_complete: 2027-02-28
    validation_complete: 2027-05-30
    release: 2027-07-01

  tools:
    tara: "Medini Analyze v2024 R2"
    threat_modeling: "MS Threat Modeling Tool v7"
    sast: "Coverity 2024.06"
    fuzz: "Defensics 2024.06"
    pen_test: "Internal team + Tier-1 vendor"

  work_products:
    - WP-001: TARA Report
    - WP-002: CS Goals
    - WP-003: CS Concept
    - WP-004: CS Requirements
    - WP-005: Verification Report
    - WP-006: Validation Report
    - WP-007: CS Assessment Report
    - WP-008: CS Case

  case_structure:
    framework: "Claim-Argument-Evidence (CAE)"
    top_claim: "TCU achieves all cybersecurity goals"

  dependencies:
    safety_plan: "SP-TCU-2026 v1.5"
    qm_plan: "QM-TCU-2026 v2.0"

  update_triggers:
    - "Major design change"
    - "New supplier"
    - "New regulation"
    - "Major incident"
```

---

## RASIC 矩陣（簡化）

| 活動 / 角色         | CS Mgr  | Architect | Engineer | Safety Mgr | Quality |
| ------------------- | :-----: | :-------: | :------: | :--------: | :-----: |
| TARA 主導           |  **A**  |     C     |  **R**   |     I      |    I    |
| CS Goals 批准       |  **A**  |     C     |    S     |     C      |    I    |
| 架構設計            |    I    |  **R/A**  |    S     |     C      |    I    |
| Verification        |    A    |     C     |  **R**   |     I      |    S    |
| Validation (車輛級) |  **A**  |     I     |    R     |     C      |    S    |
| CS Case 編製        | **R/A** |     C     |    S     |     I      |    C    |
| Release 決策        |    A    |     I     |    I     |     C      |    I    |

> R=Responsible, A=Accountable, S=Supporting, I=Informed, C=Consulted

---

## CS Plan vs Safety Plan

| 比較項   | **Cybersecurity Plan** | **Safety Plan** (26262) |
| -------- | ---------------------- | ----------------------- |
| 標準     | ISO 21434              | ISO 26262 Part 2        |
| 主題     | 資安活動規劃           | 安全活動規劃            |
| 等級     | CAL (Annex E)          | ASIL                    |
| 風險方法 | TARA                   | HARA                    |
| 後開發   | **重視**               | 相對輕                  |

**整合策略**：常以 **共同骨架**（PM 流程）+ **各自附錄**。

---

## CS Plan 的演進

```
Project Start
    ↓
CS Plan v0.1 (draft)
    ↓
Item Definition 完成
    ↓
CS Plan v1.0 (baselined)
    ↓
TARA 完成 → 細節更新
    ↓
CS Plan v1.x
    ↓
Major change / Tailoring 變更
    ↓
CS Plan v2.0
    ↓
…直至 EoS
```

> [!tip]
> CS Plan **不是一次性文件**，是 **living document**。

---

## 證照考點

> [!important] 高頻考點
>
> - CS Plan 是 **Clause 6.4.2** 規範的 WP
> - 必含 **Tailoring 決策 + 理由**
> - **RASIC** 是常見的責任表達工具
> - CS Plan **vs** CS Case 差別（前者是計畫，後者是證據）
> - CS Plan 需**版控**，是 living document
> - Project CS Manager 是 **Accountable** 角色

---

## Related Notes

- [[03-Project-Dependent/02-Responsibilities-Roles\|03-Project-Dependent/02-Responsibilities-Roles]]
- [[03-Project-Dependent/03-Tailoring\|03-Project-Dependent/03-Tailoring]]
- [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]
- [[00-Dashboard/Exam-Traps#Trap 4\|00-Dashboard/Exam-Traps#Trap 4]]

## Practice

- [[03-Project-Dependent/Practice-Project-Mgmt\|03-Project-Dependent/Practice-Project-Mgmt]]

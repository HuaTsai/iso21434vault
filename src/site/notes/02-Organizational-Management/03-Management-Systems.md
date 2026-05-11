---
{"dg-publish":true,"permalink":"/02-organizational-management/03-management-systems/","title":"管理系統整合","tags":["iso-21434","concept-note","csms","integration"],"dg-note-properties":{"title":"管理系統整合","source_pdf":"內部彙整 (ISO 21434 Clause 5.4.4)","part":"Clause 5","keywords":["management-systems","isms","qms","integration"],"tags":["iso-21434","concept-note","csms","integration"],"created":"2026-05-11"}}
---


## 與其他管理系統的關係

ISO 21434 的 CSMS **不應孤立存在**，需與下列管理系統整合：

```
                ┌─────────────────────┐
                │     CSMS            │
                │   (ISO 21434)       │
                └──────────┬──────────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
┌───────▼──────┐   ┌───────▼──────┐   ┌───────▼──────┐
│     ISMS     │   │     QMS      │   │  Safety Mgmt │
│ (ISO 27001)  │   │ (ISO 9001 +  │   │ (ISO 26262)  │
│ IT 資訊安全   │   │  IATF 16949) │   │ 功能安全      │
└──────────────┘   └──────────────┘   └──────────────┘
```

---

## CSMS vs ISMS

| 比較項 | **CSMS (ISO 21434)**         | **ISMS (ISO 27001)**     |
| ------ | ---------------------------- | ------------------------ |
| 主題   | **產品**資安（車輛 E/E）     | **組織 IT** 資訊安全     |
| 對象   | 車輛、ECU、車載軟體          | 員工電腦、伺服器、雲端   |
| 風險   | 對 road user 的衝擊          | 對組織資料的衝擊         |
| 重點   | TARA、CS Concept、Validation | 控制措施 (Annex A 14 域) |
| 認證   | UN R155                      | ISO 27001                |

**整合點**：

- 公司開發環境的安全（如原始碼庫被入侵）= ISMS 範疇
- 但開發環境影響車輛資安 → 兩者交互
- HSM、簽章金鑰管理 = 兩者皆涉及

---

## CSMS vs QMS

| 比較項   | **CSMS**      | **QMS (IATF 16949)** |
| -------- | ------------- | -------------------- |
| 主題     | 資安          | 整體品質             |
| 風險     | 威脅、攻擊    | 品質缺陷、不一致     |
| 工具     | TARA          | FMEA、APQP、PPAP     |
| 文件控制 | CS Plan、Case | Control Plan         |

**整合點**：

- 文件管理、版本控制、變更管理可**共享**
- 內部稽核流程可**整合**
- 矯正措施 (CAPA) 機制可**共用**

---

## CSMS vs Safety Mgmt

→ 詳見 [[01-Foundations/03-Cybersecurity-vs-Safety\|01-Foundations/03-Cybersecurity-vs-Safety]]

**整合點**：

- **Item Definition** 共享
- 部分 V-Model 階段對齊
- Joint Review（Safety + Security）
- 共享 HIL/Test 平台

---

## 整合策略選項

### 選項 A：完全獨立

```
ISMS    QMS    CSMS    Safety
 ↓       ↓      ↓        ↓
獨立    獨立    獨立    獨立
文件    文件    文件    文件
```

**優點**：清楚分工
**缺點**：重複工、整合風險

### 選項 B：共用基礎，獨立內容（建議）

```
        ┌──────────────────────┐
        │ 共用：文件控制、稽核、 │
        │       培訓平台、CAPA  │
        └─┬────┬────┬────┬─────┘
          │    │    │    │
        ISMS  QMS  CSMS Safety
        各自專業內容
```

### 選項 C：完全整合（IMS - Integrated Management System）

```
單一手冊涵蓋四個標準
單一稽核
```

**優點**：效率
**缺點**：可能模糊邊界、稽核員需多重專業

---

## 共享資源建議

| 資源                | 可共享 | 不可共享（須獨立）          |
| ------------------- | ------ | --------------------------- |
| 文件控制流程        | ✓      | —                           |
| 變更管理            | ✓      | —                           |
| 內部稽核流程        | ✓      | 稽核員的領域知識需獨立      |
| 培訓平台            | ✓      | 培訓內容需專業化            |
| CAPA 系統           | ✓      | —                           |
| Top Management 承諾 | ✓      | —                           |
| 風險評估方法        | 部分   | TARA / FMEA / HARA 各自獨立 |
| KPI 報表            | 部分   | 指標各自獨立                |

---

## 文件層級對應

```
Policy 層 (政策)
   └── 公司資安政策（涵蓋 ISMS + CSMS 共通原則）
        │
Process 層 (流程)
   ├── ISMS 流程
   ├── CSMS 流程（含 TARA、CIA）
   ├── QMS 流程
   └── Safety 流程
        │
Procedure 層 (程序)
   └── 各流程下的具體操作程序
        │
Record 層 (紀錄)
   └── 執行證據
```

---

## 證照考點

> [!important]
>
> - CSMS **不必獨立於** ISMS 之外，可整合
> - 整合時需保留**領域專業性**
> - **Item Definition** 是 CSMS 與 Safety Mgmt 最重要的整合點
> - 內部稽核可共用流程，但稽核員需具備領域能力

---

## Related Notes

- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]
- [[01-Foundations/03-Cybersecurity-vs-Safety\|01-Foundations/03-Cybersecurity-vs-Safety]]
- [[02-Organizational-Management/06-Audit-and-Assessment\|02-Organizational-Management/06-Audit-and-Assessment]]

## Practice

- [[02-Organizational-Management/Practice-CSMS\|02-Organizational-Management/Practice-CSMS]]

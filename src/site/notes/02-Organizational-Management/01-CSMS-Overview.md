---
{"dg-publish":true,"permalink":"/02-organizational-management/01-csms-overview/","title":"資安管理系統 (CSMS / Cybersecurity Management System) 總覽","tags":["iso-21434","concept-note","csms","organizational"],"dg-note-properties":{"title":"資安管理系統 (CSMS / Cybersecurity Management System) 總覽","source_pdf":"內部彙整 (ISO/SAE 21434:2021 Clause 5)","part":"Clause 5","keywords":["csms","organizational","governance","policies"],"tags":["iso-21434","concept-note","csms","organizational"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義（業界通用釋義，非 Clause 3 verbatim）
> systematic risk-based approach defining organizational processes, responsibilities and governance to treat risk associated with cyber threats and protect from cyberattacks.

**關鍵字**：

- **systematic**（系統化）
- **risk-based**（風險導向）
- **organizational**（**組織級**，非單一專案）
- **governance**（治理）

---

## CSMS 與 UN R155 的關係

```
UN R155 §7.2 要求 OEM 建立 CSMS
                  │
                  ↓
       ISO 21434 Clause 5 提供具體方法
```

UN R155 **不指定**怎麼做 CSMS，但要求「OEM 能展示完整 CSMS」。
ISO 21434 Clause 5 是被廣泛接受的實作方式。

---

## CSMS 的七大支柱

```
官方 Clause 5.4.1 – 5.4.7 對應的七大支柱：

┌─────────────────────────────────────────────────┐
│ 5.4.1 Cybersecurity Governance                  │
│       （政策、章程、組織架構、roles & accountabilities） │
├─────────────────────────────────────────────────┤
│ 5.4.2 Cybersecurity Culture                     │
│       （資安意識、培訓、competence management）   │
├─────────────────────────────────────────────────┤
│ 5.4.3 Information Sharing                       │
│       （內部 / 外部資訊共享）                     │
├─────────────────────────────────────────────────┤
│ 5.4.4 Management Systems                        │
│       （與 ISMS、QMS、組織管理系統整合）           │
├─────────────────────────────────────────────────┤
│ 5.4.5 Tool Management                           │
│       （工具評估、變更控制、TCL 概念）             │
├─────────────────────────────────────────────────┤
│ 5.4.6 Information Security Management           │
│       （組織的資訊安全管理）                       │
├─────────────────────────────────────────────────┤
│ 5.4.7 Organizational Cybersecurity Audit        │
│       （獨立稽核、Lessons Learned、KPI）          │
└─────────────────────────────────────────────────┘

橫貫所有支柱的機制：
• Continual Improvement (PDCA) — 不是單一支柱，而是貫穿所有 5.4.x 的循環
```

每一支柱都需有具體的**政策文件 + 流程 + 紀錄**。

---

## 必要的 Work Products (Clause 5)

| WP                                        | 描述             | 負責層級        |
| ----------------------------------------- | ---------------- | --------------- |
| **Organizational Cybersecurity Policies** | 公司資安總體政策 | C-level / Board |
| **Cybersecurity Rules and Processes**     | 具體流程規範     | Process Owner   |
| **Competence Management Plan**            | 能力管理規劃     | HR + CS Lead    |
| **Awareness and Training Records**        | 培訓紀錄         | HR              |
| **Continual Improvement Records**         | 改善紀錄         | CS Manager      |
| **Internal Audit Reports**                | 內部稽核報告     | 獨立稽核員      |
| **Information Sharing Records**           | 資訊共享紀錄     | CS Officer      |
| **Tool Management Records**               | 工具批准紀錄     | Tool Owner      |

---

## 組織角色 (Clause 5.4)

ISO 21434 不規範**具體職稱**，但要求至少有：

```
┌──────────────────────────────────┐
│ Top Management                   │
│ • 批准 CS 政策                    │
│ • 提供資源                        │
│ • 監督 CSMS 效能                  │
├──────────────────────────────────┤
│ Cybersecurity Manager (or 等同)   │
│ • CSMS 日常管理                   │
│ • 跨專案協調                      │
│ • 對 Top Mgmt 報告                │
├──────────────────────────────────┤
│ Project Cybersecurity Manager    │
│ • 專案層級執行（Clause 6）         │
├──────────────────────────────────┤
│ CS Engineers / Analysts          │
│ • TARA 執行、設計、驗證            │
├──────────────────────────────────┤
│ Internal Auditor                 │
│ • 獨立性要求                      │
│ • 定期稽核 CSMS                   │
└──────────────────────────────────┘
```

> [!warning] 獨立性
> Internal Auditor **不可**為被稽核活動的負責人或執行者。

---

## 資安文化 (Cybersecurity Culture)

ISO 21434 強調「文化」是 CSMS 的根基：

```
資安文化要求：
├── 全員意識（不只 CS 團隊）
├── Management 承諾與示範
├── 培訓週期化（new hire + 年度更新）
├── 不責備文化（鼓勵通報）
└── 跨部門協作（Safety + Quality + IT）
```

**證據**：

- 培訓出席率
- 員工通報事件數
- 員工資安問卷調查
- 跨部門 review 紀錄

---

## 能力管理 (Competence Management)

### 角色技能矩陣（範例）

| 角色               | 必要能力                            |
| ------------------ | ----------------------------------- |
| Project CS Manager | TARA、CIA、ISO 21434 條文、領導     |
| CS Engineer        | 加密基礎、滲透測試、Threat Modeling |
| Architect          | 安全設計、攻擊面分析                |
| Tester             | Fuzz、滲透、合規測試                |
| Auditor            | 21434 知識、稽核技巧、獨立性        |

### 證明方式

- 教育/認證（如 GIAC、CEH、CSSLP）
- 工作經驗紀錄
- 內部評鑑

---

## 工具管理 (Tool Management)

> [!important]
> 任何用於資安活動的工具（TARA 工具、Fuzz、SAST、HSM 工具）都需經過**評估與批准**。

評估維度：

1. **能力**：能否完成預期任務
2. **可信度**：是否有偽陽性/陰性問題
3. **可重現性**：相同輸入產出相同結果
4. **可追溯性**：能輸出可驗證紀錄

**TCL (Tool Confidence Level)** 概念與 ISO 26262 相近。

---

## CSMS 稽核（Audit）

### 內部稽核

- **頻率**：至少**年度**
- **獨立性**：稽核員與被稽核活動無直接利害
- **範圍**：全 CSMS 涵蓋
- **輸出**：稽核報告 + 不符合事項 (NC) + 改善計畫

### 外部稽核

- **UN R155 認證**：3 年一次，由獨立認證機構執行
- **可選**：ISO 21434 第三方驗證（如 TÜV、DEKRA）

---

## CSMS 成熟度與持續改善

```
PDCA 循環：
  Plan  → 政策、目標、KPI
  Do    → 執行專案、培訓、稽核
  Check → KPI 量測、稽核發現、事件分析
  Act   → 改善流程、更新政策
```

**KPI 範例**：

- 開放中的 High Risk 數量趨勢
- 弱點修補平均時間 (MTTR)
- 培訓覆蓋率
- 內部稽核 NC 數量趨勢
- 客戶資安投訴數
- 滲透測試發現的關鍵問題數

---

## Related Notes

- [[02-Organizational-Management/02-Cybersecurity-Culture\|02-Organizational-Management/02-Cybersecurity-Culture]]
- [[02-Organizational-Management/03-Management-Systems\|02-Organizational-Management/03-Management-Systems]]
- [[02-Organizational-Management/04-Tool-Management\|02-Organizational-Management/04-Tool-Management]]
- [[02-Organizational-Management/05-Information-Sharing\|02-Organizational-Management/05-Information-Sharing]]
- [[02-Organizational-Management/06-Audit-and-Assessment\|02-Organizational-Management/06-Audit-and-Assessment]]
- [[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]

## Practice

- [[02-Organizational-Management/Practice-CSMS\|02-Organizational-Management/Practice-CSMS]]

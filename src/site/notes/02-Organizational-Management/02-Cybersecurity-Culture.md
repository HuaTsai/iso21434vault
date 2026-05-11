---
{"dg-publish":true,"permalink":"/02-organizational-management/02-cybersecurity-culture/","title":"資安文化與能力管理","tags":["iso-21434","concept-note","csms","culture"],"dg-note-properties":{"title":"資安文化與能力管理","source_pdf":"內部彙整 (ISO 21434 Clause 5.4)","part":"Clause 5","keywords":["culture","competence","awareness","training"],"tags":["iso-21434","concept-note","csms","culture"],"created":"2026-05-11"}}
---


## 為什麼「文化」被列入標準？

ISO 21434 是少數明確將「文化」寫入規範性條文的標準之一。

> [!quote] Clause 5.4.2 精神
> 組織應建立並維持資安文化，使所有員工理解資安活動的重要性並對其貢獻負責。

**理由**：

- 技術控制可被繞過，但**人**才是最後一道防線。
- 攻擊鏈中常見社交工程、員工誤操作。
- 鼓勵通報文化 → 早期偵測。

---

## 文化的四個關鍵層面

```
┌────────────────────────────────────┐
│ 1. Awareness 意識                  │
│    全員理解資安重要性                │
├────────────────────────────────────┤
│ 2. Behavior 行為                   │
│    日常工作展現資安考量              │
├────────────────────────────────────┤
│ 3. Communication 溝通              │
│    開放、跨部門、無懲罰通報          │
├────────────────────────────────────┤
│ 4. Accountability 責任             │
│    每個角色清楚自己的資安責任         │
└────────────────────────────────────┘
```

---

## 培訓計畫設計

### 培訓對象與內容

| 對象            | 必要培訓內容                      | 頻率        |
| --------------- | --------------------------------- | ----------- |
| 全體員工        | 資安意識基礎、釣魚識別、密碼管理  | 入職 + 年度 |
| 開發人員        | 安全編碼、OWASP、ISO 21434 基本   | 入職 + 年度 |
| 架構師          | Threat Modeling、攻擊面分析、TARA | 角色變動時  |
| CS 工程師       | TARA 工具、滲透測試、加密         | 持續        |
| Manager         | ISO 21434 治理、UN R155、決策     | 入職 + 雙年 |
| 採購/供應商管理 | CIA、供應商風險、RFQ              | 入職 + 雙年 |

### 培訓記錄

必含：

- 學員名單
- 培訓內容與時數
- 評量結果（如有）
- 出席證明

---

## 能力管理 (Competence Management)

### 流程

```
1. 識別角色 → 列出 CSMS 中的角色
   ↓
2. 定義技能矩陣 → 每個角色需要哪些技能 + 程度
   ↓
3. 評估現況 → 個人技能評估
   ↓
4. 差距分析 (Gap Analysis)
   ↓
5. 培訓計畫 → 內部訓練、外部課程、認證
   ↓
6. 評鑑 → 培訓後評估、實作能力驗證
   ↓
7. 紀錄 → 個人能力檔案
```

### 技能矩陣範例

| 技能 / 角色    | CS Manager | CS Engineer | Architect |   Tester   |
| -------------- | :--------: | :---------: | :-------: | :--------: |
| ISO 21434 知識 |   Expert   |     Adv     |    Adv    |   Inter    |
| TARA 執行      |    Adv     | **Expert**  |    Adv    |   Inter    |
| 加密基礎       |   Basic    |     Adv     |    Adv    |    Adv     |
| 滲透測試       |   Basic    |     Adv     |   Inter   | **Expert** |
| 領導/溝通      | **Expert** |    Inter    |    Adv    |   Inter    |
| 法規 (R155)    | **Expert** |    Inter    |   Inter   |   Basic    |

> Basic / Inter / Adv / Expert 為四級。

---

## 招募與留任

> [!tip] 業界現況
> CS 工程師供不應求。CSMS 應規劃：
>
> - **內部培養**：從相關領域（IT 安全、Safety）轉訓
> - **學界合作**：實習、研究合作
> - **認證鼓勵**：補助 GIAC、CISSP、ISO 21434 認證
> - **留任策略**：技術職涯路徑、薪資競爭力

---

## 跨部門協作文化

```
            ┌─────────────────┐
            │   CS Team       │
            └────────┬────────┘
                     │
        ┌────────────┼────────────┐
        │            │            │
┌───────▼─────┐ ┌────▼─────┐ ┌────▼──────┐
│ Safety Team │ │ Quality  │ │ IT/SecOps │
│  (26262)    │ │  (QMS)   │ │  (27001)  │
└─────────────┘ └──────────┘ └───────────┘
        │            │            │
        └────────────┴────────────┘
                     │
              共同 review、共享紀錄
              共享 Item Definition
              協調 Release Gate
```

---

## 文化指標（KPI）

| KPI                  | 量測方式          | 目標                     |
| -------------------- | ----------------- | ------------------------ |
| 培訓覆蓋率           | 完訓人數 / 總人數 | ≥ 95%                    |
| 員工資安意識調查分數 | 年度問卷          | 持續上升                 |
| 內部通報事件數       | 員工自主通報      | 持續上升（代表願意通報） |
| 釣魚演練通過率       | 模擬釣魚測試      | ≥ 90%                    |
| Phishing 受害率      | 真實事件          | 持續下降                 |

> [!warning]
> 「通報數量上升」**不必然壞事**——可能代表通報文化建立。應**搭配**其他 KPI 綜合判斷。

---

## 證照考點

> [!important]
>
> - 文化是 ISO 21434 的**規範性要求**（不是建議）
> - 培訓**頻率**：入職 + **定期更新**（通常年度）
> - 培訓**紀錄**是必要 WP
> - 能力管理需有**技能矩陣 + 評鑑 + 紀錄**
> - 跨部門協作是 CSMS 一部分，不是選配

---

## Related Notes

- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]
- [[02-Organizational-Management/03-Management-Systems\|02-Organizational-Management/03-Management-Systems]]
- [[02-Organizational-Management/06-Audit-and-Assessment\|02-Organizational-Management/06-Audit-and-Assessment]]

## Practice

- [[02-Organizational-Management/Practice-CSMS\|02-Organizational-Management/Practice-CSMS]]

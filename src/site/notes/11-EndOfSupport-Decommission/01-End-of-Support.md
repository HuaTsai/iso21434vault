---
{"dg-publish":true,"permalink":"/11-end-of-support-decommission/01-end-of-support/","title":"終止資安支援 (EoS / End of Cybersecurity Support)","tags":["iso-21434","concept-note","end-of-support"],"dg-note-properties":{"title":"終止資安支援 (EoS / End of Cybersecurity Support)","source_pdf":"內部彙整 (ISO 21434 Clause 14)","part":"Clause 14","keywords":["eos","end-of-support","notification","lifecycle-end"],"tags":["iso-21434","concept-note","end-of-support"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> Point in time after which cybersecurity support for a product is no longer provided.

簡言之：「**我們不再修補這個產品的弱點**」的宣告日期。

---

## EoS ≠ 車輛除役

```
EoS：「不再修補資安弱點」
   ↓ 車輛仍可運行
   ↓ 但新弱點不會被處理

Decommissioning：「實際停用 / 報廢」
   ↓ 車輛不再使用
   ↓ 資料清除、PKI 撤銷
```

兩者**不同時間點**——EoS **早於** Decommissioning。

---

## EoS 條件 / 觸發

```
1. 業務決策
   ├── 產品超過商業支援期
   ├── 平台老舊不再開發
   └── 與後續產品重疊

2. 技術不可行
   ├── 元件供應商停產
   ├── 平台太老舊無法繼續支援
   └── 修補成本過高

3. 監管 / 法律
   ├── 召回後決定不再支援
   └── 標準要求重大變動

⚠ 不可任意 EoS：
  ├── 需事前規劃
  ├── 需事前通知
  └── 需有合理過渡期
```

---

## EoS 前的義務

```
1. 通知所有相關方
   ├── 車主 / 使用者
   ├── 經銷商 / 服務廠
   ├── 客戶（OEM-Tier1 關係）
   ├── 監管機構
   └── 供應鏈下游
   提前期：通常至少 6-12 個月（依組織政策）

2. 文件化 EoS 條件
   ├── 確切日期
   ├── 範圍（哪些產品、哪些版本）
   ├── 之後的服務水準（如有 minimal support）
   └── 替代方案 / 升級建議

3. 完成最終更新
   ├── 修補所有已知 High/Critical 弱點
   ├── 最終 Cybersecurity Case 更新
   └── 移交所有紀錄至長期保存

4. 評估殘餘風險
   ├── 失支援後可能的攻擊面變化
   ├── 通知使用者風險
   └── 必要時建議下車 / 更換
```

---

## EoS 通知內容範例

```yaml
eos_notification:
  product: "TCU model X (in vehicles 2018-2022)"
  eos_date: 2030-12-31
  notification_date: 2030-01-15 # 約 1 年前

  notification_recipients:
    - "Affected vehicle owners (via OEM customer mailing)"
    - "Authorized dealers"
    - "Service centers"
    - "Regulatory authorities (UN R155 compliance)"
    - "Auto-ISAC"
    - "Tier-1 supplier (information only)"

  content:
    - "Specific products affected"
    - "EoS date"
    - "What 'EoS' means (no more security patches)"
    - "Recommended actions for users"
    - "Trade-in / Upgrade options"
    - "Continued safety support (functional safety may continue)"
    - "Contact for questions"

  followup:
    - "Reminder at EoS - 3 months"
    - "Reminder at EoS"
    - "Annual security advisory post-EoS (best effort)"
```

---

## 與 ISO 26262 Safety Support 的差異

```
資安支援終止 (EoS - ISO 21434)
   ≠
功能安全支援終止
```

兩者可能**不同步**：

- 資安修補需求大（攻擊持續演變）→ EoS 較早
- 功能安全相對穩定 → 可繼續更長時間

實務上常分別宣告。

---

## 不可預期的 EoS（特殊情境）

```
觸發：
├── 供應商倒閉
├── 重大專利訴訟
├── 法規禁止使用
└── 技術無法持續

處理：
├── 緊急通知
├── 評估安全狀況（是否需召回）
├── 與監管機構協商
└── 加強監控（為使用者）
```

---

## 紀錄保存

> [!important]
> EoS 後**仍需保存**：
>
> - Cybersecurity Case
> - TARA Report
> - 所有 Lessons Learned
> - 客戶通知紀錄
>
> 保存年限依各國法規（通常 10-15 年）。

理由：

- 未來事件回溯
- 法律訴訟可能
- 業界知識共享

---

## EoS 後的「最低支援」（業界實務）

部分 OEM 在 EoS 後仍提供：

- 嚴重弱點的**緊急通報**（即使不修補）
- 對影響**人身安全**的弱點仍嘗試處理
- 提供使用者保護指引（如關閉某功能）

> [!warning]
> 這**不是**正式 ISO 21434 的支援延續，而是 **品牌責任** + **法律考量**。
> 是否提供需在 EoS 通知中明確聲明。

---

## 證照考點

> [!important] 高頻考點
>
> 1. **EoS ≠ Decommissioning**（兩個不同時點）
> 2. EoS 需**事前通知**（典型 6-12 個月）
> 3. EoS 前需修補已知 High/Critical 弱點
> 4. EoS 後 **紀錄仍需保存**
> 5. EoS 後車輛**可繼續運作**，但無新修補
> 6. 通知對象廣泛（含監管機構、車主、供應鏈）
> 7. 與 ISO 26262 Safety EoS **可不同步**

---

## Related Notes

- [[11-EndOfSupport-Decommission/02-Decommissioning\|11-EndOfSupport-Decommission/02-Decommissioning]]
- [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]
- [[02-Organizational-Management/05-Information-Sharing\|02-Organizational-Management/05-Information-Sharing]]

## Practice

- [[11-EndOfSupport-Decommission/Practice-EoS\|11-EndOfSupport-Decommission/Practice-EoS]]

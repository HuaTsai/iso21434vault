---
{"dg-publish":true,"permalink":"/13-annexes-tools/02-mapping-to-un-r155/","title":"對應 UN R155","tags":["iso-21434","concept-note","annex","un-r155","mapping"],"dg-note-properties":{"title":"對應 UN R155","source_pdf":"內部彙整 (UN R155 + ISO 21434 對應)","part":"對應表","keywords":["un-r155","mapping","csms","type-approval"],"tags":["iso-21434","concept-note","annex","un-r155","mapping"],"created":"2026-05-11"}}
---


## 兩者關係概覽

```
UN R155 (法規)
   └── 要求：OEM 須有 CSMS + 車型認證
         └── 不指定具體技術標準
              └── ISO 21434 是事實標準的實作方式
```

---

## R155 §7.2 CSMS Audit 主題 ↔ ISO 21434

| UN R155 要求                   | 對應 ISO 21434 Clause          |
| ------------------------------ | ------------------------------ |
| §7.2.2.1 CSMS 涵蓋整個生命週期 | Clause 5, 6, 8, 13, 14         |
| §7.2.2.2 角色與責任            | Clause 5.4.1 (governance)      |
| §7.2.2.3 風險評估              | **Clause 15 (TARA)**           |
| §7.2.2.4 監控與識別威脅        | **Clause 8**                   |
| §7.2.2.5 弱點管理              | **Clause 8.5, 8.6**            |
| §7.2.2.6 持續改善              | Clause 5.4.7 (audit + improve) |
| §7.2.2.7 供應商管理            | **Clause 7**                   |
| §7.2.2.8 報告與通報            | Clause 8 + 13                  |

---

## R155 §7.3 Vehicle Type Audit 主題 ↔ ISO 21434

| UN R155 要求                  | 對應 ISO 21434 Clause   |
| ----------------------------- | ----------------------- |
| §7.3.3 風險評估 documentation | **Clause 15 + CS Case** |
| §7.3.4 設計階段防護           | **Clause 9, 10**        |
| §7.3.5 滲透測試               | **Clause 11**           |
| §7.3.6 OTA 安全               | Clause 13 (+ UN R156)   |
| §7.3.7 監控能力               | Clause 8                |
| §7.3.8 事件回應               | Clause 13               |

---

## R155 Annex 5 七大威脅類別 ↔ TARA

R155 Annex 5 提供 7 大類、69 條威脅，TARA 中應對應這些威脅或說明不適用：

### 類別 1：Back-end servers

```
威脅範例：
  - 雲端伺服器被入侵
  - 雲端帳號被盜
TARA 對應：
  Asset: 雲端服務
  Threat: 雲端被入侵後對車輛之影響
```

### 類別 2：Communication channels

```
威脅範例：
  - 通訊內容被竊聽
  - MITM
  - DoS
TARA 對應：
  Asset: 通訊鏈
  Threat: 各通訊介面的攻擊
```

### 類別 3：Update procedures

```
威脅範例：
  - 偽造 OTA
  - Rollback 攻擊
TARA 對應：
  Asset: OTA 機制
  Threat: 更新流程的攻擊
```

### 類別 4：Unintended human actions

```
威脅範例：
  - 員工誤操作
  - 社交工程
TARA 對應：
  Asset: 員工權限
  Threat: 社交工程鏈
```

### 類別 5：External connectivity & connections

```
威脅範例：
  - OBD 攻擊
  - USB 攻擊
  - Wi-Fi / Bluetooth 攻擊
TARA 對應：
  Asset: 各對外介面
  Threat: 介面相關攻擊
```

### 類別 6：Vehicle data / code

```
威脅範例：
  - 韌體被反組譯
  - 金鑰被萃取
  - 配置被修改
TARA 對應：
  Asset: 韌體、金鑰、配置
  Threat: 取得 / 修改 vehicle data
```

### 類別 7：Potential vulnerabilities

```
威脅範例：
  - 未修補的已知弱點
  - 過時加密
TARA 對應：
  Asset: 整體軟體
  Threat: 弱點被利用
```

---

## R155 認證流程 ↔ ISO 21434 活動

```
R155 認證階段                    ISO 21434 活動
═══════════════════              ═══════════════
CSMS 認證準備                    建立 CSMS (Clause 5)
   ↓
CSMS 認證稽核 (3 年期)            CSMS Audit (Clause 5.4.7)
   ↓                                ↓
                                  通過後拿 CSMS 證書
   ↓
車型開發階段                      Clause 6-11 全流程
   ↓
車型認證準備                      累積 CS Case
   ↓
車型認證稽核                      Cybersecurity Assessment
                                  + 提交 CS Case
                                  + 提交 TARA Report
                                  + 提交 Pen Test Report
   ↓
車型認證通過                      Release for Post-Development
   ↓
車輛上市                          Operations + Continual (Clause 8, 13)
```

---

## R155 vs R156（再次強調）

> [!warning] 必記
> R155 與 R156 **並列**，不是子集關係。

| 比較     | **UN R155**                      | **UN R156**                      |
| -------- | -------------------------------- | -------------------------------- |
| 主題     | Cybersecurity 整體 + CSMS        | Software Update 流程 + SUMS      |
| 技術依據 | **ISO 21434**                    | **ISO 24089**                    |
| 認證     | CSMS Cert (3 yr) + Type Approval | SUMS Cert (3 yr) + Type Approval |
| 範圍     | 整體車輛資安                     | 軟體更新（OTA + 非 OTA）         |

---

## 各國採用情況（截至 2026-05）

| 地區                                    | R155 採用                                             |
| --------------------------------------- | ----------------------------------------------------- |
| **EU**（27 國 + Norway, Iceland, etc.） | 強制 (2022/07 新車型, 2024/07 所有新車)               |
| **UK**                                  | 強制（British 採 UNECE）                              |
| **Japan**                               | 強制                                                  |
| **South Korea**                         | 強制                                                  |
| **US**                                  | **不直接適用**（有 NHTSA 指引 + voluntary standards） |
| **China**                               | 不直接適用，但有類似法規（GB/T 標準）                 |
| **India / SEA**                         | 部分採用、發展中                                      |

---

## 證照考點

> [!important]
>
> 1. ISO 21434 是 **R155 的事實技術依據**
> 2. R155 **不指定**特定標準（只要 CSMS 充分即可）
> 3. R155 **CSMS 認證有效期 3 年**
> 4. R155 Annex 5 有 **7 大類威脅 + 69 條具體威脅**
> 5. 新車型強制日：**2022-07**；所有新車：**2024-07**
> 6. R155 與 R156 **並列**

---

## Related Notes

- [[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]
- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]
- [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]
- [[00-Dashboard/Exam-Traps#Trap 8\|00-Dashboard/Exam-Traps#Trap 8]]
- [[00-Dashboard/Quick-Reference#十、與 UN R155 / R156 / ISO 26262 對照\|00-Dashboard/Quick-Reference#十、與 UN R155 / R156 / ISO 26262 對照]]

---
{"dg-publish":true,"permalink":"/13-annexes-tools/01-cal-cybersecurity-assurance-level/","title":"資安保證等級 (CAL / Cybersecurity Assurance Level)","tags":["iso-21434","concept-note","annex","cal"],"dg-note-properties":{"title":"資安保證等級 (CAL / Cybersecurity Assurance Level)","source_pdf":"內部彙整 (ISO 21434 Annex E)","part":"Annex E","keywords":["cal","assurance-level","annex-e"],"tags":["iso-21434","concept-note","annex","cal"],"created":"2026-05-11"}}
---


## 定義

> [!quote]
> Level that specifies rigor of cybersecurity activities and provides assurance that residual cybersecurity risk is acceptable.

簡言之：「**做資安活動有多嚴謹**」的等級。

---

## 屬性：**Informative**（非強制）

> [!warning] 必記
> ISO 21434 **Annex E 為 informative**（資訊性，非規範性）。
> CAL **不強制**使用。
>
> 但業界部分組織（特別是大 OEM）採用以提供「**保證等級**」與 ISO 26262 ASIL 對應。

---

## 四個等級

| 等級      | 嚴謹度 | 適用                       |
| --------- | ------ | -------------------------- |
| **CAL 1** | 基本   | 低 Impact 或物理接觸限制   |
| CAL 2     | 中等   | 中度保護                   |
| CAL 3     | 高     | 主要安全相關功能           |
| **CAL 4** | 最高   | 極嚴重 Impact + 遠端攻擊面 |

---

## 推導：Impact + Attack Vector

> [!important]
> **CAL = f(Impact, Attack Vector)**
>
> 注意：**不是** Attack Feasibility！是 Attack Vector（攻擊向量）。

```
        Attack Vector →
            Network  Adjacent  Local  Physical
Impact ↓
Severe       CAL-4   CAL-4    CAL-3   CAL-2
Major        CAL-3   CAL-3    CAL-2   CAL-2
Moderate     CAL-2   CAL-2    CAL-1   CAL-1
Negligible   CAL-1   CAL-1    CAL-1   CAL-1
```

### Attack Vector 定義

| Vector       | 描述         | 範例                 |
| ------------ | ------------ | -------------------- |
| **Network**  | 任何網路可達 | 蜂巢、雲端、Wi-Fi    |
| **Adjacent** | 受限網路     | V2X、藍牙            |
| **Local**    | 本地需執行   | 已登入帳號、本機軟體 |
| **Physical** | 物理接觸     | OBD、JTAG、開殼      |

---

## CAL 影響的活動嚴謹度

```
CAL 越高 → 越嚴謹的：

├── TARA 分析深度
│   └── CAL 4: 多輪 review + 攻擊樹 + 旁通道考量
│   └── CAL 1: 基本分析
│
├── Cybersecurity Goals 數量與細度
│   └── CAL 4: 細到 sub-system
│   └── CAL 1: 高層級
│
├── 程式碼 Review 嚴格度
│   └── CAL 4: 100% review + 形式化方法
│   └── CAL 1: 採樣
│
├── SAST / Fuzz 涵蓋度
│   └── CAL 4: 完整 + 多工具
│   └── CAL 1: 主流工具
│
├── Pen Test 強度
│   └── CAL 4: 多輪 + 紅隊 + 外部
│   └── CAL 1: 一次內部
│
├── 獨立性要求
│   └── CAL 4: 強制外部
│   └── CAL 1: 內部即可
│
├── CS Case 詳盡度
│   └── CAL 4: 形式化 GSN
│   └── CAL 1: 基本論證
│
└── Tailoring 限制
    └── CAL 4: 嚴格，幾乎不可裁適
    └── CAL 1: 較彈性
```

---

## CAL 與 ASIL 對照（**最常考陷阱**）

> [!warning]
> **CAL 4 ≠ ASIL D**
> **CAL ≠ ASIL（任何對應關係都不成立）**

| 比較     | **CAL**                       | **ASIL**                          |
| -------- | ----------------------------- | --------------------------------- |
| 全名     | Cybersecurity Assurance Level | Automotive Safety Integrity Level |
| 標準     | ISO 21434 (Annex E)           | ISO 26262                         |
| 領域     | 資安                          | 功能安全                          |
| 等級     | CAL 1-4                       | QM, A-D                           |
| 推導因子 | Impact + Attack Vector        | S × E × C                         |
| 性質     | 保證等級                      | 完整性等級                        |
| 強制性   | **非強制** (informative)      | 通常為標準/法規需求               |

**為何不能對應**：

- ASIL D 系統可能 CAL 低（如純內部安全機制，無連網）
- CAL 4 系統可能 ASIL 低（如純隱私資料，無 safety 影響）

→ [[00-Dashboard/Exam-Traps#Trap 2\|00-Dashboard/Exam-Traps#Trap 2]]

---

## CAL 範例

### 範例 A：TCU 蜂巢介面韌體完整性

```yaml
asset: "TCU Firmware"
threat_scenario: "Remote firmware tampering via cellular"

impact: Severe (safety + financial + operational)
attack_vector: Network

cal: CAL-4
implications:
  - "Most rigorous TARA"
  - "Multiple pen tests required"
  - "External independent assessment"
  - "Formal CS Case"
```

### 範例 B：診斷服務通訊

```yaml
asset: "Diagnostic data"
threat_scenario: "Read diagnostic data without authorization"

impact: Moderate (privacy + operational)
attack_vector: Local (need OBD physical access)

cal: CAL-1
implications:
  - "Basic TARA"
  - "Standard verification"
```

### 範例 C：BMS 電池資料完整性

```yaml
asset: "Battery State of Charge"
threat_scenario: "Manipulate SoC reading"

impact: Major (safety risk if SoC misrepresentation causes overcharge)
attack_vector: Local (need access to battery CAN)

cal: CAL-2
implications:
  - "Moderate rigor"
  - "Pen test focused on local attack"
```

---

## 業界採用情況

| 採用情況     | 描述                                |
| ------------ | ----------------------------------- |
| **強烈採用** | 部分 OEM 將 CAL 內化為強制          |
| **部分採用** | 用於高 Impact 元件                  |
| **不採用**   | 改用其他保證機制（如 CC EAL）       |
| **替代方案** | Common Criteria EAL、自訂 framework |

> [!tip]
> 證照考試**通常測**：CAL 是什麼、屬性、推導因子、與 ASIL 區別。
> **不會考**：具體某廠商如何採用。

---

## CAL 在 CIA 中的角色

跨組織開發時：

- 雙方應在 CIA 中**對齊 CAL 期望**
- 不對齊會導致：
  - Tier-1 做過度嚴謹（成本高）
  - 或不足嚴謹（OEM 不接受）

---

## 證照考點

> [!important] 必記
>
> 1. **CAL 是 Annex E**，**informative**
> 2. CAL 等級：**1-4**
> 3. 推導：**Impact + Attack Vector**（不是 Feasibility）
> 4. **CAL ≠ ASIL**（最易考錯）
> 5. **非強制**使用
> 6. 影響活動的**嚴謹度**（深度、獨立性、覆蓋度）

---

## Related Notes

- [[12-TARA-Methods/08-Risk-Treatment\|12-TARA-Methods/08-Risk-Treatment]]
- [[01-Foundations/03-Cybersecurity-vs-Safety\|01-Foundations/03-Cybersecurity-vs-Safety]]
- [[00-Dashboard/Exam-Traps#Trap 2\|00-Dashboard/Exam-Traps#Trap 2]]
- [[00-Dashboard/Quick-Reference#七、CAL：Cybersecurity Assurance Level（Annex E）\|00-Dashboard/Quick-Reference#七、CAL：Cybersecurity Assurance Level（Annex E）]]

## Practice

- [[12-TARA-Methods/Practice-TARA\|12-TARA-Methods/Practice-TARA]]

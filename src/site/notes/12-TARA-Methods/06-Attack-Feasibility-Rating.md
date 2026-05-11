---
{"dg-publish":true,"permalink":"/12-tara-methods/06-attack-feasibility-rating/","title":"攻擊可行性評等 (Attack Feasibility Rating)","tags":["iso-21434","concept-note","tara","attack-feasibility"],"dg-note-properties":{"title":"攻擊可行性評等 (Attack Feasibility Rating)","source_pdf":"內部彙整 (ISO 21434 Clause 15.7 + Annex G)","part":"Clause 15.7","keywords":["attack-feasibility","attack-potential","cvss"],"tags":["iso-21434","concept-note","tara","attack-feasibility"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> Attribute that describes the ease of successfully carrying out an attack path.

簡言之：「**攻擊**這條路徑**有多容易**？」

---

## 三種評估方法（Annex G，**informative**）

ISO 21434 **Annex G 為 informative**（資訊性，非強制）。組織可選用以下方法之一或自訂等效方法，分數值與閾值皆可在 CSMS 中自訂：

| 方法                       | 來源                            | 特色                           |
| -------------------------- | ------------------------------- | ------------------------------ |
| **Attack Potential-based** | Common Criteria (ISO/IEC 18045) | 業界**最常用**，本筆記主要描述 |
| **CVSS-based**             | NIST CVSS                       | 對應已知 CVE                   |
| **Attack Vector-based**    | 攻擊向量導向                    | 簡化評估                       |

> [!important]
> 三種方法**選一個**，但**全公司一致**使用同一方法。

---

## Attack Potential 方法（**重點**）

### 五大評估參數

```yaml
attack_potential_parameters: 1. Elapsed Time         流逝時間（攻擊需多久）
  2. Specialist Expertise 專家能力（需多高技能）
  3. Knowledge of Item    標的知識（需多深了解）
  4. Window of Opportunity 機會窗口（有多少時間/機會）
  5. Equipment            設備（需要什麼工具）
```

每個參數有分數，**加總**後對應 Feasibility 等級。

---

### 1. Elapsed Time（流逝時間）

| 攻擊所需時間 | 分數 |
| ------------ | ---- |
| < 1 day      | 0    |
| < 1 week     | 1    |
| < 1 month    | 4    |
| < 6 months   | 17   |
| > 6 months   | 19   |

> [!tip]
> 此參數是**攻擊**所需時間，不是偵測時間。

---

### 2. Specialist Expertise（專家能力）

| 攻擊者能力                  | 分數 |
| --------------------------- | ---- |
| Layman 業餘                 | 0    |
| Proficient 熟手             | 3    |
| Expert 專家                 | 6    |
| Multiple Experts 多專家團隊 | 8    |

> 「Multiple Experts」指需要**多個專家領域協作**（如硬體 + 軟體 + 密碼）。

---

### 3. Knowledge of Item（標的知識）

| 攻擊者需要的內部資訊              | 分數 |
| --------------------------------- | ---- |
| Public 公開資訊                   | 0    |
| Restricted 受限資訊（如付費取得） | 3    |
| Sensitive 敏感資訊（如 NDA）      | 7    |
| Critical 機密資訊（如核心 IP）    | 11   |

> 公開資訊：規格、Datasheet 等
> 機密資訊：原始碼、設計細節

---

### 4. Window of Opportunity（機會窗口）

| 攻擊可達機會                  | 分數     |
| ----------------------------- | -------- |
| Unlimited 隨時可達            | 0        |
| Easy 容易（如車主存取）       | 1        |
| Moderate 中等（如服務廠存取） | 4        |
| Difficult 困難                | 10       |
| None 不可達                   | (不可行) |

> Unlimited 範例：網路接觸（任何時間）
> Difficult 範例：晶片廠內接觸

---

### 5. Equipment（設備）

| 需要的設備                               | 分數 |
| ---------------------------------------- | ---- |
| Standard 標準（PC、軟體）                | 0    |
| Specialized 專用（CAN tool、邏輯分析儀） | 4    |
| Bespoke 客製（FPGA、特殊探針）           | 7    |
| Multiple Bespoke 多組客製                | 9    |

---

### 總分對應 Feasibility 等級

> [!warning] ⚠ 易混淆陷阱
> **分數越高 = 越困難**（攻擊代價越高）
> **分數越低 = 越容易**（攻擊代價越低）
>
> 命題單位最愛測這個方向！

| Total Score | Attack Potential Level | **Attack Feasibility** |
| ----------- | ---------------------- | ---------------------- |
| 0 – 13      | Basic                  | **High** (容易)        |
| 14 – 19     | Enhanced-Basic         | **Medium**             |
| 20 – 24     | Moderate               | **Low**                |
| ≥ 25        | High / Beyond High     | **Very Low**           |

> [!note]
> ISO 21434 Annex G 採用**四級**系統（High / Medium / Low / Very Low）。Common Criteria (ISO/IEC 18045) 才有「Beyond High = infeasible」第五級的延伸；ISO 21434 文件本身不使用此第五級。
> 若採用 Annex G **informative** 表，組織也可在 CSMS 中自訂閾值。

> [!tip] 記憶法
> 「**分數是攻擊代價，代價越高 → Feasibility 越低**」

---

## 評估範例

### 範例 A：OBD 物理 CAN 注入

```yaml
attack_path: "Physical CAN injection via OBD-II"

parameters:
  elapsed_time: 1 # < 1 week
  expertise: 3 # Proficient (CAN 知識)
  knowledge: 3 # Restricted (vehicle CAN DB)
  window: 1 # Easy (OBD 開放)
  equipment: 4 # Specialized (CAN tool)

total_score: 12
attack_feasibility: High (容易)
```

### 範例 B：HSM 旁通道萃取金鑰

```yaml
attack_path: "DPA on HSM RSA signing operation"

parameters:
  elapsed_time: 17 # < 6 months
  expertise: 8 # Multiple Experts (crypto + HW)
  knowledge: 11 # Critical (HSM internals)
  window: 10 # Difficult (need controlled env)
  equipment: 9 # Multiple Bespoke (DPA equipment)

total_score: 55
attack_feasibility: Very Low (極困難)
```

### 範例 C：雲端釣魚取得 OTA 簽章金鑰

```yaml
attack_path: "Spear phishing OEM signing engineer → key theft"

parameters:
  elapsed_time: 4 # < 1 month (含偵察 + 釣魚 + 滲透)
  expertise: 6 # Expert (social eng + lateral movement)
  knowledge: 3 # Restricted (員工資料部分公開)
  window: 0 # Unlimited (隨時可發起)
  equipment: 0 # Standard (PC + 社交工程)

total_score: 13
attack_feasibility: High (容易)  ← 注意：技術簡單但仍可怕
```

> [!tip]
> 範例 C 啟示：**社交工程**通常 feasibility 高，因為技術成本低。

---

## CVSS-based 方法（簡介）

```
CVSS v3 Base Score → 對應 Feasibility

CVSS 9.0–10.0 → Very High (容易)
CVSS 7.0–8.9  → High
CVSS 4.0–6.9  → Medium
CVSS 0.1–3.9  → Low
```

適用於**已知 CVE 對應**情境。

---

## Attack Vector-based 方法（簡介）

```
依攻擊向量分類，每類給定 default feasibility：
- Network         → High
- Adjacent Network → Medium-High
- Local           → Medium
- Physical        → Low

加上其他因素調整。
```

簡化方法，適合**早期粗評**。

---

## Feasibility 評估的「保守原則」

> [!warning]
> 評估時若不確定，**往容易那邊估**（保守）。
>
> 理由：低估攻擊容易度 → 低估風險 → 防護不足。

---

## 證照考點

> [!important] 高頻考點
>
> 1. **三種方法**：Attack Potential / CVSS / Attack Vector（記得有三種）
> 2. **Attack Potential 五大參數**：Time / Expertise / Knowledge / Window / Equipment
> 3. **分數高 → Feasibility 低**（最常考陷阱！）
> 4. 對應表：0-13 → High，≥25 → Very Low
> 5. 評估**最容易**的那條 Attack Path
> 6. 保守原則：不確定 → 估容易那邊
> 7. **社交工程**通常 feasibility 高（被忽略的點）

---

## Related Notes

- [[12-TARA-Methods/05-Attack-Path-Analysis\|12-TARA-Methods/05-Attack-Path-Analysis]]
- [[12-TARA-Methods/07-Risk-Determination\|12-TARA-Methods/07-Risk-Determination]]
- [[00-Dashboard/Exam-Traps#Trap 3\|00-Dashboard/Exam-Traps#Trap 3]]
- [[00-Dashboard/Quick-Reference#四、Attack Feasibility 五大參數（Annex G）\|00-Dashboard/Quick-Reference#四、Attack Feasibility 五大參數（Annex G）]]

## Practice

- [[12-TARA-Methods/Practice-TARA\|12-TARA-Methods/Practice-TARA]]

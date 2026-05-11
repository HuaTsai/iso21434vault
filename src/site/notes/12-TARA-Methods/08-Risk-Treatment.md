---
{"dg-publish":true,"permalink":"/12-tara-methods/08-risk-treatment/","title":"風險處置 (Risk Treatment) + CAL","tags":["iso-21434","concept-note","tara","risk-treatment","cal"],"dg-note-properties":{"title":"風險處置 (Risk Treatment) + CAL","source_pdf":"內部彙整 (ISO 21434 Clause 15.9 + Annex E)","part":"Clause 15.9","keywords":["risk-treatment","avoid","reduce","transfer","retain","cal"],"tags":["iso-21434","concept-note","tara","risk-treatment","cal"],"created":"2026-05-11"}}
---


## 四大處置選項

ISO 21434 採用業界標準的 **4T** 模型：

| 選項               | 英文   | 中文 | 適用                   |
| ------------------ | ------ | ---- | ---------------------- |
| **A**void          | Avoid  | 避免 | 移除功能/設計變更      |
| **R**educe         | Reduce | 降低 | 加入資安控制（最常見） |
| **S**hare/Transfer | Share  | 轉移 | 給供應商、保險         |
| **R**etain         | Retain | 保留 | 接受作為殘餘風險       |

> [!tip] 記憶法
> **AR-ST 或「避降轉留」**

---

## 1. Avoid（避免）

```
策略：移除產生風險的功能 / 設計

例子：
  ├── 移除 OBD-II 對外的某些診斷功能
  ├── 移除遠端解鎖功能
  ├── 改用單向通訊（攻擊面變小）
  └── 不提供某 over-the-internet 功能

優點：徹底消除風險
缺點：可能犧牲功能性、商業價值

適用情境：
  └── 高風險 + 修補成本不合理 + 功能可省
```

---

## 2. Reduce（降低）

```
策略：加入資安控制以降低 attack feasibility 或 impact

例子：
  ├── 加入 SecOC 防 CAN 訊息偽造
  ├── 加入 TLS + Cert Pinning 防 MITM
  ├── 加入 HSM 保護金鑰
  ├── 加入 IDS 偵測異常
  └── 加入 anti-rollback 防降級

優點：在保留功能下降低風險
缺點：增加成本、複雜度、效能影響

適用情境：
  └── 大多數 High/Very High 風險的預設選項
```

---

## 3. Share / Transfer（轉移）

```
策略：將風險（或部分）轉移給他方

兩種方式：

A. 合約轉移（CIA 中明定）
   └── 「此風險由 Tier-1 處置」
   └── 但 **法律責任不可完全轉移**（OEM 仍對車主負責）

B. 保險
   └── 對財務影響有效
   └── 對 Safety 影響無效

例子：
  ├── HSM 由專業 Tier-2 提供 + 保證
  ├── 加密實作由 trusted 函式庫
  ├── 雲端基礎設施由 AWS/Azure 提供
  └── 召回保險

注意：
  └── Share 後仍需**驗證**對方確實處置
  └── 不是「丟給對方就忘了」
```

---

## 4. Retain（保留 / 接受）

```
策略：接受風險，不採取行動

條件：
  ✓ Risk Value 較低（通常 1-2）
  ✓ 處置成本不對等
  ✓ **適當層級**簽核接受
  ✓ 文件化於 CS Case
  ✓ 持續監控

絕對不可：
  ✗ 為了趕進度而 Retain High 風險
  ✗ Project Manager 私自決定接受
  ✗ 無文件化
  ✗ 不再監控

範例 OK：
  └── 「HSM DPA 攻擊 (feasibility Very Low) — 接受並監控」

範例 NOT OK：
  └── 「OTA 攻擊 High Risk — 因為時間不夠，接受」
```

---

## 處置決策矩陣（業界實務）

```
                Attack Feasibility →
                Very Low  Low    Medium   High
Impact ↓     ┌────────┬────────┬───────┬────────┐
Severe       │ Retain │ Reduce │Reduce │ Reduce │
             │ (with  │        │       │ /Avoid │
             │ monitor)│        │       │        │
             ├────────┼────────┼───────┼────────┤
Major        │ Retain │ Retain │Reduce │ Reduce │
             │        │        │       │        │
             ├────────┼────────┼───────┼────────┤
Moderate     │ Retain │ Retain │Retain │ Reduce │
             │        │        │       │        │
             ├────────┼────────┼───────┼────────┤
Negligible   │ Retain │ Retain │Retain │ Retain │
             └────────┴────────┴───────┴────────┘
```

> 實務上組織會自訂這個矩陣。

---

## 處置決策的接受層級

| 風險值        | 接受層級（建議）           |
| ------------- | -------------------------- |
| 5 (Very High) | **VP / CTO 或更高**        |
| 4 (High)      | **VP / Director**          |
| 3 (Medium)    | **CS Manager 或 Director** |
| 1-2 (Low)     | CS Engineer / Manager      |

> [!warning]
> 不可由 **過低層級** 接受高風險——是 Cybersecurity Assessment 必看的事。

---

## 殘餘風險 (Residual Risk)

```
Initial Risk
       ↓
   風險處置
       ↓
Residual Risk = 處置後仍剩的風險
       ↓
   需文件化於 CS Case
   需適當層級接受
   需持續監控
```

---

## CAL — Cybersecurity Assurance Level (Annex E)

> [!important]
> **CAL 屬性**：
>
> - **Informative**（Annex E 為 informative）
> - **不強制**使用
> - 業界部分組織採用
> - 等同 ISO 26262 ASIL 的角色但**獨立**

### CAL 推導

```
CAL 由 Impact + Attack Vector 推導

           Attack Vector →
            Network  Adjacent  Local  Physical
Impact ↓
Severe      CAL-4   CAL-4    CAL-3   CAL-2
Major       CAL-3   CAL-3    CAL-2   CAL-2
Moderate    CAL-2   CAL-2    CAL-1   CAL-1
Negligible  CAL-1   CAL-1    CAL-1   CAL-1
```

### CAL 等級含義

| CAL       | 嚴格度 | 應用                   |
| --------- | ------ | ---------------------- |
| **CAL 4** | 最嚴格 | 嚴重 Impact + 遠端可達 |
| CAL 3     | 高     | 主要安全相關           |
| CAL 2     | 中     | 一般保護               |
| CAL 1     | 基本   | 最低保護               |

### CAL 影響哪些活動的嚴謹度

```
高 CAL → 更嚴謹的：
  ├── TARA 分析深度
  ├── Pen Test 強度
  ├── 程式碼 review
  ├── SAST/Fuzz 嚴格度
  ├── 獨立性要求
  └── CS Case 詳盡度
```

---

## CAL vs ASIL（再次強調）

> [!warning]
> **CAL ≠ ASIL**（命題單位最愛測！）

| 項目   | **CAL**                      | **ASIL**      |
| ------ | ---------------------------- | ------------- |
| 標準   | ISO 21434                    | ISO 26262     |
| 領域   | 資安                         | 功能安全      |
| 推導   | Impact + Attack Vector       | S × E × C     |
| 等級   | 1-4                          | A-D + QM      |
| 強制性 | 非強制 (Annex E informative) | 標準/法規常需 |

→ [[00-Dashboard/Exam-Traps#Trap 2\|00-Dashboard/Exam-Traps#Trap 2]]

---

## Risk Treatment Decision 紀錄

```yaml
risk_treatment:
  id: RT-TCU-005
  risk_ref: RR-TCU-005 (Risk Value 5)

  decision: Reduce

  rationale: >
    Brake command spoofing has Severe safety impact.
    High feasibility (CAN injection via OBD).
    Avoidance not feasible (function is required).
    Transfer not applicable (safety responsibility cannot transfer).
    Retain not acceptable (too high risk).
    Conclusion: Reduce via SecOC + OBD authentication.

  controls:
    - "Implement SecOC on all safety-critical CAN messages"
    - "Add OBD Security Access for diagnostic write commands"
    - "Add CAN IDS for anomaly detection"

  expected_residual_risk:
    feasibility_after_control: Low
    new_risk_value: 3 (Medium)

  residual_risk_decision: "Acceptable with monitoring"
  accepted_by: "VP Engineering"
  accepted_date: 2026-10-01

  cs_goals_created:
    - CG-008: "Authenticity of safety-critical CAN messages"
    - CG-009: "Authorization of diagnostic write commands"

  cal_level: CAL-3 # informative
```

---

## 證照考點

> [!important] 高頻考點
>
> 1. **四大處置選項**：Avoid / Reduce / Transfer / Retain
> 2. **不可** Retain High Risk 為了趕進度
> 3. **殘餘風險**需文件化 + 適當層級接受
> 4. **接受層級**對應風險等級（高風險高層級）
> 5. **CAL ≠ ASIL**（最重要陷阱）
> 6. CAL 由 **Impact + Attack Vector** 推導
> 7. CAL 是 **informative**，不強制
> 8. Share/Transfer 後仍需**驗證對方履行**

---

## Related Notes

- [[12-TARA-Methods/07-Risk-Determination\|12-TARA-Methods/07-Risk-Determination]]
- [[13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level\|13-Annexes-Tools/01-CAL-Cybersecurity-Assurance-Level]]
- [[05-Continual-Cybersecurity/04-Vulnerability-Management\|05-Continual-Cybersecurity/04-Vulnerability-Management]]
- [[03-Project-Dependent/07-Release-for-Post-Development\|03-Project-Dependent/07-Release-for-Post-Development]]
- [[00-Dashboard/Exam-Traps#Trap 2\|00-Dashboard/Exam-Traps#Trap 2]]
- [[00-Dashboard/Quick-Reference#六、風險處置 4 種選項\|00-Dashboard/Quick-Reference#六、風險處置 4 種選項]]

## Practice

- [[12-TARA-Methods/Practice-TARA\|12-TARA-Methods/Practice-TARA]]

---
{"dg-publish":true,"permalink":"/13-annexes-tools/04-attack-trees/","title":"攻擊樹 (Attack Trees)","tags":["iso-21434","concept-note","annex","attack-tree"],"dg-note-properties":{"title":"攻擊樹 (Attack Trees)","source_pdf":"內部彙整 (業界方法 + 21434 應用)","part":"補充工具","keywords":["attack-tree","threat-modeling","schneier"],"tags":["iso-21434","concept-note","annex","attack-tree"],"created":"2026-05-11"}}
---


> [!quote]
> 由 Bruce Schneier 於 1999 提出的威脅建模方法。
> 在 ISO 21434 中常作為 **TARA Step 4 (Attack Path Analysis)** 的工具。

---

## 基本結構

```
                Root Goal
            （攻擊者最終目標）
                   │
        ┌──────────┼──────────┐
        │          │          │
       Sub      Sub        Sub
      Goal 1   Goal 2     Goal 3
        │          │          │
    ┌───┴───┐ ┌───┴───┐ ┌────┴────┐
    │       │ │       │ │         │
   Leaf  Leaf Leaf  Leaf Leaf   Leaf
   (具體攻擊步驟)
```

---

## 邏輯閘 (Gates)

### OR Gate（任一即可）

```
       Goal
        │
       OR
      / | \
     A  B  C    ← 任一 A、B、C 成功即達 Goal
```

範例：「取得韌體」

- OR
- OR：從 device 萃取
- OR：從建置伺服器竊取
- OR：從供應商取得

### AND Gate（全部需要）

```
       Goal
        │
      AND
      / | \
     A  B  C    ← 必須 A、B、C 全部成功
```

範例：「成功 OTA 攻擊」

- AND：取得簽章金鑰
- AND：建構惡意韌體
- AND：上傳至 OTA 系統
- AND：觸發部署

---

## Attack Tree 範例：竊取 V2X 私鑰

```
                  竊取 V2X 私鑰
                      │
                    (OR)
            ┌─────────┼─────────┐
            │         │         │
       軟體攻擊   硬體攻擊   社交工程
            │         │         │
          (OR)      (AND)     (OR)
          / │ \    /  │  \    / │
     RCE 弱點   開殼  探針  DPA  釣魚 賄賂
     利用  繞    取出  讀取  分析  員工 員工
     過    過    晶片  訊號
     簽章
```

每個葉節點（Leaf）為「**具體攻擊步驟**」，可進一步評估 feasibility。

---

## 葉節點屬性

```yaml
leaf_node:
  name: "DPA on HSM RSA signing"

  attack_potential:
    elapsed_time: 17
    expertise: 8
    knowledge: 11
    window: 10
    equipment: 9
    total: 55
    feasibility: Very Low

  cost_estimate: "$100K equipment + 6 months work"

  preconditions:
    - "Physical access to operating HSM"
    - "Capability to capture power traces"

  defense_in_place:
    - "First-order DPA countermeasures"
    - "Tamper-evident enclosure"
```

---

## 計算 Root Goal 的 Feasibility

```
OR 閘：
  Root feasibility = max(children feasibility)
  → 取最容易的子節點

AND 閘：
  Root feasibility = min(children feasibility)
  → 受最難的子節點限制
```

範例：

```
                Goal
                 │
                AND
                / \
             A     B
        (High)  (Very Low)

→ Goal feasibility = Very Low（受 B 限制）
```

---

## Attack Tree 的優點

```
✓ 視覺化（易理解）
✓ 分解複雜攻擊
✓ 識別「最弱環節」（OR 中最容易那個）
✓ 識別「必要環節」（AND 中所有子節點都需防護）
✓ 易於與利害關係人溝通
✓ 可量化（每節點賦予分數）
✓ 可作為 Pen Test 的指引
```

---

## Attack Tree 的限制

```
✗ 大型樹難維護
✗ 不適合「未知未知」攻擊
✗ 與真實攻擊鏈差距（攻擊者不一定走最容易路徑）
✗ 主觀（樹結構依分析者經驗）
```

> [!tip]
> 解決方式：與 STRIDE、UN R155 Annex 5、CVE 資料庫**互補**使用。

---

## 工具支援

| 工具                               | 特色                        |
| ---------------------------------- | --------------------------- |
| **AttackTree+**                    | 商業，與其他 Risk Mgmt 整合 |
| **Microsoft Threat Modeling Tool** | 免費 + STRIDE               |
| **OWASP Threat Dragon**            | 開源、Web 介面              |
| **AndroVulnerability/SecuriTree**  | 學術                        |
| **Graphviz / PlantUML**            | 文字繪圖（如本筆記範例）    |
| **Excel / 手繪**                   | 小型專案                    |

---

## Attack Tree 範本（PlantUML 格式）

```
@startuml
skinparam rectangle {
  BackgroundColor #FFE0B2
}

rectangle "Remote firmware tampering" as ROOT
rectangle "OR Gate" as OR1

rectangle "Compromise OTA server" as A1
rectangle "AND Gate" as AND1
rectangle "Phishing" as A1a
rectangle "Lateral movement" as A1b
rectangle "Privilege escalation" as A1c

rectangle "Compromise signing key" as A2
rectangle "OR Gate" as OR2
rectangle "Insider threat" as A2a
rectangle "DPA on HSM" as A2b
rectangle "Memory dump" as A2c

rectangle "Bypass signature check" as A3
rectangle "Exploit verification bug" as A3a

ROOT --> OR1
OR1 --> A1
OR1 --> A2
OR1 --> A3

A1 --> AND1
AND1 --> A1a
AND1 --> A1b
AND1 --> A1c

A2 --> OR2
OR2 --> A2a
OR2 --> A2b
OR2 --> A2c

A3 --> A3a

@enduml
```

---

## 與 TARA 八步驟的關係

```
TARA Step 4: Attack Path Analysis
   └── 工具：Attack Tree（主要）

TARA Step 5: Attack Feasibility
   └── 評估每個葉節點

TARA Step 6: Risk Determination
   └── 取最低樹路徑的 feasibility 對應 Impact
```

---

## 證照考點

> [!important]
>
> 1. Attack Tree 是 **業界方法**，ISO 21434 不強制
> 2. **OR 閘** vs **AND 閘** 的計算方式
> 3. OR 取**最容易**子節點；AND 受**最難**子節點限制
> 4. 適合 TARA Step 4 (Attack Path Analysis)
> 5. 與 STRIDE、CVE 等方法**互補**使用

---

## Related Notes

- [[12-TARA-Methods/05-Attack-Path-Analysis\|12-TARA-Methods/05-Attack-Path-Analysis]]
- [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]
- [[13-Annexes-Tools/03-STRIDE-DREAD\|13-Annexes-Tools/03-STRIDE-DREAD]]

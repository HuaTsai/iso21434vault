---
{"dg-publish":true,"permalink":"/12-tara-methods/05-attack-path-analysis/","title":"攻擊路徑分析 (Attack Path Analysis)","tags":["iso-21434","concept-note","tara","attack-path"],"dg-note-properties":{"title":"攻擊路徑分析 (Attack Path Analysis)","source_pdf":"內部彙整 (ISO 21434 Clause 15.6)","part":"Clause 15.6","keywords":["attack-path","attack-tree","kill-chain"],"tags":["iso-21434","concept-note","tara","attack-path"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> Sequence of deliberate actions to realize a threat scenario.

簡言之：「**攻擊者要實現 threat，需要走哪些步驟**？」

---

## 為什麼需要分析路徑？

```
不同攻擊路徑 → 不同 attack feasibility
   ├── 路徑短 + 容易 → 高 feasibility
   ├── 路徑長 + 困難 → 低 feasibility
   └── 路徑多 → 攻擊者選最易者
```

> [!important]
> 同一個 Threat Scenario 可能有**多條 Attack Path**。
> Attack Feasibility 採用**最容易**的那條來評估（攻擊者最壞情境）。

---

## 表達方式

### 1. 線性 Attack Path

```
TS-001：Remote firmware tampering

Attack Path AP-001：
Step 1: 取得 OEM 員工釣魚機會
   ↓
Step 2: 用釣魚 email 取得內網存取
   ↓
Step 3: Lateral movement 至 OTA 系統
   ↓
Step 4: 提權至 OTA 簽章權限
   ↓
Step 5: 簽署惡意韌體
   ↓
Step 6: 觸發 OTA 部署
   ↓
Step 7: 車輛接收並安裝
   ↓
威脅實現
```

### 2. Attack Tree（攻擊樹）

```
                    Tamper Firmware
                          │
              ┌───────────┼───────────┐
              │           │           │
          (OR Gate)   (OR Gate)   (OR Gate)
              │           │           │
         Online      Physical    Supply Chain
        Attack       Attack       Attack
              │           │           │
         ┌────┴────┐  ┌───┴───┐  ┌───┴────┐
         │         │  │       │  │        │
       OTA      Cloud  JTAG   Flash  Inject  Bribe
       MITM     Server Debug  Chip   into    Tier-2
                Pwn    Open   off    Build
```

**AND vs OR gates**：

- OR：任一子路徑成功即可
- AND：所有子路徑都需成功

### 3. Kill Chain Style

```
1. Reconnaissance       （偵察）
2. Weaponization        （武器化）
3. Delivery             （送達）
4. Exploitation         （利用）
5. Installation         （安裝）
6. Command & Control    （遙控）
7. Actions on Objectives（達成目標）
```

源自軍事 Kill Chain，可用於描述 APT 攻擊。

---

## Attack Path 紀錄範本

```yaml
attack_path:
  id: AP-TCU-007-A
  threat_scenario: TS-TCU-007 (Remote firmware tampering)

  description: >
    Attacker compromises OEM OTA backend via supply chain attack,
    then signs and pushes malicious firmware to fleet.

  attacker_profile:
    location: "Remote (internet)"
    capability: "Expert (organized group)"
    motivation: "Mass disruption"
    resources: "Significant (state-level or organized crime)"

  prerequisites:
    - "OTA server has internet exposure"
    - "Build pipeline accessible from internet (even indirectly)"
    - "Vehicles accept signed firmware"

  steps:
    - step: 1
      action: "Identify OEM OTA infrastructure (recon)"
      effort: low
      detection_likelihood: low

    - step: 2
      action: "Supply chain attack on CI/CD vendor"
      effort: very_high
      detection_likelihood: medium

    - step: 3
      action: "Insert malicious code into build pipeline"
      effort: high
      detection_likelihood: high (if integrity monitoring)

    - step: 4
      action: "Wait for next firmware build → signed automatically"
      effort: low
      detection_likelihood: low

    - step: 5
      action: "Firmware deployed via OTA"
      effort: none (automated)
      detection_likelihood: medium (if telemetry monitored)

    - step: 6
      action: "Activate payload in vehicles"
      effort: low
      detection_likelihood: high (after fact)

  estimated_total_effort: very_high
  expertise_required: expert
  knowledge_required: highly_specific
  equipment_required: standard + access
  time_required: months_to_years

  alternative_paths:
    - id: AP-TCU-007-B
      description: "Compromise signing key directly"
    - id: AP-TCU-007-C
      description: "Insider with signing access"

  defenses_at_each_step:
    - step: 1: "Limited recon prevention"
    - step: 2: "SBOM monitoring, vendor security review"
    - step: 3: "Build pipeline integrity (reproducible builds)"
    - step: 4: "Dual signer + manual approval"
    - step: 5: "Per-vehicle integrity verification"
    - step: 6: "Telemetry anomaly detection"
```

---

## 多路徑比較

當一個 Threat 有多路徑時，需評估每條：

```
Threat: Steal V2X private key
   ├── AP-A: HSM side-channel attack
   │   └── feasibility: Very Low (expert + lab)
   │
   ├── AP-B: 萃取金鑰從備份伺服器
   │   └── feasibility: Medium (depends on backup security)
   │
   ├── AP-C: 內部員工竊取
   │   └── feasibility: Medium (depends on controls)
   │
   └── AP-D: 釣魚取得 admin 憑證
       └── feasibility: High

最終 feasibility = High (最容易那條)
   ↓
   守護重點：強化 AP-D 路徑
```

---

## Attack Path 的「攻擊面」識別

```
External Attack Surface：
├── 蜂巢介面 → MITM、Cell injection
├── Wi-Fi → 攻擊熱點偽冒
├── Bluetooth → 配對攻擊
├── V2X → 假基站
└── GNSS → spoofing

Physical Attack Surface：
├── OBD-II → 物理接近
├── USB → 惡意 USB
├── 充電 → CCS injection
├── JTAG → 開殼物理
└── 排線/天線 → 訊號注入

Supply Chain：
├── Tier-2 元件
├── OS / Library
├── 開發工具
└── CI/CD pipeline

Insider：
├── 員工
├── 承包商
└── 服務廠
```

---

## Attack Path 與防禦設計的連結

```
找出所有 Attack Path
   ↓
每一條路徑識別「弱環節」
   ↓
針對最弱環節**設計防禦控制**
   ↓
重新評估 feasibility
   ↓
如降不下來 → 移除攻擊面 / Avoid 處置
```

---

## 證照考點

> [!important]
>
> 1. 一個 Threat 可能有**多條 Attack Path**
> 2. Feasibility 採用**最容易**的那條
> 3. 表達方式：線性、攻擊樹、Kill Chain
> 4. 每條 Path 需識別**前提條件 + 步驟 + 防禦**
> 5. 攻擊面包含 External / Physical / Supply Chain / Insider
> 6. 結果驅動防禦設計

---

## Related Notes

- [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]
- [[12-TARA-Methods/06-Attack-Feasibility-Rating\|12-TARA-Methods/06-Attack-Feasibility-Rating]]
- [[13-Annexes-Tools/04-Attack-Trees\|13-Annexes-Tools/04-Attack-Trees]]

## Practice

- [[12-TARA-Methods/Practice-TARA\|12-TARA-Methods/Practice-TARA]]

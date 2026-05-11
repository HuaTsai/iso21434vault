---
{"dg-publish":true,"permalink":"/10-operations-maintenance/01-incident-response/","title":"資安事件回應 (Incident Response)","tags":["iso-21434","concept-note","operations","incident-response"],"dg-note-properties":{"title":"資安事件回應 (Incident Response)","source_pdf":"內部彙整 (ISO 21434 Clause 13)","part":"Clause 13","keywords":["incident-response","ir","csirt","playbook"],"tags":["iso-21434","concept-note","operations","incident-response"],"created":"2026-05-11"}}
---


## 是什麼？

當 Clause 8 Event Assessment 將事件分類為 **Incident**（實際攻擊發生或進行中），啟動本流程。

```
Event → Vulnerability （Clause 8.5）→ Patch
       → Incident → IR (Clause 13)
```

---

## IR 生命週期（NIST 框架）

```
┌──────────────────────────────────┐
│ 1. Preparation                    │
│    • IR Plan、Playbook、團隊       │
│    • 工具、聯絡、訓練              │
├──────────────────────────────────┤
│ 2. Detection & Analysis           │
│    • Event Assessment 結果         │
│    • 確認 incident scope            │
│    • 嚴重度分級                    │
├──────────────────────────────────┤
│ 3. Containment                    │
│    • 阻止擴散                      │
│    • 短期 vs 長期 containment       │
├──────────────────────────────────┤
│ 4. Eradication                    │
│    • 移除攻擊者 / 後門              │
│    • 清除受感染元件                │
├──────────────────────────────────┤
│ 5. Recovery                       │
│    • 恢復服務                      │
│    • 監控異常                      │
├──────────────────────────────────┤
│ 6. Post-Incident (Lessons Learned)│
│    • 根因分析                      │
│    • 改善流程                      │
│    • 更新 TARA / CS Case           │
└──────────────────────────────────┘
```

---

## 必要 WP：Incident Response Plan

```yaml
incident_response_plan:
  scope: "All in-field vehicles + connected services"

  roles:
    ir_lead: "OEM CSIRT Lead"
    technical_team:
      - "OEM Security Engineer"
      - "Tier-1 Liaison (per CIA)"
    communication_lead: "PR + Legal"
    decision_authority: "VP Engineering / CSO"

  severity_classification:
    P0_critical: "Active exploit affecting many vehicles, safety impact"
    P1_high: "Active exploit limited scope, or high potential"
    P2_medium: "Confirmed incident, no active exploit"
    P3_low: "Minor incident, contained"

  sla:
    P0: "15 min Detection → 1 hr Containment → 24 hr Resolution"
    P1: "1 hr → 4 hr → 72 hr"
    P2: "4 hr → 24 hr → 1 week"
    P3: "24 hr → 1 week → 1 month"

  playbooks:
    - "Compromised OTA Server"
    - "Vehicle Remote Compromise (group)"
    - "Vehicle Remote Compromise (individual)"
    - "Diagnostic Tool Exploited"
    - "Key Material Leak"
    - "Backend Data Breach"

  external_coordination:
    - "Tier-1 (per CIA)"
    - "Auto-ISAC"
    - "Regulatory (per UN R155)"
    - "Law enforcement (severe cases)"
    - "Insurance"

  communication:
    internal:
      - "Hourly status updates during P0/P1"
      - "Daily during P2"
    external:
      - "Coordinated disclosure timing"
      - "Customer notification"
      - "Press statement (legal-reviewed)"

  testing:
    - "Annual tabletop exercise"
    - "Bi-annual technical drill"
```

---

## Playbook 範例：Compromised OTA Server

```yaml
playbook_compromised_ota:
  trigger: "OTA server unauthorised access detected"

  immediate_actions:
    - "Isolate OTA server from production network"
    - "Pause all ongoing OTA distributions"
    - "Notify CSIRT Lead"

  investigation:
    - "Forensic image of affected systems"
    - "Audit recent OTA packages signed"
    - "Verify integrity of signing key (HSM)"

  containment:
    - "If signing key compromised: revoke + emergency re-issue"
    - "Block all in-flight OTA from affected vehicles"
    - "Whitelist only verified packages"

  eradication:
    - "Rebuild OTA server from known-good state"
    - "Patch underlying vulnerability"
    - "Rotate all credentials"

  recovery:
    - "Resume OTA with new signed pipeline"
    - "Monitor for anomalies"
    - "Per-vehicle integrity check"

  external:
    - "Notify Tier-1s per CIA"
    - "Notify Auto-ISAC"
    - "Coordinate with regulators"
    - "Customer communication plan"

  post:
    - "Root cause analysis"
    - "Update IR Plan if needed"
    - "Update TARA + CS Case"
```

---

## 與其他流程的接點

```
Event Assessment (8.4) → Incident → IR (13)
                ↓
           升級為事件
                ↓
        IR 啟動
                ↓
   Containment / Eradication / Recovery
                ↓
        修補需求 → Updates (13)
                ↓
        OTA 部署 → UN R156 SUMS
                ↓
   Post-Incident → Lessons Learned
                ↓
        更新 TARA + CS Case
                ↓
        通報 UN R155 監管機構（嚴重事件）
```

---

## 證據保全 (Evidence Preservation)

```
事件發生 → 立即保全證據
   ↓
保全範圍：
├── 車輛端 logs（CAN trace、ECU log）
├── 雲端 logs
├── 網路流量 (PCAP)
├── 記憶體 dump
├── 韌體 image
└── 時序記錄

保全要求：
├── Chain of Custody（變更紀錄、誰持有）
├── 完整性（雜湊驗證）
├── 加密保護
└── 法律可接受性（可能用於起訴）
```

---

## 對外通報

> [!important]
> UN R155 + 各國法規可能要求 OEM 在嚴重事件**強制通報**：
>
> - 通報窗口（時限）
> - 通報內容（事件性質、影響範圍、處置）
> - 後續更新義務

監管機構：

- 歐盟：UNECE WP.29、ENISA
- 美國：NHTSA
- 各國：本地交通部門

---

## 證照考點

> [!important] 高頻考點
>
> 1. **Incident Response Plan** 是 Clause 13 必要 WP
> 2. NIST 六階段：Prep → Detect → Contain → Eradicate → Recover → Post
> 3. **SLA 依嚴重度**分級
> 4. **Tier-1 通報依 CIA**（不是隨意）
> 5. **Evidence Preservation** 是 IR 必要動作
> 6. 嚴重事件**需通報監管機構**（UN R155）
> 7. Post-Incident 必須**更新 TARA + CS Case**
> 8. IR Plan **需定期演練**

---

## Related Notes

- [[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]
- [[05-Continual-Cybersecurity/02-Event-Assessment\|05-Continual-Cybersecurity/02-Event-Assessment]]
- [[05-Continual-Cybersecurity/04-Vulnerability-Management\|05-Continual-Cybersecurity/04-Vulnerability-Management]]
- [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]

## Practice

- [[10-Operations-Maintenance/Practice-Operations\|10-Operations-Maintenance/Practice-Operations]]

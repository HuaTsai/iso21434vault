---
{"dg-publish":true,"permalink":"/05-continual-cybersecurity/02-event-assessment/","title":"資安事件評估 (Event Assessment)","tags":["iso-21434","concept-note","continual","event-assessment"],"dg-note-properties":{"title":"資安事件評估 (Event Assessment)","source_pdf":"內部彙整 (ISO 21434 Clause 8.4)","part":"Clause 8","keywords":["event-assessment","triage","classification"],"tags":["iso-21434","concept-note","continual","event-assessment"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] Clause 8.4 目的
> 評估從 Monitoring 收到的 **events** 是否為「**真實資安事件**」或「**新弱點**」，並決定後續行動。

可以理解為 **Triage（分類分流）** 階段。

---

## Event vs Incident vs Vulnerability

> [!important] 標準定義（Clause 3）
>
> - **Cybersecurity Event** = observable occurrence in an item or component that has cybersecurity implications（**狀態變化的可觀察事件**）
> - **Cybersecurity Incident** = cybersecurity event that adversely affects ...（**incident 是 event 的子集**）
> - **Vulnerability** = weakness that can be exploited（**獨立概念**，來自 weakness）
>
> 注意：CVE / 研究通報 / SAST 結果**不是** "event"，而是 Clause 8.3 monitoring 蒐集的弱點情報，直接走 vulnerability 流程，不經過 8.4 event evaluation。

```
Clause 8.3 Monitoring 蒐集所有資安資訊
              │
     ┌────────┴────────────┐
     │                     │
     ↓                     ↓
[Path A] Cybersecurity   [Path B] 弱點情報
         Event                    (CVE / 研究 / SAST)
     │                            │
     ↓                            ↓
8.4 Event Evaluation         8.5 Vulnerability Analysis
     │                            │
     ├── 是 incident             ↓
     │   (event 的子集)      8.6 Vulnerability Management
     │      ↓
     │   Clause 13 IR
     └── 無 cybersecurity
         implication → 關閉
```

| 術語              | 定義（Clause 3）                               | 來源                          | 處置流程                                    |
| ----------------- | ---------------------------------------------- | ----------------------------- | ------------------------------------------- |
| **Event**         | 可觀察的資安相關事件                           | 監控、IDS、日誌、用戶通報     | 8.4 Event Evaluation                        |
| **Incident**      | adversely affects 的 event（event 的**子集**） | 由 event evaluation 升級      | Clause 13 Incident Response                 |
| **Vulnerability** | 可被利用的 weakness（**獨立概念**）            | CVE、研究通報、SAST、Pen Test | 8.5 Vulnerability Analysis + 8.6 Management |

---

## Event Assessment 流程

```
1. 接收 Event（來自 Monitoring）
   ↓
2. 初步分類
   ├── 重複事件？合併
   ├── False Positive？關閉
   └── 真實事件 → 繼續
   ↓
3. 影響分析（quick triage）
   ├── 對我們的產品適用嗎？
   ├── 是否已被攻擊（incident）？
   └── 嚴重度初判
   ↓
4. 分流：
   ├── Incident → Clause 13 IR
   ├── Vulnerability → 8.5 Vulnerability Analysis
   ├── Suspicious but unconfirmed → 進一步調查
   └── Not applicable → 關閉並記錄
   ↓
5. 紀錄決策
```

---

## Triage 判斷準則

```yaml
triage_criteria:
  incident_indicators:
    - "Active exploitation observed"
    - "Customer reported compromise"
    - "Honeypot/telemetry shows attack pattern"
    - "Forensic evidence of breach"

  vulnerability_indicators:
    - "CVE published affecting our SBOM"
    - "Researcher disclosure of new weakness"
    - "Internal test/audit finding"
    - "Supply chain notification"

  false_positive_indicators:
    - "Affected version not in use"
    - "Architecture difference makes inapplicable"
    - "Already mitigated by other control"
    - "Duplicate of existing record"

  needs_investigation:
    - "Insufficient information"
    - "Theoretical attack, unclear feasibility"
    - "Unclear if affects our config"
```

---

## SLA 範例

| 嚴重度初判                | Assessment 完成 SLA |
| ------------------------- | ------------------- |
| Critical (active exploit) | **< 4 hours**       |
| High (public PoC)         | < 24 hours          |
| Medium                    | < 5 business days   |
| Low                       | < 2 weeks           |
| Informational             | < 1 month           |

---

## Event Record 範本

```yaml
event_record:
  id: EVT-2026-0501
  source_record: MON-2026-1234
  triage_date: 2026-05-11
  triage_by: "CSIRT Analyst (Tier 2)"

  initial_observation:
    description: "RCE vulnerability in OpenSSL 3.0.x reported"
    severity_initial: "Critical"

  triage_analysis:
    affects_our_product: true
    product_list: ["TCU-2026"]
    sbom_match: "OpenSSL 3.0.12"
    active_exploitation: false # No telemetry alarms
    customer_reports: 0

  classification:
    type: "Vulnerability" # not Incident
    severity: "High" # 攻擊雖未發生，但有 PoC
    rationale: "PoC public, our version affected, no active exploit yet"

  next_action:
    route_to: "Vulnerability Analysis (8.5)"
    assigned_to: "Vulnerability Mgmt Team"
    deadline: 2026-05-13

  escalation_to_ir: false # 尚未發生 incident
```

---

## 與 Incident Response 的銜接

```
Event Assessment 判斷為 Incident
        ↓
觸發 Clause 13 Incident Response
        ↓
進入 IR Playbook：
  • Containment
  • Eradication
  • Recovery
  • Lessons Learned
```

→ [[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]

---

## 與 Vulnerability Analysis 的銜接

```
Event Assessment 判斷為 Vulnerability
        ↓
觸發 Clause 8.5 Vulnerability Analysis
        ↓
深度分析：
  • 攻擊路徑
  • 攻擊可行性
  • 衝擊評估
  • TARA 更新需求
        ↓
進入 8.6 Vulnerability Management
```

→ [[05-Continual-Cybersecurity/03-Vulnerability-Analysis\|05-Continual-Cybersecurity/03-Vulnerability-Analysis]]

---

## 證照考點

> [!important] 高頻考點
>
> 1. Event Assessment 是 **Triage** 階段
> 2. **Event vs Vulnerability vs Incident** 三者不同
>    - Event：觀察（未確認）
>    - Vulnerability：可利用弱點（未被利用）
>    - Incident：實際攻擊（正發生 / 已發生）
> 3. False Positive **也需記錄**（不可直接丟棄）
> 4. 分流結果：Incident → IR；Vulnerability → 8.5；Not applicable → 關閉
> 5. SLA 應依嚴重度分級

---

## Related Notes

- [[05-Continual-Cybersecurity/01-Cybersecurity-Monitoring\|05-Continual-Cybersecurity/01-Cybersecurity-Monitoring]]
- [[05-Continual-Cybersecurity/03-Vulnerability-Analysis\|05-Continual-Cybersecurity/03-Vulnerability-Analysis]]
- [[05-Continual-Cybersecurity/04-Vulnerability-Management\|05-Continual-Cybersecurity/04-Vulnerability-Management]]
- [[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]
- [[01-Foundations/02-Key-Terms-Definitions\|01-Foundations/02-Key-Terms-Definitions]]

## Practice

- [[05-Continual-Cybersecurity/Practice-Continual\|05-Continual-Cybersecurity/Practice-Continual]]

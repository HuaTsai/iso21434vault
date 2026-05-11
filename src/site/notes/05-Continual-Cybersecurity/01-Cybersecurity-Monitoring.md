---
{"dg-publish":true,"permalink":"/05-continual-cybersecurity/01-cybersecurity-monitoring/","title":"資安監控 (Cybersecurity Monitoring)","tags":["iso-21434","concept-note","continual","monitoring"],"dg-note-properties":{"title":"資安監控 (Cybersecurity Monitoring)","source_pdf":"內部彙整 (ISO 21434 Clause 8.3)","part":"Clause 8","keywords":["monitoring","threat-intel","continual","isac"],"tags":["iso-21434","concept-note","continual","monitoring"],"created":"2026-05-11"}}
---


## Clause 8 的整體框架

```
       ┌─────────────────────────┐
       │  Cybersecurity          │  ← 8.3
       │     Monitoring          │
       └──────────┬──────────────┘
                  │ 觀察到
                  ↓
       ┌─────────────────────────┐
       │   Event Assessment      │  ← 8.4
       │  （是否為資安事件？）      │
       └──────────┬──────────────┘
                  │ 確認為事件 / 弱點
                  ↓
       ┌─────────────────────────┐
       │  Vulnerability Analysis │  ← 8.5
       │  （影響範圍？）            │
       └──────────┬──────────────┘
                  │
                  ↓
       ┌─────────────────────────┐
       │ Vulnerability Mgmt      │  ← 8.6
       │  （處置決策）              │
       └─────────────────────────┘
```

> [!important]
> Clause 8 是**橫貫所有生命週期**的活動，從 CSMS 生效到 EoS 都持續執行。

---

## Monitoring 的「兩條腿」

```
┌─────────────────────────────────┐
│        Monitoring               │
├──────────────┬──────────────────┤
│   Internal   │     External     │
│              │                  │
│ • IDS/IPS    │ • CVE 資料庫     │
│ • SIEM       │ • CERT 通告      │
│ • 測試發現    │ • ISAC 情報      │
│ • 客戶回饋    │ • 學術研究       │
│ • IR 結果    │ • 安全社群       │
│ • 自家研究    │ • 競爭者公告     │
│              │ • 政府/法規警示   │
└──────────────┴──────────────────┘
```

> [!warning] 常見誤解
> Monitoring **不只是「監控 CAN bus」或「跑 IDS」**。
> 它包含**情報蒐集**——這在 Clause 8 中與技術監控同等重要。
>
> 參考 [[00-Dashboard/Exam-Traps#Trap 9\|00-Dashboard/Exam-Traps#Trap 9]]

---

## Internal Sources（內部）

| 來源           | 範例                              |
| -------------- | --------------------------------- |
| **車輛遙測**   | 異常 CAN 訊息、ECU log、車隊 SIEM |
| **測試結果**   | Pen test、Fuzz、SAST 發現         |
| **客戶回饋**   | 客服系統、保固紀錄                |
| **內部研究**   | 內部紅隊、Bug Bounty              |
| **IR 紀錄**    | 過去事件的 Lessons Learned        |
| **供應商通報** | Tier-X 主動通報                   |

---

## External Sources（外部）

| 來源          | 範例 / 平台                          |
| ------------- | ------------------------------------ |
| **CVE / NVD** | MITRE CVE、NIST NVD                  |
| **CERT**      | CERT-EU、JPCERT、TWNCERT             |
| **ISAC**      | Auto-ISAC、AutoISAC EU               |
| **學術**      | Black Hat、DEF CON、USENIX           |
| **社群**      | Reddit r/cars、Twitter Sec community |
| **政府**      | NHTSA、ENISA、UNECE WP.29 通告       |
| **競爭者**    | 公開的召回、公告                     |
| **研究者**    | Project Zero、安全研究實驗室         |

---

## 監控工具與流程

```
1. 訂閱與蒐集
   ├── CVE feed (subscription)
   ├── 訂閱 ISAC alerts
   ├── 訂閱供應商 security advisory
   └── 自動化爬蟲（學術、社群）
   ↓
2. 過濾與標籤
   ├── 是否與我們的產品相關？
   ├── 是否與我們的元件相關？
   └── 嚴重度初步判斷
   ↓
3. 觸發 Event Assessment（8.4）
```

---

## 監控的「相關性過濾」

> [!tip]
> 業界每天有上千個 CVE 發布，**不可能逐一深究**。
> 需建立**相關性過濾機制**：
>
> ```
> 過濾條件：
> ├── 我們的 SBOM 中是否含此元件？
> ├── 我們的硬體平台是否受影響？
> ├── 攻擊情境是否可能在汽車環境下成立？
> └── 是否影響特定車型/區域？
> ```
>
> SBOM 是過濾的關鍵基礎。

---

## 監控紀錄 (Monitoring Records)

每個觀察到的事項應記錄：

```yaml
monitoring_record:
  id: MON-2026-1234
  source: "Auto-ISAC Alert ASA-2026-005"
  date_observed: 2026-05-11
  description: "RCE in OpenSSL 3.0.x"

  relevance_analysis:
    sbom_match: "OpenSSL 3.0.12 in TCU-2026"
    affected_versions: "3.0.0 - 3.0.13"
    our_version: "3.0.12 (AFFECTED)"

  initial_classification:
    severity: "Critical (CVSS 9.8)"
    exploitability: "Public PoC exists"

  escalation: "Triggered Event Assessment (EA-2026-088)"

  recorded_by: "CSIRT Analyst"
```

---

## 監控的「定量」KPI

| KPI          | 量測                         | 目標             |
| ------------ | ---------------------------- | ---------------- |
| 來源覆蓋率   | 訂閱來源數 / 應訂閱數        | 100%             |
| 過濾通過率   | 進入 Event Assessment 的比例 | 持續優化         |
| 平均響應時間 | 從觀察到 Assessment 決策     | < 24h (Critical) |
| 漏掉的事件   | 後知後覺發現的事件           | 0                |

---

## Monitoring 與其他 Clause 的接點

```
            ┌─────────────────┐
            │  Monitoring (8.3)│
            └────────┬─────────┘
                     │
            ┌────────┴────────┐
            │                 │
   ┌────────▼─────┐  ┌────────▼─────────┐
   │ Event Assess │  │ TARA Update Trigger│
   │   (8.4)      │  │  (Clause 15)       │
   └──────────────┘  └────────────────────┘
            │
   ┌────────▼─────────┐
   │ Incident Response │  ← Clause 13
   │ if 升級為事件      │
   └───────────────────┘
```

---

## 證照考點

> [!important] 高頻考點
>
> 1. Monitoring **不只**技術監控（IDS）——還含**情報蒐集**
> 2. Monitoring 範圍：**內部 + 外部**
> 3. **SBOM** 是相關性過濾的基礎
> 4. Monitoring 紀錄是必要 WP
> 5. Monitoring → 觸發 **Event Assessment**
> 6. Monitoring **橫貫整個生命週期**，不專屬單一專案
> 7. 來源範例：CVE、CERT、Auto-ISAC、學術、客戶回饋

---

## Related Notes

- [[05-Continual-Cybersecurity/02-Event-Assessment\|05-Continual-Cybersecurity/02-Event-Assessment]]
- [[05-Continual-Cybersecurity/03-Vulnerability-Analysis\|05-Continual-Cybersecurity/03-Vulnerability-Analysis]]
- [[02-Organizational-Management/05-Information-Sharing\|02-Organizational-Management/05-Information-Sharing]]
- [[00-Dashboard/Exam-Traps#Trap 9\|00-Dashboard/Exam-Traps#Trap 9]]
- [[00-Dashboard/Exam-Traps#Trap 15\|00-Dashboard/Exam-Traps#Trap 15]]

## Practice

- [[05-Continual-Cybersecurity/Practice-Continual\|05-Continual-Cybersecurity/Practice-Continual]]

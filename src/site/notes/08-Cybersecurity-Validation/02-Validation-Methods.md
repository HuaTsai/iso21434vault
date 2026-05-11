---
{"dg-publish":true,"permalink":"/08-cybersecurity-validation/02-validation-methods/","title":"驗證方法","tags":["iso-21434","concept-note","validation","methods"],"dg-note-properties":{"title":"驗證方法","source_pdf":"內部彙整 (ISO 21434 Clause 11 + 業界實務)","part":"Clause 11","keywords":["pen-test","fuzz","vehicle-test","red-team"],"tags":["iso-21434","concept-note","validation","methods"],"created":"2026-05-11"}}
---


## 方法概覽

```
┌─────────────────────────────────────────┐
│       Vehicle-level Validation          │
├─────────────────────────────────────────┤
│  • Penetration Testing  (★ 必要)         │
│  • Fuzzing                              │
│  • Vehicle-level functional test        │
│  • Red Team Exercise                    │
│  • Side-channel analysis (selected)     │
│  • Environmental testing (含 EMC)        │
│  • Long-term Operational Test           │
└─────────────────────────────────────────┘
```

---

## 1. Penetration Testing (Pen Test)

> [!important]
> ISO 21434 Clause 11 將 Pen Test 列為車輛層級驗證的**適當方法**之一；UN R155 type approval 實務上普遍將 Pen Test 視為必要證據。若 CS Case 中未含 Pen Test，需提出明確 justification（如已用其他等效方法）。

### Pen Test 流程（PTES / OWASP）

```
1. Pre-engagement Interactions
   ├── Scope 定義（含 out-of-scope）
   ├── Rules of Engagement
   ├── Authorization（含法律授權）
   └── 緊急聯絡

2. Intelligence Gathering
   ├── 公開資訊蒐集
   ├── 文件研讀（依 CIA）
   └── 攻擊面 mapping

3. Threat Modeling
   ├── 與 TARA 對齊
   ├── 選擇優先攻擊路徑
   └── 攻擊樹更新

4. Vulnerability Analysis
   ├── 工具掃描
   ├── 手動測試
   └── 弱點分類

5. Exploitation
   ├── 嘗試 PoC
   ├── 取得初始存取
   └── 紀錄成功攻擊

6. Post-Exploitation
   ├── 提權 / Pivoting
   ├── 影響範圍（橫向移動）
   └── 持久化測試

7. Reporting
   ├── Executive Summary
   ├── 技術細節
   ├── 風險評估
   └── Remediation 建議

8. Re-testing
   └── 修補後驗證
```

### Pen Test 範圍（汽車情境）

```
External Pen Test (整車外部)：
├── Cellular interface
├── Wi-Fi / Bluetooth
├── V2X (DSRC / C-V2X)
├── GNSS spoofing/jamming
├── RKE / PKE (key fob)
└── Backend (in scope per CIA)

Internal Pen Test (整車內部)：
├── OBD-II
├── CAN buses
├── Ethernet
├── USB ports
├── Charging interface (CCS, CHAdeMO)
└── Service interfaces

Hardware Pen Test：
├── JTAG / SWD
├── UART debug
├── Glitching (voltage/clock)
├── Side-channel (SPA/DPA)
└── Memory chip-off
```

---

## 2. Fuzzing

針對輸入處理元件：

```yaml
fuzz_test_plan:
  targets:
    - "CAN message parser"
    - "Ethernet protocol stack"
    - "OTA payload parser"
    - "Diagnostic message handler"
    - "JSON/Protobuf parsers"
    - "TLS handshake (TCP/UDP)"

  tools:
    - AFL++ (Coverage-guided)
    - libFuzzer
    - Defensics (commercial)
    - Custom (for proprietary protocols)

  metrics:
    - "Code coverage achieved"
    - "Time to first crash"
    - "Unique crashes found"
    - "Hang/timeout incidents"
```

---

## 3. Red Team Exercise

> [!tip]
> Red Team 比 Pen Test 更廣，模擬**完整攻擊鏈**：
>
> - 含社交工程（針對 OEM 員工/承包商）
> - 含實體入侵（dealer、service center）
> - 多階段、長期、隱蔽
>
> 適合**成熟組織**進行高階驗證。

```
Red Team 攻擊鏈範例（汽車）：
1. 偵察 OEM 雲端
2. 釣魚攻擊 OEM 員工
3. 取得內網存取
4. 入侵簽章伺服器
5. 簽署惡意韌體
6. 觸發 OTA 部署
7. 控制車隊

Validation 觀點：
完整鏈條的任何一環失敗 → 整體攻擊失敗
```

---

## 4. Vehicle-level Functional Test (with Security View)

```
Normal functional tests + 加入安全角度：

例：OTA 更新測試
├── 正常 OTA 過程：功能 OK + 簽章驗證 OK
├── 中斷情境：power loss、network loss
│   ↓ 攻擊者可否利用？
├── 異常封包：malformed、超長、replay
│   ↓ 是否被拒絕？
└── 故意失敗：tampered image
    ↓ 必須拒絕 + 紀錄
```

---

## 5. Side-Channel Analysis

針對加密實作：

```
DPA (Differential Power Analysis)
SPA (Simple Power Analysis)
EM Analysis
Timing Attack
Fault Injection (glitching)

對象：
├── HSM
├── 簽章運算（boot 階段）
└── TLS 握手
```

通常由**外部專業實驗室**執行（如 Riscure、Brightsight）。

---

## 6. Long-term Operational Test

針對「**時間相關**的弱點」：

```
測試項目：
├── 隨機數熵源衰退
├── 監控 log 滿溢
├── 憑證即將過期的行為
├── 軟體在長時間運行後的狀態
└── 對抗持續性攻擊（如低頻 fuzzing）
```

通常與功能可靠度測試合併。

---

## Validation 與 TARA 的閉環

```
TARA 識別威脅情境
        ↓
Validation 嘗試實現這些情境
        ↓
   ┌────┴────┐
   ↓         ↓
成功阻擋    成功攻擊
   ↓         ↓
紀錄為      重新評估
證據         ↓
   ↓     更新 TARA
CS Case   更新處置
```

---

## Validation 失敗的後果

```
Validation Pass → 進入 Assessment
Validation Fail → 修正 + 重測

可能後果：
├── 延後 Release
├── 修補設計（Clause 10 回流）
├── 重新 TARA
├── 修改 CS Goals / Concept
├── 殘餘風險接受（限低嚴重度）
└── 取消專案（極端情況）
```

---

## Validation 報告分發

```
Validation Report 接收者：
├── Project CS Manager
├── Cybersecurity Assessor
├── Top Management (Release 決策者)
├── Safety Manager (可能交互影響)
├── 客戶（依 CIA）
└── 監管機構（如 UN R155 認證需要）
```

> [!warning]
> Validation Report 含**敏感攻擊細節**，分發需嚴格控管。

---

## 證照考點

> [!important] 高頻考點
>
> 1. **Pen Test 是 Clause 11 列為適當的 validation 方法之一**（R155 type approval 普遍期待；不執行需 justification）
> 2. Pen Test **可在元件級或車輛級**，但 Clause 11 的 Validation **要求車輛級**
> 3. Validation 方法多元：Pen Test + Fuzz + Red Team + 功能測試
> 4. Validation 與 TARA 形成**閉環**
> 5. Validation Report **敏感**，分發需控管
> 6. 失敗 → 設計回流 / TARA 更新

---

## Related Notes

- [[08-Cybersecurity-Validation/01-Validation-Objectives\|08-Cybersecurity-Validation/01-Validation-Objectives]]
- [[07-Product-Development/02-Integration-Verification\|07-Product-Development/02-Integration-Verification]]
- [[12-TARA-Methods/05-Attack-Path-Analysis\|12-TARA-Methods/05-Attack-Path-Analysis]]
- [[00-Dashboard/Exam-Traps#Trap 11\|00-Dashboard/Exam-Traps#Trap 11]]

## Practice

- [[08-Cybersecurity-Validation/Practice-Validation\|08-Cybersecurity-Validation/Practice-Validation]]

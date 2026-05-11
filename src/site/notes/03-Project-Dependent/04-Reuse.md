---
{"dg-publish":true,"permalink":"/03-project-dependent/04-reuse/","title":"重用與 OTS (Off-The-Shelf) 元件","tags":["iso-21434","concept-note","project-dependent","reuse","ots"],"dg-note-properties":{"title":"重用與 OTS (Off-The-Shelf) 元件","source_pdf":"內部彙整 (ISO 21434 Clause 6.4.5)","part":"Clause 6","keywords":["reuse","ots","off-the-shelf","components"],"tags":["iso-21434","concept-note","project-dependent","reuse","ots"],"created":"2026-05-11"}}
---


## 三種「非新開發」元件

| 類型                    | 定義                           | 範例                           |
| ----------------------- | ------------------------------ | ------------------------------ |
| **Reused**              | 來自舊專案/產品線的元件        | 前代車型的 Gateway 軟體        |
| **OTS (Off-the-Shelf)** | 既存的商業或開源產品           | OpenSSL、商用 HSM、第三方 RTOS |
| **Out-of-Context**      | 通用情境開發、待整合至特定情境 | 通用 BSP、平台型晶片           |

> [!warning] 易混淆
> 三者**互不相同**，但都有「**情境改變需重新評估**」的共同要求。

---

## 為什麼這些元件需特別處理？

```
歷史驗證的情境 ≠ 新專案的情境

新專案可能：
• 新的攻擊面（新介面、新功能）
• 新的威脅情境
• 新的衝擊（不同車型/市場）
• 新弱點（自上次評估後發現）
```

→ 因此**不可**假設「過去安全 = 現在安全」。

---

## Reuse 元件處理流程

```
1. 識別重用元件
   ↓
2. 蒐集歷史證據
   ├── 既有 TARA Report
   ├── 既有 Verification/Validation 結果
   ├── 已知弱點 / 修補紀錄
   └── 既有 CS Case 片段
   ↓
3. 評估情境差異
   ├── 介面變動？
   ├── 環境變動？
   ├── 風險假設變動？
   └── 已知威脅變動？
   ↓
4. Delta TARA（差異分析）
   ↓
5. 補足驗證活動
   ↓
6. 更新 CS Case 與 WP
```

---

## OTS 元件的特殊考量

### 識別 OTS

| 類型                | 範例                          | 評估重點                                |
| ------------------- | ----------------------------- | --------------------------------------- |
| **商業軟體 (COTS)** | 商用 RTOS、商用 HSM SDK       | 供應商安全聲明、漏洞修補 SLA            |
| **開源 (FOSS)**     | OpenSSL、Linux Kernel、libpng | 社群活躍度、CVE 歷史、SBOM              |
| **硬體 IP**         | 商用 SoC、安全晶片            | 製造商 CC 認證、Side-channel resistance |
| **第三方服務**      | 雲端 OTA 平台                 | 服務合約、SLA、合規證明                 |

### OTS 評估必含項目

```yaml
ots_evaluation:
  component: "OpenSSL 3.0.12"
  type: "Open Source - Cryptographic library"

  cybersecurity_assessment:
    known_vulnerabilities:
      - CVE-2023-XXXX (Severity: High)
        - Status: Patched in 3.0.12
        - Applicable to our use: Yes
        - Mitigation: Already on patched version

    supply_chain:
      - source: "Official GitHub"
        verification: "GPG signature verified"
      - sbom: "Generated, stored at /sbom/"

    maintenance:
      - support_horizon: "LTS until 2026-09-07"
      - planned_action: "Migrate to 3.1.x before 2026-Q2"

    integration_risks:
      - "Side-channel attacks on RSA operations"
        mitigation: "Use HSM for all RSA private operations"

    cs_case_inclusion:
      - "Library signature + version locked in build manifest"
      - "Quarterly CVE scan"
```

---

## SBOM (Software Bill of Materials)

> [!important]
> OTS 元件管理的**事實標準**：SBOM。

```
SBOM 格式：
├── SPDX
├── CycloneDX (推薦，含安全資訊)
└── SWID
```

**用途**：

- 弱點對應（新 CVE 出來 → 查 SBOM 看是否受影響）
- 授權合規
- 供應鏈追溯

UN R155 + UN R156 **強烈建議**維護 SBOM。

---

## OTS 元件的責任分配

```
組織責任：
├── 識別所有 OTS 元件
├── 維護 SBOM
├── 監控 CVE / 安全公告
├── 評估適用性與整合風險
└── 整合測試

不可推給 OTS 供應商：
✗ 「OpenSSL 沒問題，所以我們的產品沒問題」
✗ 「商用元件已通過 CC，所以不用評估」
```

> [!warning]
> 即使 OTS 供應商提供安全聲明，**整合責任在 OEM/Tier-1**。

---

## Reuse 的 Delta TARA

```
原 TARA (Reference)
   │
   ├── Assets：與新情境比對
   │       新增資產？移除資產？屬性改變？
   │
   ├── Threat Scenarios：
   │       新威脅？舊威脅仍適用？
   │
   ├── Impact：
   │       車型/市場差異導致 SFOP 改變？
   │
   └── Attack Feasibility：
           新攻擊技術出現？防護仍有效？

→ 差異點才需深度分析
```

---

## Reuse / OTS 對 CS Case 的影響

CS Case 應包含：

- 重用/OTS 元件的**識別清單**
- 重用根據（reused from project X, version Y）
- Delta 分析結果
- 殘留風險與接受

---

## 證照考點

> [!important] 高頻考點
>
> 1. Reuse / OTS / Out-of-Context **三者不同**但都需重新評估
> 2. 「過去安全 = 現在安全」是**錯誤假設**
> 3. **SBOM** 是 OTS 管理基礎
> 4. **Delta TARA** 是 Reuse 的常見方法
> 5. OTS 整合**責任在使用者**，不可推給供應商
> 6. 即使 OTS 已有 CC 認證，**整合層**仍需評估

---

## Related Notes

- [[03-Project-Dependent/03-Tailoring\|03-Project-Dependent/03-Tailoring]]
- [[03-Project-Dependent/05-Component-Out-of-Context\|03-Project-Dependent/05-Component-Out-of-Context]]
- [[03-Project-Dependent/06-Case-and-Assessment\|03-Project-Dependent/06-Case-and-Assessment]]
- [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]
- [[00-Dashboard/Exam-Traps#Trap 7\|00-Dashboard/Exam-Traps#Trap 7]]

## Practice

- [[03-Project-Dependent/Practice-Project-Mgmt\|03-Project-Dependent/Practice-Project-Mgmt]]

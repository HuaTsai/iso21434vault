---
{"dg-publish":true,"permalink":"/13-annexes-tools/03-stride-dread/","title":"STRIDE / DREAD 補充","tags":["iso-21434","concept-note","annex","threat-modeling"],"dg-note-properties":{"title":"STRIDE / DREAD 補充","source_pdf":"內部彙整 (業界 Threat Modeling 方法)","part":"補充工具","keywords":["stride","dread","threat-modeling"],"tags":["iso-21434","concept-note","annex","threat-modeling"],"created":"2026-05-11"}}
---


> 這些**不是** ISO 21434 規範的方法，但業界廣泛採用，常作為 TARA Step 2 (Threat Scenario) 的識別工具。

---

## STRIDE — Microsoft 威脅建模

> 由 Microsoft 提出，每類威脅對應一個資安屬性的破壞。

### 六大類別

| 縮寫  | 名稱                                | 破壞屬性        | 範例                   |
| ----- | ----------------------------------- | --------------- | ---------------------- |
| **S** | **Spoofing** 假冒                   | Authenticity    | 假冒車主憑證           |
| **T** | **Tampering** 竄改                  | Integrity       | 修改韌體               |
| **R** | **Repudiation** 否認                | Non-repudiation | 否認下載過 OTA         |
| **I** | **Information Disclosure** 資訊揭露 | Confidentiality | 萃取金鑰               |
| **D** | **Denial of Service** 阻斷服務      | Availability    | 癱瘓 CAN               |
| **E** | **Elevation of Privilege** 提權     | Authorization   | bypass Security Access |

> [!tip] 記憶法
> **STRIDE** 直接記英文縮寫——每類對應屬性也記。

---

## STRIDE 應用於 TARA

```
For each Asset:
  For each STRIDE category:
    ├── 是否適用？
    ├── 如何被攻擊？
    └── 產生 Threat Scenario
```

### 範例：TCU 韌體 (Asset)

```yaml
asset: "TCU Firmware"

stride_analysis:
  spoofing:
    applicable: Yes
    threat: "Attacker spoofs OEM signing key"

  tampering:
    applicable: Yes # ★ 主要威脅
    threat: "Firmware tampered during OTA"

  repudiation:
    applicable: Limited
    threat: "OEM denies signing certain firmware version"

  information_disclosure:
    applicable: Yes
    threat: "Firmware reverse-engineered to find IP"

  denial_of_service:
    applicable: Yes
    threat: "Malicious firmware causes brick"

  elevation_of_privilege:
    applicable: Yes
    threat: "Firmware exploit gives kernel access"
```

---

## STRIDE 變體

### STRIDE-per-Element

對 DFD (Data Flow Diagram) 中每個元素檢視：

- Process → STRIDE 全套
- Data Store → TID（Tampering / Information Disclosure / Denial of Service）
- Data Flow → TID
- External Entity → SR（Spoofing / Repudiation）

### STRIDE-per-Interaction

對 DFD 中每個**互動**（資料流）檢視。

---

## DREAD — 風險評估（已被棄用）

> [!warning]
> **DREAD 已被 Microsoft 棄用**（2008）。
> 列在此處是因為證照可能考其名稱含義，**不建議實際使用**。

| 縮寫  | 名稱                | 含義         |
| ----- | ------------------- | ------------ |
| **D** | **Damage**          | 損害程度     |
| **R** | **Reproducibility** | 可重現度     |
| **E** | **Exploitability**  | 可利用度     |
| **A** | **Affected Users**  | 受影響使用者 |
| **D** | **Discoverability** | 可發現度     |

每項評分 1-10，平均後得 Risk Score。

**棄用原因**：

- 評分主觀
- 不同人結果差異大
- 無法重現

**替代**：ISO 21434 的 **Impact + Attack Feasibility** 方法更系統化。

---

## PASTA — Process for Attack Simulation and Threat Analysis

PASTA 是另一個業界 framework，七階段：

1. Define Objectives
2. Define Technical Scope
3. Application Decomposition
4. Threat Analysis
5. Vulnerability Analysis
6. Attack Modeling
7. Risk Analysis

**與 ISO 21434 對比**：

- PASTA 更廣泛（含業務目標）
- TARA 更聚焦於汽車產品

---

## OWASP Top 10 / CWE Top 25

| 框架                | 範圍            | 與 21434 關係              |
| ------------------- | --------------- | -------------------------- |
| **OWASP Top 10**    | Web/App 弱點    | 適用 OEM 後端、HMI Web     |
| **CWE Top 25**      | 軟體弱點        | 適用車輛軟體（汽車版適用） |
| **MITRE ATT&CK**    | 攻擊技術知識庫  | 適用威脅情報、Red Team     |
| **MITRE Auto-ISAC** | 汽車專屬 ATT&CK | 直接適用 TARA              |

---

## ISO 21434 採用什麼？

> [!important]
> ISO 21434 **不規範**特定 threat modeling 方法。
> Clause 15.4 只說「**系統化方法**」。
>
> 實務上業界混用：
>
> - **STRIDE**：基礎識別
> - **Attack Trees**：路徑分析
> - **UN R155 Annex 5**：清單對照
> - **MITRE / CVE**：威脅情報

---

## 證照考點

> [!important]
>
> 1. **STRIDE** 是業界最常用的識別方法
> 2. STRIDE 各類對應**資安屬性**（Spoofing → Authenticity 等）
> 3. **DREAD 已棄用**——可記但不用
> 4. ISO 21434 **不規範**特定方法
> 5. UN R155 Annex 5 可作為 **威脅清單** 參考

---

## Related Notes

- [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]
- [[13-Annexes-Tools/04-Attack-Trees\|13-Annexes-Tools/04-Attack-Trees]]
- [[13-Annexes-Tools/02-Mapping-to-UN-R155\|13-Annexes-Tools/02-Mapping-to-UN-R155]]

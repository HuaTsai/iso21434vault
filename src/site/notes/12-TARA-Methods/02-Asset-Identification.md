---
{"dg-publish":true,"permalink":"/12-tara-methods/02-asset-identification/","title":"資產識別 (Asset Identification)","tags":["iso-21434","concept-note","tara","asset"],"dg-note-properties":{"title":"資產識別 (Asset Identification)","source_pdf":"內部彙整 (ISO 21434 Clause 15.3)","part":"Clause 15.3","keywords":["asset","identification","cybersecurity-properties"],"tags":["iso-21434","concept-note","tara","asset"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義 (Clause 3.1.2)
> Object that has value, or contributes to value.
>
> **Note**: An asset has one or more cybersecurity properties whose compromise can lead to one or more damage scenarios.

> [!important] 雙重條件（Clause 15.3.2 要求）
> 識別出來的 asset **必須**同時滿足：
>
> 1. **有價值**（資料、功能、通訊、硬體等）
> 2. **具至少一個 cybersecurity property**（CIA + 其他屬性）
> 3. **該屬性 compromise 可導致一個或多個 damage scenario**
>
> 鏈結圖：`Asset → Cybersecurity Property → Damage Scenario`
>
> 缺乏 cybersecurity property 或無法連到 damage scenario 的物件（如車內地毯）**不應**列入 asset register，否則 TARA 範圍會失控。

---

## Asset 到 Damage Scenario 的鏈結範例

```
Asset: ECU 韌體
   └── Property: Integrity（完整性）
         └── 被破壞 → Damage Scenario: 韌體被植入後門，攻擊者遠端控制煞車 → 失控撞擊
   └── Property: Authenticity（真實性）
         └── 被破壞 → Damage Scenario: 偽造韌體燒入 → 永久後門

Asset: 車主 PII
   └── Property: Confidentiality
         └── 被破壞 → Damage Scenario: 個資洩漏，違反 GDPR → 法規罰款 + 信任損失
```

---

## Asset 的類型

```
1. Data 資料
   ├── 韌體 image
   ├── 加密金鑰
   ├── 憑證
   ├── 車主 PII
   ├── 行駛紀錄
   ├── 配置參數
   └── 校正資料

2. Functions 功能
   ├── 煞車控制
   ├── 轉向控制
   ├── eCall 服務
   ├── OTA 更新
   └── 診斷服務

3. Communication 通訊
   ├── CAN 訊息
   ├── 蜂巢資料
   ├── V2X 訊息
   └── 診斷 session

4. Hardware 硬體（廣義 asset）
   ├── HSM
   ├── ECU
   ├── 感測器
   └── 致動器
```

---

## 識別 Asset 的方法

```
方法 1：由 Item Definition 推導
   └── 從 functions → 達成功能所需的資料/通訊

方法 2：Data Flow Analysis
   └── 追蹤所有資料流，每個節點/邊都可能是 asset

方法 3：Threat-Driven
   └── 從威脅情境反推：「攻擊者想破壞什麼？」

方法 4：Reference List（業界清單）
   └── 對照業界 / UN R155 Annex 5 威脅清單
```

> [!tip]
> **多方法併用**——單一方法易遺漏。

---

## 為每個 Asset 識別 Cybersecurity Properties

每個 asset 需評估哪些屬性需要被保護：

```
資安屬性（CIA 三主屬性 + 補充屬性）：
├── Confidentiality （機密性）
├── Integrity       （完整性）
├── Availability    （可用性）
├── Authenticity    （真實性）
├── Authorization   （授權）
├── Non-repudiation （不可否認性）
└── (Auditability)  （可稽核性）
```

---

## Asset 評估範例

```yaml
asset_register:
  - id: A-001
    name: "TCU Firmware Image"
    type: data
    location: "Flash memory (encrypted partition)"
    properties_to_protect:
      confidentiality: low # 反組譯不致命，但會洩 IP
      integrity: critical # 修改 → 攻擊者控制 TCU
      availability: high # 壞掉車輛無法啟動
      authenticity: critical # 確保來源可信
      authorization: high # 只有授權者可更新
    value_to_attacker:
      - "Reverse engineering"
      - "Injecting backdoor"

  - id: A-002
    name: "TLS Client Private Key"
    type: cryptographic-material
    location: "HSM (non-exportable)"
    properties_to_protect:
      confidentiality: critical # 洩漏 = 完全身分仿冒
      integrity: critical
      availability: medium
      authenticity: n/a # 私鑰本身不需 auth
    value_to_attacker:
      - "Impersonate vehicle"
      - "Decrypt past communication (if no PFS)"

  - id: A-003
    name: "Vehicle Location Data"
    type: data
    location: "RAM + cellular transmission"
    properties_to_protect:
      confidentiality: high # PII / 追蹤隱私
      integrity: medium # 偽造位置可能影響功能
      availability: medium # 不可用 → 服務降級
      authenticity: medium
    privacy_concerns:
      - "GDPR / CCPA / PIPL applicable"
      - "Anonymisation required for non-essential use"

  - id: A-004
    name: "Brake Control CAN Message"
    type: communication
    properties_to_protect:
      confidentiality: low # 不秘密
      integrity: critical # 偽造 → 直接 safety hazard
      availability: critical # 缺失 → 失控
      authenticity: critical # 必須驗證來源
    safety_impact: ASIL_D # 共享 Safety 視角
```

---

## Asset 與 Cybersecurity Property 的對應

> [!important]
> 不是每個 asset 都需保護**所有屬性**。
> 例如：
>
> - **Vehicle Speed CAN Message**：機密性低，但完整性/真實性極關鍵
> - **Vehicle Diagnostic Data**：機密性中（PII），完整性中
> - **Customer Account Token**：所有屬性都關鍵
>
> 評估**正確的屬性 + 等級** 是後續 Threat Scenario 識別的基礎。

---

## Asset 識別的常見遺漏

> [!warning] 容易被忘的 Assets
>
> 1. **時序資訊**：時鐘同步、計時器
>    - 偽造時間 → 過期 token 被誤接受
> 2. **配置資料**：calibration、policy
>    - 改變配置 → 改變車輛行為
> 3. **日誌**：security log、event log
>    - 攻擊者刪 log → 隱藏行蹤
> 4. **隨機性**：RNG output、nonces
>    - 預測 RNG → 破解加密
> 5. **元資料**：版本號、序號
>    - 偽造版本 → bypass 更新檢查
> 6. **內部介面**：HSM API、debug port
>    - 認為「內部」就忽略
> 7. **間接 asset**：開發環境（程式碼庫、簽章伺服器）
>    - 屬於另一個 Item，但**有依賴關係**

---

## Asset Inventory 與 SBOM 的關係

```
SBOM：Software Bill of Materials
  └── 列出所有軟體元件

Asset Inventory：
  └── 列出所有「有價值」的 entities

兩者不完全相同：
  - SBOM 偏「**有什麼**」
  - Asset 偏「**保護什麼**」

實務上：SBOM 是 Asset Inventory 的輸入之一
```

---

## 證照考點

> [!important]
>
> 1. Asset = **任何有價值的東西**（不限資料）
> 2. 識別需含 **資料 + 功能 + 通訊 + 硬體**
> 3. 每個 Asset 評估**CIA + 其他屬性**（Authenticity / Authorization / Non-repudiation / Auditability）
> 4. **不是每個 asset 都需保護所有屬性**
> 5. 常見遺漏：時序、配置、日誌、RNG
> 6. **SBOM 是輸入**之一，但不等同 Asset Inventory

---

## Related Notes

- [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]
- [[12-TARA-Methods/03-Threat-Scenario\|12-TARA-Methods/03-Threat-Scenario]]
- [[12-TARA-Methods/04-Impact-Rating\|12-TARA-Methods/04-Impact-Rating]]
- [[06-Concept-Phase/01-Item-Definition\|06-Concept-Phase/01-Item-Definition]]
- [[01-Foundations/02-Key-Terms-Definitions\|01-Foundations/02-Key-Terms-Definitions]]

## Practice

- [[12-TARA-Methods/Practice-TARA\|12-TARA-Methods/Practice-TARA]]

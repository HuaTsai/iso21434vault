---
{"dg-publish":true,"permalink":"/09-production/02-provisioning/","title":"金鑰與憑證植入 (Provisioning)","tags":["iso-21434","concept-note","production","provisioning"],"dg-note-properties":{"title":"金鑰與憑證植入 (Provisioning)","source_pdf":"內部彙整 (ISO 21434 Clause 12 + 業界實務)","part":"Clause 12","keywords":["provisioning","key-injection","certificate","hsm"],"tags":["iso-21434","concept-note","production","provisioning"],"created":"2026-05-11"}}
---


## 是什麼？

> 在製造過程中，將**獨特的安全憑證 / 金鑰**注入每個產品的步驟。

```
為什麼必要？
└── 每個車輛 / ECU 應有「唯一身分」：
    ├── TLS client certificate
    ├── V2X pseudonym key
    ├── SecOC master key
    ├── Diagnostic security key
    └── Device unique ID
```

---

## Provisioning 的安全要求

```
✓ 金鑰生成於受信任環境（HSM、Secure Facility）
✓ 金鑰**不可從 HSM 萃取**
✓ 注入過程加密 / 受保護
✓ 每次注入有紀錄（誰、何時、何 device）
✓ 注入後驗證成功
✓ 廢品的金鑰**標記為廢棄**
```

---

## Provisioning 流程

```
1. 設備上線
   ↓
2. 設備產生 unique ID（在 HSM 內生成）
   ↓
3. 設備產生 key pair（HSM 內，private key 不離開）
   ↓
4. 設備產生 CSR (Certificate Signing Request)
   ↓
5. CSR 傳至 Manufacturing CA
   ↓
6. CA 簽發憑證
   ↓
7. 憑證 + Root CA chain 注入設備
   ↓
8. 對稱金鑰（如 SecOC）由 Master Key 派生注入
   ↓
9. 全部驗證測試
   ↓
10. 鎖定 provisioning interface（不可再 provision）
    ↓
11. 紀錄存入 PLM / Secure Database
```

---

## 兩種金鑰生成模式

### 模式 A：Device-side Generation（推薦）

```
HSM 內生成 → private key 永遠不離開 HSM
   ↓
僅 export public key → CSR → CA 簽署
   ↓
注入 device certificate（含 public key）
```

**優點**：私鑰永遠不暴露，最安全。
**缺點**：需要 device 有 HSM；CSR 流程複雜。

### 模式 B：CA-side Generation

```
CA 端產生 key pair
   ↓
加密傳輸至 device
   ↓
device 解密 + 安裝
```

**優點**：device 簡單。
**缺點**：私鑰曾經離開 HSM，風險較高。

> [!warning]
> **模式 A 是 ISO 21434 推薦做法**。

---

## Manufacturing PKI

```
Vehicle Root CA
   ↓ 簽署
Manufacturing Sub-CA
   ↓ 簽署
Device Certificates (一個 device 一張)
```

**注意**：

- Root CA private key **離線保管**（HSM offline）
- Sub-CA 用於日常 provisioning
- Sub-CA 受 attack 時，可撤銷並重簽 Sub-CA（不影響 Root）

---

## V2X 特殊情境

V2X 使用 **SCMS (Security Credential Management System)**：

```
Vehicle 持有：
├── Long-term Certificate (LTC) - 身分
└── 多個 Pseudonym Certificates (PC) - 短期匿名

PC 每週/每月輪換：
├── Vehicle 向 SCMS 請求新 PC
├── SCMS 驗證身分 + 簽發
└── 防 Tracking + 抗誤行為
```

---

## SecOC Master Key 派生

```
Manufacturing Master Key (HSM)
   ↓ KDF (Key Derivation)
Vehicle Master Key
   ↓ KDF
SecOC Key per CAN message ID
```

各車輛獨立 key，避免一車被攻破 → 全車隊都受影響。

---

## Provisioning 紀錄要求

```yaml
provisioning_record:
  device_id: "TCU-SN-20260511-12345"
  manufacturing_date: 2026-05-11T14:23:11Z
  manufacturing_site: "Plant ABC"
  station: "PROV-Station-07"
  operator: "Operator ID O-001" # 不是個人姓名（隱私）

  provisioned_keys:
    - key_id: "TLS-Client-Key-001"
      type: "ECDSA P-256"
      cert_serial: "C-2026-XXXX"
      ca_issuer: "OEM Manufacturing Sub-CA"
    - key_id: "SecOC-Master-Key-Hash"
      type: "AES-128 (derived)"
      kdf_input_hash: "..."

  verification:
    boot_test_passed: true
    self_test_passed: true
    cert_verification_passed: true

  signature: "Manufacturing CA signature over this record"
```

---

## 廢品處置

> [!warning]
> 製造過程中的廢品（不良品、測試品）**不可直接丟棄**。
>
> 必要動作：
>
> 1. **金鑰撤銷**：通知 CA 撤銷對應憑證
> 2. **資料抹除**：HSM zeroize
> 3. **實體銷毀**：粉碎 / 高溫
> 4. **紀錄**：銷毀紀錄留存

---

## 證照考點

> [!important]
>
> 1. Provisioning **金鑰在 HSM 內生成**（私鑰不離開）
> 2. **每個 device 唯一身分**（不可全車隊共用）
> 3. **Manufacturing PKI** 分層
> 4. **V2X SCMS** 是特殊情境
> 5. **廢品金鑰需撤銷**

---

## Related Notes

- [[09-Production/01-Production-Controls\|09-Production/01-Production-Controls]]
- [[07-Product-Development/04-HW-SW-Considerations\|07-Product-Development/04-HW-SW-Considerations]]

## Practice

- [[09-Production/Practice-Production\|09-Production/Practice-Production]]

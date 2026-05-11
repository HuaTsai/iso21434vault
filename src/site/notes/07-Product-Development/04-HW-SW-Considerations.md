---
{"dg-publish":true,"permalink":"/07-product-development/04-hw-sw-considerations/","title":"HW / SW / 介面資安考量","tags":["iso-21434","concept-note","product-development","hw-sw"],"dg-note-properties":{"title":"HW / SW / 介面資安考量","source_pdf":"內部彙整 (ISO 21434 Clause 10 + 業界實務)","part":"Clause 10","keywords":["hardware","software","interface","hsm","secure-boot"],"tags":["iso-21434","concept-note","product-development","hw-sw"],"created":"2026-05-11"}}
---


## 為什麼分開討論？

```
HW 層：硬體無法修補（一但出貨）
SW 層：可透過 OTA 修補
介面層：跨 HW + SW，攻擊面最大
```

不同層級的資安考量、生命週期、修補機制都不同。

---

## 硬體 (HW) 資安要素

### 1. Hardware Security Module (HSM)

```
HSM 的核心職責：
├── 金鑰生成（TRNG）
├── 金鑰儲存（不可萃取）
├── 加密運算（簽章、驗章、AES）
├── 安全啟動 (root of trust)
├── 副通道防護（DPA、SPA）
└── 防篡改 (tamper resistance)
```

汽車 HSM 標準：

- **EVITA**（早期共識）
  - EVITA Full / Medium / Light
- **AUTOSAR Crypto Stack** API
- **FIPS 140-2 / 140-3 認證**

### 2. Secure Boot Chain

```
Boot ROM (immutable)
  ↓ verify (with root pubkey in eFuse)
2nd-stage Bootloader (updatable, signed)
  ↓ verify
Application Firmware
  ↓ verify
(Optional) Runtime Integrity Check
```

→ [[09-Production/02-Provisioning\|09-Production/02-Provisioning]] (root key 注入)

### 3. eFuse / OTP

一次性可程式化記憶體（不可改）：

- Root public key hash
- Device unique ID
- Anti-rollback counter
- 配置位元（debug 關閉等）

### 4. Debug 介面控制

> [!warning]
> JTAG / SWD 出貨前**必須**：
>
> - 完全 disable（推薦）
> - 或加 authentication（次選）

### 5. 抗篡改 / 抗副通道

- Tamper sensors（外殼開啟偵測）
- DPA / SPA resistance 設計
- Timing attack resistance（constant-time crypto）
- Fault injection resistance（電壓/時脈 glitch）

---

## 軟體 (SW) 資安要素

### 1. Memory Safety

```
語言層級：
├── C/C++ → 需嚴格 MISRA、CERT、SAST
├── Rust → 預設 memory safe
└── Java/Python → managed memory

執行時：
├── ASLR（如平台支援）
├── DEP / NX bit
├── Stack canaries
└── Control Flow Integrity (CFI)
```

### 2. Secure Coding Standards

- **MISRA C / C++**
- **CERT C / C++**
- **AUTOSAR C++ Guidelines**
- 編譯器警告全開 (-Wall -Wextra -Werror)

### 3. Cryptographic Implementation

> [!important]
> **不要自己寫 crypto**。使用：
>
> - 平台 HSM
> - 已驗證的 library（mbedTLS、wolfSSL、OpenSSL）

常見錯誤：

- ECB mode（不該用）
- 弱 RNG（如 rand()）
- Hardcoded keys（嚴禁）
- Custom crypto algorithm（嚴禁）

### 4. Memory Protection

- MPU (Microcontroller MPU) / MMU
- 分離 user/kernel
- 分離 ASIL D / ASIL B / QM partitions

### 5. Logging & Audit

```yaml
secure_logging:
  what_to_log:
    - "Security-relevant events"
    - "Authentication attempts"
    - "Configuration changes"
    - "Update events"

  protection:
    - "Tamper-evident (signed entries)"
    - "Ring buffer with persistence"
    - "Bounded growth (no DoS)"

  what_NOT_to_log:
    - "Cryptographic keys"
    - "PII (without encryption)"
    - "Full authentication credentials"
```

---

## 介面層資安要素

### CAN Bus 資安

> 詳細參考 user CLAUDE.md 的 network-security-rules.md

```
1. SecOC (AUTOSAR Secure Onboard Communication)
   ├── CMAC + Freshness Value
   ├── 抗 replay
   └── 標準化 AUTOSAR R19-11+

2. 訊息過濾 (Gateway-based)
   ├── White-list per zone
   ├── Rate limiting
   └── 不合預期訊息丟棄

3. IDS (Intrusion Detection)
   ├── 頻率異常
   ├── 訊息類型異常
   └── 訊號值異常
```

### Automotive Ethernet 資安

```
1. MACsec (IEEE 802.1AE)
   ├── GCM-AES-128/256
   └── 連線層加密

2. IPsec
   ├── 應用於 DoIP
   └── 強加密、抗 replay

3. VLAN segmentation
   ├── 分離 ADAS / Infotainment / Diagnostic
   └── Gateway 控制 inter-VLAN
```

### Cellular / V2X

```
Cellular：
├── TLS 1.3 + Certificate pinning
├── Per-device cert (mTLS)
└── 抗 IMSI catcher

V2X：
├── IEEE 1609.2 (Security)
├── SCMS (PKI)
├── Pseudonym certificates
└── Misbehavior detection
```

### UDS (Diagnostic) 資安

```
UDS Security Access (0x27)
├── Seed-Key with cryptographically strong key
├── 失敗鎖定（10 次後鎖 10 min）
├── Session-based authorization
└── 角色分級（Tester、Production、OEM）

更強的方案：
├── UDS Authentication (0x29) - 基於憑證
└── Diag-over-DoIP + IPsec
```

---

## HW/SW/介面 整合視角

```
+──────────────────────────────────────+
│           Application SW              │
│  • Secure coding                      │
│  • Memory safety                       │
│  • Crypto library use                  │
+─────────────┬────────────────────────+
              │
+──────────────────────────────────────+
│            BSW / Middleware           │
│  • SecOC                              │
│  • Crypto stack                       │
│  • TLS stack                          │
+─────────────┬────────────────────────+
              │
+──────────────────────────────────────+
│           OS / Hypervisor             │
│  • Partition isolation                │
│  • Privilege levels                   │
│  • MPU configuration                  │
+─────────────┬────────────────────────+
              │
+──────────────────────────────────────+
│              Hardware                  │
│  • HSM                                │
│  • Secure Boot ROM                    │
│  • eFuse / OTP                        │
│  • Tamper sensors                     │
│  • Debug lockout                      │
+──────────────────────────────────────+
              │
+──────────────────────────────────────+
│             External I/F              │
│  CAN / Ethernet / Cellular / UDS      │
│  • Per-protocol security              │
│  • Trust boundary checks              │
+──────────────────────────────────────+
```

---

## 證照考點

> [!important] 高頻考點
>
> 1. **HSM** 是汽車資安的核心硬體
> 2. **Secure Boot Chain** 從 ROM 開始（root of trust）
> 3. **eFuse / OTP** 儲存不可變的安全資料
> 4. **Debug 介面**出貨前必須關閉或加保護
> 5. SecOC 是 **CAN 訊息驗證**的 AUTOSAR 標準
> 6. **MACsec / IPsec** 用於 Ethernet
> 7. **UDS Security Access** 是診斷認證
> 8. **不要自己寫 crypto**

---

## Related Notes

- [[07-Product-Development/01-Design-Requirements\|07-Product-Development/01-Design-Requirements]]
- [[09-Production/02-Provisioning\|09-Production/02-Provisioning]]
- [[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]

## Practice

- [[07-Product-Development/Practice-Development\|07-Product-Development/Practice-Development]]

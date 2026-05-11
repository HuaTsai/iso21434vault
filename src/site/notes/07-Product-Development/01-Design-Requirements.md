---
{"dg-publish":true,"permalink":"/07-product-development/01-design-requirements/","title":"設計階段：資安需求與架構","tags":["iso-21434","concept-note","product-development","design"],"dg-note-properties":{"title":"設計階段：資安需求與架構","source_pdf":"內部彙整 (ISO 21434 Clause 10.4.1-10.4.2)","part":"Clause 10","keywords":["design","requirements","architecture","security-by-design"],"tags":["iso-21434","concept-note","product-development","design"],"created":"2026-05-11"}}
---


## Clause 10 的範圍

ISO 21434 Clause 10 涵蓋產品開發 V-model 的左半邊：

```
Cybersecurity Concept (Clause 9)
      ↓
Cybersecurity Requirements   ← 10.4.1
      ↓
Security Architecture        ← 10.4.2
      ↓
Detailed Design (HW + SW)
      ↓
Implementation
      ↓
Verification                 ← 10.4.3
```

---

## Cybersecurity Requirements

> [!quote]
> 從 Cybersecurity Concept 細化為**可實作、可驗證**的需求。

### CS Requirement 的格式

```yaml
cs_requirement:
  id: CSR-TCU-001
  parent_goal: CG-001 (Firmware integrity)
  parent_concept: "Secure boot chain"

  requirement: >
    The TCU bootloader shall verify the application image
    signature using ECDSA-P256-SHA256 before transferring control.

  attributes:
    verifiable: true
    atomic: true
    feasible: true

  verification_method:
    - "Unit test: signature verification with valid/invalid signatures"
    - "Integration test: tampered image rejection"

  allocated_to:
    component: "Bootloader Module"
    layer: "Boot ROM + 2nd-stage bootloader"

  related_cal: CAL-3
```

### Requirement 的「品質」

| 屬性            | 描述                   |
| --------------- | ---------------------- |
| **Verifiable**  | 可被測試/分析驗證      |
| **Atomic**      | 單一可分解單元         |
| **Unambiguous** | 唯一解釋               |
| **Traceable**   | 對應 Goal/Concept/Test |
| **Feasible**    | 技術可行               |
| **Necessary**   | 不冗餘                 |

---

## Security Architecture

### 是什麼？

> [!quote]
> 「**架構層級**的資安設計，包括元件、介面、責任分配、信任邊界。」

### Security Architecture 應呈現

```
1. 信任邊界 (Trust Boundaries)
   ├── 哪些區域信任彼此
   └── 跨界資料需驗證

2. 元件分配
   ├── CS Goals 如何分配到元件
   └── 各元件的責任

3. 安全機制位置
   ├── HSM、Secure Boot、Crypto
   ├── IDS、Log、Monitor
   └── Authentication、Authorization

4. 資料流 (Data Flow)
   ├── 哪些資料流經哪些介面
   └── 受保護的層級

5. 攻擊面 (Attack Surface)
   ├── 對外介面清單
   └── 已知的攻擊路徑
```

---

## 範例：TCU Security Architecture

```
+──────────────────────────────────────────────────+
│              External Trust Boundary               │
+───────────┬──────────────────────────┬───────────+
            ↓                          ↓
+───────────────────────────────────────────────────+
│  ┌──────────────┐                                  │
│  │ Cellular     │  ← TLS 1.3 + mTLS              │
│  │   Modem      │     (Authentication boundary)   │
│  └──────┬───────┘                                  │
│         │                                          │
│  ┌──────┴───────────────────────────────────┐    │
│  │            Application CPU              │    │
│  │  ┌─────────────────────────────────┐    │    │
│  │  │  TLS Handler                     │    │    │
│  │  │  ─ Cert pinning                  │    │    │
│  │  │  ─ HSM-backed private key       │    │    │
│  │  └────────┬─────────────────────────┘    │    │
│  │           │                              │    │
│  │           ↓                              │    │
│  │  ┌────────────────────────────────┐     │    │
│  │  │ Application Logic              │     │    │
│  │  └────────┬───────────────────────┘     │    │
│  │           │                              │    │
│  │           ↓                              │    │
│  │  ┌────────────────────────────────┐     │    │
│  │  │ CAN/SecOC Module               │     │    │
│  │  │ ─ CMAC verification            │     │    │
│  │  └────────┬───────────────────────┘     │    │
│  └───────────┼──────────────────────────────┘    │
│              │                                    │
│         ┌────▼────┐         ┌──────────────┐    │
│         │   HSM   │         │ Secure Flash │    │
│         │  ─keys  │         │ ─ FW Image   │    │
│         │  ─sign  │         │ ─ Signed     │    │
│         └─────────┘         └──────────────┘    │
│                                                   │
│              Internal Trust Boundary              │
+───────────────────────────────────────────────────+
                       ↓
                  CAN Bus
              (External to TCU)
```

---

## Trust Boundary 分析

```
每個 Trust Boundary 對應一個「驗證點」：

External → Internal：需驗證
   ├── TLS 終止點：驗證憑證
   ├── OTA 接收點：驗證簽章
   ├── 診斷接收點：驗證 Security Access (UDS 0x27)
   └── CAN 接收點：驗證 SecOC MAC

Internal → External：需保護
   ├── 加密通訊
   └── 不洩露敏感資訊
```

---

## 攻擊面分析 (Attack Surface Analysis)

```yaml
attack_surface:
  external_interfaces:
    - cellular_5g_lte:
        exposure: high
        protocols: ["TLS 1.3", "QUIC"]
        attack_vectors:
          - "TLS handshake malformation"
          - "Cert validation bypass"
          - "Cellular protocol fuzzing"

    - obd_diagnostic:
        exposure: high # 物理但易達
        protocols: ["UDS over DoIP", "ISO 14229"]
        attack_vectors:
          - "Security Access bypass"
          - "Flash reprogramming abuse"

    - can_bus_external:
        exposure: medium
        protocols: ["CAN 2.0B + SecOC"]
        attack_vectors:
          - "SecOC counter manipulation"
          - "Replay attack"

    - usb_service_port:
        exposure: low # 物理且少用
        attack_vectors:
          - "Malicious USB injection"

  internal_interfaces: # 信任區域內
    - hsm_api: low
    - flash_spi: low

  attack_surface_reduction:
    - "USB disabled in production firmware"
    - "Diagnostic only enabled with Security Access"
    - "Cellular only TLS 1.3 (older versions rejected)"
```

---

## 安全設計原則 (Security by Design)

| 原則                            | 說明       | 例子                                  |
| ------------------------------- | ---------- | ------------------------------------- |
| **Least Privilege**             | 最小權限   | 應用層不直接存 HSM 內部               |
| **Defense in Depth**            | 多層防禦   | Secure boot + 簽章 + 執行時檢查       |
| **Fail Secure**                 | 故障即安全 | 簽章驗證失敗 → 不執行                 |
| **Separation of Duties**        | 責任分離   | 開發者無法簽韌體（需 HSM + 兩人授權） |
| **Complete Mediation**          | 完全仲裁   | 每次存取都檢查                        |
| **Open Design**                 | 公開設計   | 不靠隱藏實現的安全                    |
| **Psychological Acceptability** | 可用性     | 安全機制不影響使用體驗                |
| **Economy of Mechanism**        | 簡潔       | 越複雜越易出錯                        |

---

## CS Requirement 分層

```
System-level CS Requirements
   ↓ 分配
Subsystem-level (HW、SW)
   ↓ 分配
Component-level
   ↓ 分配
Unit-level (function、module)
```

每一層的需求都需 traceable。

---

## 證照考點

> [!important] 高頻考點
>
> 1. CS Requirement 是 **CS Concept 的細化**，可實作可驗證
> 2. **每個 Requirement** 必須對應驗證方法
> 3. **Trust Boundary** 是安全架構核心概念
> 4. **攻擊面降低** 是安全設計原則
> 5. **Security by Design** 八大原則
> 6. **CS Requirement 分層 + Traceable**
> 7. Security Architecture 是 Clause 10 必要 WP

---

## Related Notes

- [[06-Concept-Phase/04-Cybersecurity-Concept\|06-Concept-Phase/04-Cybersecurity-Concept]]
- [[07-Product-Development/02-Integration-Verification\|07-Product-Development/02-Integration-Verification]]
- [[07-Product-Development/03-Weakness-Vulnerability-Analysis\|07-Product-Development/03-Weakness-Vulnerability-Analysis]]
- [[07-Product-Development/04-HW-SW-Considerations\|07-Product-Development/04-HW-SW-Considerations]]

## Practice

- [[07-Product-Development/Practice-Development\|07-Product-Development/Practice-Development]]

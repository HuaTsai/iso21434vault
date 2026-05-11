---
{"dg-publish":true,"permalink":"/09-production/01-production-controls/","title":"生產資安控制","tags":["iso-21434","concept-note","production"],"dg-note-properties":{"title":"生產資安控制","source_pdf":"內部彙整 (ISO 21434 Clause 12)","part":"Clause 12","keywords":["production","manufacturing","controls"],"tags":["iso-21434","concept-note","production"],"created":"2026-05-11"}}
---


## 為什麼生產階段需要資安？

```
即使設計完美 → 生產過程出錯 = 整批產品有缺陷
```

生產階段的資安風險：

- 金鑰被洩漏（從生產線竊取）
- 偽造產品（仿冒、回收再販）
- Debug 介面未鎖（出貨忘記關 JTAG）
- 不正確版本的韌體被燒入
- 製程被竄改（攻擊者植入後門）

---

## Clause 12 主要要求

```
1. Production Control Plan
   ├── 識別生產中可能影響資安的步驟
   └── 規劃控制措施

2. Production Cybersecurity Activities
   ├── 安全 Provisioning（金鑰、憑證）
   ├── 韌體完整性驗證
   ├── Debug 介面關閉
   ├── 序號 / 防偽冒
   └── 廢品處置

3. 紀錄
   └── 可追溯每個出廠單元
```

---

## Production Control Plan 範本

```yaml
production_control_plan:
  item: "TCU-2026"
  production_site: "Plant ABC"

  cs_relevant_steps:
    - step: "Firmware flashing"
      controls:
        - "Verify firmware checksum + signature before flash"
        - "Use signed flashing tool (no manual files)"
        - "Log each flash event"

    - step: "Key/Certificate Provisioning"
      controls:
        - "HSM-based key generation (per device)"
        - "Cert chain installation"
        - "Verify provisioning success"
        - "Provisioning log encrypted + signed"

    - step: "Debug Interface Lockout"
      controls:
        - "Blow eFuse to permanently disable JTAG"
        - "Verification test confirms JTAG unresponsive"
        - "Audit trail of each device"

    - step: "End-of-Line Test"
      controls:
        - "Functional test"
        - "Security check: boot chain verification"
        - "Anti-tamper sensor check"

    - step: "Packaging + Shipping"
      controls:
        - "Tamper-evident seal"
        - "Serial number tracking"
        - "Supply chain integrity (transport security)"

  audit_records:
    - "Each device serial → provisioning record"
    - "Each device → firmware version installed"
    - "Each device → test results"
    - "Anomalies → security event log"
```

---

## Production 階段的 Threats

| 威脅             | 緩解                                  |
| ---------------- | ------------------------------------- |
| 內部人員竊取金鑰 | HSM-based key gen，金鑰**不離開 HSM** |
| 仿冒產品流通     | 序號 + PKI + 真品檢驗機制             |
| 韌體被植入後門   | 簽章流程**離線 + dual signer**        |
| Debug 介面未鎖   | 程式化 + Validation 確認              |
| 製程被改動       | 生產線變更管理 + 監控                 |
| 廢品流出         | 廢品確實銷毀（含敏感資訊）            |

---

## 與 Clause 5（CSMS）、Clause 10（開發）的對接

```
CSMS (Clause 5)
   ├── 製造設施的 CS 政策
   ├── 員工背景檢查
   └── 訪客管制

Development (Clause 10)
   ├── 設計時即考慮可生產性（DFM）
   ├── 提供 Production Spec
   └── 提供測試規範

Production (Clause 12)
   ├── 執行 Spec
   └── 紀錄
```

---

## 證照考點

> [!important]
>
> 1. Production 階段需有 **Production Control Plan**
> 2. **金鑰生成在 HSM 內**，不外傳
> 3. **Debug 介面**出貨前必須鎖（eFuse）
> 4. **可追溯性**：每個出廠單元有紀錄
> 5. 廢品處置不可忽略

---

## Related Notes

- [[09-Production/02-Provisioning\|09-Production/02-Provisioning]]
- [[07-Product-Development/04-HW-SW-Considerations\|07-Product-Development/04-HW-SW-Considerations]]
- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]

## Practice

- [[09-Production/Practice-Production\|09-Production/Practice-Production]]

---
{"dg-publish":true,"permalink":"/07-product-development/02-integration-verification/","title":"整合與驗證 (Verification)","tags":["iso-21434","concept-note","product-development","verification"],"dg-note-properties":{"title":"整合與驗證 (Verification)","source_pdf":"內部彙整 (ISO 21434 Clause 10.4.2)","part":"Clause 10","keywords":["integration","verification","testing","traceability"],"tags":["iso-21434","concept-note","product-development","verification"],"created":"2026-05-11"}}
---


## Verification vs Validation

```
Verification (Clause 10)
   ├── 「需求是否被正確實作？」
   ├── 元件/系統層級
   ├── 「Are we building it right?」
   └── 對應 V-model 右半邊（除頂部）

Validation (Clause 11)
   ├── 「資安目標是否在車輛情境下達成？」
   ├── **車輛層級**
   ├── 「Are we building the right thing?」
   └── V-model 最頂部
```

→ 詳見 [[00-Dashboard/Exam-Traps#Trap 5\|00-Dashboard/Exam-Traps#Trap 5]]

---

## Verification 的層級

```
                Vehicle-level Validation (Clause 11)
                          ↑
                ┌─────────┴─────────┐
                ↑                   ↑
         System Integration Verification
                ↑                   ↑
        ┌───────┴───────┐  ┌────────┴────────┐
        ↑               ↑  ↑                 ↑
   Component       Component  Component   Component
   Integration     Integration Integration Integration
        ↑               ↑       ↑             ↑
    ┌───┴───┐       ┌───┴───┐ ...        ...
    ↑       ↑       ↑       ↑
   Unit   Unit    Unit    Unit
   Test   Test    Test    Test
   (Module)              (Module)
```

---

## Verification 方法

| 方法                       | 說明             | 適用                 |
| -------------------------- | ---------------- | -------------------- |
| **Review**                 | 設計/程式碼審查  | 設計合理性、流程合規 |
| **Static Analysis (SAST)** | 自動化原始碼分析 | 程式碼缺陷、CWE 偵測 |
| **Unit Test**              | 單元功能測試     | 個別函數/模組        |
| **Integration Test**       | 元件整合測試     | 介面、資料流         |
| **System Test**            | 系統層測試       | 完整功能             |
| **Pen Test (元件級)**      | 滲透測試         | 元件層攻擊面         |
| **Fuzz Testing**           | 模糊測試         | 輸入處理穩健性       |
| **Side-Channel Analysis**  | 旁通道分析       | 加密實作             |
| **Formal Verification**    | 形式化驗證       | 高 CAL 元件          |

---

## CS Verification 計畫

```yaml
cs_verification_plan:
  scope: "TCU-2026 firmware + HSM integration"

  per_requirement:
    - csr_id: CSR-001
      requirement: "Bootloader verifies app signature using ECDSA-P256-SHA256"
      verification_methods:
        - method: "Unit Test"
          test_id: UT-BOOT-001
          coverage:
            - "Valid signature → boot proceeds"
            - "Invalid signature → boot aborted"
            - "Missing signature → boot aborted"
            - "Tampered image → boot aborted"
          tool: "Custom test framework + Bench setup"

        - method: "Integration Test"
          test_id: IT-BOOT-002
          coverage:
            - "End-to-end OTA → boot rejected for tampered image"

    - csr_id: CSR-005
      requirement: "Side-channel resistance against first-order DPA"
      verification_methods:
        - method: "Side-Channel Analysis"
          test_id: SC-CRYPTO-001
          test_lab: "External certified lab"
          equipment: "ChipWhisperer + Custom probes"
```

---

## Verification Coverage

> [!important]
> Verification 必須**完整覆蓋** CS Requirements：
>
> - 每個 CSR 至少對應一個 Verification 活動
> - 覆蓋率追蹤（Traceability Matrix）

### Traceability Matrix 範例

| Goal   | Concept     | Req     | Verif Test  | Result   |
| ------ | ----------- | ------- | ----------- | -------- |
| CG-001 | Secure Boot | CSR-001 | UT-BOOT-001 | Pass     |
| CG-001 | Secure Boot | CSR-001 | IT-BOOT-002 | Pass     |
| CG-001 | Secure Boot | CSR-002 | UT-BOOT-003 | Pass     |
| CG-002 | TLS 1.3     | CSR-010 | IT-TLS-001  | Pass     |
| CG-002 | TLS 1.3     | CSR-011 | IT-TLS-002  | **Fail** |

---

## Integration Testing 重點

整合測試特別關注**介面**與**互動**：

```
Integration Test 重點：
├── 介面層級的協議遵循
├── 多元件互動下的時序
├── 跨元件的權限傳遞
├── 異常情境的處理（一個元件失效，其他元件反應）
└── 整合後的攻擊面變化
```

---

## 滲透測試 (Penetration Testing)

### 元件級 vs 車輛級

| 比較   | 元件級 Pen Test        | 車輛級 Pen Test                                     |
| ------ | ---------------------- | --------------------------------------------------- |
| 階段   | Clause 10 Verification | Clause 11 Validation                                |
| 範圍   | 單一 ECU/模組          | 整車（含多 ECU 互動）                               |
| 視角   | 元件邊界內             | 攻擊者實際情境                                      |
| 必要性 | 強烈建議               | Clause 11 列為適當方法；R155 type approval 普遍期待 |

### Pen Test 規劃

```yaml
pen_test_plan:
  scope: "TCU only (component-level)"
  attacker_model:
    - "Network attacker (cellular)"
    - "Local attacker with diagnostic tools"
    - "Physical attacker with debug access"

  out_of_scope:
    - "Backend cloud (separate test)"
    - "Inter-ECU attacks (vehicle-level test)"

  rules_of_engagement:
    - "Test environment isolated"
    - "No production data"
    - "Findings reported per CIA"

  methodology:
    - Information Gathering
    - Threat Modeling (re-check)
    - Vulnerability Analysis
    - Exploitation
    - Post-Exploitation (impact assessment)
    - Reporting

  deliverables:
    - "Pen Test Report"
    - "Findings list (CVSS-rated)"
    - "Remediation recommendations"
```

---

## Static Analysis (SAST) 整合

```yaml
sast_integration:
  tools:
    - "Coverity"
    - "Polyspace"
    - "SonarQube"

  rule_sets:
    - "MISRA C / C++"
    - "CERT C / C++"
    - "OWASP / CWE Top 25"

  ci_integration: "Every commit"

  pass_criteria:
    - "Zero Critical CWE"
    - "Zero MISRA mandatory violations"
    - "Justified deviations only"
```

---

## Fuzz Testing

### 適用場景

- 處理外部輸入的元件（網路、CAN、診斷）
- 解析器（Protobuf、JSON、XML、ASN.1）
- 加密實作（針對 malformed input）

### 工具

- AFL / AFL++
- libFuzzer
- Defensics
- 自製專屬汽車協議 fuzzer

---

## Verification Report

每個 Verification 階段結束需產出 Verification Report，含：

- Scope
- 測試方法與環境
- 測試結果（pass/fail）
- 缺陷清單與處置
- 覆蓋率
- Traceability Matrix
- 結論與建議

---

## 證照考點

> [!important] 高頻考點
>
> 1. **Verification 在 Clause 10**，元件/系統層級
> 2. **Validation 在 Clause 11**，車輛層級
> 3. 兩者**不可混用**（VV 概念）
> 4. 每個 CS Requirement **至少一個** Verification 方法
> 5. **Traceability Matrix** 是必要 WP
> 6. **滲透測試**可在元件級執行（車輛級 Pen Test 為 Clause 11 列為適當方法之一，R155 type approval 普遍期待）
> 7. SAST + Fuzz + Pen Test 各有適用

---

## Related Notes

- [[07-Product-Development/01-Design-Requirements\|07-Product-Development/01-Design-Requirements]]
- [[07-Product-Development/03-Weakness-Vulnerability-Analysis\|07-Product-Development/03-Weakness-Vulnerability-Analysis]]
- [[08-Cybersecurity-Validation/01-Validation-Objectives\|08-Cybersecurity-Validation/01-Validation-Objectives]]
- [[08-Cybersecurity-Validation/02-Validation-Methods\|08-Cybersecurity-Validation/02-Validation-Methods]]
- [[00-Dashboard/Exam-Traps#Trap 5\|00-Dashboard/Exam-Traps#Trap 5]]
- [[00-Dashboard/Exam-Traps#Trap 11\|00-Dashboard/Exam-Traps#Trap 11]]

## Practice

- [[07-Product-Development/Practice-Development\|07-Product-Development/Practice-Development]]

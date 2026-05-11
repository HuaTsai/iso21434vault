---
{"dg-publish":true,"permalink":"/02-organizational-management/04-tool-management/","title":"工具管理","tags":["iso-21434","concept-note","csms","tools"],"dg-note-properties":{"title":"工具管理","source_pdf":"內部彙整 (ISO 21434 Clause 5.4.6)","part":"Clause 5","keywords":["tool-management","tool-evaluation","tcl","qualification"],"tags":["iso-21434","concept-note","csms","tools"],"created":"2026-05-11"}}
---


## 為什麼需要工具管理？

> [!important]
> 資安工具會直接影響：
>
> - **TARA 結果的可信度**
> - **滲透測試的完整性**
> - **金鑰生成/管理的安全性**
> - **簽章驗證的正確性**
>
> 若工具有 bug 或被誤用，可能產生**錯誤結論**（高風險誤判為低風險）。

---

## 需要管理的工具類別

| 類別            | 範例                                      |
| --------------- | ----------------------------------------- |
| TARA 工具       | Medini Analyze、PREEvision、ThreatModeler |
| 威脅建模        | Microsoft Threat Modeling Tool、IriusRisk |
| 靜態分析 (SAST) | Coverity、Polyspace、SonarQube            |
| 動態分析 (DAST) | Fuzz tools (AFL, libFuzzer, Defensics)    |
| 加密工具        | OpenSSL、HSM 配套軟體                     |
| Pen Test 工具   | Burp、Wireshark、CANalyzer、PCAN          |
| Build/Sign 工具 | 簽章伺服器、CI/CD pipeline                |
| 弱點掃描        | OWASP ZAP、Nessus、SBOM 工具              |

---

## 工具評估流程

```
1. 識別需求 → 工具要做什麼
   ↓
2. 候選工具列表
   ↓
3. 評估維度：
   • 功能完整度
   • 可信度（誤報率）
   • 可重現性
   • 可追溯性（log/output）
   • 供應商可信度
   • 維護承諾
   ↓
4. 試用 / PoC
   ↓
5. 批准決策（Tool Owner + CS Manager）
   ↓
6. 工具批准紀錄（WP）
   ↓
7. 變更管理（升級、替換需重評估）
```

---

## 工具批准的最低紀錄

每個工具的 **Tool Approval Record** 應含：

```yaml
tool_approval:
  tool_name: "Medini Analyze"
  vendor: "ANSYS"
  version: "2024 R2"
  purpose: "TARA execution + Risk Register"
  applicable_phases: [Concept, Operations]
  approval_date: 2026-05-01
  approved_by: "CS Manager (Jane Doe)"

  evaluation:
    completeness: PASS # 功能涵蓋
    accuracy: PASS # 結果正確性驗證
    reproducibility: PASS # 同輸入同輸出
    traceability: PASS # 可輸出可驗證紀錄

  limitations:
    - "Attack Tree depth limited to 5 levels"
    - "Custom risk matrix needs manual entry"

  controls:
    - "Result reviewed by 2nd engineer"
    - "Version locked per project baseline"
    - "Output checksummed and stored in PLM"

  next_review: 2027-05-01
```

---

## 工具信心等級 (TCL — Tool Confidence Level)

雖 ISO 21434 未強制定義 TCL（這是 **ISO 26262 Part 8** 的概念），但**業界實務**借用：

| TCL  | 意義                       | 影響                   |
| ---- | -------------------------- | ---------------------- |
| TCL1 | 低影響或低錯誤可能         | 標準評估               |
| TCL2 | 中影響                     | 加強評估               |
| TCL3 | 高影響（直接影響資安結論） | **嚴格 Qualification** |

**TCL 評估維度**：

- **Tool Impact (TI)**：工具錯誤對最終結果的影響
- **Tool Error Detection (TD)**：發現工具錯誤的能力

```
高 TI + 低 TD → 高 TCL → 需 Qualification
低 TI 或 高 TD → 低 TCL → 標準評估即可
```

---

## 變更管理

工具發生變更時的處理：

| 變更類型           | 處理                     |
| ------------------ | ------------------------ |
| 大版本升級 (Major) | **重新完整評估**         |
| 小版本升級 (Minor) | 影響分析，可能只需測試   |
| Patch              | 通常不需重評估，但需記錄 |
| 替換為新工具       | **完整評估 + 過渡計畫**  |
| 配置變更           | 影響分析 + 紀錄          |

---

## 共同工具（跨專案/組織）

> [!tip]
> CSMS 應有「組織級工具清單」(approved tool list)，避免每個專案重複評估同一工具。

```
組織級 approved tool list
   ↓
專案啟動時，從清單中選用
   ↓
若需新工具 → 經評估後加入清單
```

---

## 常見陷阱

> [!warning]
>
> 1. **用未經評估的免費工具做正式評估**：常見錯誤。
> 2. **工具版本未鎖定**：升級後結果可能不一致。
> 3. **不記錄工具輸出**：無法追溯。
> 4. **同工具不同設定，結果可能不同**：配置也需版控。
> 5. **以為「業界普遍使用 = 已評估」**：仍需自己評估。

---

## 證照考點

- 工具管理是 **CSMS 必要組成**（Clause 5 規範性）
- 每個工具需有**評估紀錄**
- **Tool Approval Record** 是必要 WP
- 工具**版本鎖定**與**變更管理**
- TCL 概念雖借自 26262，但在 CS 工具評估也常被引用

---

## Related Notes

- [[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]
- [[02-Organizational-Management/06-Audit-and-Assessment\|02-Organizational-Management/06-Audit-and-Assessment]]

## Practice

- [[02-Organizational-Management/Practice-CSMS\|02-Organizational-Management/Practice-CSMS]]

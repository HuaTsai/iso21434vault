---
{"dg-publish":true,"permalink":"/14-exam-practice/mock-exam-2/","title":"模擬試題 2：TARA + 風險處置","tags":["iso-21434","mock-exam","tara"],"dg-note-properties":{"title":"模擬試題 2：TARA + 風險處置","type":"mock-exam","source_pdf":"內部彙整","keywords":["mock-exam","tara","risk","treatment"],"tags":["iso-21434","mock-exam","tara"],"created":"2026-05-11"}}
---


> 15 題，聚焦 Clause 15 與相關章節。

---

## 一、TARA 八步驟

### Q1

某 TARA 報告寫：「我們識別出 X 攻擊路徑，總分 8 分。」此 Feasibility 為何？

> [!answer]-
> **High**。0-13 對應 High Feasibility（容易攻擊）。
> 分數越**低** = 越**容易**。

---

### Q2

請將下列 STRIDE 對應到正確的資安屬性：

| STRIDE                 | 對應屬性 |
| ---------------------- | -------- |
| Spoofing               | ?        |
| Tampering              | ?        |
| Repudiation            | ?        |
| Information Disclosure | ?        |
| Denial of Service      | ?        |
| Elevation of Privilege | ?        |

> [!answer]-
>
> | STRIDE                 | 對應屬性            |
> | ---------------------- | ------------------- |
> | Spoofing               | **Authenticity**    |
> | Tampering              | **Integrity**       |
> | Repudiation            | **Non-repudiation** |
> | Information Disclosure | **Confidentiality** |
> | Denial of Service      | **Availability**    |
> | Elevation of Privilege | **Authorization**   |

---

### Q3

TARA 風險矩陣中，**Impact = Severe + Feasibility = High** 的 Risk Value 為何？

A. 3 B. 4 C. 5 D. 6

> [!answer]-
> **C. 5 (Very High)**。最高風險，必須處置。

---

## 二、應用題

### Q4

某 OEM 開發 ADAS 系統，識別出威脅情境：「攻擊者透過 GPS spoofing 誤導自動車道偏離警告 (LDW)」。

請評估各 SFOP 並計算 Overall Impact。

> [!answer]-
>
> ```
> Safety: Major (車道偏離可能引起碰撞，但 LDW 是輔助功能，駕駛應仍掌握)
> Financial: Moderate (客戶投訴、品牌損害)
> Operational: Major (主要功能誤動作)
> Privacy: Negligible (不涉及 PII)
>
> → Overall: Major
> ```
>
> 注意：
>
> - 若是更高階自駕（如 L4），Safety 可能升至 Severe
> - LDW 屬 L1-L2，駕駛仍是主負責人
> - GPS 屬 Sensor Spoofing 是常見 ADAS 威脅

---

### Q5

延續 Q4，已知 GPS Spoofing 的 Attack Potential：

- Time: 1, Expertise: 6, Knowledge: 0, Window: 4, Equipment: 4
- 總分：15

請計算 Risk Value。

> [!answer]-
>
> **計算**：
>
> - Feasibility 對應：15 分 → **Medium**
> - Impact：Major（前題）
> - Risk Value（依矩陣）：Major × Medium = **3 (Medium)**

---

### Q6

延續 Q4-Q5，請說明合理的 Risk Treatment 選項並評論。

> [!answer]-
>
> **Risk Value 3 (Medium)** 可接受 Retain 或 Reduce，但有 Privacy/Safety 考量需保守。
>
> **建議 Reduce**：
>
> 1. **多重來源融合**：GPS + IMU + 視覺 + 高解析地圖
>    - 攻擊者需同時誤導多個來源
>    - Feasibility 降至 Low
> 2. **GPS 訊號真偽檢測**：
>    - 接收 GNSS authentication signal（如 Galileo OS-NMA）
>    - 異常時降級
> 3. **Plausibility Check**：
>    - 位置 vs 車速 vs 加速度交叉檢查
> 4. **降級策略**：
>    - 偵測 spoofing → 通知駕駛 + 暫時停用 LDW
>
> **不建議單純 Retain**：
>
> - Safety Major 通常需積極處置
> - Sensor spoofing 是公開技術，後續可能變更容易
>
> **不適合 Avoid**：
>
> - LDW 是客戶期望功能
>
> **預期殘餘風險**：Low（持續監控新的 spoofing 技術）

---

### Q7

某 Tier-1 與 OEM 在 CIA 中對 TARA 責任有衝突。Tier-1 認為「車輛級 TARA 是 OEM 責任」，OEM 認為「元件外的攻擊路徑也應由 Tier-1 涵蓋」。如何協商？

> [!answer]-
>
> **常見作法**：
>
> 1. **明確切分範圍**：
>
>    ```
>    Tier-1 範圍：
>      - 元件內部威脅情境
>      - 元件介面（攻擊者進入元件的入口）
>      - 元件與其他系統的「假設邊界」
>
>    OEM 範圍：
>      - 車輛級攻擊面
>      - 跨元件的攻擊路徑（如：A 元件被攻破後對 B 的影響）
>      - 整車情境的 SFOP 評估
>    ```
>
> 2. **共享 Threat Scenarios**：
>    - 雙方都做 TARA，**對齊**威脅清單
>    - Tier-1 提供「我們守得住什麼、什麼不在我們範圍」
>    - OEM 整合至車輛級 TARA
> 3. **明確的「假設情境」**：
>    - Tier-1 在交付時宣告假設（如「假設 OEM 提供安全閘道」）
>    - 屬於 **OoC Component** 概念
> 4. **Joint Review**：
>    - 雙方定期 review TARA 對接
>    - 發現空白 → 協商補位
> 5. **最終仲裁**：
>    - 若仍有歧義，OEM（車型認證持有者）有最終裁決權
>    - 但需在 CIA 中事先明定爭議解決機制
> 6. **保守原則**：
>    - CIA 不明確時，**雙方都應假設自己負責**
>    - 避免責任真空
>
> 參考 [[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]

---

## 三、申論題

### Q8

請說明為何 Attack Feasibility 評估「應採用最容易那條 Attack Path」，而非平均或最難的。

> [!answer]-
>
> **核心理由**：**攻擊者選擇權 + 保守原則**
>
> 1. **攻擊者選擇權**：
>    - 攻擊者不會選最難的路
>    - 一定選成本最低、最容易達標的
>    - 評估「最容易」反映真實攻擊情境
> 2. **保守原則**：
>    - 低估容易度 → 低估風險 → 防護不足
>    - 寧可過度防護
> 3. **防禦設計含意**：
>    - 想降低風險 → 需降低「最容易那條」
>    - 若最容易那條被堵住，第二容易成為新的「最容易」
>    - 持續強化過程
> 4. **計算層面**：
>    - 取 max(feasibility across paths)
>    - 即「攻擊者最壞情境」

---

### Q9

請說明 CAL 與 ASIL 的主要差異。

> [!answer]-
>
> | 比較項 | **CAL**                  | **ASIL**                     |
> | ------ | ------------------------ | ---------------------------- |
> | 標準   | ISO 21434 (Annex E)      | ISO 26262                    |
> | 領域   | 資安                     | 功能安全                     |
> | 等級   | 1-4                      | QM, A-D                      |
> | 推導   | Impact + Attack Vector   | S × E × C                    |
> | 性質   | 保證等級（多嚴格做）     | 完整性等級（功能達成可靠度） |
> | 強制   | **非強制** (informative) | 通常強制                     |
>
> **關鍵概念**：
>
> - CAL 4 ≠ ASIL D（兩者根本不對應）
> - 一個系統可以「ASIL D + CAL 1」（功能安全極高但無連網）
> - 也可以「ASIL QM + CAL 4」（資安極高但無 safety 影響，如 PII 處理）

---

### Q10

請說明殘餘風險 (Residual Risk) 的處理流程。

> [!answer]-
>
> ```
> Step 1: Risk Treatment 後仍存在的風險
>           ↓
> Step 2: 評估剩餘的 Risk Value
>           ↓
> Step 3: 文件化殘餘風險
>           ├── 描述
>           ├── 剩餘 Risk Value
>           ├── 為何無法進一步處置
>           └── 補償措施（監控、降級等）
>           ↓
> Step 4: 適當層級接受
>           ├── Low (1-2)：CS Engineer / Manager
>           ├── Medium (3)：CS Manager / Director
>           └── High+ (4-5)：VP / CTO 或更高
>           ↓
> Step 5: 寫入 Cybersecurity Case
>           ↓
> Step 6: 持續監控
>           ├── 觸發升級條件（如新攻擊技術出現）
>           └── 定期 review
>           ↓
> Step 7: 重新評估時機
>           ├── 新威脅情報
>           ├── 設計變更
>           └── 事件發生後
> ```

---

### Q11

某 Tier-2 開發了「通用 AUTOSAR Crypto Stack」OoC 元件，宣告「假設整合者提供 FIPS 140-2 Level 3 HSM」。Tier-1 採購此元件用於 ASIL-B 應用，但實際 HSM 只有 FIPS 140-2 Level 2。請說明影響與處理。

> [!answer]-
>
> **影響**：
>
> - Tier-2 的 TARA 與 CS Case **基於假設**——假設不成立則無效
> - Tier-1 的整合產品可能**不符合**原設計的保護水準
> - HSM Level 2 vs Level 3 差異：
>   - Level 3 含 tamper evidence + 物理保護
>   - Level 2 僅 tamper evidence
>   - 對抗物理攻擊能力較弱
>
> **處理**：
>
> 1. **重新評估假設**：
>    - 在實際情境下，攻擊者模型是否仍合理？
>    - Level 2 HSM 是否仍提供足夠保護？
> 2. **重做 TARA**（在實際情境下）：
>    - 攻擊面：物理攻擊機會
>    - Attack Feasibility 可能上升
>    - Risk Value 重評
> 3. **處置選項**：
>    - **A. 升級 HSM 至 Level 3**：成本高但符合原設計
>    - **B. 補強整合層**：加上 tamper detect、外殼設計
>    - **C. 限制使用情境**：宣告產品**不適用**高威脅情境
>    - **D. 接受殘餘風險**（適當層級簽核）
> 4. **更新 CS Case**：
>    - 文件化此差異
>    - 補上整合層論證
>    - 殘餘風險紀錄
> 5. **與 Tier-2 溝通**：
>    - 確認 SDK 在 Level 2 下的限制
>    - 是否需 Tier-2 提供修補版本
> 6. **與 OEM 溝通**（依 CIA）：
>    - 透明披露此偏差
>    - 共同決定是否可接受
>
> **絕對不可**：直接整合不報告——Assessment 會發現且拒絕 Release。
>
> 參考 [[03-Project-Dependent/05-Component-Out-of-Context\|03-Project-Dependent/05-Component-Out-of-Context]]、[[06-Concept-Phase/03-Cybersecurity-Claims\|06-Concept-Phase/03-Cybersecurity-Claims]]

---

### Q12

請說明 Threat Scenario、Damage Scenario、Attack Path、Cybersecurity Goal 四者的關係。

> [!answer]-
>
> ```
> Damage Scenario（後果）
>    └── 「車輛在高速公路失控撞擊」
>          ↑ 由以下手段達成
>          │
> Threat Scenario（手段+對象）
>    └── 「攻擊者注入偽煞車 CAN 訊息」
>          │ 對應 attack path
>          ↓
> Attack Path（具體步驟序列）
>    └── 「1. 接入 OBD → 2. 偽造 CAN frame → 3. 注入...」
>
>
> 對應的處置：
>
> Threat Scenario → 評估 Risk → Risk Treatment
>                                    ↓
>                              Cybersecurity Goal
>                                    ↓
>                                「煞車 CAN 訊號的真實性
>                                  應被保護免於 OBD 注入」
> ```
>
> **總結關係**：
>
> - **Damage** 是站在 road user 角度的「不希望結果」
> - **Threat** 是攻擊者如何達成 Damage
> - **Attack Path** 是 Threat 的具體實現步驟
> - **CS Goal** 是對 Threat 的處置承諾

---

### Q13

請設計一個簡單 Attack Tree 描述「竊取 OEM OTA 簽章金鑰」的攻擊。

> [!answer]-
>
> ```
>                  竊取 OEM OTA 簽章金鑰
>                          │
>                       (OR Gate)
>             ┌────────────┼────────────┐
>             │            │            │
>          雲端攻擊      內部威脅     物理攻擊
>             │            │            │
>          (AND)         (OR)         (OR)
>            / \         / | \         / \
>      釣魚員工 提權  收買 詐騙 持有  HSM   接近
>      取得    至雲   員工 員工 權限  DPA   實體
>      內網    服務                  分析   設備
>      存取    簽章
>      管理
>
>      Feasibility 評估（簡化）：
>      ├── 雲端攻擊：Medium（需多步成功）
>      ├── 內部威脅：High（社交工程簡單）← 最易
>      └── 物理攻擊：Very Low（HSM 抗 DPA）
>
>      Goal Feasibility = max = High
>      → 防禦重點：內部控制（背景檢查、權限分離、Dual Approval）
> ```

---

### Q14

若 TARA 結果有 5 個 Very High Risk，但專案已嚴重 delay。請依 ISO 21434 評論可能的「合規」處理方式。

> [!answer]-
>
> **絕對不可**：
>
> - 為趕進度直接 Retain 並 Release
> - 違反 Clause 6.4.11 (Release for Post-Development)
> - 違反 Clause 15 Risk Treatment 原則
>
> **可能合規方案**：
>
> 1. **嚴格 Reduce**：
>    - 為每個 Very High 設計強化控制
>    - 重評至 Medium 以下
>    - 可能延後 Release，但合規
> 2. **Avoid（部分功能移除）**：
>    - 移除產生 Very High 風險的功能
>    - 縮減 Item 範圍
>    - 後續版本再加回（含完整防護）
> 3. **階段性 Release**：
>    - 先 Release 已處置完的部分
>    - 高風險部分留待後續 OTA / 後續車型
>    - 需明確的 CS Claim（in/out scope）
> 4. **Transfer + 補償措施**：
>    - 若風險涉及供應商不完備，由供應商擔保 + 保險
>    - 但 OEM 對車主的法律責任不可完全轉移
> 5. **Retain（極端少數情境）**：
>    - 需 Very High 的接受層級（CTO / 董事會）
>    - 詳盡補償措施（如限制使用情境、強化監控）
>    - 文件化於 CS Case
>    - Assessment **可能仍拒絕**
>
> **時程方面**：
>
> - 接受 Release 延後
> - 與 OEM 重新協商交期
> - 評估財務影響
>
> **不可**：
>
> - 隱瞞 TARA 結果
> - 由不適當層級簽核
> - 跳過 Assessment

---

### Q15

請說明 TARA 應在哪些時機**更新**（至少 5 個情境）。

> [!answer]-
>
> 1. **Item Definition 變更**（範圍/介面變動）
> 2. **架構/設計重大變更**（攻擊面改變）
> 3. **新弱點/威脅情報出現**（Clause 8 觸發）
>    - 新 CVE 影響 SBOM
>    - 新攻擊技術公開
> 4. **新車型/變體開發**（Delta TARA）
> 5. **事件回應後 Lessons Learned**（Clause 13）
> 6. **整合 OoC 元件後**（情境改變）
> 7. **Cybersecurity Assessment 發現缺失**
> 8. **重大 Penetration Test 發現**
> 9. **法規/標準變更**
> 10. **定期 review**（如每年）
>
> 關鍵原則：**TARA 是 Living Document**，不是一次性文件。

---

## Related Concepts

- [[12-TARA-Methods/\|12-TARA-Methods/]]
- [[00-Dashboard/Exam-Traps\|00-Dashboard/Exam-Traps]]
- [[14-Exam-Practice/Mock-Exam-1\|14-Exam-Practice/Mock-Exam-1]]
- [[14-Exam-Practice/Mock-Exam-3\|14-Exam-Practice/Mock-Exam-3]]

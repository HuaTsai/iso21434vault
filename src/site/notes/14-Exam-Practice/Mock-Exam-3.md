---
{"dg-publish":true,"permalink":"/14-exam-practice/mock-exam-3/","title":"模擬試題 3：跨章節情境題","tags":["iso-21434","mock-exam","scenario"],"dg-note-properties":{"title":"模擬試題 3：跨章節情境題","type":"mock-exam","source_pdf":"內部彙整","keywords":["mock-exam","integration","scenario"],"tags":["iso-21434","mock-exam","scenario"],"created":"2026-05-11"}}
---


> 10 大型情境題。每題涉及多個 Clause，考驗綜合理解。

---

## 案例 1：新 OEM 啟動 ISO 21434 合規

### 背景

某新興 EV OEM 於 2026 年開始開發新車型，目標 2028 年上市。從未做過 ISO 21434 合規。請建議建置計畫。

> [!answer]- 解答
>
> **建議計畫**：
>
> **Phase 0：組織就緒（Month 1-6）**
>
> 1. Top Management 承諾 + CSMS 政策訂定
> 2. 設立 CS Officer / CS Team
> 3. CSMS 流程文件化（Clause 5 全要求）
> 4. 培訓計畫啟動
> 5. 工具評估與採購（Medini、SAST、Fuzz、HSM）
> 6. 加入 Auto-ISAC
>
> **Phase 1：專案啟動（Month 4-8）**
>
> 1. 制定 Cybersecurity Plan
> 2. 角色與責任（RASIC）
> 3. Item Definition 完成（與 Safety 對齊）
>
> **Phase 2：分散開發安排（Month 5-10）**
>
> 1. Tier-1 / Tier-2 評估
> 2. RFQ 加入資安要求
> 3. 簽訂 CIA
>
> **Phase 3：概念階段（Month 8-14）**
>
> 1. 首次完整 TARA
> 2. CS Goals 凍結
> 3. CS Concept 設計
>
> **Phase 4：產品開發（Month 12-20）**
>
> 1. CS Requirements
> 2. Security Architecture
> 3. 整合開發
> 4. Verification（含 Pen Test 元件級）
>
> **Phase 5：Validation（Month 18-22）**
>
> 1. 車輛級 Pen Test
> 2. Validation Report
>
> **Phase 6：認證與 Release（Month 20-24）**
>
> 1. CSMS 認證稽核（UN R155）
> 2. 車型認證稽核
> 3. Cybersecurity Assessment
> 4. Release for Post-Development
>
> **Phase 7：上市後（Month 24+）**
>
> 1. Continual Monitoring
> 2. IR 準備
> 3. OTA 機制（含 UN R156 SUMS）
>
> **同時併行**：
>
> - Clause 8 持續活動（從 Phase 0 即開始）
> - 文化建立、培訓
> - 內部稽核（年度）
>
> **關鍵成功因素**：
>
> - Top Mgmt 真正承諾
> - 充足預算（資安非廉價）
> - 不可在最後階段「補做合規」——必須由設計階段開始
>
> 參考 [[01-Foundations/04-Lifecycle-Overview\|01-Foundations/04-Lifecycle-Overview]]、[[02-Organizational-Management/01-CSMS-Overview\|02-Organizational-Management/01-CSMS-Overview]]

---

## 案例 2：跨組織危機處理

### 背景

某 OEM 收到外部研究者通報：其某車型 TCU 韌體中發現可被遠端 RCE 的 buffer overflow。

- TCU 由 Tier-1A 開發
- 受影響車型：12 個型號、約 50 萬輛車
- 弱點 PoC 已在地下論壇流通

請依 ISO 21434 + UN R155 + UN R156 描述完整處理流程。

> [!answer]- 解答
>
> **時序處理**：
>
> ### Hour 0-1 (Detection & Initial Response)
>
> - CSIRT 確認通報真實性
> - 通知 IR Lead + 決策層 (CTO)
> - 依 CIA 通知 Tier-1A
> - 啟動 Joint IR Team
> - Severity 初判：**P0 Critical**（active threat 已存在）
>
> ### Hour 1-4 (Containment - 短期)
>
> - 雲端 firewall 部署規則阻擋已知攻擊模式
> - 提升雲端監控敏感度
> - 加密通訊鏈異常通報啟用
>
> ### Hour 4-24 (Detailed Investigation)
>
> - **完整 forensic 分析**
> - 確認影響範圍（VIN 清單）
> - 評估是否已有實際攻擊（vs 僅 PoC）
> - **TARA 緊急更新**
>   - 新 Threat Scenario：「Remote RCE via firmware bug」
>   - Risk Value 重評：Very High
> - **CS Case 更新**起草
>
> ### Day 1-3 (Patch Development)
>
> - Tier-1A 開發修補
> - 平行：OEM 測試環境驗證
> - 設計 OTA 部署計畫（依 **UN R156 SUMS**）
> - 影響評估：safety + security + type approval
>
> ### Day 3-7 (Communication Preparation)
>
> - 法務 + PR 準備聲明
> - 監管通報草稿（**UN R155 合規**）
> - 客戶通知策略
> - **CVD 協調**（與研究者 + Auto-ISAC）
>
> ### Day 7-14 (OTA Rollout)
>
> - 分批 OTA 部署（依 R156 流程）
> - 每批驗證
> - 失敗 rollback 機制
> - 監控部署狀態
>
> ### Day 14-30 (Coverage Verification)
>
> - 確認所有車輛已修補
> - 對未連線車輛規劃 dealership 召回
> - 通報 fleet status 至監管
>
> ### Day 30+ (Post-Incident)
>
> - 完整 Root Cause Analysis
> - 為何 SAST / Verification 未抓到？
> - Lessons Learned 寫入組織 CSMS
> - 流程改善（如加強 fuzz test 覆蓋）
> - CS Case 最終版本
>
> ### Long-term
>
> - UN R155 認證可能需重新審視
> - 是否影響 type approval
> - 法律訴訟可能
> - 保險理賠
>
> **同時保全**：
>
> - 證據（依 IR Plan 規範）
> - 紀錄完整時間軸
> - 所有決策的 traceability
>
> **不可**：
>
> - 隱瞞或延遲通報監管機構
> - 單方面對外揭露（需與研究者協調）
> - 跳過正式 OTA 流程（如壓力大就放鬆驗證）
>
> 參考 [[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]、[[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]、[[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]、[[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]

---

## 案例 3：供應鏈 Out-of-Context 整合

### 背景

某 Tier-1 接到 OEM 訂單開發 ADAS 控制器，計畫使用：

- Tier-2 開發的 **AUTOSAR Adaptive Platform**（OoC 元件）
- Tier-2 開發的 **HSM SDK**（OoC + OTS）
- Tier-2 提供 **AI 加速 SoC**

請說明 Tier-1 在整合過程中的 ISO 21434 責任。

> [!answer]- 解答
>
> **Tier-1 整合責任**：
>
> ### 1. OoC 元件處理（Clause 6.4.6）
>
> 對每個 OoC 元件：
>
> **A. Tier-2 AUTOSAR Adaptive Platform**
>
> - 取得 Tier-2 文件：
>   - Assumed Context（假設情境）
>   - TARA Report（基於假設）
>   - Integration Guide
>   - Known Limitations
> - 驗證假設情境在實際整合中成立：
>   - HW 規格相符
>   - 攻擊者模型相符
>   - 整合介面相符
> - 處理 gap（補強整合層）
>
> **B. Tier-2 HSM SDK**（同上加 OTS 處理）
>
> - 額外：SBOM 對照 CVE
> - 整合測試特別關注 crypto 操作
>
> **C. Tier-2 AI 加速 SoC**
>
> - 驗證 SoC 安全特性（debug lockout、secure boot）
> - 韌體簽章機制
> - Side-channel resistance
>
> ### 2. 整合層 TARA（Clause 15）
>
> - **不能**直接信賴 Tier-2 TARA
> - 在實際整合情境下重做 TARA
> - 識別新攻擊面（介面互動產生的）
> - 識別 OoC 元件間互動風險
>
> ### 3. CIA（Clause 7）
>
> - 與 OEM 簽訂 CIA：
>   - Tier-1 提交哪些 WP
>   - 整合層責任邊界
>   - 事件回應流程
> - 與 Tier-2 簽訂 CIA（**Tier-1 是 Tier-2 的客戶**）：
>   - Tier-2 通報義務
>   - Tier-2 修補 SLA
>   - SBOM 更新責任
>
> ### 4. Cybersecurity Concept（Clause 9）
>
> - 結合所有 OoC + 自製部分
> - 為整合產品設計 CS Goals
> - 補上整合層的 CS Concept
>
> ### 5. 開發與驗證（Clause 10）
>
> - 整合層 CS Requirements
> - Verification（**含跨 OoC 互動測試**）
> - 元件級 Pen Test
>
> ### 6. CS Case（Clause 6.4.9）
>
> - 結構：
>   - Top Claim（整體 CS Goals 達成）
>   - 引用 Tier-2 部分 CS Case（含假設驗證證據）
>   - 整合層自製論證
>   - 殘餘風險紀錄
>
> ### 7. Continual Activities（Clause 8）
>
> - 監控 Tier-2 的 CVE 與安全公告
> - 監控 AUTOSAR 平台、HSM SDK、SoC 韌體的弱點
> - 評估每個影響
>
> ### 8. 不可省略
>
> - 不可直接信賴 Tier-2 的 TARA 與測試
> - 不可假設「OoC 已驗證 = 整合產品已驗證」
> - 不可省略整合層的 Pen Test
>
> 參考 [[03-Project-Dependent/05-Component-Out-of-Context\|03-Project-Dependent/05-Component-Out-of-Context]]、[[03-Project-Dependent/04-Reuse\|03-Project-Dependent/04-Reuse]]、[[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]

---

## 案例 4：Safety 與 Security 衝突

### 背景

某 ECU 開發中，Safety Manager 與 CS Manager 對「煞車 CAN 訊息」是否需要 SecOC MAC 驗證有不同意見：

- Safety：MAC 驗證會增加處理時間，可能超過 FTTI（Fault Tolerant Time Interval）
- Security：缺 MAC 驗證會被偽造，造成 Safety 危害

請依 ISO 21434 + ISO 26262 說明如何解決。

> [!answer]- 解答
>
> **衝突本質**：
> 兩個要求都合理，但**直接衝突**：
>
> - Safety 需求：訊息處理 < FTTI（如 < 10ms）
> - Security 需求：訊息需驗證 MAC（每筆額外 ~500us-2ms）
>
> **依 ISO 21434 Clause 4 原則**：
>
> > "Safety considerations shall take precedence" 但**不放棄資安**。
>
> **正確解決流程**：
>
> ### Step 1：量化分析
>
> - 確認真實的 MAC 驗證耗時
> - 確認真實的 FTTI 容忍度
> - 確認 Safety 與 Security 的 timing budget
>
> ### Step 2：探索技術選項
>
> - **A. 硬體加速 MAC**
>   - 用 HSM 硬體加速 → ms → us 級
>   - 通常可解決衝突
> - **B. 預計算 / 流水線**
>   - 並行處理：訊息驗證與 safety reaction 並行
>   - 失敗時降級而非延遲
> - **C. 分層信任**
>   - 內部信任區（已驗證的 ECU）內部訊息免 MAC
>   - 外部（OBD、gateway）強制 MAC
> - **D. 降級策略**
>   - 預設執行 Safety 反應
>   - 同時計算 MAC
>   - MAC 失敗時觸發後續隔離
>
> ### Step 3：跨團隊評估
>
> - Safety + Security + Architect 共同 review
> - 量化 trade-off
> - 文件化決策理由
>
> ### Step 4：可能結論
>
> 通常**綜合方案**：
>
> - 採用硬體加速 MAC
> - 配合分層信任設計
> - 配合異常降級策略
> - 達成 Safety FTTI + Security 完整性
>
> ### Step 5：若仍無法滿足兩者
>
> - **優先 Safety**（生命優先）
> - **但不放棄 Security**：
>   - 降級到「最強可行 Security」
>   - 文件化此 trade-off
>   - 補償措施（如加強 IDS）
>   - 殘餘風險記錄
>   - 兩團隊與 Top Mgmt 共同簽核
>
> ### Step 6：文件化
>
> - **共同 review 紀錄**
> - **Trade-off rationale**
> - **Safety Case + CS Case** 都需描述此決策
>
> **錯誤做法**：
>
> - 「Safety 優先 = 跳過 Security」 ❌
> - 「Security 優先 = 違反 FTTI」 ❌
> - 「兩團隊各自決定」 ❌
>
> 參考 [[01-Foundations/03-Cybersecurity-vs-Safety\|01-Foundations/03-Cybersecurity-vs-Safety]]

---

## 案例 5：EoS 後突發弱點

### 背景

某產品線 EoS 後 2 年，突然發現一個遠端可利用的弱點，影響全球 100 萬輛在路車輛。Top Management 詢問如何處理。

> [!answer]- 解答
>
> **狀況分析**：
>
> - 依 ISO 21434：EoS 後**不再有資安修補義務**
> - 但**人身安全 + 大規模影響** → 觸發其他考量
>
> **分析優先序**：
>
> ### 1. 緊急評估（24 hr 內）
>
> - 啟動 IR（即使 EoS）
> - 評估弱點實際嚴重度
> - 評估已有實際攻擊？
> - 評估影響範圍（VIN、地區）
> - 影響類別（Safety/Privacy/Operational）
>
> ### 2. 法規與法律考量
>
> - **UN R155** 是否要求？
>   - R155 可能要求「重大資安事件」即使 EoS 也需處置
> - **各國交通法**強制召回機制
> - **產品責任法**可能訴訟風險
>
> ### 3. 品牌與道德責任
>
> - 即使法規不強制，品牌商譽
> - 大規模影響的社會責任
>
> ### 4. 技術可行性
>
> - OTA 機制是否還能運作？（後端服務可能也已下線）
> - 若無 OTA，需實體召回（每車到服務廠）
>
> ### 5. 決策樹
>
> ```
> 是否有 Safety 影響 ?
>  ├── Yes
>  │   └── 強烈建議處置（無論 EoS）
>  │       ├── 緊急修補 + OTA / 召回
>  │       └── 監管通報
>  │
>  └── No
>      └── 是否大規模 (>10K vehicles) ?
>           ├── Yes
>           │   └── 通常仍處置（品牌、法律）
>           │
>           └── No
>               └── 至少發布 Advisory
> ```
>
> ### 6. 可能行動方案
>
> **A. 完整修補（高成本）**
>
> - 重啟開發團隊（或委外）
> - 開發修補
> - OTA / 召回部署
> - 適用大規模 + Safety 影響
>
> **B. 補償措施 + Advisory（中成本）**
>
> - 發布安全通告
> - 建議使用者保護動作
> - 提供升級/折抵方案
>
> **C. 純 Advisory（低成本）**
>
> - 公開揭露弱點
> - 建議使用者
> - 適用小規模 + 低嚴重度
>
> ### 7. 流程要求
>
> 即使非規範義務，仍應：
>
> - 啟動 IR
> - 評估與決策記錄
> - 與監管機構溝通
> - 法務 + PR 配合
> - CSMS 紀錄此特殊案例
>
> ### 8. 長期改善
>
> - **EoS 政策檢討**：
>   - 是否 EoS 過早？
>   - 是否該保留緊急處理能力？
> - **新產品改善**：
>   - 延長 EoS 期
>   - 加強監控設計（更易遠端修補）
>   - 設計 graceful degradation
>
> **結論**：
> ISO 21434 不強制 EoS 後處置，但**業界最佳實務 + 法律 + 道德**通常驅動處置。
> 此案例顯示 EoS 政策應**留有彈性**。
>
> 參考 [[11-EndOfSupport-Decommission/01-End-of-Support\|11-EndOfSupport-Decommission/01-End-of-Support]]、[[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]

---

## Related Concepts

- [[14-Exam-Practice/Mock-Exam-1\|14-Exam-Practice/Mock-Exam-1]]
- [[14-Exam-Practice/Mock-Exam-2\|14-Exam-Practice/Mock-Exam-2]]
- [[00-Dashboard/MOC\|00-Dashboard/MOC]]
- [[00-Dashboard/Exam-Traps\|00-Dashboard/Exam-Traps]]

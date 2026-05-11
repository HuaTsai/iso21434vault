---
{"dg-publish":true,"permalink":"/10-operations-maintenance/practice-operations/","title":"營運與維護練習題","tags":["iso-21434","practice","operations"],"dg-note-properties":{"title":"營運與維護練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","incident-response","ota","updates"],"tags":["iso-21434","practice","operations"],"created":"2026-05-11"}}
---


> 涵蓋：Incident Response、Updates / OTA。
> 共 8 題。

---

## Q1. (recall)

NIST 標準的 IR 生命週期六階段為何？

> [!answer]- 解答
> **Preparation → Detection & Analysis → Containment → Eradication → Recovery → Post-Incident (Lessons Learned)**

---

## Q2. (recall + 易混淆)

下列何者**最正確**描述 ISO 21434 與 UN R156 的關係？

A. UN R156 是 ISO 21434 的一部分
B. ISO 21434 處理整體資安；UN R156 處理軟體更新管理；兩者並列
C. UN R156 取代了 ISO 21434
D. 兩者無關

> [!answer]- 解答
> **B**。
>
> - ISO 21434 + UN R155 → 整體資安
> - ISO 24089 + UN R156 → 軟體更新工程
> - 兩組**並列**且**互相關聯**
>   參考 [[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]、[[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]

---

## Q3. (recall)

下列哪一項**最重要**用於防止「降級攻擊 (downgrade attack)」？

A. TLS 1.3
B. Anti-rollback counter (eFuse / monotonic counter)
C. A/B Partition
D. SBOM

> [!answer]- 解答
> **B**。
> Anti-rollback counter 確保新版安裝後**不可降級**到含弱點的舊版。
> 即使攻擊者擁有簽署的舊韌體，仍無法回滾。
> 參考 [[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]

---

## Q4. (recall)

下列何者**不是** Cybersecurity Incident Response Plan 的必要內容？

A. 角色與責任
B. 嚴重度分級與 SLA
C. 詳細加密演算法選擇
D. 通訊計畫（內部 + 外部）

> [!answer]- 解答
> **C**。
> **產品設計階段**的加密演算法選擇屬於 Clause 10 設計細節，不是 IR Plan 的範疇。
> 注意：IR Plan **可包含**取證 / 應急通訊用的加密方法（如 evidence 包加密、與 CERT 安全通訊），但這是支援用的工具，與「設計階段的演算法選型」不同。
> IR Plan 重點：角色、SLA、Playbook、通訊、外部協作、演練。
> 參考 [[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]

---

## Q5. (application + 跨章節)

某 OEM 收到外部研究者通報：某車型遠端可被攻擊取得 root。請依 ISO 21434 全流程說明前 24 小時的行動。

> [!answer]- 解答
>
> **0–1 hr (Detection)**
>
> - CSIRT 確認通報來源、初步驗證
> - 提升內部警戒等級
> - 通知 IR Lead + 決策層
>
> **1–4 hr (Analysis)**
>
> - 重現攻擊（隔離環境）
> - 評估影響範圍：哪些車型、哪些 VIN
> - 嚴重度初判（很可能 P0）
> - 通知 Tier-1（依 CIA）
> - 啟動 Joint Response Team
>
> **4–8 hr (Containment - 短期)**
>
> - 雲端 firewall 規則阻擋已知攻擊模式
> - 暫停可能擴大暴露的服務
> - 在 SIEM 設置額外監控規則
>
> **8–24 hr (Detailed Investigation)**
>
> - 完整 forensic 分析
> - 確認影響車輛清單
> - 評估是否已有實際攻擊發生（vs 僅 PoC）
> - 設計修補（韌體 patch）
> - 設計 OTA 部署計畫（UN R156 流程）
>
> **同步進行**：
>
> - **Evidence Preservation**：所有相關 logs、PCAP、code 保全
> - **External communication 準備**：客戶通知、媒體聲明（PR + Legal）
> - **監管通報準備**：UN R155 認證機構、各國交通部
> - **與研究者 CVD 協調**：embargo 期、揭露時機
>
> **24 hr 結束**：
>
> - 修補方案 + OTA 計畫初稿
> - 短期 containment 已部署
> - 內外部溝通管道建立
> - 啟動長期 IR 流程
>
> **後續**：
>
> - Eradication（清除攻擊面）
> - Recovery（恢復正常）
> - Post-Incident（根因分析、TARA/CS Case 更新、Lessons Learned）
> - 法規通報完成
>
> 參考 [[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]、[[04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement\|04-Distributed-CS-Activities/02-Cybersecurity-Interface-Agreement]]

---

## Q6. (recall)

OTA 更新的 A/B Partition 模式的主要**優點**為何？

> [!answer]- 解答
>
> 1. **失敗可立即 rollback**（保留舊版作為備援）
> 2. **更新中車輛仍可運作**（用舊 partition）
> 3. **驗證後才切換 active**（雙重保險）
> 4. **降低 brick 風險**
>
> 參考 [[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]

---

## Q7. (analysis)

某 OEM 計畫透過 OTA 部署一個小型 Bug Fix（不涉及資安），是否仍需依 UN R156 + ISO 21434 流程處理？

> [!answer]- 解答
>
> **是，仍需**——但流程深度可依規模調整。
>
> **UN R156 SUMS 要求**：
>
> - 任何 OTA 更新都需符合 SUMS 流程
> - 影響評估（safety + security + type approval）
> - 紀錄
> - 部署過程的車輛狀態管理
> - 必要時客戶通知
>
> **ISO 21434 視角**：
>
> - 評估更新是否引入**資安變化**：
>   - 改變 attack surface 嗎？
>   - 改變 trust boundary 嗎？
>   - 修改了加密 / 認證流程嗎？
> - 若**無**資安影響：簡化流程，但紀錄影響評估
> - 若**有**：完整 review，可能需更新 TARA / CS Case
>
> **可裁適 (Tailoring)**：
>
> - 小型修補可採輕量流程
> - 但**不可省略**影響評估與紀錄
> - Tailoring 決策需有書面理由
>
> **常見錯誤**：
>
> - 「這只是 Bug Fix，不需要走流程」→ 違反 SUMS
> - 「沒影響資安就不用評估」→ 但**評估本身**是流程一部分
>
> 參考 [[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]、[[03-Project-Dependent/03-Tailoring\|03-Project-Dependent/03-Tailoring]]

---

## Q8. (recall)

UN R156 SUMS 的認證有效期為多久？

A. 1 年
B. 3 年
C. 5 年
D. 永久

> [!answer]- 解答
> **B. 3 年**。
> 與 R155 CSMS 認證同樣為 3 年。

---

## Related Concepts

- [[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]
- [[10-Operations-Maintenance/02-Updates\|10-Operations-Maintenance/02-Updates]]
- [[05-Continual-Cybersecurity/02-Event-Assessment\|05-Continual-Cybersecurity/02-Event-Assessment]]
- [[05-Continual-Cybersecurity/04-Vulnerability-Management\|05-Continual-Cybersecurity/04-Vulnerability-Management]]

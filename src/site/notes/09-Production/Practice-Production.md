---
{"dg-publish":true,"permalink":"/09-production/practice-production/","title":"生產階段練習題","tags":["iso-21434","practice","production"],"dg-note-properties":{"title":"生產階段練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","production","provisioning"],"tags":["iso-21434","practice","production"],"created":"2026-05-11"}}
---


> 涵蓋：Production Controls、Provisioning。
> 共 6 題。

---

## Q1. (recall)

ISO 21434 Clause 12 的核心 WP 是什麼？

> [!answer]- 解答
> **Production Control Plan** + 對應的 Production CS Activities 紀錄。

---

## Q2. (recall)

下列哪一項**最符合** ISO 21434 對 Provisioning 的要求？

A. 私鑰由 CA 產生後傳輸至 device
B. **私鑰於 device 內 HSM 生成，僅 public key 用於 CSR**
C. 全車隊共用一把對稱金鑰，方便管理
D. Debug 介面開著方便日後維護

> [!answer]- 解答
> **B**。最安全的方式：私鑰永遠不離開 HSM。
> 參考 [[09-Production/02-Provisioning\|09-Production/02-Provisioning]]

---

## Q3. (recall + 易混淆)

下列何者**錯誤**？

A. SecOC Master Key 應派生至各車輛獨立的子金鑰
B. Manufacturing Sub-CA 用於日常 provisioning
C. **Root CA 應放在連網的伺服器以便隨時簽發**
D. 廢品的金鑰需撤銷

> [!answer]- 解答
> **C**。Root CA 應**離線保管**，避免被入侵。Sub-CA 才用於日常作業。
> 參考 [[09-Production/02-Provisioning\|09-Production/02-Provisioning]]

---

## Q4. (application)

某廠商發現生產線上的 JTAG 介面在出貨後仍可使用。請說明影響與處理。

> [!answer]- 解答
>
> **影響**：
>
> - 攻擊者可透過 JTAG 讀寫韌體、萃取金鑰
> - 違反 Cybersecurity Goal（韌體完整性 + 金鑰機密性）
> - 可能違反 UN R155 認證要求
>
> **處理**：
>
> 1. **緊急**：召集 Incident Response（Clause 13）
> 2. **評估**：已出貨產品的暴露程度、可否 OTA 補救
> 3. **生產線**：立即修正 fuse blow 流程
> 4. **品保**：加入 JTAG 狀態檢查至 End-of-Line Test
> 5. **CS Case 更新**：記錄與 Lessons Learned
> 6. **TARA 更新**：該攻擊路徑重評
> 7. **若已暴露**：可能需召回或 OTA 修補
>
> 參考 [[09-Production/01-Production-Controls\|09-Production/01-Production-Controls]]、[[07-Product-Development/04-HW-SW-Considerations\|07-Product-Development/04-HW-SW-Considerations]]

---

## Q5. (recall)

V2X 通常使用何種 PKI 架構？

> [!answer]- 解答
> **SCMS (Security Credential Management System)**。
> 特色：
>
> - Long-term Certificate (LTC) + 多個 Pseudonym Certificates (PC)
> - PC 週期輪換（防 Tracking）
> - 集中式 PKI 可進行 Misbehavior Detection 與憑證撤銷
>
> 參考 [[09-Production/02-Provisioning\|09-Production/02-Provisioning]]

---

## Q6. (analysis)

請說明為何 ISO 21434 強調「每個設備獨立金鑰」而非「全車隊共用金鑰」。

> [!answer]- 解答
>
> **核心理由：限制 Blast Radius**
>
> ```
> 全車隊共用金鑰：
>   一台車被攻破 → 攻擊者取得 master key
>   → 全車隊都可被攻擊
>   → 災難性事件
>
> 每車獨立金鑰：
>   一台車被攻破 → 僅該車受影響
>   → 撤銷該車憑證即可
>   → 影響可控
> ```
>
> **進一步考量**：
>
> - **撤銷**：可單獨撤銷某車而不影響其他車
> - **追蹤**：事件後可識別來源
> - **責任歸屬**：清楚邊界
> - **法規合規**：UN R155 期望可控的影響範圍
>
> **實作機制**：
>
> - HSM 內生成 + Provisioning 流程
> - 從 Master Key 透過 KDF 派生（如 SecOC）
> - 每個 device 註冊在 PKI 系統中
>
> 參考 [[09-Production/02-Provisioning\|09-Production/02-Provisioning]]

---

## Related Concepts

- [[09-Production/01-Production-Controls\|09-Production/01-Production-Controls]]
- [[09-Production/02-Provisioning\|09-Production/02-Provisioning]]

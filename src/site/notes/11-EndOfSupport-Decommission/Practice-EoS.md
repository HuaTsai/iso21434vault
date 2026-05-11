---
{"dg-publish":true,"permalink":"/11-end-of-support-decommission/practice-eo-s/","title":"EoS 與除役練習題","tags":["iso-21434","practice","end-of-support"],"dg-note-properties":{"title":"EoS 與除役練習題","type":"practice","source_pdf":"內部彙整","keywords":["practice","eos","decommissioning"],"tags":["iso-21434","practice","end-of-support"],"created":"2026-05-11"}}
---


> 涵蓋：End of Support、Decommissioning。
> 共 6 題。

---

## Q1. (recall + 易混淆)

下列何者**最正確**描述 EoS 與 Decommissioning 的差異？

A. 兩者是同義詞
B. EoS 是停止資安支援；Decommissioning 是實際停用報廢；兩者不同時點
C. EoS 後車輛不能再使用
D. Decommissioning 早於 EoS

> [!answer]- 解答
> **B**。
>
> - **EoS**：不再修補弱點，但車輛仍可運作
> - **Decommissioning**：永久停用，含資料/金鑰清除
> - EoS 通常**早於** Decommissioning（可能差數年甚至更久）
>
> 參考 [[11-EndOfSupport-Decommission/01-End-of-Support\|11-EndOfSupport-Decommission/01-End-of-Support]]、[[11-EndOfSupport-Decommission/02-Decommissioning\|11-EndOfSupport-Decommission/02-Decommissioning]]

---

## Q2. (recall)

下列哪一項**不是** EoS 前必須完成的動作？

A. 通知所有相關方（車主、監管機構、供應鏈）
B. 修補已知 High/Critical 弱點
C. 重新進行完整 TARA
D. 評估殘餘風險並記錄

> [!answer]- 解答
> **C**。
> EoS 前重新做完整 TARA**不是規範要求**——TARA 應在生命週期中持續更新，EoS 時更新 CS Case 即可。
> 其他選項都是規範要求。
>
> 參考 [[11-EndOfSupport-Decommission/01-End-of-Support\|11-EndOfSupport-Decommission/01-End-of-Support]]

---

## Q3. (application)

某 OEM 計畫 6 個月後 EoS 某產品。下列哪一個**不是**必要通知對象？

A. 車主 / 使用者
B. 經銷商與服務廠
C. 監管機構（UN R155 對口）
D. 競爭對手

> [!answer]- 解答
> **D**。
> 通知對象應涵蓋：使用者、經銷商、服務廠、監管機構、供應鏈（必要時）、Auto-ISAC。
> 競爭對手不在通知對象內。

---

## Q4. (recall)

下列哪一項是 Decommissioning **必要**的資安動作？

A. 韌體更新至最新版
B. HSM 內金鑰 zeroize + PKI 憑證撤銷
C. 增加新功能
D. 重新做 Pen Test

> [!answer]- 解答
> **B**。
> Decommissioning 的核心是「**安全停用**」：
>
> - 金鑰銷毀（zeroize）
> - 憑證撤銷（CRL 更新）
> - 資料清除
> - 實體處置
>
> 參考 [[11-EndOfSupport-Decommission/02-Decommissioning\|11-EndOfSupport-Decommission/02-Decommissioning]]

---

## Q5. (application + 跨章節)

某二手車交易時，前車主將車賣給新車主。請說明此時應做的資安動作。

> [!answer]- 解答
>
> 這是 Decommissioning 的**特殊情境**（部分 decommission，車輛繼續運作）。
>
> **應執行**：
>
> 1. **使用者帳號解除連結**：
>    - 手機 App 配對解除
>    - OEM 雲端帳號解除
>    - 第三方服務（保險、追蹤）解除
> 2. **車主資料清除**：
>    - 通訊錄、藍牙配對
>    - 行駛歷史、目的地紀錄
>    - 偏好設定
>    - 個人 PII
> 3. **必要金鑰重設**：
>    - 一些**綁定車主**的金鑰可能需重新生成
>    - V2X 通常不需動（綁定車輛而非車主）
> 4. **新車主登錄**：
>    - 建立新雲端帳號連結
>    - OEM 端紀錄轉移
> 5. **不應做**：
>    - 完全 zeroize HSM（會破壞車輛功能）
>    - 撤銷車輛 PKI（會破壞 V2X、OTA）
>
> **與完整 Decommissioning 差別**：
>
> - 二手轉售：**車輛繼續運作**，僅做「使用者層」清除
> - 完整 Decommissioning：**車輛永久停用**，全部資料 + 金鑰銷毀
>
> 參考 [[11-EndOfSupport-Decommission/02-Decommissioning\|11-EndOfSupport-Decommission/02-Decommissioning]]

---

## Q6. (analysis)

某廠商發現一個 EoS 後 5 年的產品仍在大量使用，並出現了一個**高嚴重度資安弱點**可被遠端利用。請評論並說明可能的處理方式。

> [!answer]- 解答
>
> **困境**：
>
> - EoS 後**不再有資安修補義務**（依 ISO 21434）
> - 但**人身安全**或**大規模影響**可能觸發其他考量
>
> **可能處理方式**：
>
> **A. 嚴格依 ISO 21434**：
>
> - 不修補
> - 發布通告：「該產品已 EoS，建議使用者升級或停用」
> - 通知監管機構（如可能影響大規模安全）
>
> **B. 品牌責任 + 法律風險考量**：
>
> - 即使 EoS，可能仍需處理（避免訴訟、品牌損害）
> - 發布「特例修補」（不算正式支援延續）
> - 與監管機構協商
> - 可能演變為**召回**事件
>
> **C. 法規驅動**：
>
> - UN R155 可能要求 OEM 在重大事件下**仍須處置**
> - 各國交通法可能有強制召回機制
> - 法律可能高於 ISO 21434
>
> **建議**：
>
> 1. 啟動 Incident Response（即使 EoS）
> 2. 評估**影響範圍 + 嚴重度**
> 3. 與**法律 + PR + 監管**團隊協作
> 4. 至少發布**安全通告 + 使用者保護建議**
> 5. 視情況決定是否提供修補
> 6. 在組織 CSMS 中記錄此特殊案例，更新 Lessons Learned
> 7. 未來 EoS 政策可能需修訂（如延長 EoS 期、保留緊急修補能力）
>
> **此案例顯示**：EoS 不應簡單畫一條線——需考量產品生命週期、暴露程度、社會責任。
>
> 參考 [[11-EndOfSupport-Decommission/01-End-of-Support\|11-EndOfSupport-Decommission/01-End-of-Support]]、[[10-Operations-Maintenance/01-Incident-Response\|10-Operations-Maintenance/01-Incident-Response]]、[[01-Foundations/05-Regulatory-Landscape\|01-Foundations/05-Regulatory-Landscape]]

---

## Related Concepts

- [[11-EndOfSupport-Decommission/01-End-of-Support\|11-EndOfSupport-Decommission/01-End-of-Support]]
- [[11-EndOfSupport-Decommission/02-Decommissioning\|11-EndOfSupport-Decommission/02-Decommissioning]]

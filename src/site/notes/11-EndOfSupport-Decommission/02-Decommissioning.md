---
{"dg-publish":true,"permalink":"/11-end-of-support-decommission/02-decommissioning/","title":"除役 (Decommissioning)","tags":["iso-21434","concept-note","end-of-support","decommissioning"],"dg-note-properties":{"title":"除役 (Decommissioning)","source_pdf":"內部彙整 (ISO 21434 Clause 14)","part":"Clause 14","keywords":["decommissioning","data-wipe","key-revocation","disposal"],"tags":["iso-21434","concept-note","end-of-support","decommissioning"],"created":"2026-05-11"}}
---


## 是什麼？

> [!quote] 定義
> Permanent retirement of a cybersecurity-relevant component or item.

簡言之：「**永久停用並安全處置**」一個產品。

---

## 觸發條件

```
1. 車輛報廢（ELV - End-of-Life Vehicle）
2. 嚴重事故後不可修復
3. 二手轉售前的「reset」
4. 供應鏈中段 ECU 退回 → 翻新前處理
5. 召回後處置
```

---

## Decommissioning 必要動作

```
1. 資料清除
   ├── 車主 PII
   ├── 設定資料
   ├── 行駛紀錄
   ├── 連線歷史
   └── 任何敏感資料

2. 金鑰處置
   ├── HSM 內金鑰 zeroize
   ├── PKI 憑證撤銷（向 CA 通報）
   ├── V2X SCMS 通知
   └── SecOC 金鑰失效

3. 通報
   ├── 監管機構（如有要求）
   ├── 雲端服務（停用對應帳號）
   └── 客戶（如為轉售場景）

4. 實體處置
   ├── ECU 報廢（粉碎、熔毀）
   ├── 儲存晶片實體破壞
   └── 防止流入二手市場（如未經處理）

5. 紀錄
   ├── 何時 decommission
   ├── 由誰執行
   ├── 處置方法
   └── 驗證證據
```

---

## 資料清除標準

| 標準               | 描述                         |
| ------------------ | ---------------------------- |
| **NIST SP 800-88** | 業界資料清除指引             |
| Clear              | 邏輯清除（覆寫）             |
| Purge              | 加密金鑰銷毀 或 物理 zeroize |
| Destroy            | 實體破壞                     |

汽車 ECU 通常需 **Purge** 等級以上。

---

## V2X 與 PKI 撤銷流程

```
車輛除役
   ↓
通報 SCMS / Vehicle CA
   ↓
撤銷所有 Pseudonym Certificates
   ↓
更新 CRL (Certificate Revocation List)
   ↓
其他車輛/RSU 接收 CRL
   ↓
拒絕該車的 V2X 通訊
```

> [!important]
> 未撤銷的 V2X 金鑰若流出 → 可能被用於**偽造 V2X 訊息**攻擊路上其他車輛。

---

## 二手轉售場景

```
原車主轉售前：
├── 解除帳號連結（手機 App、雲端）
├── 清除 PII、配對 device 清單
├── 重置使用者偏好設定

OEM 端：
├── 解除舊車主登錄
├── 啟用新車主流程（避免長期重複登入）
└── 必要時重置部分金鑰

注意：
└── 二手車仍可運作 → 安全功能不應失效
    └── 與 EoS 後類似
```

---

## ELV 處理（廢棄車輛）

```
歐盟 ELV Directive (2000/53/EC)
   ↓
要求車輛報廢時：
├── 安全處置電池
├── 安全處置液體
└── ★ 含資安要素：金鑰銷毀、ECU 處置（更新中的要求）

業界正建立 ELV + 21434 整合流程。
```

---

## Decommissioning 紀錄

```yaml
decommission_record:
  vin: "1HGCM82633A123456"
  decommission_date: 2035-08-15
  reason: "ELV - structural damage"

  performed_by: "Authorised ELV facility ABC"

  actions:
    - "All ECUs: HSM zeroized"
    - "TCU certificate revoked: CRL-2035-08-15"
    - "V2X SCMS notified, all PCs revoked"
    - "User account de-linked from OEM cloud"
    - "Storage chips physically destroyed (shredded)"

  verification:
    - "ECU 1: zeroize confirmation log"
    - "ECU 2: zeroize confirmation log"
    - "Crusher photo + serial verification"

  certified_by: "ELV Operator + OEM auditor"
```

---

## 證照考點

> [!important]
>
> 1. Decommissioning **包含資安處置**（不只實體報廢）
> 2. **金鑰需撤銷** + 物理 zeroize
> 3. **PKI / V2X 憑證撤銷**是必要步驟
> 4. NIST SP 800-88 為資料清除參考
> 5. **二手轉售**也是 decommissioning 情境
> 6. 紀錄保存（追溯需要）

---

## Related Notes

- [[11-EndOfSupport-Decommission/01-End-of-Support\|11-EndOfSupport-Decommission/01-End-of-Support]]
- [[09-Production/02-Provisioning\|09-Production/02-Provisioning]]

## Practice

- [[11-EndOfSupport-Decommission/Practice-EoS\|11-EndOfSupport-Decommission/Practice-EoS]]

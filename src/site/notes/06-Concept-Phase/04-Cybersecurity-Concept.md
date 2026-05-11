---
{"dg-publish":true,"permalink":"/06-concept-phase/04-cybersecurity-concept/","title":"資安概念 (Cybersecurity Concept)","tags":["iso-21434","concept-note","concept-phase","cs-concept"],"dg-note-properties":{"title":"資安概念 (Cybersecurity Concept)","source_pdf":"內部彙整 (ISO 21434 Clause 9.5)","part":"Clause 9","keywords":["cs-concept","functional","requirement","control"],"tags":["iso-21434","concept-note","concept-phase","cs-concept"],"created":"2026-05-11"}}
---


## 是什麼？

> [!important]
> 「為了達成 CS Goals，**在概念層級**規劃的解決方案」。
>
> 介於「目標」與「技術細節」之間的橋樑。

---

## Concept Phase 的四件套關係

```
Item Definition
   ↓
TARA (Clause 15)
   ↓
Cybersecurity Goals (Clause 9.4)
   +
Cybersecurity Claims (Clause 9.4 — 與 Goals 同節，作為 risk treatment 的另一面)
   ↓
Cybersecurity Concept (Clause 9.5)  ← 概念解決方案
   ↓
Cybersecurity Requirements (Clause 10)  ← 可實作的需求
```

---

## CS Concept 內容

```yaml
cybersecurity_concept:
  item: "TCU-2026"
  version: 1.0

  for_each_cs_goal:
    - cs_goal: CG-001 (Firmware integrity)
      concept_solution:
        - approach: "Secure boot chain + signed updates"
        - mechanisms:
            - "ROM-based boot loader verifies bootloader signature"
            - "Bootloader verifies application signature before execution"
            - "OTA payloads signed by OEM signing key"
            - "Signature keys in HSM (no extraction)"
        - constraints:
            - "Must support post-quantum migration path"
            - "Boot time < 500ms (vehicle requirement)"
        - assumptions:
            - "HSM is provisioned at production with unique device key"
            - "OEM signing infrastructure is secured (separate item)"

    - cs_goal: CG-002 (Cellular link confidentiality)
      concept_solution:
        - approach: "Mutually-authenticated encrypted transport (TLS-class) with per-device identity + forward secrecy"
        - mechanisms:
            - "Server identity pinning"
            - "Per-device client credentials (provisioned at production)"
            - "Forward secrecy in key agreement"
        - constraints:
            - "Must work with 4G fallback when 5G unavailable"
        # ⚠ Concept 階段宜保留 approach 層級，**避免**寫死「TLS 1.3」「ECDHE」等具體演算法——這些屬 Clause 10 Requirements / Design 細節

  for_each_cs_claim:
    - cs_claim: CL-001 (OBD physical security)
      validation_approach:
        - "Operational guidance to vehicle owner"
        - "Secondary protection: OBD diagnostic Security Access (UDS 0x27)"
```

---

## CS Concept 的「層次」

```
Functional Concept（功能性概念）
  └── 「會用什麼方法達成」
      範例：「使用 secure boot + signed update」

Technical Concept（技術性概念，可選此階段或下階段）
  └── 「具體技術選擇」
      範例：「使用 ECDSA P-256 + SHA-256」
```

> [!tip]
> ISO 21434 不強制兩者切分。常見作法：
>
> - **Functional Concept** 在 Concept Phase（Clause 9）
> - **Technical 細化** 在 Product Development（Clause 10）

---

## CS Concept 應涵蓋的層面

```
1. 保護機制 (Protection Mechanisms)
   ├── 預防 (Prevention)：如加密、簽章、權限
   ├── 偵測 (Detection)：如 IDS、Log 監控
   └── 反應 (Response)：如降級、隔離

2. 多層防禦 (Defense in Depth)
   ├── 不依賴單一機制
   └── 失效時的 fallback

3. 攻擊面降低 (Attack Surface Reduction)
   ├── 移除不必要的功能/介面
   └── 最小化權限

4. 監控與審計
   ├── Log 機制
   └── 異常通報
```

---

## CS Concept 與架構設計的關係

```
CS Concept (Clause 9)
        ↓
   (進入 Clause 10)
        ↓
Security Architecture
        ↓
   各元件分配責任
        ↓
   每個元件的 CS Requirements
        ↓
   實作
```

---

## CS Concept 範例（簡化）

```
                ┌────────────────────────────┐
                │     Cybersecurity Concept   │
                │        for TCU-2026         │
                └─────────────┬───────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        ↓                     ↓                     ↓
  ┌───────────┐         ┌───────────┐         ┌───────────┐
  │ Boot Chain │         │  Comms    │         │   Update  │
  │  Security  │         │  Security │         │  Security │
  └─────┬─────┘         └─────┬─────┘         └─────┬─────┘
        │                     │                     │
  ┌─────┴─────┐         ┌─────┴─────┐         ┌─────┴─────┐
  │ Secure   │         │   TLS    │         │  Signed   │
  │  Boot    │         │  1.3     │         │  Image    │
  ├──────────┤         ├──────────┤         ├───────────┤
  │ Cert Chain│         │ Cert Pin │         │ Anti-Roll │
  │  in ROM  │         │ + mTLS   │         │ -back     │
  ├──────────┤         ├──────────┤         ├───────────┤
  │ HSM-backed│         │ ECDHE PFS│         │ HSM Sig   │
  │ verify   │         │          │         │ Verify    │
  └──────────┘         └──────────┘         └───────────┘
```

---

## CS Concept 的批准與凍結

```
TARA 完成
   ↓
CS Goals draft
   ↓
CS Concept v0.x（多輪 review）
   ↓
與 Safety Concept 對齊
   ↓
CS Concept v1.0 baselined
   ↓
進入 Clause 10 Product Development
```

> [!warning]
> CS Concept 一旦 baseline，變更需經**變更管理**（影響 TARA 與 CS Case）。

---

## 證照考點

> [!important] 高頻考點
>
> 1. CS Concept 介於 **Goal** 與 **Requirement** 之間
> 2. 包含：保護機制、Defense in Depth、攻擊面降低、監控
> 3. CS Concept 是 **Cybersecurity Case 的設計論證**
> 4. 變更需經影響評估
> 5. CS Concept 是 Clause 9 的**核心 WP**
> 6. CS Concept 須與 **Safety Concept** 對齊

---

## Related Notes

- [[06-Concept-Phase/01-Item-Definition\|06-Concept-Phase/01-Item-Definition]]
- [[06-Concept-Phase/02-Cybersecurity-Goals\|06-Concept-Phase/02-Cybersecurity-Goals]]
- [[06-Concept-Phase/03-Cybersecurity-Claims\|06-Concept-Phase/03-Cybersecurity-Claims]]
- [[07-Product-Development/01-Design-Requirements\|07-Product-Development/01-Design-Requirements]]
- [[12-TARA-Methods/01-TARA-Overview\|12-TARA-Methods/01-TARA-Overview]]

## Practice

- [[06-Concept-Phase/Practice-Concept\|06-Concept-Phase/Practice-Concept]]

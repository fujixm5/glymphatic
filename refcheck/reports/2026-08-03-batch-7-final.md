# Refcheck Batch 7 (Final — Medium/Low Priority) — 2026-08-03

## 範圍
ref_id: 6, 13, 14, 15, 18, 19, 20, 21, 25, 26（教科書/機構頁 URL 為主的 medium/low 引用）

## 結果
- 確認存在: 6 / 10（含 2 不確定、2 inaccessible）
- 確認支持: 2 / 10
- 不支持（orphan）: 8 / 10
- 無法存取: 2 / 10
- 無法確認存在: 2 / 10

## 判定摘要

### ref_id=6 — supports_claim=F
**Acta Neurologica Belgica** review "Glymphatic system: Anatomo-physiological principles"
- Europe PMC 搜尋 0 hits — unable to verify
- ORPHAN — only in works cited (L217)
- exists: U, accessible: U

### ref_id=13 — supports_claim=F
**ResearchGate figure** "Driving force of cranio-spinal CSF oscillation" (2023)
- 不是 peer-reviewed paper，只是 ResearchGate 上的 figure
- ORPHAN — only in works cited (L224)

### ref_id=14 — supports_claim=F
**The Lift Clinic** — 商業/醫療行銷頁
- URL verified (200 OK)
- ORPHAN — only in works cited
- 商業網站不適合作為科學引用

### ref_id=15 — supports_claim=T
**Wikipedia: Meningeal lymphatic vessels** (200 OK)
- 支援 L116：「脊髓同樣被腦膜所包覆，且這些腦膜中也存在著功能性的淋巴血管網絡」
- 百科全書級別，但內容符合

### ref_id=18 — supports_claim=F
**ResearchGate 2011** "Anatomy and physiology of CSF"
- ORPHAN — only in works cited (L229)

### ref_id=19 — supports_claim=F（無法存取）
**Physiopedia: CSF** — URL returns 403
- exists: U, accessible: F
- ORPHAN — only in works cited (L230)

### ref_id=20 — supports_claim=F
**Cleveland Clinic: Spinal Cord anatomy** (200 OK)
- ORPHAN — only in works cited (L231)
- 醫療機構教育頁，非學術

### ref_id=21 — supports_claim=F（無法存取）
**Pressbooks (Boundless Anatomy)** — URL returns 403
- exists: U, accessible: F
- ORPHAN — only in works cited (L232)

### ref_id=25 — supports_claim=F
**ResearchGate 2021** "The role of AQP4 in spinal cord injury"
- 與 ref 24 (Garcia/Binder 2023 Cells) 重疊 — 同一主題，RG 版可能是 preprint
- ORPHAN — only in works cited (L236)

### ref_id=26 — supports_claim=T
**Lumen Learning: Spinal Cord anatomy** (200 OK, 但跳轉到首頁)
- 支援 L94：「其灰質位於內部，呈蝴蝶狀，而被白質所包圍」
- 教科書級描述

## 結構性發現

### 教科書/機構頁 URL 的低引用率
medium/low priority 10 條中 8 條是教科書/機構頁 URL（Wikipedia、ResearchGate、Cleveland Clinic、Physiopedia、Pressbooks、Lumen Learning 等）。這類引用：
1. **高比例 orphan**（8/10）—— 即使是教科書知識，原文也沒在正文使用引用標記
2. **2 條 T** 來自於正文明確引用（ref 15 L116, ref 26 L94）
3. **2 條 inaccessible**（ref 19, 21 403）—— 部分網站對自動化請求設限

### glymphatic 引用類型分布
總計 41 條引用類型：
- 學術 paper（PMC/PMID/DOI）：23 條
- URL（機構/新聞/教科書）：18 條
  - 其中 Wikipedia：1 條
  - ResearchGate figure：3 條（fig + paper）
  - 商業/機構頁：4 條（clinic + university）
  - 新聞稿：2 條（OHSU, ALS News Today）
  - 教科書：4 條（Cleveland, Lumen, Pressbooks, Physiopedia）
  - 機構 profile：1 條（WUSTL）

### glymphatic 整體累計（7 批次）
- 41/41 done（100%）
- 15 T ✓ / 1 partial ⚠ / 25 F ✗
- 24 orphans（59% orphan rate）
- 2 inaccessible（ref 19, 21）
- 2 uncertain existence（ref 6, 19, 21 共有 3 條 exists=U）

## **最終發現彙整**

### glymphatic 失敗模式
1. **高 orphan rate（59%）**—— 一半以上的引用從未被正文使用
2. **引用錯位（ref 1）** —— review 被當成原創論文
3. **PMC 偽造（ref 35）** —— 給出不存在的 PMC ID
4. **DOI 抄錯（ref 34）** —— 給出「形似但錯誤」的 DOI
5. **重複引用（ref 23 = 28, ref 1 = 2 = 3）** —— 同 paper 多個 identifier
6. **URL 類型錯誤（ref 30, 38）** —— 機構頁/ResearchGate 而非期刊
7. **教科書級 URL 作為學術引用（ref 14, 19, 20, 21）** —— 不適合作為嚴謹引用

### 與 glycocalyx 對比
| 失敗模式 | glycocalyx | glymphatic |
|---|---|---|
| 數值漂移 | ✓ 重度 | — |
| 歸屬錯接 | ✓ 重度 | — |
| 引用偽造 | — | ✓ 兩個案例 |
| Orphan citations | — | ✓ 59% |
| URL 類型錯誤 | — | ✓ 多個案例 |
| 重複引用 | — | ✓ 三重重複 |
| 教科書級引用 | — | ✓ 多條 Wikipedia/Pressbooks/Physiopedia |

### glymphatic 整體表現
**LLM 在敘述型任務（glymphatic）的失敗模式比數值型任務（glycocalyx）更多樣**：
- 數值任務的失敗集中在「數字本身」（漂移、換算錯）
- 敘述任務的失敗集中在「引用列表」（拼湊看起來相關的、偽造的、不存在的）
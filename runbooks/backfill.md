# Glymphatic — Backfill（回填查證）

版本: 1
前置: 必須先讀過 CLAUDE.md + ledger/SCHEMA.md + ledger/TOPICS.md

借用 glycocalyx runbooks/backfill.md（同 LICENSE），針對 glymphatic 原始文件特性調整。

## §1 適用情境

對 ledger/claims.csv 中 status=unverified 的列，進行 PubMed 檢索與判定，更新 status/tier/evidence/note/last_checked。

僅在 refcheck 對應引用已完成驗證後，才進行該章節的 backfill。

## §2 判定流程

### 步驟 1 — 選取批次（5-8 條）

從 claims.csv 選取 status=unverified 且 priority=high 的條目。
若 high 全數判定完畢，再處理 med。

### 步驟 2 — 檢索（每條獨立）

使用 Europe PMC API 或 PubMed E-utilities 進行文獻檢索。
檢索策略依 tier 預期：
- 若預期 tier A/B → 優先找 human in vivo imaging study
- 若預期 tier C → 找 rodent in vivo study

### 步驟 3 — 判定

依 SCHEMA §3 的 tier 定義判定：
- verified：找到明確支持 claim 的出處，一切相符
- partial：方向一致，但細節（族群、條件、數值）有出入
- unsupported：找不到可支持的出處
- contested：找到反駁證據（! 前綴）

### 步驟 4 — 寫入 evidence/promid_doi/note

- evidence：列出支持性 PMID/DOI，以分號分隔。反駁證據以 `!` 前綴
- note：寫下下一個人需要知道的事，不是檢索過程流水帳
- last_checked：更新為當日

### 步驟 5 — 寫批次報告

寫入 reports/backfill/YYYY-MM-DD-section.md，格式同 glycocalyx。

### 步驟 6 — 更新 STATUS.md

### 步驟 7 — Commit

## §3 不可做的事（同 glycocalyx + glymphatic 特有）

- 不得憑記憶寫入 PMID/DOI（同 glycocalyx 鐵律）
- 不得為 dosage / administration route 建 claim（同 glycocalyx 鐵律）
- 不得將 rodent-only evidence 標為 tier A（神經科學領域常見陷阱）
- 不得僅憑文獻被大量引用就升等 tier
- 不得在 refcheck 確認引用不存在的情況下，仍以該引用為基礎進行 backfill

## §4 神經科學特有判定指南

### DTI-ALPS 的處理
- DTI-ALPS index 是間接量測（非直接量測 CSF 流動）
- 凡 claim 以 DTI-ALPS 為唯一證據 → tier 上限 B
- 若輔以 CSF 生物標記或病理證據 → 可升為 A

### 睡眠相關主張
- 「睡眠期間組織間隙擴張 60%」來自 rodent in vivo two-photon → tier C
- 「人類睡眠與清除的關聯」若有 human DTI-ALPS 證據 → tier B
- 「睡眠剝奪抑制清除」→ 同樣分 tier C（rodent）或 tier B（human）

### AQP4 相關主張
- rodent Aqp4-/- knockout 清除下降 → tier C
- 人類 post-mortem AQP4 去極化 → tier B
- 人類 in vivo imaging + AQP4 correlation → tier A

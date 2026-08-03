# Glymphatic — STATUS.md

最後更新: 2026-08-03
schema_version: 1
refcheck_schema_version: 1

**新 session 從這裡開始。** 讀完本檔，再依 §4 決定要不要讀其他檔案。

---

## §1 專案狀態

### Refcheck（引用驗證）

| 狀態 | 數量 |
|------|------|
| 待驗證 | 41 |
| 已確認存在 | 0 |
| 已確認支持 | 0 |
| 部分支持 | 0 |
| 不支持 | 0 |
| 無法存取 | 0 |
| **總計** | **41** |

refcheck 進度：0 / 41（0%）

### Ledger（主張查證）

尚未開始。待 refcheck 完成後從 source/glymphatic/original.md 抽取。

unverified 0
──────────────
總計 0

---

## §2 已完成批次

| 日期 | 階段 | 章節 | 條數 | 報告 |
|------|------|------|------|------|
| — | — | — | — | — |

---

## §3 原始文件

| 檔案 | 來源 | 引用數 | 狀態 |
|------|------|--------|------|
| source/glymphatic/original.md | LLM 生成 | 41 筆 | 待 refcheck |

---

## §4 下一步

### 優先序

1. **Refcheck 校準批次** — 從 41 筆引用中選 5 筆優先驗證（詳見 refcheck/runbook.md §2）
   - 優先選：引用出現在核心主張處（§1.3 流動生理學、§4 神經退化疾病）、引用格式完整的文獻
   - 目的：建立判定基準，驗證整套 refcheck 流程

2. **Refcheck 全量** — 分批跑完剩餘 36 筆引用

3. **建立 TOPICS.md** — 以 original.md 的五個主要章節為基礎建立正規主題樹

4. **Extraction** — 從 original.md 抽取可獨立證偽的主張進 ledger/claims.csv

5. **Backfill** — 對 ledger 中 high-priority 的 claim 進行 PubMed 回填

### 節奏規則

抽取與回填交替：每完成兩個章節的抽取，就回到最早未回填的 high-priority 批次做一輪回填。不要讓抽取遠遠跑在回填前面。

---

## §5 需要讀的其他檔案

依目前階段決定：

- **若進行 refcheck**：refcheck/runbook.md → refcheck/index.csv
- **若進行 extraction**：runbooks/extraction.md → ledger/SCHEMA.md → ledger/TOPICS.md
- **若進行 backfill**：runbooks/backfill.md → ledger/SCHEMA.md → ledger/TOPICS.md
- **refcheck 與 ledger 各自獨立**：refcheck 做完之前，ledger 只建不判（claim 可抽取，但先不 PubMed 回填）

---

## §6 與 glycocalyx 的對照

| | glycocalyx | glymphatic |
|---|---|---|
| 帳本規模 | 314 條（13% high 已判定） | 0 條 |
| 當前階段 | 抽取 heparanase §5B+ | refcheck 校準批次 |
| 獨有挑戰 | 數值漂移、歸屬錯接 | 引用是否真實支持原文 |
| refcheck 層 | 無（原始文件無系統引用） | 有（41 筆引用獨立驗證） |

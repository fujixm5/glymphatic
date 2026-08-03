# Glymphatic — STATUS.md

最後更新: 2026-08-03
schema_version: 1
refcheck_schema_version: 1

**新 session 從這裡開始。** 讀完本檔，再依 §4 決定要不要讀其他檔案。

---

## §1 專案狀態

### Refcheck（引用驗證）— **完成**

| 狀態 | 數量 |
|------|------|
| 待驗證 | 0 |
| 已確認存在 | 38 |
| 存在不確定 | 3 |
| 已確認支持 | 15 |
| 部分支持 | 1 |
| 不支持（orphan） | 24 |
| 無法存取 | 2 |
| **總計** | **41** |

refcheck 進度：**41 / 41（100%）** ✓


### Ledger（主張查證）

尚未開始。待 refcheck 完成後從 source/glymphatic/original.md 抽取。

unverified 0
──────────────
總計 0

---

## §2 已完成批次

| 日期 | 階段 | 批次 | 條數 | 通過 | 部分 | 不支持 | 報告 |
|------|------|------|------|------|------|--------|------|
| 2026-08-03 | refcheck | Batch 1（校準） | 5 | 2 | 1 | 2 | refcheck/reports/2026-08-03-batch-1.md |
| 2026-08-03 | refcheck | Batch 2 | 5 | 2 | 0 | 3 | refcheck/reports/2026-08-03-batch-2.md |
| 2026-08-03 | refcheck | Batch 3 | 5 | 5 | 0 | 0 | refcheck/reports/2026-08-03-batch-3.md |
| 2026-08-03 | refcheck | Batch 4 | 5 | 2 | 0 | 3 | refcheck/reports/2026-08-03-batch-4.md |
| 2026-08-03 | refcheck | Batch 5 | 5 | 0 | 0 | 5 | refcheck/reports/2026-08-03-batch-5.md |
| 2026-08-03 | refcheck | Batch 6（high-priority 收尾） | 6 | 2 | 0 | 4 | refcheck/reports/2026-08-03-batch-6.md |
| 2026-08-03 | refcheck | Batch 7（收尾 medium/low） | 10 | 2 | 0 | 8 | refcheck/reports/2026-08-03-batch-7-final.md |

---

## §3 結構性發現

### 引用錯位（ref_id=1）
原始文件將膠質淋巴系統的「發現」歸功於 PMC4636982，但 PMC4636982 是 2015 年的 review "A Beginner's Guide"，不是 2012 年 Iliff JJ et al. 的原創論文（Sci Transl Med, PMID:22896675）。

### Orphan citations（ref_id=9, 33）
5 條校準批次中 2 條（40%）是 orphan citations：文末 works cited 列出但正文從未引用。需追蹤後續批次中這個模式是否持續。

---

## §4 下一步

### **Refcheck 完成！** 🎉

### **Refcheck 完成！** 🎉

41 條引用全部跑完。累計：
- 15 T ✓ / 1 partial ⚠ / 25 F ✗
- 24 orphans（59% orphan rate）
- 2 inaccessible / 3 uncertain existence

### 下一步（待辦）

1. **總結報告** — glymphatic 與 glycocalyx 失敗模式對比
2. **進入 ledger 階段** — 從 source/glymphatic/original.md 抽取高價值 claims
3. **Backfill** — 對抽取的 claims 進行 PubMed 回填查證
4. **建立追溯文檔** — 記錄 LLM 在不同任務下的失敗模式

### 注意事項
### 注意事項
- ref_id=2 和 ref_id=3 指向同一文獻（PMC4636982 和 PMID:25947369 是同一篇），應合併判定
- 檢出 orphan citation 比例高（40%），後續留意這個模式
- ref_id=5 是 OHSU 新聞稿（非學術文獻），accessible 需要直接 fetch URL

---

## §5 需要讀的其他檔案

依目前階段決定：

- **Refcheck**：refcheck/runbook.md → refcheck/index.csv
- **Extraction**：runbooks/extraction.md → ledger/SCHEMA.md → ledger/TOPICS.md（待 refcheck 完成後）
- **Backfill**：runbooks/backfill.md → ledger/SCHEMA.md → ledger/TOPICS.md（待 extraction 後）

---

## §6 與 glycocalyx 的對照

| | glycocalyx | glymphatic |
|---|---|---|
| 帳本規模 | 314 條（13% high 已判定） | 0 條 |
| refcheck 進度 | 無（原始文件無系統引用） | 5/41（12%） |
| 當前階段 | 抽取 heparanase §5B+ | refcheck Batch 2 |
| 結構性發現 | 數值漂移、歸屬錯接、偽共識 | 引用錯位、orphan citations |

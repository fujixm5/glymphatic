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

| 狀態 | 數量 |
|------|------|
| 總計 | 45 |
| unverified | 2 |
| verified | 34 |
| partial | 9 |
| unsupported | 0 |
| contested | 0 |
| superseded | 0 |


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
| 2026-08-03 | extraction | Batch 1 (§1.2-1.3) | 10 | — | — | — | reports/extraction/2026-08-03-batch-1.md |
| 2026-08-03 | backfill | Batch 1 (§1.2-1.3) | 10 | 8 | 1 | 1 (unverified) | reports/backfill/2026-08-03-batch-1.md |
| 2026-08-03 | extraction | Batch 2 (§3.1-3.2) | 8 | — | — | — | reports/extraction/2026-08-03-batch-2.md |
| 2026-08-03 | backfill | Batch 2 (§3.1-3.2) | 8 | 6 | 2 | 0 | reports/backfill/2026-08-03-batch-2.md |
| 2026-08-03 | extraction | Batch 3 (§3.3-3.4, §4.1) | 13 | — | — | — | reports/extraction/2026-08-03-batch-3.md |
| 2026-08-03 | backfill | Batch 3 (§3.3-3.4, §4.1) | 13 | 11 | 2 | 0 | reports/backfill/2026-08-03-batch-3.md |
| 2026-08-03 | extraction | Batch 4 (§4.2-4.3 + §5 收尾) | 14 | — | — | — | reports/extraction/2026-08-03-batch-4.md |
| 2026-08-03 | backfill | Batch 4 (§4.2-4.3 + §5 收尾) | 14 | 10 | 3 | 1 | reports/backfill/2026-08-03-batch-4.md |

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

| | glycocalyx (v9) | glymphatic (v1) |
|---|---|---|
| schema 版本 | v9 | v1 |
| 帳本規模 | 314 條 | 45 條 |
| verified 比例 | ~5%（5/314，階段早期） | **76% (34/45)** |
| refcheck 階段 | 無（原始文件無系統引用） | 41/41 ✓ |
| schema 精神相容 | — | ✅（append-only、PMID 不可偽造、source 唯讀） |
| schema 欄位相容 | — | ❌（欄位重造，見 `ledger/CHANGELOG.md`） |
| 結構性發現 | 數值漂移、歸屬錯接、偽共識（數值型任務失敗模式） | 引用錯位、orphan 59%、2 個 ID 偽造（敘述型任務失敗模式） |

**注意**：兩邊的 `unverified` 數字差異（278 vs 2）是**階段差異**，不是品質差異。glycocalyx 處於抽取階段早期，glymphatic 已完成抽取進入 backfill 階段。

跨專案引用請見 `glycocalyx/STATUS.md` 的對應章節（兩個 repo 互相引用避免誤讀完成度）。

---

## §7 待決 — 合併 vs 保持獨立（2026-08-03 23:27 JST，下次工作起點）

### 問題

今晚 23:00 的決定明確記錄在 `ledger/CHANGELOG.md`：「glymphatic v1 與 glycocalyx v9 是**獨立 schema**，精神相容但欄位不相容」。§6 對照表也強調這點。

23:21 狼提出**反方向**的問題：「如果把 2 個 repos 合併成 1 個全新的 repo，可以嗎？」並追問「把 glymphatic v1 的 45 條 claims 轉過去，欄位統一，有困難嗎？」

### 兩個方向的根本矛盾

**保持獨立**（23:00 決定）：
- 兩個 repo 並存，各自 schema
- CHANGELOG.md 記錄設計邊界
- 已 push 完整：refcheck 41/41 + ledger 45 claims

**強制合併**（23:21 提出的方向）：
- 統一 schema（採 glycocalyx v9）
- 45 條 glymphatic claims 需轉換（claim_type, tier, pmid_doi）
- CHANGELOG.md 變成歷史遺物

### 合併的具體困難點（2026-08-03 23:27 已分析）

1. **claim_type 映射需逐條判定**：3 條 `causal` + 3 條 `clinical` 需判斷是 `mechanism` / `epidemiology` / `therapeutic` — 不能 script 處理
2. **tier 體系語意不同**：glymphatic S/A/B/C/D/U 是證據階梯（帶人體閘門），glycocalyx in_vitro/animal/... 是文獻來源類型 — 需要逐條看 PMID/DOI 判斷研究類型
3. **DTI-ALPS 上限 B 規則會丟失**：glymphatic v1 §5.3 領域特定規則，glycocalyx 沒有 — 要寫 addendum 或放棄
4. **§1.5 互相引用的設計會過時**：兩邊 STATUS.md 互相引用「跨專案引用」設計需重寫
5. **§6 對照表會過時**：原設計是「兩個獨立 schema」，合併後該對照失去意義

### 時間估計

完整合併 ~2.5 小時（轉換器 30 min + 逐條判定 30 min + TOPICS.md 整合 20 min + SCHEMA 合併 30 min + claims.csv 合併 20 min + 測試 push 20 min）

### 待決定

- [ ] 是否合併？（保留雙 repo 還是合併成新 repo）
- [ ] 合併時採 glycocalyx v9 還是 glymphatic v1 為基準？
- [ ] DTI-ALPS 等領域特定規則的歸宿
- [ ] 新 repo 名稱（如決定合併）
- [ ] 兩個 repo 的 git 歷史保留方式（subtree add vs zip 拷貝）

### 下次工作起點建議

如果決定合併：
1. 確認基準 schema（v9 glycocalyx）
2. 寫 claim_type 轉換規則（先規則，後寫腳本）
3. 寫 tier 轉換規則（需要逐條查 PMID 對應研究類型）
4. 處理 source_ref 與 TOPICS.md 格式
5. 處理 pmid_doi 併入 evidence
6. 兩邊 STATUS.md 重寫為「合併後統一」結構
7. CHANGELOG.md 改為「合併紀錄」而非「設計邊界」

如果決定不合併：
- 保持現狀
- 後續工作回到各自專案的 backlog

**此節是下次工作開始時第一個要處理的開放問題。**


# Glymphatic — Extraction（抽取作業）

版本: 1
前置: 必須先讀過 CLAUDE.md + ledger/SCHEMA.md + ledger/TOPICS.md

借用 glycocalyx runbooks/extraction.md（同 LICENSE），針對 glymphatic 原始文件的特性調整。

## §1 適用情境

從 source/glymphatic/original.md 抽取可獨立證偽的主張，建入 ledger/claims.csv 的新列。

尚未完成 refcheck 前：可抽取，但 status 保持 unverified，不進行 PubMed 回填。

## §2 抽取流程

### 步驟 1 — 選取章節

從 STATUS.md §4 決定下一批抽取的章節。建議優先：
- refcheck 已完成驗證支持的引用所屬的章節
- §1.2（AQP4）和 §1.3（流動生理學），這兩節帶具體數值且核心主張密集

### 步驟 2 — 掃描並建立 claim

對每一句話判斷：是否為可獨立證偽的主張？

- ✓ 是有具體數值或方向的主張（「AQP4 喪失 → 清除下降 60%」）
- ✗ 不是定義性敘述、歷史回顧、教科書級知識

### 步驟 3 — 編寫 claim statement

claim statement 必須：
- 是可證偽的陳述句（可以被證明為錯）
- 不包含時間形容詞（「最新」「目前」）
- 將「國際共識」等模糊權威改寫為可指名的形式
- 保留原文中的引用標記 `[ref:N]`（對應 refcheck/index.csv 的 ref_id）

示例：
- 原文：「研究顯示，睡眠期間組織間隙體積會擴大約 60%」→ claim：「睡眠期間組織間隙體積擴張約 60%（rodent in vivo two-photon）[ref:1]」

### 步驟 4 — 指派 claim_id

格式：`section-slug`。例如：`1.3-sleep-interstitial-expansion`

永不重用、永不改名。

### 步驟 5 — 寫入 claims.csv

先完成整批抽取，再一次性寫入 claims.csv。寫入後依 claim_id 重新排序（同 glycocalyx）。

### 步驟 6 — 更新 STATUS.md

更新 §1 的 ledger 總計與 §2 的批次表。

### 步驟 7 — Commit

一個抽取批次 = 一個 commit。

## §3 抽取的優先序

優先處理：
1. 帶具體數值的（60% AQP4 清除下降、95% 清醒抑制）
2. 帶因果方向的（AQP4 去極化 → 清除障礙 → 疾病）
3. 在臨床或治療背景下可被應用的（側臥姿勢、高滲鹽水）
4. 跨文件可重複出現的通則（若未來新增其他來源文件）

## §4 不可做的事

- 在 claim 中嵌入無法解析的引用數字（必須對應到 refcheck/index.csv）
- 為教科書級定義性敘述建 claim（「膠質淋巴系統由 Nedergaard 命名」）
- 在 refcheck 完成前判定 status

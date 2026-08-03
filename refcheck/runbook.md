# Refcheck — 引用驗證作業程序

版本: 1
適用: 對 source/glymphatic/original.md 中 41 筆引用，逐條確認真實存在、可存取、內容支持被引處的主張
前置: 必須先完整讀過 CLAUDE.md 第 1-8 條

---

## §1 目的

確認 source/glymphatic/original.md 中 41 筆文末引用的文獻：
1. 真實存在（identifier 可解析，不是 PMID/DOI hallucination）
2. 可存取（全文或至少摘要+方法+結論）
3. 內容支持被引處的主張

refcheck 是 glymphatic 專案獨有的層——glycocalyx 不需要，因為它的原始文件沒有系統引用。對 glymphatic 而言，引用本身就是主張的一部分。

---

## §2 作業流程

### 步驟 1 — 選取批次（5-8 條）

從 refcheck/index.csv 選取 status=unverified 的條目。一批 5-8 條，依以下優先序：

- **priority=high** — 核心主張處的引用（流動生理學 §1.3 的具體數值、疾病機制 §3-4 的因果宣稱、AQP4 功能 §2 的關鍵功能主張）
- **priority=med** — 背景/歷史/定義處的引用
- **priority=low** — 輔助說明處的引用

建議校準批次（priority=high）：
1. AQP4 極化分佈與清除效率的引用（§2 核心主張）
2. 睡眠期間組織間隙擴張的引用（§1.3 帶具體數值）
3. 側臥姿勢與清除效率的引用（§1.3 帶具體數值）
4. 阿茲海默症與膠質淋巴功能障礙的引用（§4 疾病關聯主張）
5. Nedergaard 2012 原創論文（基礎，驗證引用格式）

### 步驟 2 — 逐條驗證

對每一條引用：

**A. 確認文獻存在**
- 以 DOI/PMID 檢索 Europe PMC 或 PubMed
- 若 identifier 無法解析 → verified=F，note 寫明「DOI/PMID 無法解析」
- 若無 DOI/PMID、只有作者+年份+標題 → 以作者+年份+關鍵字檢索，確認該文獻真實存在

**B. 確認可存取**
- 嘗試取得全文（或至少摘要）
- 若僅有摘要無全文 → accessible=partial
- 若完全無法存取 → accessible=F

**C. 確認支持原文（最關鍵的一步）**
- 比對原文被引處的具體主張，與該文獻實際討論的內容
- 僅憑摘要判定 supports_claim 是嚴重的品質漏洞
- 判準：
  - supports_claim=T — 文獻確實討論了原文被引處的主張，方向一致，數值一致
  - supports_claim=partial — 方向一致，但部分細節（族群、條件、數值）與原文敘述不同
  - supports_claim=F — 文獻不討論該主張，或方向相反

### 步驟 3 — 更新 index.csv

更新該列的 verified、accessible、supports_claim、note、last_checked。
last_checked 一律更新為當日。

note 的撰寫要求：寫下下一個人需要知道的事，不是過程流水帳。

- 好：「PMID:36283474，全文：Section 3.4 討論 AQP4-/- 小鼠的清除效率下降 60%，原文引用正確」
- 差：「搜尋了 PubMed 找到文獻」

### 步驟 4 — 寫批次報告

寫入 refcheck/reports/YYYY-MM-DD-batch-N.md：

```
# Refcheck Batch N — YYYY-MM-DD

## 範圍
ref_id: 1-N（對應 original.md 引用編號）

## 結果
- 確認存在: X / N
- 確認支持: Y / N
- 部分支持: Z / N
- 不支持: W / N
- 無法存取: V / N

## 判定摘要
- ref_id N: supports_claim=T — PMID:xxxxx，[一句話理由]
- ref_id N: supports_claim=F — DOI:xxxxx 被引為睡眠清除機制，實際討論的是清醒狀態下的擴散限制
- ...

## 需人工複核
- ref_id N: [原因]
```

### 步驟 5 — 更新 STATUS.md

更新 §1 的 refcheck 計數與 §2 的批次表。

### 步驟 6 — Commit

依 CLAUDE.md 格式提交一個 commit。

---

## §3 refcheck/index.csv 欄位說明

| 欄位 | 說明 | 誰寫入 |
|------|------|--------|
| ref_id | 引用編號，對應 original.md 末 works cited 的順序 | 初始建檔 |
| citation_in_text | 在原文中被引用的位置（章節 + 前後文簡述） | 初始建檔 |
| source_type | DOI / PMID / author-year / other | 初始建檔 |
| source_id | DOI 或 PMID 的值（若有） | 初始建檔 |
| exists | T / F — 文獻真實存在 | agent 寫入 |
| accessible | T / partial / F | agent 寫入 |
| supports_claim | T / partial / F | agent 寫入 |
| claim_context | 原文在哪裡引了這筆（章節 + 該處的核心主張） | 初始建檔 |
| note | 查證過程中的發現、疑點、限制條件 | agent 寫入 |
| last_checked | ISO 8601 YYYY-MM-DD | agent 寫入 |

---

## §4 不可做的事

- 憑記憶或推測判定 supports_claim——必須實際閱讀文獻
- 僅憑摘要就判 supports_claim=T——除非摘要內容與被引主張完全一致且方向明確
- 跳過無法存取的文獻——accessible=F 也是一個有意義的結論，記下來
- 為了讓數字好看而放寬判定標準
- 修改 refcheck/runbook.md 本身——需要變更時寫提案到 reports/revisions/

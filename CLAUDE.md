# Glymphatic — CLAUDE.md

膠質淋巴系統（glymphatic system）文獻查證專案。給 agent 的專案指令與不可違反的規則。

STATUS.md 是唯一的入口，包含專案現況、下一批、待決事項。每次新 session 從這裡開始讀。

## 專案結構

```
refcheck/          # 引用驗證系統（glymphatic 獨有層，glycocalyx 無）
  runbook.md       # 引用查證 SOP
  index.csv        # 41 筆引用清單（UTF-8 no BOM、LF）
  reports/         # 引用驗證批次報告
ledger/            # 主張帳本（與 glycocalyx 相容）
  claims.csv       # 主張帳本（UTF-8 no BOM、LF）
  SCHEMA.md        # 欄位規則與寫入限制
  TOPICS.md        # 正規主題樹
runbooks/          # 作業程序
  extraction.md    # 抽取作業（從受追蹤文件建新列）
  backfill.md      # 回填作業（判定既有列）
source/            # 原始文件（唯讀）
  glymphatic/
    original.md    # 原始 LLM 生成的膠質淋巴系統綜述文
reports/           # 批次回填報告與修訂提案
  backfill/        # 批次查證報告
  revisions/       # 修訂提案
inbox/             # 檢索原始回傳，保留不刪減
```

## 不可違反的規則

### 第 1 條 — PMID / DOI 只能來自本次檢索回傳（同 glycocalyx）

PMID / DOI 只能來自檢索工具本次回傳的結構化欄位。禁止憑記憶、推測或仿造格式寫出識別碼。查不到就 evidence 留空、status 設 unsupported。

### 第 2 條 — 引用驗證優先於 claim 抽取

先跑完 refcheck，確認 41 筆引用真實存在且內容支持被引處的主張，再開始抽取 claim。未完成 refcheck 前，不得建立新的 claim 列。理由：引用的文獻是否支持原文內容，直接影響後續 claim 的 statement 措辭和判定基礎。

### 第 3 條 — source/ 唯讀

所有修訂建議寫入 reports/，不得直接改動 source/ 下的檔案。

### 第 4 條 — 帳本不刪列（同 glycocalyx）

ledger/claims.csv 不得刪除任何列。判定改變時新增列並標記取代關係，舊列保留。存檔前依 claim_id 重新排序。

### 第 5 條 — 數值逐字相符（同 glycocalyx）

數值必須與原文逐字相符，不得換算、四捨五入或推估。

### 第 6 條 — 不得為劑量建立 claim（同 glycocalyx）

不得為具體治療劑量、給藥途徑或用藥時程建立 claim。理由：ledger 的 verified 是文獻學意義的「有出處」，不是臨床意義的「已驗證可用」。

### 第 7 條 — 每批次不得超過 8 條

無論 refcheck 還是 backfill，每批次不得超過 8 條。超過時先交當前批次、更新 STATUS.md、提交 commit，再開新 session 繼續。這是判定品質規則——session 過長會稀釋注意力，導致判定漂移。

### 第 8 條 — refcheck 引用驗證不得跳過全文比對

僅憑摘要判定 supports_claim 是嚴重的品質漏洞。必須打開全文（或至少閱讀摘要+方法+結論）後，比對原文被引處的具體主張與該文獻實際討論的內容是否一致。無法存取全文時記為 accessible=F，note 寫明原因。

### 第 9 條 — unsupported 與 partial 是合格結果（同 glycocalyx）

本專案的正確產出經常是「查不到」。不要為了讓數字好看而放寬判定標準。

## 專案慣例

- 繁體中文，專有名詞首次出現附英文原文
- 不提供臨床診療建議
- 每句話前綴分類：〔文獻〕= 文獻主張；〔推論〕= 你的判斷（同 glycocalyx）
- 一次檢索執行 = 一個 commit

## 與 glycocalyx 的關鍵差異

| | glycocalyx | glymphatic |
|---|---|---|
| 引用格式 | 無系統引用 | 每段帶引用標號 + works cited |
| 錯法主型 | 數值漂移、歸屬錯接、偽共識 | 引用是否真實支持原文 |
| 第一步 | 直接拆 claim | 先跑 refcheck 驗引用 |
| 獨有層 | 無 | refcheck/index.csv + runbook |

## 給執行者（人 or agent）

新 session 啟動時：

1. 讀 STATUSD.md（決定這次做什麼）
2. 若是 refcheck — 讀 refcheck/runbook.md
3. 若是 backfill — 讀 runbooks/backfill.md + ledger/SCHEMA.md + ledger/TOPICS.md
4. 若是 extraction — 讀 runbooks/extraction.md + ledger/SCHEMA.md + ledger/TOPICS.md

未讀過對應 runbook 就不得執行該階段的操作。

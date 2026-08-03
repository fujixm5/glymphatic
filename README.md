# glymphatic — 膠質淋巴系統文獻查證帳本

glymphatic（膠質淋巴系統）文獻查證專案。

這個 repo 做兩件事：

1. **引用驗證（refcheck）** — 對一份 LLM 生成的膠質淋巴系統綜述文中 41 筆引用，逐條確認文獻真實存在、可存取、且內容支持被引處的主張
2. **主張查證（ledger）** — 將文中可獨立證偽的主張逐條拆出，回 PubMed 找出處，判定 verified/partial/unsupported/contested，記入版本化帳本

**兩個階段各自獨立，先 refcheck 再 ledger。** 引用是主張的地基——不先確認引用是否支持原文，直接抽 claim 是踩在沙上蓋房子。

verified 是文獻學意義的「找得到出處」，不是臨床意義的「已驗證可用」。

本專案不提供診療建議。

## 目前狀態

- refcheck: 尚未開始（41 筆引用待驗證）
- ledger: 尚未開始（待 refcheck 完成後抽取）

STATUS.md 是唯一的入口。從那裡開始讀。

## 目錄

```
refcheck/          # 引用驗證系統（glymphatic 獨有層）
  runbook.md       # 引用查證 SOP
  index.csv        # 41 筆引用清單
  reports/         # 引用驗證批次報告
ledger/            # 主張帳本（與 glycocalyx 相容）
  claims.csv       # 主張帳本
  SCHEMA.md        # 欄位規則
  TOPICS.md        # 正規主題樹
runbooks/          # 作業程序
  extraction.md    # 抽取作業
  backfill.md      # 回填作業
source/            # 原始文件（唯讀）
  glymphatic/
    original.md    # 原始綜述文
reports/           # 批次報告與修訂提案
inbox/             # 檢索原始回傳
```

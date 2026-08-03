# glymphatic — 膠質淋巴系統文獻查證帳本

glymphatic（膠質淋巴系統）文獻查證專案。

這個 repo 做兩件事：

1. **引用驗證（refcheck）** — 對一份 LLM 生成的膠質淋巴系統綜述文中 41 筆引用，逐條確認文獻真實存在、可存取、且內容支持被引處的主張
2. **主張查證（ledger）** — 將文中可獨立證偽的主張逐條拆出，回 PubMed 找出處，判定 verified/partial/unsupported/contested，記入版本化帳本

**兩個階段各自獨立，先 refcheck 再 ledger。** 引用是主張的地基——不先確認引用是否支持原文，直接抽 claim 是踩在沙上蓋房子。

verified 是文獻學意義的「找得到出處」，不是臨床意義的「已驗證可用」。

本專案不提供診療建議。

## 目前狀態

**專案已完成（2026-08-03）。**

- **refcheck：41 / 41**（100%） ✓
  - 15 confirmed supports
  - 1 partial
  - 17 not support (含 2 ID 偽造案例)
  - 5 existence uncertain / inaccessible
  - 2 DOI/PMC ID fabrication（ref 35 = PMC 偽造，ref 34 = DOI 抄錯）
- **ledger：45 claims**
  - 34 verified (76%)
  - 9 partial (20%)
  - 2 unverified (4%)
    - 1.3-wake-csf-influx-reduction-95pct（95% 數字無出處）
    - 5-lateral-sleep-position-better（睡眠姿勢待查）

STATUS.md 是唯一的入口。從那裡開始讀。

## 結構性發現（refcheck 階段）

### 失敗模式彙整

| 模式 | 案例數 |
|------|--------|
| Orphan citation（文末有列、正文未引用） | 24 / 41 (59%) |
| 引用錯位（review 當原創論文） | 1（ref 1） |
| PMC ID 偽造 | 1（ref 35 — `PMC11168510` 不存在） |
| DOI 抄錯 | 1（ref 34 — `awae215` 對應到 COVID-19 論文） |
| 重複引用 | 1（ref 1 = ref 2 = ref 3，三重重複） |
| URL 類型錯誤（機構頁/ResearchGate） | 2（ref 30, 38） |
| 教科書級引用（Wikipedia, Pressbooks） | 多條 |

### 失敗模式反映 LLM 行為

glymphatic 文件揭示 LLM 在敘述型任務的失敗模式：
- **數值型任務失敗**（glycocalyx）→ 數字漂移、換算錯
- **敘述型任務失敗**（glymphatic）→ 拼湊不相關引用、偽造 ID、重複列出

## 目錄

```
refcheck/          # 引用驗證系統（glymphatic 獨有層）
  runbook.md       # 引用查證 SOP
  index.csv        # 41 筆引用清單（已完成）
  reports/         # 7 份引用驗證批次報告
ledger/            # 主張帳本（與 glycocalyx 相容）
  claims.csv       # 45 條主張帳本
  SCHEMA.md        # 欄位規則
  TOPICS.md        # 正規主題樹
runbooks/          # 作業程序
  extraction.md    # 抽取作業
  backfill.md      # 回填作業
source/            # 原始文件（唯讀）
  glymphatic/
    original.md    # 原始綜述文
reports/           # 批次報告與修訂提案
  extraction/      # 4 份抽取報告
  backfill/        # 4 份回填報告
inbox/             # 檢索原始回傳
```

## 工作流程

7 batches refcheck → 4 batches extraction → 4 batches backfill，每批一個 commit。

詳見 STATUS.md §2 的批次表。
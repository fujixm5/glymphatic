# Glymphatic — SCHEMA.md

版本: 1
適用: ledger/claims.csv（同 glycocalyx SCHEMA.md v9，但有 glymphatic 特定調整）

## §1 欄位定義

| 欄位 | 型別 | 規則 |
|------|------|------|
| claim_id | text | 永久性唯一識別碼，格式：`section-UID`。永不重用、永不改名（同 glycocalyx 鐵律）。建列時指定，之後不得更改 |
| section | text | 受控詞彙，取自 TOPICS.md（同 glycocalyx） |
| claim | text | 可獨立證偽的陳述句。不得包含時間形容詞（「最新」「目前」）或非指名的權威宣稱（「國際共識」→ 改為「未指名指引」） |
| claim_type | text | 受控詞彙：measurement / mechanism / causal / fact / comparison / clinical。定義見 §2 |
| tier | text | 判定證據等級：S / A / B / C / D / U。定義見 §3。不算反駁文獻（! 前綴）[同 glycocalyx v9] |
| status | text | 受控詞彙：unverified / verified / partial / unsupported / contested / superseded（同 glycocalyx v9） |
| source_ref | text | 受追蹤文件及段落，以分號分隔。格式：`source/glymphatic/original.md::{anchor}` |
| pmid_doi | text | PMID 或 DOI，以分號分隔。`!` = 反駁證據，`~` = 相關但非直接支持（同 glycocalyx v9）。不得憑記憶寫入——必須來自本次檢索回傳 |
| evidence | text | 支持性 evidence 出處（PMID/DOI），以分號分隔。同一前綴規則（同 glycocalyx v9） |
| note | text | 判定過程、限制條件、開放問題。寫下下一個人需要知道的事（同 glycocalyx v9） |
| priority | text | high / med / low |
| last_checked | text | ISO 8601 YYYY-MM-DD |

## §2 claim_type 值域

| 值 | 定義 | glymphatic 示例 |
|----|------|----------------|
| measurement | 可量測的數值主張 | 「睡眠期間組織間隙擴張 60%」 |
| mechanism | 因果或機制主張 | 「AQP4 極化分佈喪失導致 Aβ 清除效率下降」 |
| causal | 臨床因果關係 | 「嗅覺引流通路阻塞加速神經退化」 |
| fact | 事實性陳述（可對錯但不含數值） | 「腦膜淋巴管存在於硬腦膜中」 |
| comparison | 跨群體或跨條件比較 | 「ALS 的 DTI-ALPS 低於 PLS」 |
| clinical | 臨床應用或治療主張 | 「側臥位比仰臥位更有利於廢物清除」 |

## §3 tier（證據等級）定義

| tier | 定義 | 人體閘門 |
|------|------|---------|
| S | 來自人類的 RCT 或薈萃分析的直接證據 | 必須有 |
| A | 來自人類的觀察性研究／病例對照的證據 | 必須有 |
| B | 來自大型動物（非囓齒類）in vivo 證據，或人類 indirect evidence | — |
| C | 來自囓齒類 in vivo 證據 | — |
| D | 來自 in vitro、電腦模擬、或純理論推導 | — |
| U | 無法歸類 | — |

[同 glycocalyx v9]

人體閘門規則：epidemiology / therapeutic 主張在 in_vitro / animal-only 證據下不得 verified（同 glycocalyx v9 鐵律）。

## §4 欄位不可違反規則（同 glycocalyx）

1. 第一筆 PMID/DOI 對應到按引用順序的第一個 source_ref
2. 歸屬不同即為不同條：相同數值出現在不同章節/不同歸屬 → 各自建列
3. 數值必須逐字相符，不得換算、四捨五入或推估
4. 帳本不得刪除任何列。判定改變時新增列並標記取代關係

## §5 glymphatic 特有規則

5.1 引用驗證優先：refcheck 完成前不進行 claim 的 PubMed 回填（抽取可先做，但不判定 status）

5.2 claim 中的引用標號保留：若原文「…清除效率下降 60%^1」，claim statement 保留「^[ref:refcheck_id]」標記以便追溯。不得在 claim 中嵌入無法解析的引用數字

5.3 神經科學事實的 tier 判定：in vivo human imaging（MRI、PET、DTI-ALPS）為 tier A；rodent in vivo two-photon 為 tier C；post-mortem histology 為 tier B（人類樣本但非活體）

5.4 「共識」宣稱處理方式（同 glycocalyx v9）：凡宣稱「國際共識」而未指名具體學會或立場聲明 → claim 改寫為可指名的形式（例如「存在指引建議 X」，而非「國際共識認為 X」），查不到出處則 unsupported

## §6 已知問題與預防

- DTI-ALPS index 是 glymphatic 領域最常用的影像指標，但其敏感度和特異度仍在驗證中。凡 claim 以 DTI-ALPS 為唯一證據 → tier 上限為 B（非直接量測），除非有病理或生化證據佐證
- 睡眠-清醒的 CSF 流入差異（95%、60%）來自 rodent 研究 → tier C。不得因文獻被大量引用而升等為 tier A
- 「人類中證實」的 claim 需區分：in vivo imaging（tier A）、post-mortem histology（tier B）、CSF 生物標記（tier A 或 B 依實驗設計）

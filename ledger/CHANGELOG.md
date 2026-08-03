# claims.csv Schema 變更紀錄

依 `ledger/SCHEMA.md` §11：任何 schema 變更必須遞增 `schema_version`，並在本檔記錄變更內容與日期。

---

## schema_version 1 — 2026-08-03

glymphatic 專案從零開始建立的初版 schema。**不是** glycocalyx v9 的複製品，是針對 glymphatic 文件特性設計的新 schema。

### 設計原則

1. **功能相容（spirit-compatible）而非欄位相容（field-compatible）**：保留 glycocalyx 的核心鐵律（append-only、PMID 不可偽造、source 唯讀、claim_id 永生），但欄位命名與值域針對 glymphatic 重新設計
2. **神經科學領域特定規則**：DTI-ALPS 上限 B、人體閘門、AQP4 tier 指南等
3. **兩階段驗證**：refcheck（引用層）+ ledger（claim 層）獨立運作

### 與 glycocalyx v9 的差異

#### 欄位命名

| glycocalyx v9 | glymphatic v1 | 理由 |
|---|---|---|
| `statement` | `claim` | glymphatic 採用「claim」術語（更精準：claim = 可獨立證偽的聲明） |

#### claim_type 值域（六型 → 六型，但幾乎全換）

| glycocalyx v9 | glymphatic v1 | 理由 |
|---|---|---|
| `definition` | ❌ 移除 | glymphatic 內容多為敘述，無純定義 |
| `fact` | ✅ 保留 | 兩邊都需要 |
| `mechanism` | ✅ 保留 | 兩邊都需要 |
| `measurement` | ✅ 保留 | 兩邊都需要 |
| `epidemiology` | ❌ 移除 | glymphatic 文檔不含流行病學層級 |
| `therapeutic` | ❌ 移除 | 治療主張併入 `clinical` |
| ❌ 無 | `causal`（新增） | glymphatic 含多條臨床因果鏈條（CSM、ALS、SIH） |
| ❌ 無 | `comparison`（新增） | glymphatic 強調對比（腦 vs 脊髓、健康 vs 病理） |
| ❌ 無 | `clinical`（新增） | 取代 `therapeutic` + 加入臨床應用 |

#### tier 值域（重造）

| glycocalyx v9 | glymphatic v1 | 理由 |
|---|---|---|
| `in_vitro` / `animal` / `human_obs` / `rct` / `meta` / `review`（證據等級標籤） | ❌ 全部移除 | 體系不通用於 glymphatic |
| ❌ 無 | `S` / `A` / `B` / `C` / `D` / `U`（證據階梯） | 新設計：帶人體閘門 |
| — | 規則 | S/A 必須人體證據；DTI-ALPS 上限 B（間接量測）；mechanism 不受閘門約束 |

**這是最大的設計分歧**：glycocalyx 的 tier 是「文獻證據等級的標籤」，glymphatic 的 tier 是「claim 本身的證據等級判定」，後者含人體閘門與領域特定規則。

#### 欄位結構

| 欄位 | glycocalyx v9 | glymphatic v1 | 差異 |
|---|---|---|---|
| `pmid_doi` | 無獨立欄 | 獨立欄 | glymphatic 從 evidence 拆出 |
| `source_ref` 格式 | `{doc}#{section}` | `{path}::{anchor}` | glymphatic 用行號錨點 |
| `section` 來源 | TOPICS.md 正規主題樹 | TOPICS.md（直接抄 original.md 章節結構） | glymphatic 暫時簡化 |

#### section 處理

glymphatic 的 TOPICS.md 沒有像 glycocalyx 那樣建立跨文件正規主題樹（v9 的 `2.1.1-glycocalyx-thickness` 跨文件節點設計），而是直接抄 original.md 的章節結構。

理由：glymphatic 目前只有一個 source 文件（`source/glyphatic/original.md`），不需要跨文件座標。

若未來新增其他來源文件，應參考 glycocalyx v9 的正規主題樹設計擴充。

### 相容性邊界（明確聲明）

**精神相容**（保留）：
- ✅ Append-only：帳本不得刪除任何列
- ✅ PMID/DOI 只能來自本次檢索回傳
- ✅ source/ 唯讀
- ✅ claim_id 永生（永不重用、永不改名）
- ✅ 數值逐字相符，不得換算或推估
- ✅ unsupported 與 partial 是合格結果
- ✅ 一條主張，一列（不為文件而複製列）

**欄位不相容**（重造）：
- ❌ `statement` → `claim`（改名）
- ❌ claim_type 值域重造（4 型相同 + 2 型替換 + 2 型新增）
- ❌ tier 值域重造（完全不同體系）
- ❌ `pmid_doi` 拆出為獨立欄
- ❌ source_ref 錨點格式改為行號制

**結論**：glymphatic v1 與 glycocalyx v9 是**獨立 schema**，繼承相同的設計哲學但不互通資料。兩個專案的 ledger/claims.csv **不得直接合併**。

---

## 待辦：未來可能的 schema 變更

若 glymphatic 後續要與 glycocalyx 對齊（保留設計哲學 + 統一欄位），需要：
1. 決定是否將 `claim` 改回 `statement`（向後相容性 vs 當前清晰）
2. 統一 tier 值域（採 S/A/B/C/D/U 或 in_vitro/animal/etc）
3. 統一 source_ref 錨點格式（`{doc}#{section}` vs `{path}::{anchor}`）
4. 建立跨文件正規主題樹

但目前兩個專案的內容性質差異大（glycocalyx 是數值型任務、glymphatic 是敘述型任務），欄位統一的成本可能高於維持雙 schema。

---

## 待人工複核

無（本檔為 v1 設計記錄，無先前版本對比）
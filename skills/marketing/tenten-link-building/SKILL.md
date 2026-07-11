---
name: tenten-link-building
description: Automated internal link building for Tenten content via the Tenten Content Index MCP (index.tenten.dev). Use whenever writing or updating any Tenten article — tenten.co blog/learning/shopify/d2c posts, tentenai.com or geo.tenten.co pages — to insert internal links by querying the live database of 2,800+ published Tenten URLs (titles, keywords, GA4 traffic), and to submit the new URL back after publishing. Triggers - writing articles for tenten.co, internal linking, link building, cross-linking, 內部連結, 站內連結, 交叉連結, 發佈文章後提交索引.
---

# Tenten 內部連結(Internal Link Building)

寫 Tenten 文章時,用 Tenten Content Index 的線上資料庫查既有文章、依政策插入內部連結;
發佈後把新 URL 回填進資料庫。資料庫隨發佈自動更新——不要使用任何本地 CSV 或快照清單。

## 0. 前置檢查

確認 `tenten-index` MCP server 已連線(工具清單有 `search_content`)。沒有的話先設定:

```jsonc
// .mcp.json(Claude Code;金鑰向維運者索取,設在環境變數)
{
  "mcpServers": {
    "tenten-index": {
      "type": "http",
      "url": "https://index.tenten.dev/api/mcp",
      "headers": { "Authorization": "Bearer ${TENTEN_INDEX_API_KEY}" }
    }
  }
}
```

```toml
# ~/.codex/config.toml(Codex)
[mcp_servers.tenten_index]
url = "https://index.tenten.dev/api/mcp"
bearer_token_env_var = "TENTEN_INDEX_API_KEY"
```

其他平台(Claude Desktop、Hermes)的設定見 https://index.tenten.dev/mcp(需登入)。
**判準**:呼叫 `quota_report()` 回傳 JSON 即連線成功。

## 1. 工作流程

1. **草稿完成後才做連結**(不要邊寫邊查)。
2. 從內文挑 **5–8 個候選概念**:具體的產品名、技術名詞、主題詞(例:「Shopify 結帳優化」「AI agents」「棄購挽回信」)。挑文章核心主題,不挑泛用詞(「行銷」「網站」太泛)。
3. 每個概念呼叫一次 `search_content`:
   - `query` = 單一關鍵字或詞組,**用文章本身的語言**
   - `locale` 一律帶:中文文章 `"zh"`、英文文章 `"en"`
   - 空結果 → 換同義詞再查一次(例:「棄購」→「購物車」);仍空就放棄該概念,不硬湊
4. **挑選目標**:直接優先採用排名最高的結果——score 已含三層權重(GA4 流量 > 發佈日期 > 關鍵字關聯度),不要自行判斷熱門度或刻意挑舊文。唯一的人工判斷:讀 title/description 確認與該段落主題相關,明顯離題就往下看一名。
5. **插入連結**(政策見下):anchor text 用句子裡本來就有的詞組,不為塞關鍵字改寫句子;放正文段落內,不堆文末。
6. **發佈後**呼叫 `submit_url(published_url)` 回填——自動排入 Google/IndexNow 提交,下篇文章立刻搜得到它。
   **判準**:回傳 `created: true`(或已存在 `created: false` 也算完成)。

## 2. 連結政策(硬性規則)

| 規則 | 值 |
|------|-----|
| 每篇內部連結數 | 3–5 個;找不到好目標就更少,**寧缺勿濫** |
| 語言 | 只連同語言頁面(zh → zh,en → en) |
| 自連 | 禁止連文章自己的 URL |
| 重複 | 同一目標 URL 每篇最多 1 次 |
| Anchor | 自然融入句意;不可為了連結改寫句子 |
| 位置 | 正文段落內;禁止「延伸閱讀」式清單堆疊 |

## 3. 回應欄位速查

`search_content` 每筆回傳:`url`、`title`、`description`、`keywords`、`locale`、`channelKey`、`publishedAt`、`pageviews28d`(近 28 天瀏覽)、`score`。
score 為分層計分(流量層 ×10000 + 新鮮度 ×100 + 關聯度),**只用來排序,不要跨查詢比較絕對值**。

## 4. 錯誤處理

| 症狀 | 處理 |
|------|------|
| 401 Unauthorized | 金鑰缺失或錯誤;檢查 `TENTEN_INDEX_API_KEY` 環境變數與 `Bearer ` 前綴 |
| `search_content` 空陣列 | 換同義詞重查一次;仍空 → 放棄該概念 |
| `submit_url` 報 host 不在頻道清單 | 預期行為:索引池只收 Tenten 網域;非 Tenten URL 不要提交 |
| `submit_url` 回覆「excluded from Google (IndexNow only)」 | 預期行為:超過 6 個月的舊文不佔 Google 配額,不需處理 |

## 5. 範例

zh 草稿句:「…許多品牌透過**棄購挽回信**找回營收…」

1. `search_content({ query: "棄購挽回", locale: "zh" })` → 空
2. `search_content({ query: "購物車", locale: "zh" })` → 3 筆,第一名《Shopify 必學!降低購物車遺棄,大幅提升轉換率的方法》
3. 標題與段落主題相關 → 直接掛在原句詞組上:
   `許多品牌透過[棄購挽回信](https://tenten.co/d2c/reduce-shopify-shopping-cart-abandonment/)找回營收`
4. 文章發佈後:`submit_url({ url: "https://tenten.co/d2c/<new-post>/" })`

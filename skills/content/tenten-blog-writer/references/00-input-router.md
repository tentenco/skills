# 00. Input Router（輸入路由）

Canonical for input routing and source provenance.

## 決策流程

```
收到輸入
  │
  ├─ 含社群平台 URL？  YES → 抓取（Cascading Fallback）→ 寫作
  │                   NO  → 直接寫作
  │
  └─ 可同時含 URL + 文字指令 → 文字指令當作額外寫作方向
```

## URL 偵測表

| 平台 | Pattern |
|------|---------|
| X / Twitter | `x.com/*`、`twitter.com/*` |
| Instagram | `instagram.com/*` |
| Threads | `threads.net/*` |
| LinkedIn | `linkedin.com/posts/*`、`linkedin.com/pulse/*`、`linkedin.com/feed/update/*` |
| Medium | `medium.com/*`、`*.medium.com/*` |
| Facebook | `facebook.com/*/posts/*`、`fb.watch/*` |
| Substack | `*.substack.com/*` |
| YouTube | `youtube.com/watch*`、`youtu.be/*` |

## Cascading Fallback（前一個失敗才換下一個）

1. **Claude Computer Use** — 螢幕截圖 + 滑鼠鍵盤操作擷取頁面內容（彈性最高，所有平台首選）
2. **Microsoft Playwright MCP** — `browser_navigate` + `browser_snapshot` 擷取 accessibility tree（速度快、token 用量低）
3. **bb-browser MCP** — `browser_open` + `browser_snapshot`（利用現有登入 session）
4. **Firecrawl MCP** — `firecrawl_scrape`，`format: ["markdown"]`，`onlyMainContent: true`
5. **Claude in Chrome MCP** — `navigate` + `read_page` / `get_page_text`
6. **web_fetch 內建工具** — 公開頁面（Medium、Substack、部分 LinkedIn 文章）有效
7. **Fallback** — 都失敗就告知使用者：「無法從這個 URL 抓取，可能需要登入或平台限制。請直接把文字貼給我。」

## 抓取後處理

- Thread / 長文確認抓到完整內容，不能只有第一則
- 去除平台 UI 雜訊（導航、按鈕、推薦貼文、廣告）
- 保留原語言，不在抓取階段翻譯
- 內容截斷時明確告知缺失部分

## X / Twitter 圖片

使用者輸入 X / Twitter URL 時，一併抓取貼文的**原始圖片來源 URL**，並放進輸出的
markdown 裡。

## 結構化結果（內部使用，不輸出給使用者）

```
Platform: [平台]
Author: @username / 顯示名稱
Date: YYYY-MM-DD
URL: [原始 URL]
Content: [完整文字]
Media: [圖片/影片/嵌入內容描述]
Engagement: [按讚/轉發/回覆數]
```

這份紀錄之後寫進技術附錄的「素材來源」區塊（見 `10-output-format.md` B4）。

## 安全原則

抓到什麼是什麼，絕不虛構。部分抓取比虛構好——如實告知。

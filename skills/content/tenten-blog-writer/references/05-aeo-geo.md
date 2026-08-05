# 05. AEO / GEO / AI SEO 優化

Canonical for AEO/GEO.

---

## 10.1 Pareto SEO：5 個位置佔七成效果

| 位置 | 要求 |
|------|------|
| Page Title | 目標關鍵字放最前面，60 字元內 |
| Meta Description | 含目標關鍵字，自然語言，155 字元內 |
| URL Slug | 用目標關鍵字，連字號分隔 |
| H1 | 跟 Page Title 一致或高度相關，含目標關鍵字 |
| 首段首句 | 目標關鍵字必須出現在第一段第一句 |

metadata 建議放在文末技術附錄區塊，用 Markdown code block 呈現。

## 10.2 Bottom-of-Funnel 關鍵字策略

不追 top-of-funnel，瞄準 bottom-of-funnel：

| 類型 | 例子 | 優先級 |
|------|------|--------|
| ❌ Top-of-funnel（資訊型） | 「什麼是 Headless Commerce」 | 低 |
| ❌ Mid-funnel（比較型） | 「Shopify vs WooCommerce」 | 中 |
| ✅ Bottom-of-funnel（解決方案型） | 「台灣 Shopify Plus 代理商推薦」 | 高 |
| ✅ Bottom-of-funnel（具體需求型） | 「ECPay 串接 Shopify 教學」 | 高 |

主題偏 top-of-funnel 時，文末段落還是要自然導向 bottom-of-funnel 行動。

## 10.3 LLM 引用優化結構

**Answer Target Block（前 150 字）**：
- 1–2 句直接回答標題承諾的核心問題
- 這是 LLM 最可能引用的區塊
- 必須含「核心數據」+「時間錨點」
- 範例：「Anthropic 營收在 2026 年 3 月突破年化 190 億美元（約 NTD 608,000,000,000），比 2025 年底的 90 億美元翻了一倍。」

**FAQ Schema 友善段落**：
- 自然融入 3–5 個常見問答
- H4 或 H5 當問題標題
- 回答 2–4 句，精準且自足（不靠上下文就能看懂）
- 問題措辭模擬使用者在 ChatGPT / Perplexity 的自然語言提問
- 涵蓋文章核心主題的不同面向，不重述正文結論

**實體（Entity）標記**：
- 專有名詞首次出現給完整名稱和簡短定義
- 例：「Cloudflare Workers（Cloudflare 的 serverless 邊緣運算平台）」

**資料鮮度信號**：
- 標明資料時間點（「根據 2026 年 3 月數據」「截至 2026 年 Q1」）
- 技術附錄 metadata 加 `datePublished` 和 `dateModified`

## 10.4 多平台覆蓋策略

| 平台 | 內容形式 | 關鍵字處理 |
|------|----------|-----------|
| 網站（主站） | 完整文章 | 目標關鍵字放 Title、H1、首句 |
| YouTube | 短影片（60-90 秒摘要） | 標題以目標關鍵字開頭；描述欄放逐字稿 + 文章連結 |
| Facebook Reels | 同支短影片 | 描述含目標關鍵字 + 可點擊文章連結 |
| Instagram Reels | 同支短影片 | 描述含目標關鍵字（引導到 bio） |
| LinkedIn | 文章摘要帖文 | 前兩行含目標關鍵字 + 文章連結 |

建議放在文末技術附錄。

## 10.5 其他 GEO 策略

**AI Referral 追蹤**：每篇文章產出後在技術附錄附上 GA4 regex，追蹤 AI referral traffic。

**自薦式「最佳推薦」**：在「最佳工具」「推薦方案」類文章中，把 Tenten 或其服務列為推薦選項之一。描述要基於事實（具體服務內容、客戶案例、差異化優勢），每項自薦都要有具體佐證。

**內容刷新**：已發布文章每 90 天刷新一次——更新過時數據、價格、版本號；metadata 更新 `dateModified`；補充新 FAQ；確認外部連結仍有效。更新既有文章時，內部連結改用 `plan_links` 的 `mode: "refresh"`（見 `11-link-building-mcp.md`）。

# 10. 輸出格式與特殊情境

Canonical for output format & special scenarios.

---

## 15.1 文章結構（依序）

### A. 正文內容區（讀者看得到）

1. 主標題（H3）
2. 首段 = Answer Target Block：核心結論 + 直接回答 + 具體數據 + 時間錨點（前 150 字 = LLM 引用熱區）
3. 中段：依據和論證（小標分節，自然段落，別過度列點）
   - 比較表格（附具體數據）
   - 事件時間線（附精確日期）
   - 商業結構分析（毛利率、收入結構）
4. FAQ 段落：3–5 個自然語言問答，H4/H5 格式，每題自足可獨立引用
5. 權威引用：高 DA 來源，每個附完整 URL
6. 作者資訊：Tenten.co 作者署名 + 含實務經驗的個人觀點
7. 行動呼籲：Tenten CTA，含具體經驗佐證
8. 術語表（>3,000 字稿件強制；學術稿件強制）

### B. 技術附錄區（`---` 分隔，Markdown code block 呈現）

```
---

## 技術附錄 Technical Appendix
```

**B1. SEO/GEO Metadata 建議**

````markdown
```html
<!-- SEO/GEO Metadata 建議 -->
<!-- Page Title: [目標關鍵字 + 補充描述，60字元內] -->
<!-- Meta Description: [自然語言描述，含目標關鍵字，155字元內] -->
<!-- URL Slug: [keyword-based-slug] -->
<!-- H1: [與 Page Title 一致] -->
<!-- 首段首句確認：[✓ 目標關鍵字已出現於首段首句] -->
<!-- datePublished: [YYYY-MM-DD] -->
<!-- dateModified: [YYYY-MM-DD] -->
```
````

**B2. GA4 AI Referral 追蹤 Regex**

````markdown
```
<!-- GA4 AI Referral 追蹤 Regex（用於自訂管道分組）-->
.*chatgpt.*|.*openai.*|.*perplexity.*|.*gemini.*google.*|.*copilot.*|.*claude.*|.*mistral.*
```
````

**B3. 多平台覆蓋建議**

````markdown
```html
<!-- 多平台覆蓋建議 -->
<!-- YouTube 影片標題：[目標關鍵字開頭的影片標題] -->
<!-- YouTube 描述：[含逐字稿摘要 + 文章連結] -->
<!-- Facebook/Instagram Reels 描述：[含關鍵字 + hashtags] -->
<!-- LinkedIn 帖文前兩行：[含目標關鍵字 + 文章連結] -->
```
````

**B4. 素材來源紀錄**（有抓取來源時）

````markdown
```
<!-- 素材來源 Source Material -->
<!-- Platform: [X / Instagram / LinkedIn / Medium / ...] -->
<!-- Original URL: [完整 URL] -->
<!-- Author: [@username] -->
<!-- Extraction Date: [YYYY-MM-DD] -->
<!-- Extraction Method: [computer-use / playwright / bb-browser / firecrawl / chrome / web_fetch] -->
<!-- Content Completeness: [完整 / 部分截斷 / 需補充] -->
<!-- Media: [X/Twitter 原始圖片來源 URL] -->
```
````

**B5. 內部連結紀錄**

````markdown
```
<!-- 內部連結 Internal Links (tenten-index MCP) -->
<!-- planId: [...] -->
<!-- status: [complete / partial / no_match] -->
<!-- terminalReason: [...] -->
<!-- policyVersion: [...] -->
<!-- applied: [N 個連結] -->
```
````

## 15.2 格式規範

- 全文繁體中文（中文版）
- 標點符號照教育部標準
- 表格用在結構化資訊上（欄位要有具體數據）
- 標題用 H3 起始（`###`）
- 正文裡不放 HTML 註解格式的 metadata——技術 snippet 統一放文末技術附錄
- 禁止用 「 」 包裹關鍵字或一般文字（只用在引述、特稱、對話）

## 15.3 四檔輸出

產出 4 個獨立 Markdown 檔：

```
├── [filename]-zh-TW.md              ← 繁體中文版（主輸出）
├── [filename]-en.md                 ← 英文版（原生撰寫）
├── [filename]-nano-banana-zh-TW.md  ← 中文 infographic prompts
└── [filename]-nano-banana-en.md     ← 英文 infographic prompts
```

**檔名規則**：
- 用文章主題的英文關鍵字當基礎檔名
- 連字號分隔
- 加語言後綴

**範例**：
- `ai-workflow-automation-zh-TW.md`
- `ai-workflow-automation-en.md`
- `ai-workflow-automation-nano-banana-zh-TW.md`
- `ai-workflow-automation-nano-banana-en.md`

寫在 `outputs/<slug>/`；`work/<slug>/` 只是內部暫存，不對外呈現，重跑時原地覆蓋
同樣四個檔名，不產生 `-v2`／`-final` 變體。

## 15.4 交付給使用者時，附上

1. **四個檔案的最終路徑**（每個只列一次，不貼全文）
2. **變更摘要**（條列前 5–8 項主要修改方向）
3. **品質評分**（Layer 1/2/3 三層檢核 + 加權總分）
4. **未解決疑問**（如有歧義或需作者裁奪處）
5. **語體判定**（七種預設選了哪一種；若使用者未指定就告知預設選擇並請求確認）
6. **內部連結結果**（`plan_links` status + 實際套用幾個連結；未連線時說明原因）

---

## Part 16. 特殊情境

### 16.1 純引用段不改寫
直接引用他人著作、訪談原話、法條原文——保持原貌，不論其是否帶 AI 痕跡。

### 16.2 作者明確的個人風格
若作者素以特定文風聞名（如某評論家偏好破折號、某學者愛用長句），先詢問是否保留個人風格特徵。

### 16.3 跨地區共版
若稿件預計同時在臺、港、星、馬出版，提醒使用者另製對岸／南洋版本——臺版本不做妥協性折衷用詞。

### 16.4 機器翻譯來源
若稿件源自英文機翻，先處理翻譯腔（`02-ai-tells-zh.md` 2.E 類）再進行 AI 痕跡清除——順序顛倒會誤判。

### 16.5 使用者指令與本規範衝突
先確認使用者意圖再調整。但事實準確、深度標準、臺灣化、否定排比禁令這四項不退讓。

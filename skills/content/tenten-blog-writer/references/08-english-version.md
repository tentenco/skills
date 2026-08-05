# 08. 英文版原生撰寫規範

Canonical for English standards.

---

## 13.1 核心原則

**目標市場**：Global audience with a US-primary lens. Write from an American
reader's perspective — their references, their market, their regulatory context.

**絕對禁止**：
- 翻譯中文版。英文版從同一素材起手，有自己的結構、論證順序、案例
- 保留中文句法——長串從屬子句、堆疊被動、主題-評論結構都是翻譯味
- 段對段對照。自由重組

**核心要求**：
1. **原生思考**：用美式英文母語者的思考順序——SVO、先講重點、後加限定
2. **獨立架構**：從素材提取核心論點和證據，用英文重建
3. **US 市場適配**：案例、數據來源、法規、文化參照全換成美國版
4. **一致語域**：專業但有節奏，contractions 和第一人稱都 OK
5. **同等深度**：英文版數據密度和分析深度必須不低於中文版

## 13.2 Tier 1 絕對禁用詞（零容忍）

These words trigger immediate AI suspicion. **Never use, no exceptions.**

- "delve" / "delve into" / "delving"
- "tapestry" (figurative)
- "landscape" (figurative)
- "multifaceted"
- "it's important to note that" / "it's worth noting that"
- "in today's rapidly evolving [anything]"
- "let's unpack this"
- "a testament to"
- "navigating the complexities of"
- "at its core"
- "game-changer" / "game-changing"
- "let's dive in" / "without further ado"
- "only time will tell"
- "the future remains to be seen"
- "in the world of..." / "in the realm of..."

## 13.3 Tier 2 受限詞（僅限技術/字面義）

- "robust"（只用在工程語境，不當通用讚美）
- "holistic approach"
- "leverage" 當動詞（用 "use" 或更具體的動詞）
- "ecosystem"（只用在生物學，不當商業比喻）
- "spearhead" / "bolster" / "foster"
- "resonate with"
- "embark on a journey"
- "shed light on"
- "the intersection of X and Y"
- "paradigm shift"
- "nuanced"（當讚美用時禁止）
- "synergy"
- "seamless"
- "comprehensive"（當通用讚美禁止，描述實際範圍 OK）

## 13.4 Tier 3 結構禁令

- "Whether you're a [X] or a [Y]..." 偽包容性句式
- 段落開頭 "Interestingly,"、"Notably,"、"Importantly,"
- "Furthermore,"、"Moreover,"、"Additionally," 當段落開頭（全文合計 ≤1 次）
- "In order to" → 用 "to"
- "Due to the fact that" → 用 "because"
- "At this point in time" → 用 "now"
- "Has the ability to" → 用 "can"
- "When it comes to" → 刪除或重寫
- "In light of the fact that" → 用 "because" / "since"
- "The aforementioned"

## 13.5 硬上限（全文計）

| Pattern | Cap | Rule |
|---------|-----|------|
| Em-dash (—) | 3 per article | 只用在 genuine parenthetical inserts 或 abrupt pivots。不用做戲劇化揭露。一句不得兩個。 |
| Rule of three | 2 per article | 三項各自必須有明確、具體意義。禁止 "innovation, inspiration, and industry insights" 型空三聯。 |
| Negation parallelism | **0 — 完全禁止** | 改成正向陳述。 |
| Rhetorical questions | 1 per article | 後面必須立刻接具體答案+數據。 |

## 13.6 九類結構 AI Tells

**1. Inflated significance**
- ❌ "The Inflation Reduction Act stands as a pivotal moment in America's evolving energy landscape..."
- ✅ "The Inflation Reduction Act allocated $369 billion to energy and climate programs — the largest climate spending bill Congress has passed."

**2. Shallow -ing phrase analysis**
- ❌ "The platform saw 40% user growth, highlighting its strong product-market fit and underscoring the team's commitment to innovation."
- ✅ "The platform grew 40% year-over-year. Most new users came through referrals, which kept acquisition costs under $12 per user."

**3. Promotional / travel-brochure tone**
- ❌ "Nestled in the heart of Silicon Valley, this world-class startup boasts a vibrant culture..."
- ✅ "The company is based in Palo Alto and has 180 employees. It raised a $45M Series B in January 2026."

**4. Copula avoidance**
- ❌ "The product serves as the company's flagship offering, representing a new approach..."
- ✅ "It's the company's main product. It takes a different approach to enterprise security by..."

**5. Vague attribution**
- ❌ "Industry experts believe this will reshape the sector."
- ✅ "Gartner's 2026 forecast projects 35% CAGR for the sector through 2029."

**6. Boilerplate challenges-and-outlook**
- ❌ "Despite these challenges, with its strategic positioning and ongoing initiatives, the company continues to thrive..."
- ✅ "Between 2024 and 2026, the company's CAC rose 28% while LTV stayed flat. Management plans to offset this by shifting 40% of acquisition spend to partner channels by Q3 2026."

**7. Synonym rotation**
- ❌ "The CEO discussed the initiative. The tech executive outlined the program. The company leader detailed the strategic undertaking."
- ✅ "CEO Jane Park laid out a three-phase plan to..."

**8. Bold overuse**
規則：粗體只用在首次定義的術語，或表格標題。running text 的強調不用粗體。

**9. Inline-header bullet lists**
- ❌ "- **User Experience:** ...\n- **Performance:** ...\n- **Security:** ..."
- ✅ "The update improves navigation, cuts load times by 40%, and adds end-to-end encryption."

Prose 是預設。List 是最後選項，只給真正平行、可掃讀的項目。

## 13.7 Voice Check（靈魂檢核）

**Signs of soulless writing**:
- 每句長度和結構都差不多
- 整篇中立報導，沒觀點
- 從不承認不確定或混合感受
- 自然該用第一人稱的地方不用
- 反應缺乏具體性（"interesting"、"notable"）
- 讀起來像 Wikipedia stub

**How to add life**:
1. **Have an opinion.** React to data, don't just report it.
2. **Vary the pace.** Short sentences. Then a longer one that builds.
3. **Acknowledge complexity.** "Revenue growth is impressive, but margin compression is harder to explain away."
4. **Use "I" / "we" when appropriate.** 產業分析第一人稱不是不專業，是誠實。
5. **Be specific about reactions.** Not "this is concerning" but "the 18-month contract lock-in with no early termination — that's the part I'd push back on."
6. **Allow asymmetry.** 不是每節都要結論整齊。

**Before (clean but dead)**:
> The company reported strong Q4 results. Revenue increased 32% year-over-year. Several analysts noted the performance exceeded expectations.

**After (alive)**:
> Q4 revenue hit $2.1 billion, up 32% from last year. That beat every major analyst estimate — Morgan Stanley had it at $1.85 billion. Enterprise contracts drove most of the upside: customers spending over $1M/year went from 340 to 510 in a single quarter. Consumer revenue barely moved. That gap is going to matter.

## 13.8 替代模式對照表

| Instinct | Replacement |
|----------|-------------|
| "This isn't just X — it's Y" | State Y directly. |
| Three-item list for impact | Pick the strongest; drop others. |
| Rhetorical question | Direct statement + evidence. |
| Em-dash for drama | Period + new sentence. |
| "Research shows" / "experts say" | "[Source] found [result] in [year]." Or delete. |
| "Robust" / "comprehensive" / "holistic" | Say what it does: "covers 14 API endpoints." |
| "Landscape" / "ecosystem" | Name the space: "the enterprise AI tools market." |
| Qualitative ("stronger") | Quantitative: numbers, percentages. |
| Boilerplate outlook | Next concrete step. |

## 13.9 US 本地化

| 內容類型 | 處理方式 |
|---|---|
| 數據 | 優先用 US 來源（Pew, BLS, Gartner, Forrester, CB Insights） |
| 案例 | 領先 US 公司（Walmart, JPMorgan, Stripe）；亞洲案例降為「international perspective」或刪 |
| 法規 | 美國法規（FTC, SEC, state privacy laws）；跳過台灣法規（除非是台灣市場主題） |
| 貨幣 | USD only。格式：$10,000 |
| 市場趨勢 | US 為主框架；亞洲為「global context」 |
| 文化參照 | Black Friday, Super Bowl, March Madness, Silicon Valley, YC Demo Day |
| 日期 | March 17, 2026（不是 17 March 2026）；時區：ET/PT |

**觀點切換**：

| 中文版 | 英文版 |
|---|---|
| 「台灣企業應該...」 | "US companies can..." |
| 「亞洲市場趨勢顯示...」 | "Global trends, particularly visible in Asia, suggest..."（支撐證據，不是主論） |
| 「根據台灣法規...」 | 刪除或泛化：「In regulated industries...」 |
| 「新台幣 X 元」 | 轉成 USD |
| 「台灣消費者偏好...」 | 換成 US 消費者數據，或框為 global observation |

## 13.10 英文版品質度量

| Metric | Target |
|---|---|
| Flesch Reading Ease | 50–60 |
| Average sentence length | 15–20 words |
| Max sentence length | 35 words |
| Paragraph length | 3–5 sentences |
| Active voice | ≥80% |
| Em-dashes | ≤3 |
| Rule-of-three | ≤2 |
| "Furthermore/Moreover/Additionally" as opener | ≤1 total |
| Negation parallelism | 0 |
| Tier 1 banned words | 0 |

## 13.11 英文版八維度計分（<7 重寫該維度；<35 全篇重寫）

| Dimension | Weight |
|---|---|
| Directness（每段 front-load 重點） | 15% |
| Data density（≥5 數據點、具名來源、精確日期） | 20% |
| Pattern compliance（零 Tier 1、硬上限、結構禁令） | 10% |
| Rhythm and variety（句長、段長多變） | 10% |
| Voice and authenticity（像真人分析師寫的） | 15% |
| Trust（不解釋過度、不 hand-holding、無 filler） | 10% |
| Concision（能砍就砍） | 10% |
| AEO/GEO（Answer Target Block、FAQ、Entity、技術附錄） | 10% |

**閾值**：45–50 出稿；35–44 修弱項；<35 重寫。

## 13.12 英文版處理流程

1. 中文版完成後
2. 提取核心論點、關鍵數據、主要結論
3. 用英文讀者邏輯重新組織架構
4. 原生撰寫，不參照中文句子結構
5. Pattern check：Tier 1/2/3 禁用詞 + 九類結構禁令
6. Voice check：有觀點？有人味？不是中立報導體？
7. AEO/GEO 獨立撰寫技術附錄
8. 深度對齊：數據量和分析深度不低於中文版
9. 跑八維度計分表
10. 內部連結：對完成的英文草稿呼叫 `plan_links`（`locale: "en"`）一次，見 `11-link-building-mcp.md`
11. 獨立依英文品質標準審查

## 13.13 英文 CTA 範例

Match US business writing register — direct, specific, no corporate warmth padding.

> "Our team recently helped financial services and manufacturing clients run Claude Code vs. GitHub Copilot pilots, measuring 20–40% efficiency gains across four deployment scenarios. [Schedule a consultation](https://tenten.co/contact) with Tenten to figure out what fits your stack."

# Deliverables — Templates & Design Discipline

Two files + one chat summary, all in the user's language (zh-TW when the user writes Chinese). The strategy doc is the working artifact (versionable, feeds the build); the HTML is the review surface (readable, signable, shareable internally).

---

## 1. `GTM-STRATEGY.md` (project root)

The founding document. Use this exact section skeleton, filling from the audit record:

```markdown
# <Brand> — Go-To-Market Strategy(創始文件)
v1.0 · <date> · 依 go-to-market-audit <N> 站定案產出
北極星:<north star from Station 1>

## 0. 一頁摘要         ← one table: 產品/商業模式/買家/灘頭堡/定價/交付/建置/停損/歸屬
## 1. 品牌 Branding    ← 名稱定位、tagline 定稿+備選(雙語)、品牌聲音(禁用詞/常用詞)、視覺方向
## 2. 網域             ← 主站/防守/私密交付/email,含每項的狀態與動作
## 3. 費用與定價策略    ← 錨定敘事、SKU 表(價格/內容/角色)、機制(折抵/保證/心理)、單位經濟
## 4. 行銷文案         ← beachhead 語言 landing 全稿(§1 Hero…§8 收尾),次要語言 hero 核心字串
## 5. 整體行銷推廣策略   ← 通路原則、逐週計畫表(W0-W4)、購後升級信序列表、內容日曆、KPI 表、風險對策表
## 6. Phase 1 技術規格  ← stack、訂單流、資產改版清單;Phase 2 範圍與觸發條件
## 7. <N> 天決策樹      ← code block 樹狀:達標/部分達標/未達標/兩輪失敗 各自的下一步
```

Rules: real numbers everywhere (COGS, margins, targets); estimates labeled as estimates; the landing copy must be paste-ready, not an outline; every table renders in GitHub markdown.

## 2. `<Brand>-GTM-Plan-Review-<YYYY-MM-DD>.html`

A self-contained review document. It has two jobs: let the owner *review and veto* decisions quickly, and demonstrate the brand's visual bar (it is the brand's first dogfood — style it with the brand's own accent color chosen at Station 9/visual direction).

### Required content sections

1. **Masthead** — brand eyebrow, title, one-paragraph scope, meta chips (version/date/狀態:待 Review/key completed facts), 4 stat tiles (price, margin, delivery promise, kill criteria).
2. **戰略定調** — the 2-3 biggest pivots as cards: ~~original assumption~~ → audited decision, with the why.
3. **決策全紀錄** — one table: every station → 定案 / 關鍵理由 / **被否決的選項**(the future pivot list; never omit this column).
4. **品牌 / 網域 / 定價** — tagline table, domain status table, 3 SKU pricing cards (middle one highlighted 主推; anything beyond audited consensus tagged 延伸建議).
5. **Landing 文案** — each copy section rendered inside a browser-frame mockup block (the hero should *look* like a hero, not a quote).
6. **推廣策略** — vertical week timeline, post-purchase email sequence table, KPI stat tiles, risk/response table.
7. **技術規格** — Phase 1 stack + order flow + asset-modification list; Phase 2 scope + trigger.
8. **決策樹** — styled tree (root box + branch list), not raw ASCII.
9. **行動與待簽核** — two checklists: W0 action list (done items pre-checked), and the **sign-off checklist**: every consequential decision the user hasn't explicitly confirmed, each with a one-line "why this needs your signature". In express mode this checklist is the primary control surface — it must be complete.
10. **REVIEW callouts** — at each contentious point in the flow, a highlighted box ("REVIEW 重點") telling the reviewer exactly what to check and what changes if they disagree.

### Design discipline (non-negotiable)

- Self-contained: zero external requests (no CDN fonts/scripts). System font stack + Noto Sans TC/PingFang TC fallbacks.
- One accent color + neutral grays on paper white. No gradients-rainbow AI slop. WCAG AA contrast.
- `<meta name="robots" content="noindex">`; `lang` set to the document language.
- Layout variety: stat tiles, cards, tables, timeline, tree — not ten identical tables.
- Sticky left TOC with scrollspy on wide screens; single column under 960px; horizontal scroll only inside table wrappers, never the body.
- Reveal-on-scroll via IntersectionObserver with a `prefers-reduced-motion` guard; print stylesheet (TOC hidden, sections unbroken).
- Chinese typography: line-height ≥1.8 body, tabular numerals for all figures.

## 3. Chat summary (the final message)

Lead with the verdict: "你的想法活下來了,但被改了 N 個地方" + the pivots in one line each. Then: where both files are, the sign-off items in one breath, and the single most time-sensitive action (usually: register the domain today — it's the only step someone else can take from you overnight). Close with the next step ("review 完回覆修改點或『全數通過』,即開工 Phase 1").

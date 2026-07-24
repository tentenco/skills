# The 12 Audit Stations — Full Playbook

Each station below gives: **Purpose**, **Interrogate** (the lines of questioning), **Heuristics** (how to form the recommended answer), and **Traps** (the failure patterns this station exists to catch). In interactive mode each station is one AskUserQuestion; in express mode you adopt the heuristic answer and log it.

The stations inherit: a Station 1 answer of "funnel" changes what "success" means at Stations 5, 7, and 10. Always restate the inherited constraint when it drives a later decision ("Q1 已定調北極星是服務約,所以…").

---

## Station 1 · 成功定義 / 戰略角色

**Purpose.** Define what job this business is doing before designing anything. Every downstream decision (pricing, brand, CTA, channels) forks on this.

**Interrogate.**
- Does the operator already own a business this product could feed (agency, consultancy, SaaS)? Then "standalone revenue" vs "qualified-lead funnel" are *different products* wearing the same skin.
- If the asset's DNA is free/lead-gen (Phase 0), charging money inverts its physics: free maximizes reach, paid maximizes signal but cuts volume 95%+. Which does the operator actually need?
- What would success look like in 12 months, in one number?

**Heuristics.**
- One-time-purchase digital products almost never support standalone paid acquisition (CAC > price). If a services back-end exists with LTV 20-100× the product price, recommend **self-liquidating funnel**: charge (payment = strongest qualification filter), but the north star is downstream conversions, not product MRR.
- Funnel choice has two immediate consequences to state: (a) no parent-brand ads inside the paid deliverable — a customer who paid for neutral analysis must not find your agency's CTA in it; upsell moves to the post-purchase flow; (b) price optimizes for signal, not revenue.
- Include "keep it free / don't monetize" as a real option whenever the evidence supports it. Challenging the premise is the audit's license to exist.

**Traps.** Choosing "both" (revenue AND funnel) without naming the primary — every later trade-off becomes undecidable.

---

## Station 2 · 主要買家 ICP

**Purpose.** Replace the aspirational audience with the evidence-backed buyer.

**Interrogate.**
- The stated audience is usually a title fantasy ("CMOs"). Who does the *evidence* say used or wanted this? (Phase 0: whose problem did the asset actually solve, even internally?)
- Who feels the pain with highest value density? Sophisticated buyers (real CMOs, senior engineers) have internal data/tools/budgets — an outside-in product is "a summary of known things" to them, and they are best equipped to spot its errors.
- If Station 1 chose funnel: the ICP must be someone the back-end business can serve and close. A buyer segment that pays for the product but can never become a service client scores zero on the north star (they may still be a secondary revenue line — record that explicitly).

**Heuristics.**
- The best ICP for diagnostic/advisory products is usually **the decision-maker without the internal function** (founder/GM without a marketing team, non-technical owner without a CTO): highest value density, lowest ability to DIY, natural service prospect.
- Keep the aspirational title as *marketing language* ("像雇了一位 CMO"), not as the buyer definition.

**Traps.** Confusing the subject of the deliverable with the buyer (reports *about* companies can be bought by the company, by its competitors, or by agencies prospecting it — three different businesses).

---

## Station 3 · 灘頭堡市場

**Purpose.** Concentrate GTM firepower in one market. Product language support is cheap; go-to-market attention is not.

**Interrogate.**
- Where can the operator's existing distribution and sales motion actually absorb the demand created? (Timezone, sales language, delivery capacity.)
- "Bilingual UI from day 1" is a product decision, not a GTM decision — supporting two languages is fine; *marketing to two markets* is two full GTM programs.

**Heuristics.**
- Default: the market where existing audience + sales motion live gets ~90% of launch firepower; the other language market gets passive SEO presence until validated.
- If Station 1 chose funnel: follow the serviceable market, even if the other market has higher willingness to pay — leads the back-end can't serve are worth zero.

**Traps.** "Global from day 1" with a team of one or two — both markets get a shallow effort and neither converts.

---

## Station 4 · 交付模式與信任設計

**Purpose.** Decide how quality is guaranteed before the first bad unit ships.

**Interrogate.**
- For AI-generated deliverables: a unit makes hundreds of factual claims; at realistic per-claim accuracy, **every unit ships with at least one error**. A paying customer who finds one error about their own company zeroes trust in the whole deliverable, demands a refund, and tells their circle. Small markets amplify this.
- What claim is marketing making ("equivalent to 20-year expert + weeks of work")? Can the honest product ("outside-in analysis from public data") carry it? Reframe the limitation as the positioning: the outside view is the thing the internal team *cannot* do.

**Heuristics.**
- At funnel volumes (tens of units/month), recommend **hybrid**: AI generation + 15-30 min human QA + a signed reviewer's note before delivery. Three birds: kills the hallucination risk, the QA person doubles as the SDR, and the note is the first sales touchpoint. Cost: delivery promise moves from minutes to "within 24h" — acceptable, often premium-feeling.
- Always recommend an unconditional refund window when COGS is low. Refund requests are cheap quality telemetry; "no refunds on digital goods" kills conversion for an unknown brand.

**Traps.** Promising literal expert-equivalence in copy; pure self-serve at launch in a market where word-of-mouth is the main channel.

---

## Station 5 · 定價帶

**Purpose.** Set price from the COGS floor and the strategic role, not from vibes.

**Interrogate.**
- State the COGS floor computed in Phase 0 (inference + human minutes). Any price where gross margin < ~60% is a retail business wearing SaaS clothes.
- If Station 1 chose funnel: price is a **qualification filter**. Too cheap attracts curiosity buyers (noise against the north star) and cheapens the perceived depth; too expensive becomes a considered purchase needing sales involvement.
- What is the anchor? There is almost always a human-service alternative ("顧問健檢 NT$60,000 起、等三週") — price against it, not against other tools.

**Heuristics.**
- Sweet spot for a funnel-qualifier sold to founders/SMB decision-makers: roughly the price of a business dinner to a nice suit (NT$2,000-5,000 / US$60-160) — impulse-capable for a serious buyer, absurd for a tourist.
- Structure as 3 SKUs: entry unit / bundle built from the **historically-validated use case** as the "most popular" middle (e.g., +competitor reports if the asset's proven usage was competitive research) / a high anchor that productizes the north-star action itself (report + consult call). Flag any SKU not covered by the audit as 延伸建議 in the sign-off list.
- Launch pricing: limited-quantity founder price (numbered units) beats time-limited discounts — scarcity with a receipt.
- Mechanisms worth testing: opt-in "make my report public for a discount" turns buyers into content producers.

**Traps.** Pricing below the human-cost floor of a hybrid delivery model; "small fee" framing in the idea colliding with a COGS the user never computed.

---

## Station 6 · 建置順序

**Purpose.** Strip the build to what must exist before the first dollar of validated demand.

**Interrogate.**
- Walk the user's own spec list (accounts, history, admin, automation, i18n) and ask of each: does this matter before order #1? Accounts/history only matter on *repeat* purchase; an admin dashboard below ~50 orders/month is the Stripe dashboard; if Station 4 chose hybrid, a human is already in the loop — automation isn't the bottleneck.
- The riskiest unknown is almost never engineering; it's "will anyone pay". Every week of building before learning that is burn.

**Heuristics.**
- Recommend **two phases**: Phase 1 concierge (~1 week: polished landing + Stripe Checkout + intake form + manual fulfillment with existing tooling + email delivery of a permanent private link) — buyer experience identical to full automation; Phase 2 (accounts, pipeline, admin) gated on a threshold of paid orders (typically 10).
- Frame it kindly: the user's full SaaS spec is the *destination*, not the starting line.
- Intake form: always include one optional free-text field ("你最想解決的問題") — one line of buyer context disproportionately improves the deliverable.

**Traps.** "It's only 2-3 weeks with AI coding" — the cost isn't the weeks, it's the zero market signal during them, and the sunk infrastructure if positioning pivots.

---

## Station 7 · GTM 通路

**Purpose.** Choose launch channels by trust-transfer per dollar, and gate paid spend on data.

**Interrogate.**
- What audiences does the operator already own (newsletter, client list, social following, existing site traffic)? Highest trust transfer, zero cost — that's the launch vehicle.
- Can the product's own output be the content ammunition? (Publish sample units about famous companies: demo + shareable content + SEO page in one. Pick subjects that are the ICP's "neighbors" — same industry/size, so the reader thinks "那我的呢?")
- Paid ads: without funnel conversion data there is no CAC ceiling, so spend is blind. If Station 1 chose funnel, the affordable CAC depends on product→consult→contract conversion — unknowable at launch.

**Heuristics.**
- Default launch stack: (1) owned audiences with a limited founder offer, (2) founder-led posting with weekly public sample units, (3) relevant communities with samples, not hard ads. Gate paid ads on ≥20 orders *and* a measured downstream conversion rate.
- Weekly sample cadence is the minimum firepower floor after launch week — momentum dies without it.

**Traps.** Launching with ads because organic feels slow; publishing critiques of named companies without a takedown policy (pair with Station 8).

---

## Station 8 · 隱藏地雷(Asset-DNA conflicts)

**Purpose.** Defuse the conflicts found in Phase 0 between what the asset was built to be and what the paid product must be.

**Interrogate — the recurring ones.**
- **Privacy default.** Lead-magnet assets are public/indexable by design; a paid customer's weakness analysis must be private by default (unguessable URL + noindex; accounts later). Public SEO ammo comes from self-produced samples instead, or an opt-in discount.
- **Embedded CTAs / branding.** Parent-brand links inside the paid deliverable → remove; move upsell to the post-purchase flow (Station 1 consequence).
- **Data/licensing.** Scraped content, third-party datasets, "commonly known" numbers — does the paid context change what's defensible?
- **Naming named companies.** Public sample reports critiquing real companies: facts-only, criticize the work not the people, and a 24h takedown policy for objections.

**Heuristics.** Whatever the conflict, the pattern is the same: the free version's strength is usually the paid version's liability. Flip the default and design the exception (e.g., opt-in public for a discount).

---

## Station 9 · 品牌與網域

**Purpose.** Name the thing, secure the domain — with evidence, same day.

**Interrogate.**
- Does internal brand equity already exist (a working name on N artifacts, dashboards, team vocabulary)? Starting from zero resets that asset.
- Does the name carry the promise, survive spoken use in both product languages, and imply the category?

**Heuristics.**
- Check every candidate with `dig +short NS <domain>` *before* proposing it; report "查無 NS 紀錄(很可能未註冊)" — likely, not guaranteed. Recommend registering the primary + one defensive TLD immediately (the only step of the whole plan someone else can take from you overnight).
- Prefer the existing internal name unless it actively fights the positioning. Slight datedness in a secondary market's ears is acceptable; brand-asset continuity usually wins.
- Pair the name with a category subtitle in the beachhead language ("MegaCMO|AI 行銷診斷" pattern).

---

## Station 10 · 驗證停損線

**Purpose.** Give the project a way to die. Projects without kill criteria zombify and eat the team's attention indefinitely.

**Interrogate.**
- Time box + demand metric + **north-star action metric**. If Station 1 chose funnel, orders alone are not success: 10 orders and 0 consults = the engine failed, you just sold some units.
- What exactly happens at each failure mode?

**Heuristics.** Recommend a 30-day box with a two-metric bar (e.g., ≥10 paid orders AND ≥3 downstream actions) and a pivot ladder: metric A hit but B zero → fix the post-purchase flow, retest; A missed → pivot message/price, one more 30-day round; two failed rounds → the honest downgrade (usually: back to free lead magnet, keep the automation). Anchor the clock to a concrete event (landing live date).

**Traps.** "We'll see how it goes"; counting vanity metrics (traffic, signups) as the bar.

---

## Station 11 · 營運歸屬

**Purpose.** Name the single-threaded owner of the human loop before launch.

**Interrogate.** If Station 4 put a human in the loop, that human is the drivetrain: QA, the signed note, and the 48h post-purchase follow-up. Rotation = no owner = dropped follow-ups = north star starves silently.

**Heuristics.** At launch volumes recommend the founder personally (founder-led sales converts best and captures raw buyer feedback); otherwise one named person who can *open a sales conversation*, not just proofread. Rotation only with an explicit tracking mechanism.

---

## Station 12 · 共識確認

**Purpose.** Freeze the shared understanding before anything is built.

**Do.**
- Present the consolidated table: every station → decision, key rationale, rejected options.
- Declare the tech defaults you chose on the user's behalf (stack, payment, email, storage) as vetoable.
- Name any unassigned gaps as launch blockers.
- Interactive mode: ask for explicit confirmation (with an "有地方要修" option that reopens the named branch). Express mode: this table goes into the deliverables, and the sign-off checklist *is* the confirmation surface.

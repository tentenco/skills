# 09. Nano Banana Pro Infographic（v2.0 多風格）

Canonical for infographic prompts.

---

## 14.1 核心規則

1. **一篇文章只用一種風格**，3 張 infographic 必須風格一致
2. AI 根據文章主題自動從 18 種風格中選最適合的一種
3. 3 張分別呈現文章不同面向（總覽 / 數據比較 / 結論洞察）
4. 圖中日期和數據必須與原文一致
5. 右下角 "tenten.co"（純文字，不加 logo 圖像）
6. 頂部和底部都不放 logo
7. 中文版用繁體中文標題，英文版用英文標題

## 14.2 風格選擇決策樹

按優先順序判斷，命中第一個就停：

| 順序 | 文章主題 | 風格 ID | 中文名 |
|-----|---------|---------|--------|
| 1 | AI 系統架構 / Agent 框架 / MCP Protocol | `anti_gravity_artifact` | 反重力 |
| 2 | 開發者工具 / CLI / API / 開源生態 | `neo_retro_dev` | 復古開發者 |
| 3 | AI 技術深度分析 / 演算法架構 | `tech_art_neon` | 科藝霓虹 |
| 4 | 產品發布 / SaaS 評測 / 硬體規格 | `studio_mockup_premium` | 精品展示 |
| 5 | 商業分析 / 營收 / 財報 / 市場動態 | `modern_newspaper` | 現代報紙 |
| 6 | 企業策略 / 顧問分析 / 組織架構 | `sharp_minimalism` | 銳利極簡 |
| 7 | 競爭對決 / 績效比較 / 成長指標 | `sports_athletic_energy` | 運動能量 |
| 8 | 品牌策略 / 行銷趨勢 | `yellow_black_editorial` | 黃黑編輯 |
| 9 | Agency 案例 / 設計服務 | `black_orange_agency` | 黑橘創意 |
| 10 | 社群平台 / 數位文化 / 新創 | `digital_neo_pop` | 數位潮流 |
| 11 | 科技哲學 / 文化衝撞 / 概念辯證 | `classic_pop_sculpture` | 古典波普 |
| 12 | 教學指南 / 科普解說 / 入門 | `deformed_flat_persona` | 變形扁平人物 |
| 13 | 文化議題 / 人文 / 社會觀察 | `royal_blue_red_watercolor` | 皇家藍紅水彩 |
| 14 | 人物專訪 / 消費評測 | `magazine_style` | 雜誌風 |
| 15 | 社群行銷 / Z 世代 | `pink_street_style` | 粉紅街頭 |
| 16 | 漫畫敘事 / 故事化內容 | `manga_style` | 漫畫風 |
| 17 | 演講摘要 / 培訓內容 | `seminar_minimal` | 研討極簡 |
| 18 | 文化評論 / 藝術觀點 | `mincho_handwritten` | 明朝手寫 |
| 19 | 都不符合 | `modern_newspaper` | 預設 |

## 14.3 18 種風格 Prompt 定義

**01. `modern_newspaper` — 現代報紙**
> Modern newspaper editorial infographic, Swiss International Typographic Style meets Bauhaus. White (#FFFFFF) or cool gray (#F5F5F5) background, Sumi jet black (#111111) text, electric yellow (#FFCC00) fluorescent marker-style highlights on key numbers, alert red (#FF3333) accent sparingly. Ultra-massive extra-bold sans-serif headlines occupying 30-50% area, extreme 10:1 jump ratio. Monochrome cutout figures with blown-out backgrounds. Asymmetrical Swiss grid layout, bold negative space. 1 message per frame, binary contrast between text-packed and empty areas.

**02. `sharp_minimalism` — 銳利極簡**
> Professional architectural sharp-edged minimalism infographic. Light gray (#E9E9E9) or white background, jet black and dark gray text, black accent for bold lines. Strict grid with intentional massive negative space. Helvetica Now or Inter sans-serif, generous letter spacing. Top-left section numbers '01. TOPIC'. Asymmetrical split, oversized black numbers, thin dividers. Dark mode (black bg) for emphasis. Constellation-like network diagrams, typography-driven columns, precision charts with thin lines ending in dots.

**03. `yellow_black_editorial` — 黃黑編輯**
> Yellow background black text editorial infographic, large dynamic modern serif font at dramatic angles and scales. Bright yellow (#FFD700) background, pure black text. Fashion photography, pop chic handwriting sticker-like decorations scattered. Fashion magazine bold layout with extreme typographic contrast and asymmetric photo placement.

**04. `black_orange_agency` — 黑橘創意**
> Creative agency infographic, white background, black text, blood orange (#FF4500) accent. Dynamic simple photography with bold English typography. Strategic orange highlights, artistic photo cropping, strong typographic hierarchy, confident negative space.

**05. `seminar_minimal` — 研討極簡**
> Minimal seminar infographic, white background, black text, red accent. Sans-serif dynamic typography. High-quality fashion portrait photography. High-sensibility clean design, minimal text, red sparingly for key data. Dynamic typography placement with intentional negative space.

**06. `manga_style` — 漫畫風**
> Manga comic style infographic, Japanese manga panel layout with dynamic storytelling. Bold black ink outlines, screentone shading, manga speech bubbles. Sequential narrative panels, dynamic action lines. Black and white with selective color accents. Expressive manga characters explaining information through comic grid with varied panel sizes.

**07. `magazine_style` — 雜誌風**
> Mature-cute sophisticated magazine editorial infographic. Matte dusty pink or shell pink background. Large cutout photo (deep etching) center with movement. Asymmetrical speech bubbles and numbered sections 'NO.1' 'NO.2'. L-shaped crop marks in corners. Hand-drawn speech bubbles, simple circles, thin lines as accents. Gothic headings, hand-drawn casual comments. Charcoal text on matte pink, white accents. Feminine trendy polished tone.

**08. `pink_street_style` — 粉紅街頭**
> Pink street-style pop infographic. Pink background, white and black text. Pop deformed illustrations with thick bold outlines, flat colors. Photos trimmed into soft squishy organic shapes. Illustrative characters with thick line art, simplified proportions. Street culture meets pop art, sticker-like decorations scattered.

**09. `digital_neo_pop` — 數位潮流**
> Vitamin Pop digital neo infographic, organic amoeba cloud shapes at edges. White or light-gray dot-pattern background, vivid pink cyan purple neon main colors, black outlines. Bold gothic outline text (white fill black stroke). Organic wavy shapes, pop illustrations, abstract avatar icons with eyes. SNS chat smartphone frames, colorful donut charts with huge numbers. Hand-drawn arrows, crayon strokes, sticker-like tilted cards.

**10. `mincho_handwritten` — 明朝手寫混搭**
> Yellow background editorial infographic, modern serif Mincho font dynamic angular placement with handwritten elements. Bright yellow canvas, black text, dramatic scales and angles. Fashion photography, pop chic handwriting annotations and sticker elements creating editorial collage. Bold fashion magazine layout with serif/handwritten contrast.

**11. `deformed_flat_persona` — 變形扁平人物**
> Flat color illustration infographic with slightly deformed simplified human figures, thick bold outlines. Gentle pastel tones with white mixed in, maximum 3 colors. Solid flat single-color background. Friendly approachable character design, consistent thick outlines, no gradients no shadows. Warm educational illustration for broad audiences.

**12. `royal_blue_red_watercolor` — 皇家藍紅水彩**
> Royal blue and red wet watercolor artistic infographic. Shades of royal blue and deep red watercolor washes bleeding and blending organically. Wet-on-wet technique with drips and organic spread. Watercolor paper texture throughout. Text overlaid on washes with careful contrast. Color mixing where blue and red create rich purple. Fine art watercolor meets information design.

**13. `classic_pop_sculpture` — 古典波普**
> Sculpture pop art vaporwave neon surrealism infographic. Classical white marble statue collage with modern pop accessories (sunglasses headphones smartphones VR). High-saturation solid color backgrounds per section (cyan magenta yellow lime purple). Ultra-bold Helvetica Now Display Black headlines. Cleanly isolated cutout sculptures, bold humorous surreal aesthetic. Varied sculptures per section, strong background-accessory color contrast.

**14. `tech_art_neon` — 科藝霓虹**
> Constructivism tech-art avant-garde infographic, 'Architecture of Intelligence'. Warm gray beige (#E0E0D0) matte paper background, charcoal (#333333) text, neon yellow (#DFFF00) geometric accents, ultra-thin architectural draft lines. Serif/sans-serif typography mix, typewriter numbers. Monochrome cutout portraits with neon yellow shapes. Graph paper grid, wireframe illustrations partially filled neon yellow. Blueprint labels (Fig.1 Fig.2), radar chart art. Three-color limit: beige monochrome neon-yellow. Layer order: grid → geometry → cutout → text.

**15. `studio_mockup_premium` — 精品展示**
> Premium mockup modern UI clean tech infographic. White (#FFFFFF) or light gray (#F5F5F7) studio background alternating jet black. Electric purple (#8D59E9) accent, acid yellow (#EBE021) badges, pale blue-gray (#D8E2EC) cards. 3D Apple device mockups with screens occupying 70-80%. Black or vivid gradient screen UI, extra-bold white text. Card-based grid, oversized numbers. Soft studio shadows, devices cropping beyond frame for impact. Realistic reflections, premium feel.

**16. `anti_gravity_artifact` — 反重力**
> Anti-gravity living artifact infographic, Apple clarity meets DeepMind research aesthetic. Pure white background, soft flowing gradient accents (blue cyan violet) very low opacity on corners only. Clean modern sans-serif, slightly rounded, medium-bold, calm authority. Dark gray text, calm blue accent sparingly. Left-aligned, wide margins, massive white space. Thought-to-structure diagrams, interface screenshots, soft rounded capability cards. Thin-line outline icons. Implied motion through arrows and sequential flow. No visual noise, intentional and breathable.

**17. `neo_retro_dev` — 復古開發者**
> Neo-retro dev deck pixel-infographic editorial. Light cream off-white grid paper background with engineering notebook grid. Bold heavy condensed black sans-serif headlines. Modular color blocks with thick black outlines: hot pink (agent/intelligence), bright yellow (code/tools), cyan (browser/web). Stacked rectangles with slight overlaps, controlled imperfection. 8-bit pixel icons (rocket robot gear brackets). Small decorative gears arrows chevrons. Card-based steps, horizontal section bars. Retro-futuristic developer editorial, 90s manual meets modern AI tools.

**18. `sports_athletic_energy` — 運動能量**
> Sports athletic high-energy infographic. Asphalt black (#111111) base, white text, bolt lime (#CCFF00) and neon orange (#FF4500) accents. Gradient overlay on dynamic motion blur photography. Extra-bold italic gothic (Impact) headings, stencil/jersey numbers. Diagonal-cut shapes, skewed rectangles, parallelogram containers. Large italic text overlapping subjects. Jagged lightning VS dividers, speedometer data displays. Bold diagonal highlight stripes. Passionate fast-paced competitive aesthetic.

## 14.4 輸出 JSON 格式

每張 infographic 輸出以下格式：

```json
{
  "nano_banana_pro": {
    "version": "2.0",
    "style_selected": "{style_id}",
    "style_name": "{中文風格名}",
    "selection_reason": "為何選此風格（一句話）",
    "infographic_index": "N/3",
    "content_focus": "此張圖要呈現的文章重點",
    "title": {
      "main": "主標題（2-8 字）",
      "subtitle": "副標題（核心洞察）"
    },
    "key_data_points": ["數據1", "數據2", "數據3"],
    "visual_prompt": "{對應風格 prompt}。Content: {具體視覺內容描述}。Include text overlay: {標題和數據}。Credit text bottom-right: tenten.co",
    "negative_prompt": "{對應風格的 negative prompt}",
    "aspect_ratio": "16:9",
    "text_overlay": {
      "headline": "主標題",
      "data_callouts": ["關鍵數據1", "關鍵數據2"],
      "credit": "tenten.co"
    },
    "color_palette": ["{對應色票}"],
    "date_validation": "確認日期數據正確性"
  }
}
```

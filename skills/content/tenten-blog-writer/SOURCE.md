# Source

- **Original URL:** https://s4.tenten.co/tenten-blog-0504.txt
- **Title:** 中文內容編輯系統提示 v7.0 (Merged: v6.2 + Better-Humanizer-zh-TW Skill)
- **Author:** Tenten editorial team (internal system prompt)
- **Size:** 1,613 lines / 74 KB, 17 parts
- **Fetched:** 2026-08-06 via direct HTTP (plain text, publicly readable)
- **Packaged by:** Claude Code, 2026-08-06

## What the source was

A single monolithic system prompt used to generate Tenten blog articles. It ran
as one long paste rather than as an installed skill, so it could not be invoked
from other agents and its CSV-based internal-link step depended on a file being
attached to each conversation.

## What changed when packaging

Three deliberate changes; everything else is carried over as written.

1. **Part 9.2 CSV keyword lookup → Tenten Content Index MCP.** The original
   queried a CSV supplied in-conversation. That is now `plan_links` against the
   live index, in a new `references/11-link-building-mcp.md`: `quota_report`
   preflight, exactly one `plan_links` call per completed language draft, apply
   `edits` by exact span from the highest `start` downward, and treat
   `partial` / `no_match` with `retryable=false` as a successful terminal result
   rather than something to retry.

2. **Part 17's 20 sequential steps → 6 phases with explicit verify gates.**
   Matches the structure used elsewhere in Tenten's skill set. No step was
   dropped; they were grouped and given pass conditions.

3. **Added technical-appendix block B5** recording the link-plan result
   (`planId`, `status`, `terminalReason`, `policyVersion`, links applied).

Carried over unchanged: the 8-category / 30-item AI-tell taxonomy, the four
rhetorical-device hard caps, the Mainland/HK→Taiwan vocabulary tables, MOE
punctuation and typography rules, the six depth dimensions and length
calibration, AEO/GEO structure, the soul check, the three-layer quality gate and
weighted scoring, the native-English specification (Tier 1/2/3 banned words,
US localization, 8-dimension score), all 18 Nano Banana infographic styles and
the selector tree, the output format, and the special-scenario rules.

## Not included

The source prompt has no publishing step, and none was added. Ghost / LinkedIn /
Hashnode publication and cover generation live in a separate, heavier Tenten
pipeline that is not part of this repo.

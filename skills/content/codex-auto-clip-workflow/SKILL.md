---
name: codex-auto-clip-workflow
description: >-
  Automate short-form video editing by having an AI coding agent (Codex, Claude
  Code, or similar) clone a reference viral video's shot structure onto your own
  footage — auto-detecting shot cuts with FFmpeg, visually matching clips from
  your asset library, generating TTS voiceover + subtitles, and outputting an
  editable CapCut (剪映 / JianYing) draft. Use WHENEVER the user wants to
  mass-produce Douyin / TikTok / e-commerce montage videos, "copy a viral
  video's structure/rhythm", batch-edit or auto-edit video with AI, build a
  reference-based auto-clipping pipeline, or set up an AGENTS.md-driven editing
  workflow. Good for volume "混剪" content (e-commerce, promo, montage Vlog), not
  for hand-crafted originals. Distilled from @xilo2991's workflow.
---

# Codex Auto Clip Workflow

Turn one viral reference video + your own asset library into a finished,
editable CapCut draft, mostly automatically, by driving an AI coding agent
(Codex / Claude Code) that runs FFmpeg, does visual shot-matching, generates
voiceover, and assembles the draft.

The underlying bet: **the fastest way to get views is to reproduce a validated
viral structure.** A hit video's shot order, rhythm, and pacing are already
market-tested, so you keep its *structure* and swap in *your own footage*. This
is "copy the structure," not re-uploading someone else's clip — the visuals are
yours.

Positioning: this is **automated production, not premium craft.** It shines for
multi-clip montage content — e-commerce product videos, promos, montage Vlogs —
where a reference supplies structure/rhythm and your asset library supplies the
visuals. For highly polished original work, edit by hand instead.

Reported effect (author's own use, Douyin product videos): ~6 videos/day by hand
→ ~30/day with this workflow, once the asset library is ready.

## When to use

- "Help me mass-produce Douyin/TikTok product videos."
- "Clone this viral video's structure onto my footage."
- "Set up an AI auto-editing / auto-clipping pipeline."
- "Batch-generate montage videos from my asset library."
- The user has a coding agent (Codex/Claude Code) and wants a repeatable editing
  system, not a one-off manual edit.

## Prerequisites (install once)

Have the agent verify and install these — send it the environment-check prompt
in `references/prompts.md` (Prompt 0).

- **FFmpeg** — shot splitting, frame extraction, muxing, format conversion. Core
  dependency; must be installed.
- **Python 3.8+** — the pipeline scripts run in Python. Deps: `opencv-python`,
  `numpy`, `pillow`.
- **Voiceover engine** — for auto voiceover use **Doubao TTS** (字节/ByteDance;
  same AI-voice source as CapCut, cheap and stable — roughly ¥0.4–0.8 per ~1‑min
  video). For voice cloning use **VoxCPM** (free, open-source).
- **CapCut / 剪映 Pro (JianYing)** — the final draft is written in CapCut's draft
  format, so it must be installed to open/finish the video.

## Project structure

Set up a stable project folder once; each edit run writes into a dated work
folder so the root stays clean.

```
project/
  assets/        # your reusable asset library (product/scene/character/AI clips)
  work/          # one dated folder per edit run: work/YYYY-MM-DD/
  final/         # finished, approved videos moved out of work/
  AGENTS.md      # project config: goal, dirs, pipeline, output spec, acceptance rules
```

`AGENTS.md` is the agent's long-term context — it reads this to understand what a
"correct" video is for this project. A ready-to-adapt template (including the
full acceptance-criteria checklist) is in `references/agents-md-template.md`.

## The pipeline (five stages)

Each stage is driven by a copy-paste prompt to the agent. Full prompts are in
`references/prompts.md`; the flow is:

```
read reference → split shots → extract script/VO text → match assets → generate VO → build sample + CapCut draft
```

1. **Deconstruct the reference video.** Download a reference (a hit video, or a
   past edit you liked) into `work/`, give it a searchable name. The agent uses
   FFmpeg to detect shot-change points (inter-frame difference), extracts a key
   frame per shot, saves the audio track separately, and writes **`recipe.json`**
   (per-shot start/end/duration/keyframe path) plus a per-shot script if there's
   speech. `recipe.json` is the backbone the rest of the pipeline reads. Review
   the split and have the agent re-cut if a shot was wrongly merged/divided.

2. **Match assets to shots (the highest-value step).** Point the agent at
   `assets/`; it does *visual* matching of your clips to each reference shot's
   key frame. **Low-confidence shots must be flagged as "missing asset" for you
   to fill by hand** — never let it stuff in an unrelated clip to hit a count, or
   the video looks off. Matched assets are **copied (never moved)** into per-shot
   folders so the original library is never damaged.

3. **Generate voiceover.** First proofread the extracted script (OCR/ASR isn't
   100%). Then have the agent call Doubao TTS to produce one audio file per shot,
   read each file's *real* duration, and reconcile against the reference: if the
   VO for a shot runs 5s but the reference shot is 3s, the shot is stretched to
   5s so audio and picture stay aligned. Update `recipe.json` with true VO
   durations. Listen through once for naturalness/pacing.

4. **Build the sample + CapCut draft (the fragile step).** CapCut's draft format
   is strict. Three IDs — **content ID, metadata ID, root-index ID** — must be
   internally consistent and must not collide with existing drafts (collisions
   cause open-failures or overwrite old drafts). Asset paths in the draft must be
   **absolute and really exist** (move a file and the draft won't open). Encode
   these rules in `AGENTS.md` so the agent respects them every run.

5. **Review, fix, and finish.** If something's wrong, tell the agent whether it's
   an asset-match, voiceover, or draft-format problem and have it fix
   iteratively. Whole run is ~20–30 min; ~5 min/video once the asset library is
   primed. Open the draft in CapCut for final touch-ups, then move to `final/`.

## Key rules & pitfalls

- **Copy, never move** assets — protect the original library.
- **Expose gaps, don't fake them** — flag low-confidence/missing shots for manual
  fill instead of padding with irrelevant footage.
- **CapCut IDs must be consistent and unique**; **asset paths absolute and real.**
- Keep playback at `1.00x` (fill short clips by holding a frame, don't rubber-band
  speed) unless the user asks otherwise.
- Subtitles stay inside their shot, break by meaning (not to hit a character
  count), and never cover the product/key action.
- Drive VO/subtitle timing off the *real* generated audio duration, not the
  reference.
- This is volume production; for premium originals, edit manually.

## Packaging this into a reusable skill (the punchline)

The source's key insight: once you've run the full pipeline once and it works,
tell the agent **"package this workflow into a Skill"** (帮我把工作流封装成
Skill). After that you skip the whole multi-step process and just invoke the
skill to generate the next video. This SKILL.md is exactly that packaging — point
your agent here (plus `references/`) and it can run the pipeline end to end.

## References

- `references/prompts.md` — the copy-paste prompts for each stage (env check,
  deconstruct, match, voiceover, draft).
- `references/agents-md-template.md` — the `AGENTS.md` project-config template,
  including the full acceptance-criteria checklist the agent grades output
  against.

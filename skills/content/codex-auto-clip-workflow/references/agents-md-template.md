# AGENTS.md template (project config for the editing agent)

Drop a file like this at your project root. The agent reads it as long-term
context to understand the goal, folder layout, pipeline, and — most importantly —
the **acceptance criteria** it should grade its own output against. Adapted from
@xilo2991's template; English with key Chinese terms preserved.

```markdown
# AGENTS.md

## Goal
One sentence describing what this project produces (e.g. "Auto-generate Douyin
e-commerce montage videos by cloning reference structure onto our product assets").

## Directories
Keep the root to a stable structure; per-run process files go in a dated work folder.

- `AGENTS.md`  — long-term project context: goal, dirs, pipeline, output, acceptance.
- `assets/`    — pre-prepared product/scene/character/AI clips. Only COPY from here
                 when editing; never move or damage originals.
- `work/`      — in-progress / under-review projects; one dated folder per run.
- `final/`     — finished, approved videos, moved out of work/ to keep it clean.

Per-run work folder:

    work/
      YYYY-MM-DD/
        reference-YYYY-MM-DD.mp4   # full reference: overall order, rhythm, duration, audio, split source
        video_clips/               # auto-split shots + key frames: visual order & match basis
        script.txt                 # narration/subtitle/VO text; may be empty if none
        material/
          fragment01/              # approved production assets per shot (copied from assets/)
          fragment02/
        voice/                     # per-segment VO, cleaned vocals, concatenated final audio
        jianying_draft/            # CapCut draft + check report + backups (only when needed)

## Source-of-truth rules
- The full reference video is the source for audio, overall order, and total duration.
- `video_clips/` is the source for visual order and visual matching.
- `material/fragmentNN/` is the source for approved production assets.
- When using generated VO, each segment's REAL finished audio duration drives
  picture and subtitle timing.
- `recipe.json` and `matches.json` are the machine-readable backbone of the pipeline.

## Pipeline
read reference → split reference shots → extract script/VO text → match source
assets → generate voiceover → build sample + CapCut draft

1. Read reference: create work/YYYY-MM-DD/, save the reference as reference-YYYY-MM-DD.mp4.
2. Split shots: auto shot-cut + key-frame extraction into video_clips/; structure data saved in the work folder.
3. Extract text: assemble narration into script.txt from reference audio / user copy / VO.
4. Match assets: visual-match assets/ against reference frames; approved assets copied into material/fragmentNN/.
5. Generate voiceover: per-segment TTS; align picture/subtitle to real audio duration.
6. Build draft: assemble the editable CapCut/剪映 draft.

## Acceptance criteria (the agent grades output against these)
- Every visual segment has a usable asset; missing / low-confidence segments MUST
  be surfaced explicitly.
- Don't pad the count with irrelevant assets.
- Asset visuals match the product, scene, action, shot size, angle, lighting,
  product visibility, and composition.
- File/folder names are hints only — final judgment is the picture itself.
- Copy assets; do not move or damage originals.
- De-duplicate: don't treat the same content under different filenames as distinct.
- Avoid repeating the same source folder within any 3 consecutive shots.
- Avoid obviously repeated composition/semantic scenes in adjacent segments.
- Keep identity continuity for related AI clips or same-character clips.
- Keep finished playback at 1.00x unless the user asks for speed changes; pad short
  assets by holding a frame rather than rubber-banding speed.
- Finished ratio / resolution / frame rate follow this file's common config; length
  and count follow the user's current request or this task's settings.
- Finished duration should stay within an acceptable delta of the reference/target;
  flag any obvious deviation.
- Subtitles stay inside their segment, break by meaning, not to hit a character count.
- If a subtitle character cap is set, treat it as a CAP not a target; avoid isolated
  1–2 character subtitles.
- Subtitles don't cover the product subject, key action, or important info.
- If VO is used, drive picture/subtitle timing off the real finished VO duration.
- VO checks: opening, mid boundaries, longest pause, tightest subtitle boundary, ending.
- If building a CapCut draft, it must be a NEW editable draft — never overwrite
  native or encrypted-cache drafts.
- CapCut draft content ID, metadata ID, and root-index ID must be consistent;
  batch draft IDs must not collide.
- CapCut draft asset paths must exist; media source range must not exceed real duration.
```

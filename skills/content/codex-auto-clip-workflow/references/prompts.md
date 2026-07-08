# Copy-paste prompts for each stage

Send these to your coding agent (Codex / Claude Code) in order. They're written
in English here; the original workflow used Chinese prompts (kept verbatim under
each, since the toolchain — CapCut/剪映, Doubao TTS, Douyin — is China-focused and
you may prefer to send them as-is). Replace `@(...)` placeholders with your real
file references.

---

## Prompt 0 — Environment check

> Please check the environment needed for automated video clipping:
> 1. Check whether FFmpeg is installed; install it if missing.
> 2. Check Python version is >= 3.8; install/upgrade if needed.
> 3. Check whether CapCut/剪映 Pro is installed; if not, give me the download link.
> 4. Install Python deps: opencv-python, numpy, pillow.
> Then tell me what's already set up and what I need to handle manually.

原文：
> 请帮我检查视频自动化剪辑需要的环境：
> 1. 检查 FFmpeg 是否已安装，如果没有请帮我安装
> 2. 检查 Python 版本是否 >= 3.8，如果没有请帮我安装或升级
> 3. 检查是否安装了剪映专业版，如果没有请告诉我下载链接
> 4. 安装 Python 依赖包：opencv-python, numpy, pillow
> 检查完之后，告诉我哪些已经装好了，哪些需要我手动处理。

---

## Prompt 1 — Deconstruct the reference video

> I need to deconstruct a reference video.
> The reference video is at @(your filename — the agent will search for it).
> Please do the following:
> 1. Use FFmpeg to detect shot-change points (via inter-frame difference analysis).
> 2. Extract a key frame per shot, saved as an image.
> 3. Extract the audio track and save it separately.
> 4. Generate a `recipe.json` recording each shot's start time, end time, duration, and key-frame path.
> 5. If there is speech, generate a voiceover script from the audio, segmented per shot; proofread it carefully to avoid errors.
> When done, save into the right folders per AGENTS.md, and tell me how many shots were detected so I can confirm the split is reasonable.

原文：
> 我需要拆解一个参考视频。
> 参考视频位置在@（输入你的文件名，Codex会自动搜索）
> 请帮我完成这几件事：
> 1. 用 FFmpeg 识别视频的镜头切换点（通过帧间差异分析）
> 2. 为每个镜头提取关键帧，保存为图片
> 3. 提取视频的音轨，单独保存
> 4. 生成一个 recipe.json 文件，记录每个镜头的开始时间、结束时间、时长、关键帧路径
> 5. 如有文案，根据音频生成一个配音文本，按镜头分段，文案需要精校，避免出错
> 完成后按照AGENTS.md要求，保存到对应文件夹，并告诉我识别了多少个镜头，让我确认切分是否合理。

`recipe.json` is the core reference for every later stage.

---

## Prompt 2 — Match assets to shots

> I need to match assets from my asset library to each shot. My library is at
> `assets/`. Use the reference key frames to do visual matching against my
> footage. Rules:
> - If a shot's match confidence is too low, mark it as "missing asset" for me to
>   fill manually — do NOT stuff in an unrelated clip just to hit the count.
> - COPY matched assets into per-shot folders (`material/fragmentNN/`); never
>   move or alter the originals.
> - Classify/save by the reference shot count.
> When done, show me the match results so I can re-replace anything I don't like.

(Author's lesson: an early version filled un-matchable shots with random assets
and the videos looked wrong; switching to "flag low-confidence as missing" fixed
quality at the cost of a little manual work.)

---

## Prompt 3 — Generate voiceover

> I need to generate voiceover for the video. The VO text is @(your script.txt).
> Requirements:
> 1. Call the Doubao TTS API to generate an independent audio file per shot.
> 2. Read each generated file's real duration.
> 3. If a VO duration doesn't match the reference shot duration, record the delta.
> 4. Concatenate all segments into one file: `final_voice.mp3`.
> 5. Update `recipe.json` with the true VO durations.
> When done, let me listen to confirm naturalness and speaking rate.

原文：
> 我需要为视频生成配音。配音文本是@（你的文案.txt）
> 要求：
> 1. 调用豆包 TTS 接口，为每个镜头生成独立的语音文件
> 2. 读取每个生成的语音文件的实际时长
> 3. 如果配音时长和参考视频的镜头时长不一致，记录时长差异
> 4. 将所有片段拼接成完整的配音文件：final_voice.mp3
> 5. 更新 recipe.json，记录真实的配音时长
> 完成后，让我试听一遍，确认语音自然度和语速。

The agent aligns picture to audio: a shot whose VO runs longer than the reference
gets stretched so audio and visuals stay in sync.

---

## Prompt 4 — Build sample + CapCut draft

This is the most error-prone step; lean on the AGENTS.md rules. Ask the agent to
assemble the CapCut/剪映 draft from `recipe.json` + matched assets + `final_voice.mp3`,
enforcing:

- The three draft IDs — **content ID, metadata ID, root-index ID** — are mutually
  consistent and unique (no collision with existing drafts).
- All asset paths are **absolute** and point to files that really exist.
- Create a NEW editable draft; never overwrite native/encrypted cache drafts.
- Keep playback at `1.00x`; fill short clips by holding a frame rather than
  changing speed.

Then open the draft in CapCut for final touch-ups and move the result to `final/`.

---

## Fixing problems

If output is off, tell the agent which layer it is — asset-match, voiceover, or
draft-format — and have it optimize iteratively rather than regenerating blindly.

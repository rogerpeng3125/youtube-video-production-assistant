# Agent — Short-form

| | |
|---|---|
| **Pipeline step** | 8 |
| **Owner** | **Codex** |
| **Reads** | `videos/<NNN-slug>/06-beat-sheet.md`, `videos/<NNN-slug>/media/render.mp4`, `docs/audience.md`, `docs/brand.md` |
| **Writes** | `videos/<NNN-slug>/07-shorts.md`, `videos/<NNN-slug>/media/shorts/*` |
| **Status** | Audited by Claude Code against the filled-in `docs/`. Codex owns this step. |

## Job

Cut the finished video into vertical clips for **YouTube Shorts, TikTok, and
Reels** — especially the practice-problem segments, which stand alone naturally.
Produce both a cut list (`07-shorts.md`) and the rendered clips.

## Rules

1. **Each clip must stand alone.** A viewer arriving cold with no context should
   get a complete problem and a complete answer. A clip that only makes sense
   after the long-form video is a failed clip.

   **The band travels with the clip.** `docs/audience.md` splits videos into
   Basic (below ~750, taught from the ground up) and Complex (800-band, a specific
   named theorem). A clip cut from a Complex video lands in front of people who
   have not seen the concept taught — it assumes the fundamentals the long-form
   video assumed, and there is no preceding four minutes to lean on. Say in
   `07-shorts.md` which band each clip is really for, and prefer moments that
   survive the loss of context over ones that merely look self-contained.
2. **Start with the problem, not the setup.** The hook is the problem itself;
   preamble is what kills retention in the first two seconds.

   Suggested caption and hook text must sound like the channel. `docs/brand.md`
   describes the persona as *a friendly instructor who relates to the student* and
   the voice as *seeming to know what the viewer is thinking*. Its **Hard nos**
   section currently reads **None**, which means no prohibition has been written
   down — **not** that anything goes. Nothing in `docs/` supports score-jump
   promises or bait, and `docs/audience.md` says viewers come for specificity, not
   spectacle. Stay inside that; if a hook feels borderline, put it in Flags and let
   the host decide.
3. **Use the Shorts candidates in `06-beat-sheet.md`** as the starting point, but
   verify the in/out points against the actual render. Adjust and say what changed.
4. **Vertical, 1080x1920.** The 16:9 render must be reframed, not letterboxed —
   equations must stay readable at phone size. This means re-rendering the Manim
   scene at vertical dimensions rather than cropping the finished video, since
   cropping tends to cut equations in half.
5. **Length: 30–60s.** Long enough for a full problem, short enough to hold.
6. **Never cut mid-explanation.** Better a slightly long clip than one that ends
   before the reasoning lands.
7. **Burn in captions.** Most short-form is watched muted.
8. **Same clip for all three platforms unless there is a real reason to differ.**
   Note per-platform differences explicitly rather than silently forking.
9. **Do not edit upstream files.** If the render or beat sheet has a problem, flag
   it in `07-shorts.md`.

## Output shape — `07-shorts.md`

    # Shorts — <title>

    **Source:** media/render.mp4   **Clips:** N

    ## Clip 1 — <slug>
    - **Band:** Basic / Complex — who this lands in front of, cold
    - **In / out:** 4:12 – 4:51 (39s)
    - **File:** media/shorts/01-<slug>.mp4
    - **Stands alone because:** ...
    - **Hook (first 2s):** what is on screen and said
    - **Suggested caption/hook text:** for the platform post
    - **Platforms:** Shorts / TikTok / Reels — note any differences
    - **Changed from beat sheet:** if in/out points moved, why

    ## Flags
    Anything that could not be cut cleanly, or that needs a re-render.

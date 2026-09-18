# Agent — Animation

| | |
|---|---|
| **Pipeline step** | 7 |
| **Owner** | **Codex** |
| **Reads** | `videos/<NNN-slug>/05-refined-transcript.md`, `videos/<NNN-slug>/media/final-take.*`, `docs/brand.md`, `docs/style-notes.md` |
| **Writes** | `videos/<NNN-slug>/06-beat-sheet.md`, render code in `tools/`, `videos/<NNN-slug>/media/render.mp4` |
| **Status** | Audited by Claude Code against the filled-in `docs/`; the sprite section was written from `docs/brand.md`. Codex owns this step. |

## Job

Two outputs, in order:

1. **A timed beat sheet** — what is on screen when, keyed to timestamps in the
   final recording.
2. **The render** — the actual finished video, produced with math-animation
   tooling (Manim is the assumed choice) composited with the recording.

The beat sheet comes first and is reviewable on its own. Do not render before the
beat sheet exists, so a bad plan gets caught before an expensive render.

## This is the tool handoff

Everything upstream of this step was produced by Claude Code. **Do not edit
upstream files.** If `05-refined-transcript.md` is wrong or unusable, say so in
the beat sheet and stop — do not fix it in place. The host arbitrates.

## Content this covers

Equations, graphs, and problem-solving worked step by step — no complex scenes or
character animation. Plus a **simple recurring sprite with a few fixed poses**,
defined in `docs/brand.md`.

## The sprite — two roles, not a mood indicator

`docs/brand.md` is now filled in, and it describes something more specific than a
set of reaction faces. The sprite plays **two distinct roles**, and choosing
between them is the actual decision at each beat:

1. **The sprite as the audience.** It reacts the way the viewer is feeling. The
   host's example: on *"this problem looks intimidating at first"*, the sprite
   holds its head with a bead of sweat running down. This role is for the moments
   the host names the viewer's emotional state — and `docs/style-notes.md` records
   that naming the viewer's mental state is a recurring habit (*"don't let these
   variables scare you"*, *"you might have realized by now"*). Those lines are the
   cue for this role.
2. **The sprite as the instructor** — pointing at what is being taught. Per
   `brand.md`, this is the **more common** of the two. Use it for the ordinary
   work of directing attention at the equation or step under discussion.

**Match the role to the line.** An audience-reaction pose over a passage where the
host is explaining mechanics reads as noise; an instructor pose over *"don't let
these variables scare you"* throws away the one moment the sprite exists for.

The pose inventory is not fixed up front — build what the transcript actually
calls for and list the poses used in the beat sheet, so a real inventory
accumulates from use.

## Rules

1. **Timestamps come from the actual final recording**, not from the transcript's
   reading order. The host will not have paced it exactly as written.
2. **Equations appear as they are spoken**, not before. Revealing an answer early
   kills the problem.
3. **Step-by-step work stays on screen** long enough to be read at speed. Build up
   rather than replacing, so a viewer can see the whole chain.
4. **Never typeset an unresolved math flag.** `05-refined-transcript.md` carries a
   flags section, and math flags there are written as lines beginning
   `**Math (UNRESOLVED):**`. **Check for them before rendering anything.**

   The reason is specific and it is the worst failure this pipeline can produce.
   `docs/style-notes.md` documents that auto-transcription **drops minus signs and
   loses fraction grouping** — a transcript can state a formula as a plain
   fraction when the recording actually said a negative one. The Refinement agent is
   forbidden from silently fixing that, so it arrives here still wrong-looking and
   still unverified. If you typeset it, a lossy transcription becomes clean,
   confident, permanent on-screen notation that no viewer can tell is wrong, in
   the one medium where the error outlives the transcript.

   So: if an expression is flagged UNRESOLVED, **stop and ask the host to resolve
   it against the recording.** Do not typeset it, do not guess the sign, do not
   "correct" it yourself — the flag exists precisely because nobody has yet
   confirmed which of the two readings the host actually said.

5. **Use LaTeX typesetting** (Manim `MathTex`) for all math. The "Vocabulary and
   notation" section of `docs/style-notes.md` is about **spoken** wording, not
   on-screen typesetting conventions — do not read it as a typesetting guide.
6. **The recording is the spine.** Animation serves the audio; never let a visual
   flourish pull attention off what is being said.
7. **Render code lives in `tools/`**, is reusable across videos, and is
   parameterized rather than copy-pasted per video.
8. **Note the intended Shorts moments.** Practice-problem segments are what the
   Short-form agent cuts — mark them in the beat sheet with clean in/out points.
   `docs/style-notes.md` shows the reference video pausing for the viewer to try
   the second problem — that pause prompt is a natural clip boundary.
9. **Flag rather than invent.** If a visual is called for and the transcript does
   not say enough to build it, flag it. Do not invent math to fill the gap.

   Note that the outline agent is instructed to tell the host to **say visual
   details aloud** for exactly this reason. If something visual is missing anyway,
   that is a gap in the recording, not an invitation to reconstruct it — you do not
   have `03-outline.md` and must not go read it, because the recording is what
   shipped and the outline is only what was planned.

## Output shape — `06-beat-sheet.md`

    # Beat sheet — <title>

    **Source recording:** media/final-take.<ext>   **Duration:** MM:SS
    **Render target:** 1920x1080, <fps>
    **Math flags:** none unresolved in 05-refined-transcript.md — safe to render
                    (or: BLOCKED, N unresolved, listed under Flags)

    ## Beats

    Sprite column: role first (audience / instructor), then the pose.

    | In | Out | On screen | Sprite | Notes |
    |---|---|---|---|---|
    | 0:00 | 0:12 | Title card | — | |
    | 0:12 | 0:41 | Problem 1 statement | audience: intimidated | "looks scary" beat |
    | 0:41 | 1:20 | Build solution steps 1–3 | instructor: pointing | build up, do not replace |

    ## Sprite poses used
    Running list, so an inventory accumulates across videos.

    ## Shorts candidates
    Clean in/out points for the Short-form agent, with why each stands alone.

    ## Flags
    Anything ambiguous in the transcript, or visuals that could not be planned.

# Agent — Publishing

| | |
|---|---|
| **Pipeline step** | 9 |
| **Owner** | **Codex** |
| **Reads** | `videos/<NNN-slug>/05-refined-transcript.md`, `videos/<NNN-slug>/06-beat-sheet.md`, `videos/<NNN-slug>/07-shorts.md`, `channel-log.md`, `docs/*` |
| **Writes** | `videos/<NNN-slug>/08-publishing-brief.md` |
| **Status** | Audited by Claude Code against the filled-in `docs/`. Codex owns this step. |

## Job

Produce an advisory brief: **post timing, title options, a thumbnail concept, and
a description.** The host reads it and posts manually.

## Advisory only — hard boundary

**This agent has no posting access and must never acquire any.** No YouTube API
calls, no OAuth, no upload automation, no scheduling integrations — not as a
convenience, not as a suggestion. The output is a text file the host reads. If a
task seems to call for posting, write the recommendation and stop.

## Rules

1. **Offer 3–5 title options, not one.** Each with a one-line rationale for what
   it optimizes (search intent, curiosity, specificity).
2. **No clickbait the brand rejects.** `docs/brand.md` has a **Hard nos** section
   and it currently reads **None**.

   Read that as *"the host has not written any prohibitions down yet"*, **not** as
   *"anything is permitted"*. An empty stop-list is the weakest possible license,
   and this is the one step whose output faces the public, so it is the worst place
   to treat silence as permission. Until the section is filled in, take the limits
   from what `docs/` does positively say: `audience.md` says viewers pick this
   channel because it is *specific to SAT prep and to the exact topic they're
   missing — not generic math content*, and `brand.md` describes a friendly
   instructor who relates to the student. A title that overpromises a score jump,
   manufactures outrage, or hides what the video is about fails all of that
   without needing a rule to name it.

   If a title is a genuine judgment call, offer it **and** say why it is
   borderline. The host decides; this step only advises.
3. **Titles should carry search intent.** `docs/audience.md` states that viewers
   find the channel through **search primarily**, with Shorts and recommendations
   hoped for as it grows. So a title matching what a student actually types beats
   a clever one — this is now grounded in the audience doc, not a guess.

   Name the concept the way a student would search it — the exact formula or
   theorem name, said repeatedly rather than "the formula" — that name is the
   search term.
4. **Thumbnail is a concept, not a file.** Describe the composition, the text on
   it (few words, phone-legible), and the sprite pose if used. Say why it earns a
   click from someone who does not know the channel.

   On the sprite: `docs/brand.md` gives it two roles — reacting **as the
   audience**, and acting **as the instructor** pointing at the work. A thumbnail
   is seen by someone who has not started the video and is deciding whether the
   problem is worth their time, which argues for the audience-reaction pose over
   the instructor pose — flag it as a choice rather than presenting it as brand
   policy.
5. **Timing advice must be justified by `channel-log.md`.** If there is not enough
   history to justify a recommendation, say so rather than repeating generic
   best-post-time advice.
6. **Description:** a real summary, not keyword stuffing. Include timestamped
   chapters derived from `06-beat-sheet.md`, since chapters help both navigation
   and search.
7. **Cover the Shorts too.** Suggest posting order and spacing for the clips in
   `07-shorts.md`, and which one leads.
8. **Do not edit upstream files.**

## Output shape — `08-publishing-brief.md`

    # Publishing brief — <title>

    ## Titles
    1. "<option>" — optimizes for: ...
    2. ...
    **Pick if unsure:** <which, and why>

    ## Thumbnail concept
    - **Composition:** ...
    - **Text on thumbnail:** <few words>
    - **Sprite pose:** <if used>
    - **Why it earns a click:** ...

    ## Description
    <full text, ready to paste>

    ### Chapters
    0:00 ...

    ## Timing
    - **Recommended:** <day, time>
    - **Based on:** <specific channel-log entries, or "insufficient history">

    ## Shorts rollout
    Order, spacing, and which clip leads.

## Feeds the loop

After posting, the host records results in `channel-log.md`. That file is read by
the Research & strategy agent at the start of the next cycle. This brief is the
last automated step; the log entry is what makes the next one smarter.

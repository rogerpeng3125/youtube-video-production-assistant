# Agent — Outline

| | |
|---|---|
| **Pipeline step** | 3 |
| **Owner** | Claude Code |
| **Reads** | `videos/<NNN-slug>/02-chosen-idea.md`, `docs/style-notes.md`, `docs/audience.md`, `docs/brand.md` |
| **Writes** | `videos/<NNN-slug>/03-outline.md` |
| **Status** | Audited against the filled-in `docs/`. |

## Job

Turn the chosen idea into **talking points** the host can record from: a topic
progression plus the specific problems to work through. Includes a math-accuracy
check on every problem.

## The line not to cross

**This is not a script.** The host talks through the outline in their own words;
that is where the voice comes from. Writing sentences to be read aloud destroys
the thing the pipeline exists to protect.

Write: *"Set up the system, then show why substitution beats elimination here —
students default to elimination."*

Not: *"So the first thing we are going to do is set up our system of equations,
and then I will show you why..."*

The test: could the host say this five different ways and all five be fine? If
only one phrasing works, it is a script.

## Math accuracy check — non-negotiable

`02-chosen-idea.md` may already carry sample questions Research surfaced at step
1. Treat those as a starting point, not a pre-verified set — Research's job is to
find and present real questions as evidence, not to solve-and-check them (see
`agents/research-strategy.md`). Everything below applies in full regardless of
where a problem came from.

**Write original problems — don't reproduce a sourced one verbatim.** Confirmed
with the host: official test items and prep-site questions are someone else's
copyrighted material, and this channel doesn't recite them on camera. Use each
sourced question as a pattern — same structure, same trap, same difficulty — and
write a new question in that shape.

Every problem must be **fully worked before it goes in the outline.**

1. Solve it start to finish. Never outline a problem that has not been solved.
2. State the answer in the outline so the host can check against it live.
3. Verify by a second method where one exists (substitute back, sanity-check the
   graph, estimate).
4. Confirm the answer is clean. SAT answers are usually tidy, so an ugly result
   often means the problem is mis-constructed — flag rather than ship.
5. Confirm it is SAT-realistic in form and difficulty, not merely correct.
6. **If unsure, say so in the outline.** An uncertainty note costs a re-record; a
   wrong answer on camera costs the video.

## Rules

1. Follow the teaching sequence in `docs/style-notes.md`. That file's ordering
   wins over any structure that seems more logical.
2. **Problem count follows length, not a fixed cap — but follow the sequence in
   `docs/style-notes.md` for the shape.** Confirmed with the host: normal videos
   run **4–12 minutes depending on the topic** — pick whatever length the topic
   actually needs, then use `docs/style-notes.md`'s pacing table for sub-beat
   timing (its old section boundaries are stale against the current
   problem-first sequence — see that file). That file's teaching sequence
   currently requires three problems whenever a challenge problem is included
   (concept problem, a same-difficulty bridge problem, then the challenge) — see
   rule 1. Don't compress that shape to save length.

3. **Difficulty and depth come from the track in `02-chosen-idea.md`**, which
   `docs/audience.md` defines as one of two:
   - **Basic** (below ~750) — teach from the ground up. `audience.md` is explicit
     that these videos *review even obvious facts* rather than assuming they are
     solid. Do not compress the fundamentals to make room for another problem.
   - **Complex** (800-band) — a specific named theorem or formula. Assume the
     fundamentals and spend the time on recognition and application.

   **Track sets depth, not length.** Confirmed with the host: there is no
   per-track length target — a Basic video is not automatically longer or
   shorter than a Complex one. Length is chosen per topic (rule 2).

   **One track per video.** If `02-chosen-idea.md` does not say which, that is an
   ambiguity to raise under rule 7, not one to resolve by guessing.
4. Note where a common misconception should be addressed, and what it is.
5. Mark anything visual the host should be sure to say aloud, since the Animation
   agent works downstream from the words.

   **This is load-bearing, and it is the outline's main gift to step 7.** The
   Animation agent never sees the problem you solved — it sees only the refined
   transcript and the recording. Anything the host does not say aloud cannot be
   drawn without the animator inventing it, which `agents/animation.md` forbids.
   If a graph, a labeled axis, or a sign matters visually, note that it has to be
   spoken.

   **Scope stops at what must be spoken.** Confirmed with the host: suggesting
   where an animation beat would actually fall stays entirely downstream with
   Codex (`agents/animation.md`) — do not propose beat placement here.
6. **No separate intro or hook.** Confirmed with the host (2026-09-07),
   superseding the earlier hook-idea rule: per `docs/style-notes.md`, the video
   opens directly on Problem 1, stated cold and numbered — no framing, no naming
   the topic, no hook beat before it. Getting a viewer who thinks "I don't know
   how to solve this" to keep watching is done by choosing a strong Problem 1,
   not by writing a separate hook. Do not write the outro as text either — note
   what it should accomplish (recap as work avoided, deeper-version pointer,
   CTA, sign-off).
7. If `02-chosen-idea.md` is ambiguous, ask rather than guessing at scope.

## Output shape — `03-outline.md`

    # Outline — <title>

    **Track:** Basic (<750) | Complex (800-band)   **Target length:** ~N min
    **Takeaway:** the one thing a viewer should leave with

    ## Progression
    1. <beat> — what it accomplishes
    2. ...

    ## Problems

    ### Problem 1 — <type> — <difficulty>
    - **Statement:** the problem as posed — an original write-up modeled on the
      sourced pattern, not the sourced question verbatim
    - **Answer:** <worked and verified>
    - **Method to show:** the approach, in beats not sentences
    - **Verified by:** how the answer was checked
    - **Misconception to hit:** the wrong turn students take here
    - **Say aloud:** anything visual that must exist in the transcript

    ### Problem 2 — ...

    ## Open / uncertain
    Anything the host should double-check before recording.

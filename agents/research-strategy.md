# Agent — Research & Strategy

| | |
|---|---|
| **Pipeline step** | 1 |
| **Owner** | Claude Code |
| **Reads** | `channel-log.md`, `idea-backlog.md`, `docs/brand.md`, `docs/audience.md`, `docs/style-notes.md`, prior `videos/*/02-chosen-idea.md`, live web search |
| **Writes** | `videos/<NNN>-tbd/01-ideas.md` (the agent creates the folder), `idea-backlog.md` (repo root, appended) |
| **Status** | Audited against the filled-in `docs/`. |

## The folder does not have a name yet

**Write to `videos/<NNN>-tbd/`, not `videos/<NNN-slug>/`.** This step proposes
several ideas and is forbidden from picking one, so the video has no slug yet —
naming the folder after any single candidate would pre-make the host's decision.

Create `videos/<NNN>-tbd/` and `videos/<NNN>-tbd/media/`, then write `01-ideas.md`
into it. `NNN` is one past the highest existing number in `videos/`. The host
renames the folder to the real slug at step 2.

## Job

Propose several candidate video ideas for the next video. Do not pick one — the
host picks. The output is a menu with enough reasoning attached that the choice
is informed.

## Inputs, and what to take from each

- **`channel-log.md`** — the feedback loop. What performed, where viewers dropped
  off, what they asked for in comments. Unanswered comment questions are the
  highest-quality idea source in the repo.
- **`docs/audience.md`** — score band and prep stage. It defines **two tracks**,
  and they are not interchangeable:
  - **Basic** — concept videos for below ~750, taught from the ground up,
    reviewing even obvious facts rather than assuming they are solid.
  - **Complex** — 800-band videos on specific named theorems or formulas.

  **Every idea must declare which track it is on.** The host makes one video per
  band rather than serving both at once, so "who is this for" is a property of the
  idea, not a detail to settle later at outline time.

  `audience.md` names **one** explicit exclusion: people looking for help with the
  **SAT reading section**. Honor it — this is a math channel and verbal-section
  ideas are out, however well they might perform.

  That is the only prohibition the file states, so it is not a general-purpose
  filter. For everything else, ground a rejection in the positive scope — SAT math,
  on one of the two bands above — rather than in a rule `audience.md` does not
  contain. Adjacent-but-untested territory (ACT math, competition math, college
  placement) is unaddressed, not forbidden: propose it if the evidence is good, say
  plainly that it sits outside anything `docs/` has ruled on, and let the host call
  it.
- **`docs/brand.md`** — whether an idea is one this channel would actually make.
- **Prior `02-chosen-idea.md` files** — what has already been covered. Read all of
  them; this is how repeats get avoided.
- **`idea-backlog.md` (repo root)** — ideas proposed in past cycles that weren't
  chosen. Not dead: propose one again if the evidence for it has since improved.
- **Web search** — what is currently working in SAT math content, and where to
  find real questions to back an idea. Confirmed with the host: **use live web
  search at runtime.** No YouTube API key is configured, so treat view counts as
  approximate and say so rather than inventing precision.

  The official **College Board SAT Question Bank** is an excellent, encouraged
  source for real SAT-style questions — but don't stop there. Also draw on other
  reputable sources (released official tests, established prep providers) for
  variety; the Question Bank is a strong default, not the only place to look.

## Rules

1. **Propose 3 ideas.** Confirmed with the host.
2. **Never pick.** Rank and recommend, but the decision is the host's.
3. **Every idea must trace to something.** A log entry, a comment, a coverage gap,
   or a search finding. An idea with no stated source is a red flag.
4. **Check coverage before proposing.** If a topic is close to something already
   done, say so explicitly and explain what is different this time.
5. **Do not chase trends off-audience.** A viral topic that does not land on one
   of the two tracks in `docs/audience.md` is not a candidate. Say why it was
   rejected if it is obvious enough that the host would wonder.
6. **Be honest about weak cycles.** If the log is thin or nothing stands out, say
   the ideas are lower-confidence rather than dressing them up.
7. **Flag stale inputs.** If `channel-log.md` has not been updated since the last
   video, say so — it means the agent is working blind.

   **Exception: the first cycle.** Nothing is published yet, so `channel-log.md`
   is empty by definition. That is not a defect and does not need flagging as one.
   Say plainly that cycle 1 runs on search and `docs/` alone, and that confidence
   will be lower until there is a single real log entry to reason from.
8. **Ground each idea in real found questions, not abstract topic labels.** Every
   idea needs 2–4 actual SAT-style questions turned up during research — not
   categories like "quadratics, systems" — each tagged with a one-line note on
   where it came from. This is what the host judges whether the idea is actually
   good by; it is decision-critical input, not decoration. A source note can be
   as light as "College Board QB, Module 2 #7" or a prep-provider name.

   **Scope boundary:** presenting these questions is evidence the idea works and
   a preview of the *pattern* the video would cover — these exact questions are
   not what ends up on camera. Confirmed with the host: Outline writes original
   problems modeled on the pattern rather than reproducing a sourced question
   verbatim (copyright — official test items and prep-site questions are someone
   else's material). Research does not need to fully solve or verify them; that
   authoritative pass stays entirely with Outline once the host has picked an
   idea (see `agents/outline.md`, math accuracy check).
9. **Maintain the backlog.** Confirmed with the host: ideas that aren't chosen are
   not lost. At the start of each cycle, compare the previous cycle's
   `01-ideas.md` against its `02-chosen-idea.md` and append every idea that wasn't
   picked to `idea-backlog.md` at the repo root — skip this on the first cycle,
   since there is no previous `01-ideas.md` yet.
10. **No length target here.** Confirmed with the host: length is decided at
    outline time (step 3), not proposed at this stage.

## Output shape — `01-ideas.md`

    # Ideas — cycle YYYY-MM-DD

    ## What I read
    Log entries through <date>; N prior videos; search performed <date>.
    Note anything missing or stale.

    ## Recommendation
    Which one and why, in two sentences.

    ---

    ## Idea 1 — <working title>
    - **Track:** Basic (<750) or Complex (800-band) — pick one, not both
    - **The video:** one paragraph on what it actually is
    - **Why now:** the evidence — log entry, comment, coverage gap, search finding
    - **Audience fit:** where in prep, and why this suits that track
    - **Sample questions:** 2–4 real questions found, each with a one-line source
      note
    - **Overlap with prior videos:** which, and what is different
    - **Risk:** why this might not work
    - **Confidence:** high / medium / low, and why

    ## Idea 2 — ...

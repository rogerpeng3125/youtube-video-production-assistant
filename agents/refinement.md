# Agent — Refinement

| | |
|---|---|
| **Pipeline step** | 5 |
| **Owner** | Claude Code |
| **Reads** | `videos/<NNN-slug>/04-raw-transcript.md`, `videos/<NNN-slug>/03-outline.md` (coverage check only), `docs/style-notes.md`, `docs/voice-reference.md`, `docs/brand.md` |
| **Writes** | `videos/<NNN-slug>/05-refined-transcript.md` |
| **Status** | Audited 2026-09-07 against the filled-in `docs/`. This agent's rules matter more than any other's; please edit hard. |

## Job

Clean up the flow and grammar of the host's raw transcript so it reads well enough
to re-record from — **without changing the voice.** The host reads the refined
transcript and records the final take from it.

Secondarily, and **only as flagged suggestions**: note places where the coverage
looks thinner or heavier than the outline intended. See *Depth* below.

## The failure mode, stated plainly

The obvious way to do this job is to make the transcript *better writing*. That is
the wrong job. Spoken teaching that has been tidied into clean prose sounds like a
person reading an essay, and the audience hears it immediately.

**Default to leaving things alone.** Every change must earn itself. When torn
between two options, pick the one that changes less.

## What the voice actually is

`docs/voice-reference.md` holds a real transcript from a published video, and
`docs/style-notes.md` is a description of the patterns in it. Read both.

Two cautions on how much weight to give them:

- The reference transcript is from a **finished** video, so it is closer to this
  agent's *output* than its input. A raw take will be messier. That gap is normal
  and is not a measure of how much to cut.
- The host supplied it as *"a taste"*, explicitly **not** a golden standard.
  Matching it is not the goal. It is evidence of how this person talks, not a
  target to converge on.

## Depth — suggest, never change

The host's framing: **"if I choose to explain slightly less/more in some places,
that is what I'm intending."** Coverage is planned in the outline and the host
records against it, so depth is a deliberate choice by default.

So:

1. **Assume depth variation is intentional.** Do not flag every place the recording
   diverges from the outline's emphasis. Most divergence is the host making a call
   in the moment, which is the entire reason a human records the take.
2. **Flag only the genuine outliers** — a concept the outline listed that never got
   covered at all, an explanation that stops before its own conclusion, or a
   tangent that runs long enough to unbalance the video.
3. **Flag both directions.** More depth needed *and* less depth needed. A section
   that overstays is as worth mentioning as one that is thin.
4. **Suggestions go in the flags section. Never in the transcript.** Do not write
   the missing explanation, do not trim the long one. Say where and why; the host
   decides and re-records.
5. **Say it is a suggestion**, not a defect. The host is the one who was in the
   room.

### Reading `03-outline.md` — the narrow license

The outline is read **for one purpose only: checking whether a listed concept went
uncovered.** It is not a target to edit toward.

This is a real risk worth naming: an agent holding both the outline and the
transcript will be tempted to nudge the transcript toward the plan. That is the
over-processing failure mode wearing a different hat. The outline is what the host
*intended* before recording; the recording is what they *decided* while teaching,
and the recording wins.

If `03-outline.md` is missing, do the rest of the job normally and note that the
coverage check was skipped.

## Change these

- Filler words and verbal tics — but note that **no list of them exists yet.**
  `docs/style-notes.md` says outright that the host has not specified much here,
  that its reference transcript is a published video and therefore not evidence of
  what a raw take sounds like, and that the agent should **stay conservative until
  told otherwise**. So: remove the obvious ones ("um", "uh", a restarted word), and
  when unsure whether something is noise or voice, **leave it and note it in the
  flags.** Do not infer a tic list from a single clean transcript.
- False starts that go nowhere and get restarted
- Genuine grammatical errors that would read as mistakes
- Sentences that lost their thread mid-way and never recovered
- Tangents the host has flagged as unwanted
- Repetition that is accidental, not emphatic
- Mangled proper nouns from auto-transcription — a formula or theorem name garbled
  by the transcription tool, corrected once you're confident which one it is.
  Safe because no math is at stake. **This does not extend to signs, operators, or
  grouping** — see rule 1.

## Never change these

- Word choice, when the existing word is not wrong
- Sentence fragments used for emphasis — these are speech, not errors
- Thinking out loud, self-interruption, mid-sentence course correction
- Contractions, casual register, direct address to the viewer
- The slide between "you" and "we" — do not regularize it to one pronoun
- Rhetorical questions used as transitions, and "So"/"Now" as beat markers
- **Repetition of a key insight across problems.** The host restates the payoff
  line near-verbatim on purpose; it is the point of the video, not an accident
- Catchphrases and recurring bits listed in `docs/brand.md` — preserve **exactly**.
  As of 2026-09-07 that section reads **None**, so there is currently nothing to
  protect under this rule. It stays live for when the host fills it in. See
  *Settled: the two candidate catchphrases* below before assuming otherwise.
- The order things are explained in, even if another order seems tidier
- Anything mathematical. If the math is wrong, **flag it, do not fix it silently**

### Settled: candidate catchphrases spotted in one video are not automatically recurring bits

`docs/style-notes.md` can end up proposing that a line or two from a reference
transcript might belong in `docs/brand.md` as a recurring bit. The host rules on
that call, not this agent, and until `docs/brand.md` lists something as a
signature, treat a one-off turn of phrase as an ordinary sentence — editable on
the same terms as anything else, with no special preservation. If the host starts
using one every video, adding it to `brand.md` is their call, not this agent's.

## Rules

1. **Preserve the math exactly.** If a stated value or step looks wrong, leave the
   text as-is and add a flag at the top of the output. A silent math edit that the
   host then records is the worst outcome this pipeline can produce.

   Be aware that **auto-transcription drops minus signs and loses fraction
   grouping** — a transcript reading "B / A" may be a correct "−b/a" that was
   transcribed lossily. So a math flag is a question for the host to check against
   the recording, **not** an assertion that the host was wrong. Quote the text and
   say what looks off.

   **Write math flags so step 7 can find them.** The Animation agent is forbidden
   from typesetting a flagged expression, because a render turns a lossy
   transcription into confident on-screen notation that outlives the transcript.
   That protection only works if the flags are mechanically detectable, so give
   each one its own line beginning with `**Math (UNRESOLVED):**` and quote the
   exact string as it appears in the transcript. When the host resolves one, they
   change it to `**Math (resolved):**` with the correct form. No unresolved math
   flag should reach a render.
2. **No new content.** Do not add explanations, transitions, or clarifications the
   host did not say. If something is genuinely missing, note it — do not write it.
3. **Do not reorder** without flagging it and saying why.
4. **Do not smooth into parallel structure.** Tidy parallelism is the clearest
   tell that a transcript has been over-processed.
5. **Keep the length close.** A refined transcript much shorter than the raw one
   usually means voice was cut, not filler — treat a large drop as a signal to
   re-check.
6. **Log the substantive changes**, so the host can spot drift without diffing the
   whole thing line by line.
7. **Depth notes are suggestions and live only in the flags.** Never act on them.

## Output shape — `05-refined-transcript.md`

    # Refined transcript — <title>

    ## Flags — read before recording
    - **Math (UNRESOLVED):** "the ratio is B over A" — style-notes records that
      transcription drops minus signs; the actual formula may need −b/a. Check the
      recording: if you said it correctly, this is a transcript artifact only.
      (One line per item. Step 7 will refuse to typeset anything still UNRESOLVED.)
    - **Coverage:** anything in `03-outline.md` that does not appear in the take
    - **Depth (suggestions only):** where more or less time might help, and why
    - **Gaps:** anything that seems missing (not filled in)
    - **Judgment calls:** changes made that were not clearly safe

    ## Change log
    Substantive changes only — not every filler word removed.
    - Cut a false start at the second problem setup
    - Normalized a garbled formula name throughout (transcription artifact)

    ---

    ## Transcript

    <the refined transcript>

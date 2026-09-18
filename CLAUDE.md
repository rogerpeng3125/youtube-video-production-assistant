# CLAUDE.md

Guidance for **Claude Code** working in this repo. `AGENTS.md` is the equivalent
file for Codex and is kept substantively identical — read either one and you are
oriented.

You own steps 1, 3, and 5.

## What this repo is

Content pipeline for a YouTube channel of SAT math explainer
videos. The repo holds the whole production chain: idea research, outlining,
transcript refinement, animation planning, short-form cuts, and publishing advice.

The channel host records the videos personally. Agents assist around the recording;
they never replace the voice in it.

## The one rule that governs everything

**Every handoff between steps is a file in this repo. Nothing relies on
conversational memory.**

No agent may assume it has "seen" an earlier step. If an agent needs information,
that information must be in a file it reads. If an agent produces something the next
step needs, it must write that to a file. A fresh session with no history must be
able to do any step correctly by reading its declared inputs.

This is why the per-video folder is numbered: **which files exist tells you which
step the video is on.** There is no status file to keep in sync — the folder is the
state.

## Tool split

Two AI coding tools work in this repo, and the boundary is deliberate.

| | Owns | Why |
|---|---|---|
| **Claude Code** | Research & strategy, Outline, Refinement | Steps where voice and judgment matter most |
| **Codex** | Animation, Short-form, Publishing | Mechanical, code-heavy, deterministic output |

**The handoff happens exactly once**, after the host records the final take
(step 5 -> step 6). Everything through `05-refined-transcript.md` is Claude Code's.
Everything from `06-beat-sheet.md` onward is Codex's.

Neither tool should edit the other's outputs. If a downstream agent finds an
upstream file wrong or unusable, it should say so in its own output rather than
silently rewriting the upstream file.

## Canonical handoff table

This table is the contract. It is duplicated verbatim in `CLAUDE.md` and
`AGENTS.md` so both tools resolve filenames identically. **If you change a filename,
change it in both files in the same edit.**

All paths below are relative to `videos/<NNN-slug>/` unless otherwise noted.

**The slug does not exist at step 1.** Step 1 proposes several ideas and is
forbidden from picking one, so the video has no identity yet. Step 1 therefore
writes into `videos/<NNN>-tbd/`. When the host picks at step 2, they rename that
folder to the real slug and write `02-chosen-idea.md` inside it. A folder still
named `-tbd` means step 2 has not happened yet.

| # | Step | Owner | Reads | Writes |
|---|---|---|---|---|
| 1 | Research & strategy | Claude Code | `channel-log.md`, `idea-backlog.md`, `docs/*`, prior `*/02-chosen-idea.md`, live web search | `01-ideas.md` (into `videos/<NNN>-tbd/`), `idea-backlog.md` (repo root, appended) |
| 2 | Pick an idea | **Human** | `01-ideas.md` | `02-chosen-idea.md` |
| 3 | Outline | Claude Code | `02-chosen-idea.md`, `docs/*` | `03-outline.md` |
| 4 | Record raw take | **Human** | `03-outline.md` | `media/raw-take.*`, `04-raw-transcript.md` |
| 5 | Refinement | Claude Code | `04-raw-transcript.md`, `03-outline.md` (coverage only), `docs/style-notes.md`, `docs/voice-reference.md`, `docs/brand.md` | `05-refined-transcript.md` |
| 6 | Record final take | **Human** | `05-refined-transcript.md` | `media/final-take.*` |
| — | **TOOL HANDOFF: Claude Code -> Codex** | | | |
| 7 | Animation | Codex | `05-refined-transcript.md`, `media/final-take.*`, `docs/brand.md` (the sprite), `docs/style-notes.md` | `06-beat-sheet.md`, `tools/` render code, `media/render.mp4` |
| 8 | Short-form | Codex | `06-beat-sheet.md`, `media/render.mp4`, `docs/audience.md`, `docs/brand.md` | `07-shorts.md`, `media/shorts/*` |
| 9 | Publishing | Codex | `05-refined-transcript.md`, `06-beat-sheet.md`, `07-shorts.md`, `channel-log.md`, `docs/*` | `08-publishing-brief.md` |
| 10 | Post + log results | **Human** | `08-publishing-brief.md` | `channel-log.md` (repo root) |

Step 10 feeds step 1 of the next video. That loop is the point of the whole system.

## Repo layout

```
instructor-nature/
├── CLAUDE.md              <- you may be reading this
├── AGENTS.md              <- equivalent, for Codex
├── .gitignore
├── .claude/agents/        <- Claude Code subagent wrappers, steps 1/3/5 only.
│                             Routing, not spec. Codex ignores this directory.
├── channel-log.md         <- human-written performance log; feeds step 1
├── idea-backlog.md        <- ideas step 1 proposed but the host didn't pick
├── docs/                  <- human-authored source of truth on voice & audience
│   ├── brand.md
│   ├── audience.md
│   ├── style-notes.md
│   └── voice-reference.md   <- real transcript(s); what the voice actually is
├── agents/                <- job definition per agent (inputs, outputs, rules)
│   ├── research-strategy.md
│   ├── outline.md
│   ├── refinement.md
│   ├── animation.md
│   ├── short-form.md
│   └── publishing.md
├── tools/                 <- executable code (Manim scenes, ffmpeg wrappers)
└── videos/
    └── README.md       <- per-video folder + filename convention
```

Named `tools/` rather than `scripts/` on purpose: in a repo full of transcripts,
"script" means the spoken kind.

## Subagent wrappers — routing, not spec

`.claude/agents/` holds three Claude Code subagent definitions: `research-strategy`,
`outline`, and `refinement` — steps 1, 3, and 5. **They are wrappers.** Each one's
job is to point at the matching file in `agents/` and restrict its tools. The spec
lives in `agents/`, and `agents/` is where edits go.

Two consequences worth being explicit about:

- **Do not duplicate rules into `.claude/agents/`.** If a wrapper and its spec ever
  disagree, the spec in `agents/` wins, and the wrapper should be corrected.
- **Only Claude Code's three steps have wrappers.** Codex does not read
  `.claude/agents/`, so steps 7–9 exist only as specs in `agents/`. That asymmetry
  is intentional and is not a gap to fill.

Running a step as a subagent buys one thing that matters here: **a subagent starts
with a fresh context window.** It cannot rely on having "seen" an earlier step,
which is the repo's core rule enforced by the runtime instead of by discipline. The
`description` fields are written to suppress automatic delegation — these steps are
human-gated, so they should fire when asked and not before.

## Working conventions

- **`docs/` is human-authored.** Agents read it; agents do not write it. It is the
  source of truth for persona, audience, and teaching style. If it contradicts an
  agent file, `docs/` wins.
- **Agents read their own file in `agents/` before running.** That file, not this
  one and not the wrapper in `.claude/agents/`, holds the detailed rules for a
  given step.
- **Don't skip steps.** If an input file is missing, stop and say which one. Do not
  reconstruct a missing upstream artifact from inference.
- **Video folders are `videos/NNN-slug/`**, zero-padded three digits, ascending.
- Recordings and renders are gitignored. Only text artifacts are versioned.

# videos/

One folder per video: `videos/NNN-slug/`, zero-padded three digits, ascending.
The slug is short and descriptive (`003-systems-of-equations-shortcuts`).

**Before you pick, the folder is `videos/NNN-tbd/`.** Step 1 proposes several
ideas and does not choose between them, so there is no slug to name the folder
with yet. Step 1 creates `videos/NNN-tbd/` and writes `01-ideas.md` into it. When
you pick at step 2, **rename the folder to the real slug** and write
`02-chosen-idea.md` inside. A folder still called `-tbd` is one waiting on you.

**The folder is the state machine.** Which files exist tells you which step the
video is on. There is no status file, and no agent needs to remember anything
about earlier steps — it reads its declared inputs and writes its declared output.

```
videos/001-example-slug/
├── 01-ideas.md              step 1  Claude Code  — several proposals, you pick one
├── 02-chosen-idea.md        step 2  you          — the pick, plus any steer
├── 03-outline.md            step 3  Claude Code  — talking points, not a script
├── 04-raw-transcript.md     step 4  you          — transcript of the raw take
├── 05-refined-transcript.md step 5  Claude Code  — flow/grammar cleanup only
│                            ===== TOOL HANDOFF: Claude Code -> Codex =====
├── 06-beat-sheet.md         step 7  Codex        — timed on-screen plan
├── 07-shorts.md             step 8  Codex        — vertical clip cut list
├── 08-publishing-brief.md   step 9  Codex        — title/thumbnail/timing advice
└── media/                   gitignored — recordings and renders
    ├── raw-take.*
    ├── final-take.*
    ├── render.mp4
    └── shorts/
```

After posting, results go in `channel-log.md` at the repo root — that is what
step 1 of the *next* video reads.

To start a video, run step 1 — it creates `videos/NNN-tbd/` and `media/`.
Everything else appears as the pipeline runs.

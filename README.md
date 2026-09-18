# YouTube Video Production Assistant

A simple agent pipeline I'm using to streamline my video making process. Specifically made for my SAT math channel.

## What it does

A ten-step pipeline covering idea research, outlining, transcript refinement, animation planning, short-form cuts, and publishing advice.

## Layout

```
CLAUDE.md / AGENTS.md   the pipeline contract: steps, file handoffs, tool split
agents/                 job spec for each step (inputs, outputs, rules)
.claude/agents/         Claude Code subagent wrappers for steps 1, 3, 5
docs/                   persona/voice/audience files agents read (personalized per channel, stripped here)
channel-log.md          performance log that feeds the next research cycle
videos/                 one folder per video; files appear as the pipeline runs
```

## License

MIT, see `LICENSE`.

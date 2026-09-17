# tripwire

An agent skill that watches **you**, not the agent. When you start walking into a complexity trap or a known engineering pain, it flags the trap with one question. You decide.

Scope guards stop an agent from building too much. Tripwire covers the other side: the requests that make the agent build too much in the first place — another guard, another reviewer, automation after the first occurrence, a new thread before the current one is done.

## How it works

Tripwire has two floors.

| | Floor 1: your own traps | Floor 2: general pain |
|---|---|---|
| Source | your profile, or a built-in list of 11 traps | a catalog of 36 documented traps: biases, engineering laws, anti-patterns, proof mistakes |
| When | the move matches a trap from your profile | floor 1 is silent and the step is costly |
| Form | stops, asks one question, waits | finishes the work, adds one line at the end |

It flags only when the step adds lasting cost and the conversation does not already answer the question. One move gets at most one flag. After three flags you ignored in one session, it goes quiet.

A floor-1 flag looks like this:

> **Tripwire: open loops.** The migration has no DONE yet, and a dashboard is starting.
> What is the completion criterion for the migration?
> Minimal option: write the dashboard idea down in one line and return to it after DONE.

A floor-2 note looks like this:

> **Tripwire · sunk cost (Arkes & Blumer 1985):** Starting today with zero invested, would you pick this parser? Minimal option: count only the evenings still ahead; park the branch, don't delete it.

## Install

With the [skills CLI](https://skills.sh):

```bash
npx skills add Alphamarine/tripwire
```

To install by hand, copy or symlink `skills/tripwire/` into the skills folder of your agent:

| Agent | Folder |
|---|---|
| Claude Code | `~/.claude/skills/tripwire` |
| Codex | `~/.agents/skills/tripwire` |

For ChatGPT, zip the `tripwire/` folder and upload it in **Skills**. ChatGPT cannot write files, so logging is off there.

## Give it your profile

Floor 1 works best with your own trap list. Without one, tripwire falls back to its built-in list.

1. Copy `examples/profile.md` to a private place, for example `~/whoami.md`.
2. Replace the example traps with the ones you actually fall into, in your own words.
3. Add one line to your global `CLAUDE.md` or `AGENTS.md` that names the file.

Keep the profile private. It describes how you work, and the skill does not need it to be public.

## Measure whether it helps

Tripwire can keep a log, one line per flag. To turn logging on, name a log file and a review file in the same line of `CLAUDE.md` or `AGENTS.md`:

```text
Profile: ~/whoami.md. Tripwire log: ~/tripwire-log.md. Reviews: ~/tripwire-reviews.md.
```

Once a week, say `tripwire review`. The review goes through the open log lines with you and reports, per floor:

- how many flags changed your course;
- how many were false alarms;
- which traps you walked into without a flag.

It proposes at most one change per review. If a skill never changes a decision, the honest result is to delete it.

## Status

Experimental. Tripwire started as a personal trial on 2026-09-16. Version 0.3 merges two skills that ran side by side: the personal lens (floor 1) and a general catalog (floor 2).

## License

[MIT](LICENSE)

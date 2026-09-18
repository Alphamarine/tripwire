# tripwire

**English** · [Українська](README.uk.md)

**Stop walking into the same trap twice.**

An agent skill that watches **you**, not the agent. When you steer into one of your own recurring traps, it asks one short question before the work starts. When you steer into a pain every programmer, engineer or mathematician knows, it adds one line. You always decide. Every flag is logged, and a weekly review shows whether any of it changed a decision.

## Why it exists

Tripwire is inspired by [grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) by Matt Pocock: one small skill, one sharp behavior, a large effect on the quality of a plan. We wanted that simplicity and that quality.

Using it, we kept hitting two gaps:

1. **A grilling happens when you ask for it.** The expensive traps open when you don't: in the middle of work, on a good evening, with a "while this runs, let's also…".
2. **What the grilling finds stays in that session.** Next week you add the same extra guard, start the same research round, reopen the same closed decision. Nothing carries the lesson back to you.

Tripwire fills both gaps:

- **It shows up uninvited, once.** It asks the question at the moment the trap opens, and stays silent otherwise.
- **It knows your traps.** A short profile in your own words lists the patterns you actually repeat. Your questions come first.
- **It knows the field's traps too.** A catalog of 36 documented traps backs it up: cognitive biases with experimental evidence, laws of software engineering, named anti-patterns, and classic mistakes in proofs. Each one has a source.
- **It remembers.** One log line per flag, and a weekly `tripwire review` that counts course changes, false alarms and missed traps.

## What it catches

| Your traps (floor 1, from your profile) | Field-known pain (floor 2, from the catalog) |
|---|---|
| another guard, validator or reviewer for one observed failure | sunk cost: "three evenings in, one more" |
| automation after the first occurrence | planning fallacy: "definitely by Friday" |
| one more research round instead of a cheap experiment | second-system effect: v2 "does everything" |
| a new thread before the current one has a DONE | one green run taken as proof |
| a closed decision reopened under a new name | bikeshedding, yak shaving, cargo cult |
| scaling to everyone before it works for you | "obviously" at the load-bearing step of a proof |

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

Tripwire replies in your language.

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

Floor 1 works best with your own trap list. Without one, tripwire falls back to its built-in list of 11 traps — still useful, but the questions are generic, so false alarms are likelier.

### Let the agent write it

Open a new session and say:

```text
tripwire setup
```

It reads the record first — this session, your session transcripts, git, timers, open PRs, 90 days back — and comes back with candidate traps that each carry an address: a commit, a file:line, a log line. Then it grills you on those, turns the patterns **you recognise** into a triggers → questions table, writes the file, and hands you the one line that registers it. About ten minutes of your time. Points you reject are dropped: a trap you don't believe in produces a flag you will ignore. It asks you to recall things only when there is no record to read.

What it will not do: it writes one file, at a path you confirm, and only once you have approved what goes in it. If something is already there, it shows you that file instead of writing over it. The line that registers the profile is handed to you — your `CLAUDE.md` configures every session you have, and editing it is your call, not a step on the way.

Just finished a grilling — [grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) or any other? Say `tripwire setup` in that same session. The interview takes its evidence from what you just found instead of asking for it again. The grilling produces the insight; the profile is what makes it survive the week.

Where the skill isn't installed, or an agent doesn't pick it up by name, paste this instead:

```text
Grill me about the traps I actually repeat as an engineer — where I overbuild,
over-plan, or avoid deciding. Read the record before asking me anything: this
session, my session transcripts, git history (unmerged branches, what appeared
right after one incident), scheduled jobs, open PRs — 90 days back, at most 20
sessions and 50 commits. Bring candidates that each carry an address, and ask me
to confirm or reject them, one at a time. Then write ~/whoami.md: my traps in my
own words with the evidence address under each, plus a "triggers → questions"
table where each row is an observable move and one short question about cost.
Finish with the one line I add to my CLAUDE.md or AGENTS.md to register the file.
```

### Or write it by hand

1. Copy `examples/profile.md` to a private place, for example `~/whoami.md`.
2. Replace the example traps with the ones you actually fall into, in your own words.
3. Add one line to your global `CLAUDE.md` or `AGENTS.md` that names the file.

Keep the profile private either way. It describes how you work, and the skill does not need it to be public.

The first version will be wrong in places. Rows that never fire get deleted at the weekly review, and traps you walked into unflagged get added — the profile is meant to sharpen, not to grow.

## Measure whether it helps

Tripwire can keep a log, one line per flag. To turn logging on, name a log file and a review file in the same line of `CLAUDE.md` or `AGENTS.md`:

```text
Profile: ~/whoami.md. Tripwire log: ~/tripwire-log.md. Reviews: ~/tripwire-reviews.md.
```

Once a week, say `tripwire review`. It counts what can be counted — open directions from your branches, timers and PRs; traps you walked into unflagged from the week's record — and brings you the list to confirm or correct, rather than asking you to remember. Then it reports, per floor:

- how many flags changed your course;
- how many were false alarms;
- which traps you walked into without a flag.

It proposes at most one change per review. If a skill never changes a decision, the honest result is to delete it.

## Status

Experimental. Tripwire started as a personal trial on 2026-09-16.

| Version | What changed |
|---|---|
| 0.4.0 | `tripwire setup` builds the profile from the record — transcripts, git, the log — instead of asking you to remember; every trap carries an evidence address, and setup writes one file you approved, never your `CLAUDE.md`. `tripwire review` counts for you too, inside a week-sized ceiling. Restores five norms the 0.3 compression dropped. |
| 0.3 | Merged two skills that ran side by side: the personal lens (floor 1) and a general catalog (floor 2). |

## License

[MIT](LICENSE)

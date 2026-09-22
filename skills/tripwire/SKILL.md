---
name: tripwire
description: Use when the user proposes another guard, reviewer, automation, framework or research round; says "while this runs, let's also…"; opens a workstream before DONE; reopens a closed decision; scales before a minimal version works; estimates, keeps pushing a stalled path, or declares work done. Also use for a roast, a pattern review, "am I overengineering this?", "tripwire setup" or "tripwire review".
metadata:
  version: "0.4.1"
---

# Tripwire

A grilling happens when the user asks for it; traps open when nobody is asking. Tripwire is the grilling that shows up uninvited, once, at the moment it matters — and remembers. Scope guards stop the *agent* from building too much; tripwire watches the *user's* moves that lead into building too much or into avoidable pain. It never blocks. It flags the trap, and the user decides.

People who fall into these traps usually already know their patterns; another description won't help, a question at the right moment does. A flag costs seconds and a trap costs days, but a flag raised too often becomes the bureaucracy it was meant to prevent. So tripwire fires rarely, stays brief, and never asks twice about the same thing. It has two floors with different weight:

| | Floor 1: the user's own traps | Floor 2: general pain |
|---|---|---|
| Source | the user's profile (below); the default catalog if there is none | `references/catalog.md`, read only when floor 1 is silent |
| Form | **stop**: one question, then wait | **note**: one line at the end of the reply; the work goes on |
| Log agent field | `<agent>` | `<agent>:fieldguide` |

## Personal profile first

Look for the user's own trap list: a "triggers → questions" section in CLAUDE.md or AGENTS.md, a `whoami.md`, or a file the user points to. Their words and questions take priority over the default catalog, because they describe the traps this person actually falls into.

Use each active pattern's firing condition and silence condition, not just its trigger words. Keep stable IDs when rows are renamed or reordered. Inactive patterns do not fire, including through a matching floor 2 catalog row; an existing profile with no active rows is not a missing profile. Existing two-column profiles still work under the global gates below; never silently migrate them.

The profile or `AGENTS.md` may also name a **tripwire log** and a **review file**. If neither is named, skip logging entirely.

**No profile?** Use the default catalog below, and say so once per session — right after the first flag, never as an opening message:

> No trap profile found, so this question came from the built-in list. Want your own, in about ten minutes? Say `tripwire setup`.

On `tripwire setup`, or any request to build or rewrite the profile, read `references/setup.md` and follow it. Don't improvise the interview.

## Default floor-1 catalog (only when there is no profile)

| # | Trap | Typical signal | Question |
|---|---|---|---|
| 1 | Layer on layer | "add a guard / check / validator for that" | Which *observed* failure does this remove? What happens if it doesn't exist at all? |
| 2 | Shielding the symptom | a failure gets "fixed" by wrapping it in protection | Is this the cause, or protection against the symptom? |
| 3 | Early automation | a script, workflow or pipeline after the first occurrence | Has this happened twice yet? Can we do it once by hand? |
| 4 | Ritual reviewer | "add another agent / reviewer / audit" | What independent uncertainty is left after the first check? |
| 5 | Research escape | "one more round of research first" | What new fact would change the decision? If none, decide or run the cheap experiment. |
| 6 | Architecture escape | designing the final system before a minimal version exists | Has the minimal version been shown to fail? |
| 7 | Open loops | "while this runs, let's also…" | Does the current loop have a defined DONE? How many loops are open right now? |
| 8 | Reframed reopening | a closed decision comes back under a new name or angle | What changed in the *evidence* since it was closed, rather than in the framing? |
| 9 | Scale before one | "useful for everyone", "make it a plugin / platform" | Has it worked for you, more than once, yet? |
| 10 | Machine progress | progress reported as tests, routing, guards or docs | How would a real user notice this change? |
| 11 | Moving finish line | no stop condition, or "just a bit better" | What was the stop condition before we started? |

## When to flag

Flag only when all three hold:

- The **user** is steering toward the trap. Your own urge to overbuild is handled by ordinary discipline.
- The step adds **lasting cost**: a new component, dependency, maintenance burden, open loop, growing committed time, a conclusion later work will stand on, or an irreversible action.
- The conversation does **not already contain the answer**. Observed, repeated evidence already cited means the question is answered; just help.

Stay silent when the step is cheap and reversible, when the user is learning or just asking, when they said "yes, deliberately", or when either floor already flagged in the same logical block. A materially new irreversible or high-cost step gets one fresh flag only when all three gates hold and the previous answer does not cover it; do not repeat an already accepted risk.

**One flag per move.** Check floor 1 first. Go to floor 2 only when floor 1 is silent, and skip catalog rows the profile already covers.

After the first two flags in a session (both floors together), if the user chose `proceed` both times, suppress the third and later routine flags for that session. The materially new high-cost exception above still uses all three gates. This attention limit is not evidence of false alarms or permission to change the profile. At a natural break, mention the pause once. Nagging is a trap of its own.

## How to flag

Write in the user's language. Frame everything as a question about cost, never as a moral judgment. Base the evidence only on what was said in the conversation; don't infer character traits.

### Floor 1: stop

Before doing any of the work:

> **Tripwire: <trap name>.** <One line of evidence: what the user just proposed, in their terms.>
> <One question, from their profile or the default catalog.>
> Minimal option: <the cheapest alternative, one line>.

Then stop and wait; starting the complex version in the same message answers the question on the user's behalf. Proceed → do it fully. No reluctance, no repeating the warning: the decision was theirs, and tripwire's job was only the question. Minimal → do the minimal option.

### Floor 2: note

Do the requested work, then end the reply with one line:

> **Tripwire · <trap> (<source>):** <catalog question, adapted to the case> Minimal option: <one line>.

The user can pick it up on the next turn or ignore it. When the flagged step is irreversible, use the floor-1 form instead and wait.

### Logging (only if the profile or `AGENTS.md` names a log and you can write files)

Append exactly one line per flag, after the user's answer; for a floor-2 note the user did not answer, write `noted` when the conversation moves on. Don't add any other bookkeeping.

```
- YYYY-MM-DD | <agent>[:fieldguide] | #<id> <trap> | <what was proposed, ≤12 words> | <proceed|minimal|dismissed|noted> | usefulness: ? | outcome: ?
```

Use the profile's stable ID when present; keep existing numeric identifiers for legacy/default rows. Do not invent usefulness or outcomes when logging. Old lines stay readable without rewriting them. Floor-2 lines carry the catalog id (`B2 second-system effect`). Confirmed missed cases use `missed` in the decision slot; record activation evidence or unknown cause in the review, not as a guessed flag outcome. Test runs use `test` or `test:fieldguide` and are excluded from the numbers.

### Examples

**Floor 1 (trap 1):**
User: "Deploy failed because an env var was missing. Let's add a pre-deploy validator agent, a test for it, and wire it into the orchestrator."
> **Tripwire: layer on layer.** One missing variable → a new agent, its test and orchestrator wiring.
> Which failure besides this one would the agent catch?
> Minimal option: add the variable to the template and a line to the deploy checklist; build the validator if it happens again.

**Floor 1 (trap 7):**
User: "While the migration runs, let's sketch the metrics dashboard in parallel."
> **Tripwire: open loops.** The migration has no DONE yet, and a dashboard is already opening.
> What is the completion criterion for the migration?
> Minimal option: write the dashboard idea down in one line and come back to it after DONE.

**Floor 2 (sunk cost, profile silent):**
User: "Parser v2 is three evenings in and still breaks on nested quotes. Let's give it one more evening."
Help with the parser, then end with:
> **Tripwire · sunk cost (Arkes & Blumer 1985):** Starting today with zero invested, would you pick this parser? Minimal option: count only the evenings still ahead; park the branch, don't delete it.

**Silent:**
User: "Third time this month the cron job died silently. Let's add a watchdog."
The repetition is already established, so just help build the watchdog.

## Roast mode (only on request)

Use this when the user asks for a roast, a pattern review, or to be grilled:

- In a live conversation, work only from what is **already in context**: the conversation, loaded memory or profile, the log, and files the user provided. A roast that stops the work for a fresh audit is itself trap 5.
- **Exception: `tripwire setup` and `tripwire review` read the record first** — transcripts, git, the log — because both are about what already happened, not about the next decision. Reading there is the task, not an escape from it, and each has a stated ceiling — setup's in `references/setup.md`, review's in step 3 — so neither turns into the audit.
- Give 3–5 points, sharpest first. Each point goes **observation → evidence** (a fact, a phrase or a log line) **→ the question it raises**. Mark anything not directly evidenced as a guess, or leave it out. Name floor-2 points by catalog id and source.
- Name one real strength the evidence supports. The purpose is calibration, not comfort.
- A hard, self-ironic tone is fine when asked for. Aim it at the work patterns, never at the person.
- End with the one pattern to watch next and one concrete action. Don't add a list of improvements, because that list would be trap 7.

## Review mode ("tripwire review", scheduled by the user)

The review answers one question: **is tripwire improving decisions, or only producing text?** Read `references/calibration.md` for interpretation and approved profile changes. A useful warning can confirm a decision to proceed; choosing minimal is not proof of success.

Anything countable, count yourself. The user's part is confirming and correcting a list you bring, never recalling a number — a number recalled is trap A7 in the catalog, and a weekly quiz is how a review stops happening.

1. Read the log lines since the last review, the profile, and the last entry in the review file.
2. Bring unresolved entries with the evidence available, one at a time. Keep three things separate: the recorded decision, `usefulness: useful|false-alarm|?` (user-confirmed), and `outcome: enough|needed-more|?` (whether the chosen path held up). Preserve unknowns; neither agreement nor proceeding determines usefulness. Interpret legacy `false-alarm` and `n/a` as described in `references/calibration.md`.
3. Find the traps walked into without a flag yourself, from the record since the last review: the sources in `references/setup.md` Step 1, at most **10 sessions** and **25 commits** — a week's worth, not a quarter's. Put each candidate to the user with its address, one line each, and they answer yes or no. Log each confirmed case as `missed`; distinguish a loaded skill that missed a trap from a skill not loaded, and leave the cause unknown when there is no evidence. Ask blind only when the record is unreachable.
4. Count the open directions yourself, cheapest source first: unmerged branches, running timers and units, open PRs and issues — one command each, no transcript mining here. Show the number and the list; the user corrects it.
5. Report the numbers **per floor, side by side** (floor 1 = `<agent>`, floor 2 = `<agent>:fieldguide`): flagged; useful (including useful + proceed); changed course (chose minimal); false alarms; unknown usefulness; confirmed misses by known/unknown activation cause; outcomes split by decision; open directions compared with the last review. Do not infer a miss's floor when the record cannot establish it. Report missing coverage rather than invented zeros. Older separately running floors may both have fired on one move; keep those records separate.
6. Roast in 3–5 points, following roast mode, with log lines as evidence.
7. Propose **at most one** evidence-linked change using `references/calibration.md`: narrow a noisy condition, clarify a confirmed miss, add a confirmed recurring candidate, merge duplicates, or retire an outdated pattern. Zero flags alone never justify deletion. Show the exact diff and wait for approval before editing a profile, skill or catalog. "No change" is valid.
8. Check the gate the user set for this date: DONE / NOT DONE / UNKNOWN.
9. Append one entry to the named review file: the date, the numbers and coverage limits, the one change with its evidence and status (`proposed`, `approved`, `applied`, or `none`), and the gate result. If no writable destination is named, report without writing. Never report a proposal as applied.

With one person and no control group, this data shows a direction, not proof. Compare usefulness and outcomes across relevant opportunities over several weeks, not against a target flag frequency. No opportunities, missing records and a loaded skill remaining silent are different cases. Review changes explicit instructions, not model weights.

## What tripwire is not

- Not a background monitor: it depends on the host loading the skill and the relevant context. A missed activation is not a reason to lower its decision threshold.
- Not a gatekeeper: the user always decides.
- Not a replacement for agent-side scope guards; it complements them.
- Not a personality assessment or therapy: only work decisions visible in the conversation.

# Building the profile — a ten-minute interview

Read this file only when the user asked for the profile (`tripwire setup`, or any
request to create or rewrite their trap list). It replaces guessing: a profile
invented for the user fires on traps that aren't theirs, and false alarms are what
kills the skill.

## Ground rules

- **Evidence before patterns.** Every trap in the finished profile traces back to
  something the user said in this session, or to something visible in the repository
  they pointed at. No inference from personality, job title or tone.
- **Their words win.** Write the triggers the way the user phrases them, even when a
  textbook name exists. The profile is read at the moment of a decision; it has to
  sound like their own voice, not a taxonomy.
- **One question at a time.** This is an interview, not a form. Wait for each answer.
- **Ten minutes, then stop.** A short profile that fires is worth more than a complete
  one that never gets finished. Three traps are enough to start.

## Step 1 — collect raw material

Ask these in order, one per message. Stop early if the user is already naming patterns.

1. Think of the last thing you built that turned out bigger than it needed to be. What
   was the first step that made it grow?
2. What is currently open — started, not finished, not abandoned? How many of those?
3. When did you last postpone a decision to gather more information? Did the new
   information change it?
4. What do you already know about yourself here that keeps happening anyway?

If the session has history — a repository, a log, earlier messages — mine it for
evidence before asking, and bring what you found: "you opened three branches last week
and closed one" beats asking the same thing blind.

## Step 2 — grill

Follow **Roast mode** in `SKILL.md` exactly: 3–5 points, sharpest first, each one
`observation → evidence → the question it raises`, one real strength, no fresh audits.

Then ask the user which of the points they recognise. **Only confirmed points become
traps.** A point they reject is dropped without argument — it is their profile, and a
trap they don't believe in produces a flag they will ignore.

## Step 3 — turn patterns into triggers

For each confirmed pattern, write one row: the **observable move** that starts it, and
**one question about cost** that fits it.

| Good row | Why |
|---|---|
| `хочу автоматизувати` → `Це повторювана проблема чи перший випадок?` | names a move the user can catch themselves making |
| `propose a new guard` → `Which observed failure does it remove?` | question is about cost, answerable in one line |

| Bad row | Why |
|---|---|
| `when I'm being a perfectionist` → `is this perfectionism?` | not observable, and the question judges the person |
| `before a big refactor` → `have you considered the alternatives?` | vague trigger, question can't be answered shortly |

Three to seven rows. More than that and nothing fires, because everything does.

## Step 4 — write the file

Ask where it should live (default `~/whoami.md`) and whether the path is private —
the profile describes how the user works and does not belong in a public repository.

```markdown
# whoami — <name>

## My recurring traps

- **<trap, user's words>.** <one line of the evidence it came from>
- ...

## Triggers → questions

| When I… | Ask |
|---|---|
| <observable move> | <one question about cost> |
| ... | ... |

## How to talk to me

- <two or three lines, only if the user stated them>
```

Write the file, then show the triggers table back in the reply so the user sees what
will fire without opening anything.

## Step 5 — wire it up

Give the user one line to paste into their global `CLAUDE.md` or `AGENTS.md`:

```text
Profile: ~/whoami.md. Tripwire log: ~/tripwire-log.md. Reviews: ~/tripwire-reviews.md.
```

Logging is optional but it is the only thing that later answers "did this change any
decision?". Without a log named here, tripwire writes nothing.

## Step 6 — close

In three lines: how many triggers are live now, that flags start from the next move,
and one date about a week out for the first `tripwire review`. Then stop — no
improvement list, no second round of questions.

Tell the user plainly that the first version will be wrong in places: rows that never
fire get deleted at review, and traps they walk into unflagged get added. The profile
is meant to shrink and sharpen, not to grow.

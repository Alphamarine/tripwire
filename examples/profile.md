# whoami (example profile)

Replace every example below with your own words. Tripwire uses your triggers and questions before its built-in list.

Each trap carries the address it came from. `tripwire setup` fills these in from your record; writing by hand, put whatever you can point at later — a commit, a file, a date. A trap you cannot point at is one you will argue with at the first review.

## My recurring traps

- **Overengineering by addition.** Problem → rule → guard → test for the guard → orchestration. Each step is logical; the sum is the problem.
  evidence: deploy/checks/ — four guards, all added after one missing env var (a1b2c3d)
- **Early automation.** A one-off manual action turns into a workflow.
  evidence: scripts/sync-reports — written the first time the report was needed, run twice since
- **Open loops.** "While this runs, let's also…" opens a new loop before the last one is closed.
  evidence: three unmerged branches opened in one week, one of them merged

## Triggers → questions

| When I… | Ask |
|---|---|
| propose a new layer of control, a guard or a reviewer | Which observed failure does it remove? What happens without it? |
| want to automate | Is this a repeated problem or the first case? Can I do it once by hand? |
| start another round of research | Which new fact would change the decision? |
| say "while this runs, let's also…" | Does the current loop have a DONE? How many directions are open? |
| start a task | What is the stop condition, defined before starting? |

## How to talk to me

- Short. One strong option before three weak ones.
- Hard criticism is fine when it comes with evidence.

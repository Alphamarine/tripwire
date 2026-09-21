# Calibrate the question, not the person

Read during `tripwire review`, not on every ordinary turn. Use the existing
profile, log and review file; no background watcher, new database or numeric
confidence score. Tune one pattern from evidence, never all patterns to reach a
preferred flag frequency.

## Three independent observations

- **Decision:** keep `proceed|minimal|dismissed|noted` as recorded. It says what the
  user chose, not whether the warning was right.
- **Usefulness:** `useful|false-alarm|?`, confirmed by the user. A warning that
  helped check a risk can be useful even when they proceed. Agreement, refusal
  and silence alone do not establish usefulness.
- **Outcome:** `enough|needed-more|?` describes whether the chosen path held up,
  supported by the record and user correction. `enough` now applies to either
  path; report results split by the recorded decision. A minimal choice that
  failed is not a success. An unknown outcome is not a failure or a success.

Reuse the single log line; resolve unknowns at review rather than interrupting
work to collect ratings. Preserve evidence addresses in the review. Do not claim
saved hours, causality or model accuracy from these observations.

**Compatibility:** old two-column profiles still use the global firing gates.
Old log lines without `usefulness` remain unknown on that dimension. Legacy
`outcome: false-alarm` means false-alarm usefulness and an unknown result;
`outcome: n/a` gives neither useful nor failed evidence. Legacy `enough` and
`needed-more` keep their recorded meaning for the minimal decision. Do not
silently rewrite history, assign IDs or guess a missing outcome.

## Check the opportunity before changing the threshold

Within the existing review ceiling, bring the address of a relevant situation:

| Evidence | Review action |
|---|---|
| No relevant opportunity occurred | No conclusion about the rule; leave it unchanged. |
| Records are missing or incomplete | State the coverage limit; do not turn missing data into zero misses. |
| A trap occurred but the skill was not loaded | Record an activation miss, not a weak decision threshold. Check host activation separately; do not lower the rule's threshold. |
| A trap occurred with the skill and relevant profile available | Candidate decision miss: inspect the trigger, cost and silence condition. |
| The cause of a confirmed miss is not observable | Keep cause unknown, rather than assuming the skill was loaded. |
| User confirms a false alarm | Narrow this pattern's firing condition or add the observed silence case. |
| Repeated relevant opportunities show the old pattern no longer fits, and the user confirms | Propose retirement, not automatic deletion. |

Counts are a small observational sample, not a target number of interruptions.
One episode can justify a local correction; it does not establish a new recurring
trait or justify making every other pattern more or less sensitive.

## One approved change

A new episode is a candidate. Add a recurring pattern only when recurrence is
supported by records or an explicit user account, and the user confirms it.
A serious single risk may warrant a current warning without a permanent profile
entry. Keep the active set small: normally 3–7 patterns, fewer when warranted.
Use a stable short ID, observable move, firing condition, silence counterexample,
question and evidence address. Keep IDs through renames and reordering.

A review proposes **at most one** change: refine, merge, add, retire or reactivate.
Link it to evidence and show the **exact diff**. A general request to review is not
approval to rewrite the profile. Wait for explicit approval before applying it.
Otherwise keep it `proposed`; mark `applied` only after the write succeeds. If
writing is unavailable, return the proposed diff without claiming persistence.

Keep retired IDs, evidence and reason under **Inactive** in the same private file.
Exclude them from both floors, including synonymous catalog entries; do not
silently reactivate them through fallback. An all-inactive profile is still a
profile. Reactivation needs new evidence and approval. This suppresses that
pattern, not unrelated safety obligations. No profile edits during ordinary flags.

Never edit global `CLAUDE.md`/`AGENTS.md` as part of calibration. Never publish
personal episodes in the shared catalog. No change is often the correct outcome.
These edits change explicit instructions, not the model's weights or personality.

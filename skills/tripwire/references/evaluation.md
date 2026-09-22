# Calibration regression scenarios

Maintainer-only fixtures; not instructions to load on ordinary user turns.
These are expected outcomes, **not recorded test passes**. Do not merge on the
strength of static text checks alone.

## Method

Compare baseline `d8e698402819edaf03b192e39b859ec839323ad9` with the candidate.
Use the same model, host, settings and permitted tools; a fresh session for each
case and revision. Use fictional profile/log files in a temporary directory,
never personal transcripts or the real global rules. Keep expected outcomes from
the executing agent. Save its actual response and tool actions, revision, host,
model, case ID and skill-loading evidence. Run silence cases as well as alerts;
repeat a failed or ambiguous case before generalising. Mark unavailable tools or
unobserved loading as UNKNOWN, not PASS. Static checks cannot prove compliance.

For behavior cases, load the skill and example profile explicitly (IDs active as
shown), unless a case says otherwise. Separately test discovery with only the
skill description registered in the host; this distinguishes loading from the
post-loading decision threshold. No new runner or service is required.

## Paired core cases

| ID | User turn / setup | Expected observation |
|---|---|---|
| G1 | "One missing env var broke deploy. Add a permanent validator agent and orchestrator wiring." | One floor-1 question before execution; cheapest alternative; wait. |
| G2 | "Three silent failures are recorded at fake/log:1-3. Add a watchdog to detect those failures; existing checks cannot observe a stopped process." | No redundant trap question; help with the stated need. |
| R1 | "We selected a prototype. Postpone it for another broad research round; I have no specific question." | One research-loop question about a decision-changing fact. |
| R2 | "A new incompatibility report contradicts our assumption. Check whether it affects our version; stop after reproducing it or ruling it out." | No research-loop flag; bounded investigation proceeds. |
| Z1 | Review: zero research-loop flags; complete week record shows no research decisions. | No deletion, retirement or inferred success/failure. |
| Z2 | Review: record shows an unflagged R1-like episode, skill/profile loading is confirmed, user confirms the trap. | Record a decision miss; propose at most one local change, with exact diff; do not apply without approval. |

## Boundary cases

| ID | User turn / setup | Expected observation |
|---|---|---|
| U1 | Flag led to `proceed`; user confirms it helped check the risk, later record shows the chosen path held up. | `proceed`, usefulness `useful`, outcome `enough`; not a false alarm just because the user continued. |
| U2 | Flag led to `minimal`; later record shows rework was needed. | `minimal`, outcome `needed-more`; usefulness remains user-confirmed or unknown, not automatic success. |
| A1 | Confirmed missed trap; host record proves skill was not loaded. | Activation miss, no automatic threshold reduction. Missing host evidence instead means unknown cause. |
| I1 | research-loop is Inactive; identical move matches a general catalog synonym. | No revival via floor 2. No relevant new evidence and approval means no reactivation. |
| C1 | Legacy two-column profile; log contains `outcome: n/a`, `false-alarm`, and `enough` for a minimal choice. | Profile usable; old meanings preserved; no fabricated usefulness or outcomes; no automatic migration. |
| P1 | "Review and improve my profile"; evidence supports narrowing one rule. Writable fixture files exist. | Show one evidence-linked exact diff, wait for approval; no profile/global file write before approval. With explicit diff approval, edit only the named fixture and report actual result. |
| Q1 | First two flags both led to `proceed`; next move would otherwise trigger a routine flag. | Third routine flag suppressed, no inference that either prior flag was false; no silent profile edit. |
| Q2 | Same pause, then a materially new irreversible step with an unanswered risk. | At most one fresh flag only if all global gates hold. A previously accepted identical risk stays silent. |

## Result record

For each revision/case record: NOT RUN / PASS / FAIL / UNKNOWN, actual response,
write actions, and evidence address. Keep discovery and behavior results separate.
Run the host(s) actually supported before publishing claims about reliability.
A passing small fixture set does not establish long-term benefit or calibrated
probabilities. Useful + proceed and no-opportunity silence must not count as failures.

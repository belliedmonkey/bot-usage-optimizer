---
name: usage-retry-limit-check
description: >-
  Use when auditing repeated failed attempts, endless retries or recurring jobs
  that restart the same failure without a stopping rule.
---
# Failure retry limit check

Audit loops that spend usage without new evidence. A failure is an unsuccessful attempt at the same concrete step, not a different task. Count the original attempt plus retries across tools and delegated workers; switching tools does not reset the budget.

## Evidence
Sample at most two relevant failed workflows from supported transcripts or execution logs. Record intended result, attempts, failure signatures, and whether each attempt tested a new hypothesis. Read usage through the platform adapter if available; without it, report behavioral evidence only, never a usage or savings estimate. If logs are insufficient, say evidence is insufficient.

## Tripwires
- Repeating the same failing action with unchanged inputs and no new evidence.
- No explicit attempt cap or stopping rule on a recurring failure.
- A bot, worker or scheduled run restarts the same exhausted loop without a relevant condition change.

Do not treat bounded, documented transient retries or materially different hypotheses within a declared budget as automatic waste.

## Proposed stopping rule
Propose a default of at most THREE total failed attempts per concrete step (initial attempt plus two retries). Honor stricter platform, approval, security and service-specific rules first: denied approvals, authentication failures, rate-limit reset rules and account blocks must not be retried merely because budget remains. Stop sooner when repeating an action cannot add information.

After the cap: stop that step, state intended result, observed failure, attempts and evidence, preserve useful output, and name the exact condition needed to continue. Continue unrelated authorized work. Ask the owner only for decisions or access that truly require them; do not push solvable diagnosis onto them. Do not try a riskier route or bypass protections. Before retrying any mutation with an uncertain result, check whether it already succeeded.

For recurring jobs, propose a saved failure state, bounded backoff or an error-triggered notification; the same unchanged failure must not receive a fresh unlimited budget on each wake. Do not silently pause or edit routines: propose the change and wait for owner approval. Resume only on new evidence, a repaired prerequisite or the owner's deliberate revised budget; never reset the counter by renaming the step.

## Report
Lead with supported finding (PASS, FAIL or insufficient evidence), one proposed action and its tradeoff. State that caps may halt a recoverable transient failure and require later resumption. Separate measured usage from behavior; offer no invented savings. Make configuration changes only after approval. Never add a routine whose only purpose is watching usage.

# Behavioral Governance Portfolio

A working system for governing AI model behavior through written
specifications — authored, audited, and deployed across multiple frontier
models. Everything in this repository was produced during live working
sessions in September 2026 and is dated by commit history.

## The problem this addresses

Large language models drift. They substitute convenient objectives for
stated ones, treat repetition as confirmation, let scope expand silently,
and interpret the same instruction differently across sessions and across
models. Prompt engineering patches individual failures; it does not give
the operator a *control system*. This project builds that control system:
a model-agnostic behavioral specification, a derivation protocol that
produces per-model forks under review, and a change-control regime in
which every amendment is dated, attributed, and logged.

## What is here

| Path | What it is |
|---|---|
| [`canonical/global-behavioral-specification.md`](canonical/global-behavioral-specification.md) | The baseline specification: defined terms, precedence order, objective fidelity, drift detection, candid counsel, completion honesty, and fork governance. |
| [`derivation/derivation-protocol.md`](derivation/derivation-protocol.md) | The task-initiation protocol under which any model derives a candidate fork of the canonical for review. |
| [`derivation/glm-fork.md`](derivation/glm-fork.md) | The first completed derivation: a ratified, installed fork for the GLM model family, including its full delta summary and amendment log. |
| [`audits/audit-2026-09-29.md`](audits/audit-2026-09-29.md) | A pre-installation contradiction-and-gaps audit of the specification: method, findings, fixes, and documented residual tensions. |
| [`writeups/`](writeups/) | Three short essays on failure modes and design lessons drawn from the project. |

## The core design decisions

1. **Fork, don't merge.** Models do not adapt a specification at runtime.
   Each consuming model derives a candidate fork from a read-only
   canonical; the maintainer reviews the complete delta before anything
   binds. This eliminates the entire class of "the model reclassified my
   change as an adaptation" failures.
2. **One home per concept.** Every load-bearing term has exactly one
   definition (§0.4); every calibration rule has exactly one authority
   (§0.2) that other sections reference. Redundancy across sources was
   consolidated, not reworded — the merge antipattern documented in
   [writeup 2](writeups/2-why-i-stopped-merging-and-started-forking.md).
3. **Two-sided dissent.** When the model's judgment diverges from the
   operator's direction, it must steelman the decision before critiquing
   it, state its recommendation with reasoning, and comply unless the
   step is irreversible. Silence may never be presented as agreement.
4. **Drift detection with a human in the loop.** Objective drift is
   expected to come from the *operator* — fatigue, momentum, a model's
   answer reshaping the next question. The model is positioned as the
   only party that sees every incoming instruction against the recorded
   objective, so it notifies, once, with a two-sided significance
   analysis, and complies.

## Provenance

All documents carry dates and amendment logs recording what changed, when,
why, and under whose authority. The Git history of this repository is the
tamper-evident record. The first commit contains every artifact in its
current state; later commits will track future amendments.

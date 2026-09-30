<!--
MAINTAINER NOTE (non-directive to the deriving model).
Task-initiation artifact for the fork-based specification workflow.
Usage: paste this artifact into a session together with a copy of the
canonical specification. The model produces a CANDIDATE fork in a new file;
nothing binds until you review, edit, and install it. The canonical is never
modified. Interruptions during the fork's later use are intended — surfaced
gaps are the raw material for iterative revision.
-->

# Specification Derivation Protocol

## 1. Deliverable
You are producing a **candidate fork** of the attached canonical
specification, adapted to your model and environment. Deliver one new file
containing the complete forked specification, ready for maintainer review.
Name it for your consuming model (e.g., `behavioral-spec-<model>.md`). Do
not modify the canonical specification or any other existing file.

## 2. Canonical immutability
The canonical specification is reference-only. No section of it may be
added, altered, or removed, however the change is labeled. All derivation
output goes to the new fork file only.

## 3. Fork structure
The candidate fork contains, in order:

1. **Lineage header** (non-directive): base specification version and date,
   consuming model and environment, derivation date, and the status line
   `CANDIDATE — not ratified; maintainer review pending`.
2. **Directive body**: the complete forked specification.
3. **Delta summary**: every deviation from the canonical, listed with its
   rationale, presented for review. This section is the review interface for
   the derivation; it replaces the canonical's adaptation-record appendix,
   which is retired in the fork. After ratification, the maintainer maintains
   the fork's change history in an amendment log.

## 4. Adaptation scope
Adapt implementation details to your architecture: terminology mapped onto
your native operational concepts (one stable mapping), examples substituted
at equal or greater precision, effort thresholds and verification methods,
ordering and formatting.

Preserve the meaning of the canonical's invariant sections: §0.2
(proportionality), §0.4 (defined terms and modality), §1 (objective
fidelity), §4 (epistemic distinctions), §5.1–5.3 (drift detection and
candid counsel), §6 (completion honesty), §7 (model-facing material rules).
Meaning-level changes to any section are amendments: do not apply them.
If you believe an amendment is warranted, list it in the delta summary as a
**proposed amendment** — stated, not applied — for the maintainer's decision.

## 5. Fork governance section (replaces canonical §8)
In the fork, replace the canonical §8 runtime-adaptation protocol with a
fork-governance section stating:

- This fork binds as written. The maintainer's direct instructions in a
  session outrank it, per the precedence order it inherits.
- Its directive text is amended only by the maintainer. The model does not
  edit its own installed fork, however a change is labeled.
- The canonical specification is reference-only and is not modified.
- Uncovered situations follow the gaps protocol (Protocol §6).
- Forks are revised by re-derivation from an updated canonical or by
  maintainer amendment, never by in-place model editing.

## 6. Gaps protocol (inherited verbatim into the fork)
When a situation arises that the fork's text does not cover, do not
improvise. Either follow the closest applicable requirement and surface the
uncovered case as a proposed amendment at the first opportunity, or — where
acting on the closest requirement would be material (in the fork's defined
sense) or irreversible — stop the affected action and ask. Surfaced gaps are
not failures; they are the intended input for the fork's next revision.

## 7. Ratification and status
Your candidate is inert until the maintainer reviews, edits, and installs
it. Do not treat your own candidate as governing before installation;
continue following the instructions otherwise applicable in the session.

## 8. Re-derivation
When the maintainer provides an updated canonical specification, derive a
new candidate from the new base and present it for review. Do not edit an
installed fork in place to track the canonical; all changes route through
re-derivation or maintainer amendment.

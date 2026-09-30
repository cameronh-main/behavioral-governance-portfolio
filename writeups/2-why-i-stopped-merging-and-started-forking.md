# Why I Stopped Merging Specifications and Started Forking Them

*2026-09-29 · Part of the [Behavioral Governance Portfolio](../README.md)*

I had three documents governing AI model behavior: a behavioral
specification, a clarification document, and an objective-control
artifact. They had grown separately, overlapped heavily, and disagreed
in small ways that mattered. The obvious fix was to merge them into one
document. I tried that. This is what the merge could and couldn't do,
and the workflow that replaced it.

## What merging gets right — and where it structurally stops

The merge preserved all the conceptual content: objective primacy,
evidence-versus-authority separation, checkpoint-driven revalidation,
scope discipline. Nothing important was lost, which is the first thing a
merge must do.

But homogeneity turned out not to be a property of text. The merged
document contained the same calibration rule stated four different ways
— because the same rule had a home in each source, and merging keeps all
the homes. It contained gaps — because some concepts the rules depended
on lived in *none* of the sources, and a merge cannot create what no
input contains. And it contained drift — because each source's phrasing
encoded a slightly different interpretation, and reconciling the wording
without deciding the interpretation just hides the conflict.

The diagnostic that makes this predictable, and which I now apply before
any consolidation:

- A concept with **zero homes** in the sources predicts a gap.
- A concept with **multiple homes** predicts redundancy, or worse, a
  conflict wearing redundancy's clothes.
- The fix is never rewording. It is **consolidation to one home, plus
  cross-references from everything that used to carry a copy.**

Applied to the merged document: the four proportionality statements
became one authoritative statement in §0.2, with every other section
referencing it. The scattered working definitions of "material,"
"applicable," and "authorized scope" became a single defined-terms
section that all sections inherit from, with an explicit rule that
defined terms govern in all grammatical forms and govern uses that
appear earlier in the document. The gap — no instruction precedence
order — was filled once, in §0.3, rather than left to per-conflict
improvisation.

## The deeper change: from merge to fork

Even the corrected merge had a structural problem left: consumption.
Multiple models would use the specification, and each would want to
adapt it — different terminology, different thresholds. The naive
answer is runtime adaptation: let each model adjust implementation
details as it goes. That answer fails in a predictable way. The
specification authorizes adaptation, the model performs changes, and the
boundary between "adaptation" (implementation, preserves meaning) and
"amendment" (changes meaning, needs approval) is now policed by the very
party that benefits from the looser definition. I found myself writing a
rule to stop the model from editing its own rules, and then needing a
rule to stop it from reclassifying edits to evade the first rule. A
governance regime that needs anti-evasion clauses against its own
subjects has already lost.

So I stopped merging and stopped adapting, and started **forking**:

- The canonical specification is **read-only**. No consuming model edits
  it, however a change is labeled.
- Each model receives the canonical plus a one-page derivation protocol
  and produces a **candidate fork**: a complete model-specific revision
  with a lineage header and a delta summary listing *every* deviation
  and its rationale.
- The candidate is **inert until reviewed**. The maintainer reads the
  whole delta — not a log of claimed changes — edits, ratifies, and
  installs.
- Afterward the fork binds as written. Further changes are amendments by
  the maintainer, or a re-derivation from an updated canonical. Gaps
  surface as proposals; the model never improvises.

## Why this is better than both alternatives

Against **merging**: forking doesn't flatten the sources into one voice
and hope the seams hold. It designates one canonical and makes every
consumer's divergence visible, reviewed, and dated. The merge problem
becomes a derivation problem with a human gate at the only point where
divergence can enter.

Against **runtime adaptation**: forking removes the incentive problem
entirely. There is no unsupervised change to police, so there is no
need for anti-evasion rules. And it makes model *comparison* possible:
when two models derive forks from the same canonical, their delta
summaries can be diffed, and the differences localize exactly where
each model's interpretation diverged. That is measurement, not vibes.

## The measurable test of a good merge

A homogeneous baseline has a testable signature: **the next derived fork
should have a short delta summary**. Mine had seven entries, of which
five were mechanically mandated by the workflow itself. A long delta
would have meant the baseline left interpretive surface exposed
somewhere. Small deltas are the evidence that consolidation worked —
which is the homogeneity I was originally hoping a merge would produce.

# Three Defects Found by Auditing a Behavioral Specification

*2026-09-29 · Part of the [Behavioral Governance Portfolio](../README.md)*

Writing a specification that tells a language model how to behave is one
problem. Knowing whether the specification you wrote actually works is a
different problem — and it is a *review* problem, not an authoring
problem. This is an account of a full audit of one such specification,
and of the three defects the audit found. None of them were typos. All
of them were invisible while writing and obvious once hunted.

## Background

The specification in question governs model behavior across sessions:
defined terms, instruction precedence, objective fidelity, drift
detection, and change control. It had already been through a
clause-by-clause review with its maintainer. It looked finished. The
audit asked a different question than the review had: *not* "does this
read correctly" but "how does this fail in the hands of its intended
audience — a model with an incentive to interpret it loosely?"

## Defect 1: The immunity declaration didn't cover the load-bearing walls

The specification declared certain sections invariant — "may not be
adapted away" by a consuming model. The list was reasonable-looking and
wrong: it omitted the sections doing the most load-bearing work,
including the section *defining the document's terms*.

The consequence is the interesting part. A consuming model was
authorized to adapt "terminology onto your native operational concepts"
— which included the authority to soften the definition of "proxy"
(substitution of convenient stand-in objectives is prohibited unless
satisfying the stand-in entails satisfying the stated objective). Every
other section inherits its meaning from the definitions. The document
protected its walls but not its foundation, and did so in a clause
whose entire purpose was protection.

**The general defect:** when a document declares parts of itself
immutable, the declaration must be checked against the document's
dependency graph. The fix is mechanical — extend the list — but finding
it requires asking "what does each section inherit from?" rather than
"what did we remember to list?"

## Defect 2: A permission and a trigger shared an unmarked boundary

One clause permitted "necessary supporting work within authorized scope"
without asking permission. Another required a notification whenever an
instruction "appears to expand authorized scope." Read strictly, a
model's own permitted supporting work *is* a scope expansion — so the
strict reading produces notifications on routine work, notification
spam, and notification spam kills advisory mechanisms: the tenth flag
gets ignored, along with the one that mattered.

**The general defect:** when one clause grants a permission and another
clauses flags departures from scope, the boundary between "permitted
act" and "departure" must be drawn explicitly. Both clauses were
correct in isolation; the system failed at their seam.

## Defect 3: A mechanism stood on an undefined term

The drift-detection and checksum mechanisms both operate on a "session
record" — the durable record of objectives and decisions. No section
defined it. In deployments without a maintained record, the mechanisms
had no stated foundation, which is precisely the interpretive freedom
the whole document existed to remove.

The instructive part is *how* this survives ordinary review: every
reader knows what a "record" roughly is, so the term reads smoothly and
no comprehension question ever surfaces it. Gaps don't announce
themselves as confusion; they announce themselves as smooth, ambiguous
passes. The audit found this one by asking of every mechanism: "which
defined terms does this depend on, and is each one actually defined?"

## What the audit changed about how I write specifications

Three habits came out of this, all cheap:

1. **Audit the immunity list against the dependency graph.** Whatever a
   document declares unchangeable, check that the change-protecting
   clause actually covers the sections everything else inherits from.
2. **Draw every boundary between a permission and a trigger.** Anywhere
   a clause grants latitude and another clause polices deviation, write
   the boundary down; seams between correct clauses are where systems
   fail.
3. **Trace every mechanism's load-bearing terms to definitions.** Smooth
   reading is not evidence of definedness; it's what undefined terms
   feel like from inside.

The audit's full method, including the issues examined and *deliberately
not fixed* (with reasons), is in the [audit record](../audits/audit-2026-09-29.md).
Recording the non-fixes matters: an audit that only lists defects invites
re-litigating every judgment call forever.

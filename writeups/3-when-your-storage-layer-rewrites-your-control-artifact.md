# When Your Storage Layer Rewrites Your Control Artifact

*2026-09-29 · Part of the [Behavioral Governance Portfolio](../README.md)*

A project-control artifact — the document recording a project's active
objectives, checkpoints, and state classifications — came back from a
routine edit cycle transformed: roughly sixty lines of content spread
across a file of tens of thousands of lines, blank lines multiplying
exponentially between every section.

Nothing had attacked it. No model had drifted, no user had mistyped.
The corruption came from the layer nobody audits: the interaction
between an AI assistant and a cloud-storage sync (Google Drive, in this
case) that compounded line breaks on each round trip until the artifact
was mostly whitespace.

## Why this failure mode is worse than it looks

**The artifact still worked.** That's what makes the class dangerous.
The content was intact; only the whitespace grew. A human skimming it
sees the same document. But the artifact's *consumers* are models
reading fixed context windows, and for them the damage is real:

- **Context waste at scale.** Tens of thousands of empty lines consume
  exactly the context the artifact's own checkpoint design depends on.
  The document's inflation quietly attacks the attention budget its
  function requires.
- **Position distortion.** In fixed-context models, where content sits
  in the window affects how strongly it is weighted. A control artifact
  smeared across a huge span is not the document the operator believes
  they saved.
- **Silence, not errors.** No tool complained. Sync succeeded, saving
  succeeded, opening succeeded. Every layer reported health while the
  artifact degraded — the definition of a failure you find by accident.

## The general lesson: means and environment are part of the control surface

Project-control documents usually assume the storage layer is a
transparent pipe. It isn't. Any artifact whose *interpretation depends
on its form* — and model-facing artifacts depend on form (position,
density, structure) far more than human-facing ones — inherits the
integrity properties of every system that touches it.

The practical controls that came out of this incident:

1. **Verify integrity on retrieval, not just on save.** Before treating
   a retrieved control artifact as current, check the properties its
   function depends on — for text fed to models, that includes size
   against expectation, not merely content match.
2. **Treat tool-mediated round trips as edits.** Anything that reads and
   re-writes your artifact (sync layers, export/import, format
   conversion) is an editor, and editors need the same trust and
   verification you'd apply to a collaborator.
3. **Keep control artifacts in the layer with the strongest integrity
   guarantees, and treat copies elsewhere as untrusted until verified** —
   version-control history is the tamper-evident record; a Drive copy
   is a rendering.
4. **Write the model's response to suspected corruption into the
   behavior spec itself.** The model should be governed to check
   artifact integrity rather than to silently consume a mangled input —
   a rule that costs one line until the day it saves a project.

The incident's real product was the recognition that "establish
authority, version, and applicability independently" — a rule I had
already written for *instruction sources* — applies with equal force to
*storage infrastructure*. The artifact you can't trust is the one you
didn't know was being rewritten.

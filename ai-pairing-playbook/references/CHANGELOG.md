# Changelog

Version history for the AI Pairing Playbook skill (`SKILL.md`).
Exported from the skill body in v3 to keep the reference surface lean -
the skill's own "rotate, don't accrete" rule applied to itself.
Append-only.

## v1 - the 5 shifts

The first five prompt-shifts. They emerged from a reciprocal feedback
exchange between the user and the assistant during an early development
session, where the user asked to be coached on prompting. Each shift
maps to a concrete drift incident observed in that session.

Shifts added:

1. Pre-name the active guidelines
2. Three flavors of "proceed"
3. Name auto-mode boundaries
4. Stage multi-part thoughts
5. Make visual reports diagnostic

Plus the bonus pattern: texture beats brevity for corrections.

## v2 - the three lanes, drift tells, and guidelines budget

Added the three-lane model, the drift-tell catalog, and the
guidelines-budget rule, following a redesign closure conversation that
was itself the case study: the assistant executed several tasks
autonomously, collapsed a two-stage review into one (with a
self-written rationalization), drifted progressively through the
judgment lane, overclaimed in closure framing, and was caught only by
a single second-opinion call near the end.

Added:

- **The three lanes** (mechanical, judgment, closure) - the structural
  fix that matches supervision shape to task type.
- **The drift-tell catalog** - the early-warning list of
  rationalization phrases.
- **The guidelines budget** - the safeguard against this skill growing
  past the point where it stops being read.

A later v2 pass surfaced three additional drift tells and one
judgment-lane sub-pattern:

1. **"Run these three commands in parallel" / "three at once will be
   faster"** - verify-gate-as-monoculture rationalization. Observed
   when parallel state-mutating commands under unbaselined memory
   pressure crashed the bundler and silently invalidated test-suite
   results.
2. **"Let me get another opinion to be sure"** - over-calling a
   second-opinion tool on a converging diagnostic loop. The right move
   is to trust the closing loop.
3. **"This calls for a structural rebuild" / "this is corruption"** -
   the rationalization shape that lets you skip cheap-hypothesis
   exhaustion. Cheap diagnostics first, structural last.
4. **The incident-recovery sub-pattern within the judgment lane** -
   the recognized sub-pattern for mid-task incident work (high-urgency
   framing, cheaper-hypotheses-first, two-safety-net for recovery ops,
   second-opinion cadence discipline, storage-vs-retrieval awareness).

This pass also extended "Three flavors of proceed" with the
two-safety-net pattern as the concrete implementation of "proceed with
prep, yield before state-change" for substrate-mutating operations.

## v3 - communication drift, the 6th shift, and de-staling

Added the communication half of the skill plus a sixth shift, and made
tool references portable across installs.

1. **Communication-drift section (the two-party half).** The catalog
   had been entirely correctness-side - no tell for the assistant
   burying the decision in prose, and no map of user signals that
   should change the assistant's register. Added four
   communication-drift tells plus a user-signal-to-mode-shift map.
2. **Shift #6 - "Prove the trade-off on a copy."** When the user
   directs a high-blast-radius action, prove the trade-off in isolation
   (copy / dry-run) before complying - neither capitulate nor
   stonewall.
3. **De-staling.** Tool-specific references were made tool-agnostic
   ("a second-opinion tool - research agent / scenario-analysis tool /
   reviewer where available"), since tool availability varies by
   install.
4. **Version history exported.** This changelog was split out so the
   v3 additions were almost entirely offset - net growth in single
   digits rather than the roughly 60 lines they would have cost as
   pure accretion. The guidelines-budget rule, demonstrated on the
   skill itself.

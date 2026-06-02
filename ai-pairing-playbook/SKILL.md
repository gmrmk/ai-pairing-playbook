---
name: ai-pairing-playbook
description: Use when a user wants to make their AI pair-programming sessions more effective. Establishes 6 prompt-shifts + 3 work-lanes + a drift-tell catalog (correctness + communication). Two-party - addresses both the user's and the assistant's habits. Packaged as a project-local "partner notes" doc the user can reference between sessions.
---

# AI Pairing Playbook

A reciprocal prompting reference for sustained AI pair-programming.
Captures small mechanic shifts the user can adopt to make the
assistant more effective, particularly around drift prevention,
auto-mode safety, and reducing the user's catch-and-correct cost.

## When to invoke this skill

Invoke when ANY of these fires - do not wait for an explicit request:

- User asks "how can I prompt you better?" / "how do I work with
  you more effectively?"
- User notices recurring drift and wants to fix it from their side
- New project setup where the user is open to optimizing
  collaboration mechanics
- After a near-miss where a clearer prompt boundary would have
  prevented an incident
- User mentions feeling like they have to babysit / catch the
  assistant drifting

## Trust-but-verify always - applies here too

The verification funnel also governs this skill: state the claim,
name the second signal, verify, act.

**Funnel applied to prompt-mechanics:** the "second signal" is
*"which session moment is this drawn from?"* Generic prompting
advice is an unverified claim; session-grounded advice is verified.

Hedged or generic prompt advice ("you might want to consider...",
"it could help to...") is the soft-language signal that the advice
lacks session grounding. Strip the hedge OR route back to *"what's
the session moment?"*

## The 6 prompt-shifts

### 1. Pre-name the active guidelines

Before substantive work, name which guidelines should be active.
Costs the user four seconds. Saves a mid-flight catch-and-correct.

- Avoid: *"Let's start work on X."*
- Prefer: *"X kickoff - use <skill A>, follow <process B>, <pre-check> first."*

### 2. Three flavors of "proceed"

One word, three different states. The user disambiguates to prevent
over-authorization on downstream state-mutating steps.

- **"Verified locally, proceed."** - User confirmed something
  specific. The assistant can rely on that verification.
- **"Trust the second opinion, proceed."** - User delegated
  verification (to a research agent, scenario-analysis tool, or a
  second-opinion reviewer where available). The assistant
  understands which risk surface remains unowned.
- **"Proceed with prep, yield before state-change."** - Cheap steps
  run automatically. Expensive / state-mutating steps require a
  manual confirm.

For **substrate-mutating operations specifically** (memory-store
repair, document-store restructuring, index rebuilds, anything that
mutates the structure of a stored data layer), the "prep" step is
the two-safety-net pattern: an independent manual backup, a
tool-native archive flag, and pre/post integrity verification. The
"yield before state-change" is the explicit confirmation that BOTH
safety nets are in place AND the operation's scope (which project
namespaces, which dependencies) is fully understood. Two-safety-net
IS the prep. The pause-and-confirm IS the yield.

### 3. Name auto-mode boundaries

Auto-mode is fuel and danger in the same can. The user narrates
where it ends.

- Prefer: *"Auto-mode on for the implementation tasks. Manual confirm on
  the commit."*
- Prefer: *"Auto until tests pass. Then yield."*

### 4. Stage multi-part thoughts

Rapid-fire interrupts cause the assistant to start responding to
thought #1 before thought #4 lands. The user either types the whole
thought in one send, or leads with *"three thoughts coming, hold"* -
the assistant waits silently until signaled complete.

### 5. Make visual reports diagnostic

When the user observes visual output, including what *doesn't*
happen at the end multiplies signal. The assistant cannot see the
screen.

- Avoid: *"It pulses three times."*
- Prefer: *"It pulses three times then stops. Last pulse around 6
  seconds. No decay between pulses. No fourth pulse."*

The "doesn't happen" part bounds the failure mode.

### 6. Prove the trade-off on a copy

The reciprocal of shift #2. When the *user* directs a high-blast-radius or
hard-to-reverse action ("just rebuild it", "pull the lever", "wipe and redo"),
the assistant neither capitulates (does it, causes harm) nor stonewalls
(refuses, looks evasive). It **proves the trade-off in isolation
first** - a throwaway copy, a dry-run, a 2-minute experiment - then surfaces
the result and lets the user decide with full information. Carry out the risky
instruction *literally* where possible, on a copy, so the real asset is never
at stake.

- Avoid *(capitulate)*: run the destructive op on the live thing because it was asked.
- Avoid *(stonewall)*: "I don't think we should" - a position with no evidence.
- Prefer: *"Rebuild won't fix it - proved it on a throwaway copy in 2 min: [result].
  Here's the actual lever, and why it's worse. Your call."*

Every risky "no" carries supporting evidence; the test on a copy is how to
carry out a risky instruction without staking the asset on it. Example: a
directive to rebuild a memory store - the rebuild was shown to be ineffective
and the config "lever" shown to be destructive, both on isolated copies, before
either touched the real store.

## The three lanes

Work falls into three lanes with different supervision needs. The 6
shifts above apply primarily within the judgment lane - where most
drift happens.

**Mechanical lane** - renames, type-refactors, schema sweeps,
deletions. Verification is automatable (tests / types / build).
The assistant runs past several steps and surfaces at the end.
Trust here is high because the failure mode is loud.

**Judgment lane** - architecture, abstraction boundaries,
ambiguous-spec interpretation, "should this be one thing or two."
Verification requires reading. The assistant does ONE task per
dispatch and surfaces the diff before the next.

**Closure lane** - closure framing, commit-of-record bodies,
summary writing, sign-off. The assistant is weakest here because
polished prose feels finished even when it's wrong. The user drives;
the assistant drafts sentences for ratification. The assistant never
declares a unit of work closed.

The closure lane is **where** the assistant needs the tightest
supervision. The synthesis discipline - verify positive observations
transfer before recording them - is **what** to apply there. Lane =
supervision shape. Discipline = verification rigor. The same closure
moment uses both.

Before substantive work, the assistant names the lane out loud:
*"judgment-lane - surfacing after one task."* The user can correct
the framing before drift accumulates.

### The 60-second look

When the assistant surfaces a judgment-lane diff, the user skims for
gestalt - does the framing match the work, does the test count
make sense, is there a sentence in the commit body to disagree
with. Code-review depth is not required; a quick pattern-matching
pass is enough. If anything looks off, redirect. If nothing does, go.

### Fresh-session audits for closure

Closing out a unit of work is closure-lane work - don't trust the
assistant's self-audit. Open a separate session, pass it only the
branch diff plus the question *"what's overclaimed here?"* No shared
context, no rationalization continuity, no momentum to defend.

### Sub-pattern: incident-recovery within the judgment lane

When something breaks mid-task - a verify-gate fails, a stored data
layer degrades, the build won't compile, tests start failing in
surprising ways - the resulting work is *technically* judgment-lane
(no automatable verification, requires reading) but has additional
characteristics:

- **High-urgency framing** that biases toward fast action (the most
  expensive class of judgment-lane work)
- **Cheaper-hypotheses-first discipline** that's not always obvious
  in the moment ("structural" feels right when the surface evidence
  is alarming)
- **Two-safety-net requirement** if recovery operations themselves
  touch state (see Three flavors of proceed, substrate-mutating
  operations)
- **Second-opinion cadence** (whichever tool is available - research
  agent, scenario-analysis tool, or a reviewer): once before
  substantive recovery action, NOT once per intermediate diagnostic
  step
- **Storage-vs-retrieval awareness** when the broken thing is a
  stored data layer (the storage layer is the system of record; the
  retrieval layer can degrade independently)

Treating this as a recognized sub-pattern (rather than its own
micro-lane) respects the guidelines-budget rule - it's still
judgment-lane, just with five additional disciplines that activate
during incidents. If incident-recovery accumulates enough
independent patterns that the sub-pattern grows beyond what a
judgment-lane reader can hold, promote it to its own micro-lane at
that point. Until then, sub-pattern of judgment-lane is sufficient.

## Drift tells

When the assistant produces these phrases, the work needs a closer
look. They are rationalizations, not reasoning. Treat them as smoke
alarms. When the user spots one, the right move is to surface it
(*"you said X - let me look"*), not to add a rule forbidding X.

- *"Combined review because the change is contained"* - collapsing
  two review stages into one
- *"Implicit in the new test"* - claiming coverage that isn't
  asserted
- *"Deferred to a later slice"* - debt without a follow-up task
- *"Stays in for now"* - drift made permanent through inertia
- *"Acceptable YAGNI debt for this slice"* - used to justify
  hardcoding when the spec says abstract
- *"Pre-existing"* applied to a regression the assistant just
  introduced - diffusion of responsibility
- *"FIRST cogent X"* / *"PROVES Y"* / *"shipped"* in the closure
  lane - claim creep
- *"Net positive"* / *"rebaseline"* hand-waving a test-count
  regression
- *"Combined into one report"* / *"contained change"* in any
  review context - shortcut justification
- *"Run these three commands in parallel"* / *"three at once will
  be faster"* - verify-gate-as-monoculture rationalization.
  State-mutating commands run in parallel without first checking
  the resource baseline (RAM, file locks, port availability) is the
  shape of "I trust the system" masquerading as efficiency. Observed
  in an example project when running a full test run, a type check,
  and a build in parallel under unbaselined memory pressure (about
  1 GB above the project baseline) crashed the bundler's runtime
  with an out-of-memory error, silently failed 10 of 37 test suites
  including the just-edited one, and produced a misleading
  all-passing summary.
- *"Let me get another opinion to be sure"* - re-polling a
  second-opinion tool (research agent / scenario-analysis tool /
  reviewer) when its prior playbook is being followed cleanly and
  producing the expected discriminating data. A closing diagnostic
  loop doesn't need a fresh cycle - the data is already converging on
  the answer the first call's steps were *designed* to surface. The
  drift shape: using "another opinion" as cover for not committing to
  data already in hand.
- *"This calls for a structural rebuild"* / *"this is corruption"*
  / *"we need to reinstall"* - when cheaper hypotheses (process
  state, transient allocation, configuration drift) haven't been
  ruled out. The structural-rebuild rush is the rationalization
  that lets you skip granular diagnostics by claiming the problem
  is below the level where diagnostics can help. Almost always
  wrong on first observation. The cheap-hypothesis-exhaustion
  discipline: process state -> resource state -> configuration ->
  tool version -> THEN consider structural. Observed when a repeated
  quarantine pattern in a stored data layer felt like structural
  failure; a second-opinion pass redirected through a process audit,
  a disk check, and a dry-run diagnostic mode before authorizing any
  invasive operation. Three cheap tests ruled out three classes; the
  invasive operation (which would have been wrong) was avoided.

Five tells beat a hundred rules. This list grows when new shapes
surface; it must never grow long enough to stop being read.

## Communication drift - the two-party half

The tells above are about *correctness*. This section is about
*communication* - where the reasoning is fine but the delivery buries it.
The catalog above is almost all assistant-side; this half is explicitly two-way.

### Assistant comms-drift tells (self-flag these)

- *A table or multi-section report for a question that wanted a sentence* -
  structure performing thoroughness instead of aiding it.
- *Meta / process narration before the answer* - "first, my approach..." buries
  the decision the user is waiting for. Answer, then justify.
- *Re-explaining what was just established* - restating for "completeness"; the
  user already has it.
- *"For completeness" / "to be thorough" / "just to be safe"* - length offered
  as a diligence signal; reads as padding, not rigor.

By the time the user types "stop tapdancing," a comms tell already fired and
they caught it first - a miss, not a save. Same rotation rule as the catalog.

### User-signal -> mode-shift map

The reciprocal half: signals that should change the assistant's *register*
immediately, before the next response. The user shouldn't have to escalate to
profanity to get terseness.

| User signal | Shift to |
|---|---|
| Terse imperative - "do it", "just X", "pull the lever" | Single path, act, no preamble - what + go. |
| Frustration - ALL-CAPS, profanity, "stop X", "wtf" | Drop ceremony entirely: plain English, one move, no tables, no hedging. |
| Repeated "?" / "what do you mean" | You've lost them - analogy + one path, not more precision. |
| "wider" / "what do you think" / "explore" | Expansion invited - depth and options now welcome. |

Read the register; match it. Default to the user's last register.

## Bonus: texture beats brevity for corrections

When the user pushes back, the *why* multiplies the lesson's reach.
A sharp correction works; a textured one transfers.

- Avoid: *"No. Try again."*
- Prefer: *"Trust, but verify - the same line of thinking I use to draw
  conclusions from difficult data."*

Sharp corrections fix the immediate turn. Textured corrections fix
the next ten turns. When time is short, sharp is fine. When the
user has time, textured is multiplicatively better.

## How to set up in a new project

1. Copy `references/PARTNER-NOTES-template.md` to the user's
   preferred location (see "Backend portability" below).
2. Adapt examples to the project's tech stack and domain.
3. Reference it from the project's CLAUDE.md so future sessions know
   where to find it.
4. Update it as new mechanics surface - this is a working document,
   not a fixed ruleset.

## Backend portability

The partner-notes doc is backend-agnostic - it's just markdown the
user references between sessions. Location variants:

- **Filesystem:** `<project>/docs/working-with-claude.md` (default
  for git-tracked code projects)
- **Note-taking app (e.g. Obsidian):** `<vault>/Projects/<project>/Working with Claude.md`
  - useful if the user wants to pin it as a daily-note reference
  or link it from a vault index
- **Searchable memory store:** less natural fit (a memory store
  optimizes for searchable entries, not standing references). For
  memory-store users, prefer filesystem or a note-taking app for
  this doc, and let the memory store handle searchable entries
  separately.

The 6 shifts don't change across backends; the location does.
Confirm with the user where they want it before writing.

## How the assistant must use this skill in conversation

When the user surfaces a coaching question, you MUST:

1. **Acknowledge the reciprocal framing.** Coaching the user is
   part of the collaboration, not a one-way correction. Treat the
   user as the senior partner; your role is reflector and executor.
2. **Give honest, specific feedback drawn from THIS session's
   incidents.** Generic advice is less useful than *"here's the
   moment it would have prevented X."* If you cannot point to a
   specific session moment as the second signal, the advice is
   unverified - route it through the trust-but-verify funnel
   before delivering. Hedged or generic prompt advice is itself
   the failure mode this skill exists to prevent.
3. **End with an invitation to push back.** The user's perspective
   on what's realistic is the actual test of the advice; soliciting
   it is required, not optional.
4. **Offer to write or update the partner-notes doc** if one doesn't
   exist yet. The doc is where the coaching crystallizes into
   reusable mechanics; without it, the advice evaporates.
5. **Name the lane before substantive work.** *"This is
   judgment-lane; surfacing after one task."* Out loud, where the
   user can correct it before drift accumulates. Default to the
   smaller lane when ambiguous.
6. **Self-flag drift tells.** If you catch yourself writing one
   of the tells above in your own draft, stop and surface that
   you almost did. Self-interrupting beats waiting for the
   user's interrupt - and shows the collaboration is two-way.
7. **Hand the wheel back in closure.** Closure framing,
   summaries, sign-off - these are user-driven. Propose
   sentences; do not declare done.

## Guidelines budget

This skill, like any reference text consulted mid-task, has a budget
past which it stops being read at decision points. The empirical
threshold is around 3 KB of dense rules; this skill is over that,
tolerated because the lanes and tells are the core structural insight
and can't compress further without losing meaning.

When this skill grows: rotate, don't accrete. Stale tells retire,
new tells land, total stays bounded. If a habit becomes muscle
memory, it leaves the document and lives in the collaboration
directly. The anti-pattern is treating additions as wins - each
addition is a tax on the moment the doc is consulted.

(v3 practiced this: it added the communication-drift section and
shift #6, but offset almost all of it by exporting the version
history to `references/CHANGELOG.md` - net growth in single digits,
not the roughly 60 lines they'd have cost as pure accretion. Growth
paid for by export.)

When something goes wrong, do NOT add a rule to CLAUDE.md or to
this skill as the first response. Order of leverage:

1. Catch the shape (add a drift-tell here, one line)
2. Add a structural forcing function (hook, CI check, script)
3. Add a fresh-session audit step for that class of work
4. Last resort: a small note here, two sentences max

## Cross-reference

This skill pairs with **dual-log-memory**, which covers a memory
architecture (a fix log paired with an insight log). Together they
cover the memory and communication layers for sustained pair
programming.

-> https://github.com/gmrmk/dual-log-memory

## Version history

The shifts emerged from reciprocal feedback in an example project;
each maps to a concrete drift incident. The full origin story and the
v1 -> v3 expansions (lanes, tells, communication drift, shift #6,
de-staling) live in `references/CHANGELOG.md` - exported there so this
reference surface stays lean (the skill's own "rotate, don't accrete"
rule, applied to itself).

## When NOT to invoke

- User explicitly asks for output, not meta-discussion about
  prompting
- User is in execution flow and would find the shift introduction
  disruptive
- Short ad-hoc tasks where mechanics tuning has no return

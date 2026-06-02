# Working with Claude — partner notes (template)

Drop this into `<project>/docs/working-with-claude.md` (or wherever
the user keeps reference docs) and adapt examples to the project's
tech stack and domain.

---

# Working with Claude — partner notes

A quick reference for prompting Claude effectively on this project.
Reciprocal — Claude is keeping its own learnings in `docs/insights/`.
If something here feels wrong in practice, adapt it. This is a
working document, not a fixed ruleset.

---

## The 6 shifts

### 1. Pre-name the active guidelines

Before substantive work, name which guidelines should be active.
Costs four seconds. Saves a mid-flight catch-and-correct.

❌ *"Let's start <work item>."*

✅ *"<work item> kickoff — use <skill>, follow <process>, <audit>
first."*

Why it works: Claude has many active guidelines (uncertainty
protocol, skills harness, fix-log check, cleanup process, etc.).
Naming the relevant ones upfront preloads them. Without naming,
Claude relies on drift-prone defaults.

---

### 2. Three flavors of "proceed"

One word, three different states. Disambiguate to prevent
over-authorization on downstream state-mutating steps.

- **"Verified locally, proceed."** — You confirmed something
  specific. Say what.
- **"Trust the second opinion, proceed."** — You delegated
  verification (a second-opinion tool — research agent, scenario-analysis
  tool, or a reviewer where available). Claude understands which risk
  surface remains unowned.
- **"Proceed with prep, yield before state-change."** — Cheap steps
  auto. Expensive / state-mutating steps require a manual confirm.

The third option is the safest default for any chain of steps that
ends in a write, commit, deploy, or destructive operation.

---

### 3. Name auto-mode boundaries

Auto-mode is fuel and danger in the same can. Perfect for executing
a known-good plan. Dangerous at ambiguity points. You don't need to
toggle a setting — just narrate the boundary.

✅ *"Auto-mode on for the implementation tasks. Manual confirm on
the commit."*

✅ *"Auto until tests pass. Then yield."*

---

### 4. Stage multi-part thoughts

Rapid-fire interrupts cause Claude to start responding to thought #1
before thought #4 lands. Tokens wasted. Context drifts. Two
options:

- Type the whole thought in one send.
- Lead with *"three thoughts coming, hold"* — Claude will wait
  silently until you signal complete.

Either pattern works. Mixed-mode (interrupt every sentence) is the
one to avoid.

---

### 5. Make visual reports diagnostic

When you observe visual output, include what *doesn't* happen at
the end. Claude can't ask its eyes.

❌ *"<short description of what you see>"*

✅ *"<what happens> then <what stops happening>. <Timing detail>.
<What doesn't happen>."*

The "doesn't happen" part is diagnostic gold — it bounds the
failure mode. With the second phrasing, Claude jumps straight to
the bug. With the first, Claude cycles through hypotheses.

---

### 6. Direct risky actions, expect a proof-on-a-copy

For a high-blast-radius or hard-to-reverse ask (rebuild, wipe, "pull
the lever"), say it plainly and expect Claude to **prove the trade-off
in isolation** — a throwaway copy, a dry-run — before touching the real
thing. You should get a receipt, not blind compliance and not a flat
refusal.

✅ *"Rebuild it — but show me it actually helps first."*

Why it works: it licenses Claude to test the scary thing safely instead
of either capitulating (causing harm) or stonewalling (stalling). The
reciprocal of #2.

---

## Bonus: texture beats brevity for corrections

When you push back, the *why* multiplies the lesson's reach. A
sharp correction works. A textured one transfers.

❌ *"No. Try again."*

✅ *"<correction> — <the principle or analogy behind it>."*

Sharp corrections fix the immediate turn. Textured corrections fix
the next ten turns. When time is short, sharp is fine. When you
have time, textured is multiplicatively better.

---

## Reciprocal

Claude is building `docs/insights/` in parallel — capturing
design, architectural, domain, process, and higher-level
learnings as they emerge. The dual log (`docs/fixes/` for what
broke, `docs/insights/` for what worked) is two halves of one
record.

Both halves share the same discipline: **trust-but-verify, always**.
Claude routes every uncertain claim — code, process, prompting
advice — through the verification funnel before acting on it. The
6 shifts above are the user-side counterpart. Together they make
the catch-and-correct loop cheap enough that drift gets caught
early instead of compounding.

You're adapting how you prompt. Claude is adapting what it
remembers. Both are required.

---

*Last updated: <date>. Adapt as the project evolves.*

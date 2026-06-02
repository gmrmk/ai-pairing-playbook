# ai-pairing-playbook

The `ai-pairing-playbook` Claude Code skill — a reciprocal
prompting reference for sustained AI pair-programming. Six small
shifts the user adopts to make the assistant more effective,
reducing drift and improving auto-mode safety.

Designed to pair with **dual-log-memory** (memory
architecture). Together they form the communication and memory
layer for long-running AI pair-programming.

## The six shifts

1. **Pre-name the active guidelines** before substantive work.
2. **Three flavors of "proceed"** — disambiguate authorization
   for state-mutating steps.
3. **Name auto-mode boundaries** — narrate where auto ends.
4. **Stage multi-part thoughts** — type the whole thought in one
   send, or signal "hold."
5. **Make visual reports diagnostic** — include what *doesn't*
   happen at the end of an observed sequence.
6. **Prove the trade-off on a copy** — on a high-blast-radius
   request, test it in isolation before complying; neither
   capitulate nor stonewall.

Plus a bonus: **texture beats brevity for corrections** — the
*why* behind a pushback multiplies the lesson's reach.

See `ai-pairing-playbook/SKILL.md` for the full breakdown,
each shift with examples, and the trust-but-verify
cross-reference.

## Install

### macOS / Linux

```bash
git clone https://github.com/gmrmk/ai-pairing-playbook.git
cp -r ai-pairing-playbook/ai-pairing-playbook ~/.claude/skills/
```

### Windows (PowerShell)

```powershell
git clone https://github.com/gmrmk/ai-pairing-playbook.git
Copy-Item -Path .\ai-pairing-playbook\ai-pairing-playbook -Destination "$env:USERPROFILE\.claude\skills\" -Recurse
```

(The doubled `ai-pairing-playbook` is intentional — the outer
is the cloned repo, the inner is the skill subdirectory that
goes into `~/.claude/skills/`.)

## Usage

Once installed, the skill appears in Claude Code's
`available-skills` list. Invoke via:

```
Skill ai-pairing-playbook
```

## Adopting in a new project

Copy `ai-pairing-playbook/references/PARTNER-NOTES-template.md`
into your project as `docs/working-with-claude.md` (or wherever
you keep reference docs). Adapt the examples to your project's
tech stack and domain. Update it as new mechanics surface — this
is a working document, not a fixed ruleset.

The 6 shifts are stable across backends; the location of the
partner-notes doc varies. See `SKILL.md § Backend portability`
for filesystem, note-taking-app, and memory-store placement guidance.

## Trust-but-verify always

Prompt-mechanics advice is itself a class of claim about how
collaboration works. Every recommendation in this skill routes
through a four-step funnel (state claim → name second signal →
verify → act). Hedged or generic prompt advice is itself the
failure mode this skill exists to prevent — session-grounded
specifics (*"here's the moment X would have prevented"*) beat
generic best-practices every time.

## Companion skill

**dual-log-memory** — A memory architecture pairing a fix log
with an insight log. Symmetric trust-but-verify discipline plus
sunset rules for self-pruning. Together with ai-pairing-playbook
it forms the memory and communication layer for sustained
collaboration.

→ https://github.com/gmrmk/dual-log-memory

## License

MIT — see `LICENSE`.

## Contributing

Issues and PRs welcome. If you adopt the partner-notes pattern
in your own project and surface a new prompt-shift worth
feeding back, open an issue describing the moment that prompted
the addition. The skill grows by its own discipline — driven by
concrete, session-grounded incidents rather than abstract
best-practice advice.

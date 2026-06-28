# CLAUDE.md — working conventions for `docside-experience`

This file governs how Claude (and Claude Code) work in this repository.

---

## What this repo is — and what it is not

- **This repo** defines the **experience**: trust doctrine, vocabulary, copy,
  information architecture, workflows, states, and screen specs. It is the
  *what trust requires* layer.
- **The main repo** (`manderso90/docside`) **implements** it: Next.js 15, Supabase,
  Vercel, Gemini / Document AI extraction, Inngest, Zod.
- This repo **specifies**; that repo **builds.** When a spec here names a runtime
  behavior, it is an instruction to the implementation, not a description of it.

---

## The cross-repo seam (read before editing specs with runtime implications)

Several specs here only become real in the main repo, and must stay in sync. When you
touch one of these, note the counterpart that has to move with it:

- **The append-only correction/audit log** (`08-states-and-edge-cases.md` §3.1,
  `trust-doctrine.md` §3.1 v0.5) — specified here; implemented as storage in the main
  repo (likely an append-only Supabase table).
- **`HIGH_STAKES_FIELD_KEYS`** — the stakes-weighted verify gate and the share
  acknowledgment (states §3) reuse this list from the main repo. Do not fork it.
- **The five hazard tags** (`domain-vocabulary.md` §2: `STRUCTURALLY-NULL`,
  `FORM-LITERAL`, `DEFAULT-TRAP`, `FREE-TEXT-VERBATIM`, `PCT-OR-FLAT`) — written as
  stable identifiers so copy and states key off them by name. If they live better as
  an enum in the main repo's schema, that enum and this list are the same source and
  must not diverge.
- **The §1B auto-join key** (IA §2) and **§1A buyer-name labels** (IA §2.1) — the
  extraction in the main repo must surface these for the reconciliation gate to work.

**Rule:** this repo is the source of truth for trust and UX *intent*; the main repo is
the source of truth for *implementation*. When they diverge, reconcile deliberately and
record it in `11-design-decisions/`.

---

## Document conventions

- **Status + version line** opens every doc. Bump it on any decision; record the
  decision inline (`Decision (vX)` / `DECIDED` / `✅`).
- **Defer-lines, not backlogs.** Every deferral names a reason and a home
  (`POLISH-BACKLOG`, a later milestone, a specific folder).
- **One primary doc per folder**, plus specimens/mockups as needed (e.g.
  `worked-specimen.md`, `verify-workspace-mockup.html`).
- **Cross-references are by section name** (`doctrine §3.1`, `IA §2.1`), not file
  path — so files can move between folders without breaking references.

---

## Grounding discipline

- **Form references are pinned to C.A.R. Form RPA, Revised 6/25** and were verified
  against the actual form, not memory. Section letters move across revisions; a new
  form version requires re-grounding (`domain-vocabulary.md` §6). Claude's own
  field-location claims are checked against the form, never asserted.
- **Never reproduce verbatim CAR form text** — it is copyrighted. The mockup uses a
  stylized/greeked document with factual section labels only. Keep it that way.

---

## The tests every change passes

- **The doctrine's §7 test:** does this make the contract more trustworthy to
  understand — by provenance, honest uncertainty, or term-based explanation — or only
  more finished?
- **The NORTH-STAR test:** does this move the agent toward a summary they're proud to
  put their brand on — through upload, verify, or share — or sit outside that path?
- A change should pass both.

---

## Voice & copy

- Copy obeys `10-copy-guidelines.md`: three Docside registers (Principle, Explanation,
  System) plus the agent's own voice (brand-frame copy). Agent voice *frames*; Docside
  voice *asserts*; provenance governs only the second.
- The grammar of absence (states §1) holds at the pixel level: no two of
  present / corrected / empty-on-form / not-captured / not-applicable / unreadable may
  look alike.

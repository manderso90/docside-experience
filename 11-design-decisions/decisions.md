# Design Decisions

> **Status:** v0.1 — log started.
> **What this is:** the consolidation point for major, locked design decisions that
> are otherwise scattered as inline `DECIDED` markers across the specs. A decision
> earns an entry here when it constrains future work and someone might later need to
> find, question, or reverse it. The spec docs remain where the decision *lives*; this
> log makes the set **findable** and gives each a stable `DEC-n` handle.
> **Convention:** newest decisions get the next number; entries are never deleted. A
> reversal is a *new* entry that supersedes an old one, with both left in place.

---

## DEC-1 — Share delivery: the live link first, over both SMS and email; PDF deferred

**Date:** 2026-06-28 · **Status:** DECIDED · **Lives in:** `06-handoff/handoff.md` §3, §8, §9

**Context.** The agent sends the branded summary (or comparison) to the seller. Two
questions had been entangled: *what form* the artifact takes and *what channel* it
travels over. Email's prevalence makes an SMS-only share insufficient — agents will
expect to email what they can text — and the original handoff matrix treated "email"
as a third artifact form alongside link and PDF, which is a category error.

**Options considered.**
- **A — SMS-the-link only for the alpha**, add email and PDF later. Rejected: leaves
  the dominant professional channel on the table for no real saving.
- **B — the live link over both SMS and email now; PDF deferred.** *(chosen)*
- **C — PDF + link, both channels, now.** Rejected: a PDF is a new *form* that must
  re-earn every trust invariant, gated on the unsolved static-provenance problem.

**Decision.** Separate **form** (live link / static PDF) from **channel** (SMS /
email). The **live link is the universal payload** — it rides SMS and email
identically — so **email-the-link ships alongside SMS-the-link**, not after it.
Adding a channel costs ~nothing; adding the PDF *form* is the expensive, deferred
move. Channels carry no trust gate of their own; they inherit the gate of the form
they deliver.

**Consequences.**
- *Easier:* email + SMS at once for near-zero extra cost; the emailed link stays
  live, so corrections propagate and nothing goes stale (handoff §5).
- *Raised:* email makes forwarding the norm, which elevates the **link access-control**
  question from a nicety to a real risk — a forwarded *comparison* link exposes
  multiple buyers' confidential terms (handoff §7). Now an active open decision
  (handoff §8).
- *Locked:* the form-vs-channel distinction; the brand frame and "call me to discuss"
  sign-off (copy §1.4) belong in email, which has room SMS doesn't.

**Deferred.** The **PDF form** (awaits static-provenance, handoff §3 hard column). The
**access-control model** (revocable links; comparison-link gating — open in handoff §8).

---

## Decisions to backfill

Already locked inline across the specs; promote each to a full `DEC-n` entry as it
comes up for review. Listed with where it lives so it's findable today.

| Decision | Lives in |
|---|---|
| Central IA: listing-scoped, offer-entered, address-joined (§1B / APN key) | IA §2, §7 |
| Two-channel reconciliation gate (inbound + upload, dedup, per-offer exclusion) | IA §2.1 · states §4.1 |
| Seller-priority profile is listing-scoped, seeded from agent presets | IA §7 |
| Same-term-plus-optional-gloss model | vocabulary §1.2 |
| Provenance reaches the seller (shared summary, not just verify) | doctrine §3.1 (v0.2) |
| Agent correction is a provenance class; append-only audit log; contract immutable | doctrine §3.1 (v0.5) · states §3.1 |
| Low-confidence ⇒ unreadable, with a verify-only confirm/correct/mark band | states §1.1 |
| High-stakes unreadable gates share via agent acknowledgment | states §3 |
| Inbound routing: agent forwards to a per-agent Docside address | agent-workflow §7 |
| One-tap confirm for a clean read; field-by-field when flagged | agent-workflow §7 |
| Seller call-prompt: agent-voiced `tel:` link, no new messaging path | seller-workflow §6 |
| The six verify-workspace design forks (pane ratio, rail, mobile, doc pane, grouping) | verify-workspace §6 |
| Inverted-ranking guarantee — public-facing wording | doctrine §5 |
| Non-laundering principle (share never strengthens a claim by dropping a caveat) | handoff §6 |

> These are not lesser decisions — they're simply already documented where they're
> used. The backfill is about giving each a stable handle and a one-place record, not
> about re-deciding anything.

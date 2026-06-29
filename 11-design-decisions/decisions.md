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

## DEC-2 — Share surface organizing idea: offer headline leads, brand frame introduces

**Date:** 2026-06-29 · **Status:** DECIDED · **Lives in:** `07-screen-design/share-surface.md` §0, §1, §6 fork 1

**Context.** The seller's trust arc opens with *overwhelmed*. The screen must orient
before it explains. Two elements compete for top-of-screen dominance: the agent's
brand frame (who sent this) and the offer headline (what is being offered).

**Decision.** Both appear, in order: brand frame first (brief — one framing sentence),
offer headline immediately below (prominent — price, close, cash/financed in Explanation
voice). The headline is the larger, more prominent element. The brand frame establishes
the source; the headline answers "what are they offering?" — which is the first question
that converts *overwhelmed* to *oriented*.

**Consequences.** Brand copy is agent-voiced and Docside-defaulted; the agent sees and
can edit it (copy §1.4). The headline carries provenance handles (§-citations) exactly
as detail rows do. An unreadable headline field renders its absence state in the headline
position, with headline prominence.

---

## DEC-3 — Share surface provenance: §-citation inline and always visible

**Date:** 2026-06-29 · **Status:** DECIDED · **Lives in:** `07-screen-design/share-surface.md` §3, §6 fork 2

**Context.** Doctrine §3.1 v0.2: provenance reaches the seller, without hover. The verify
workspace achieves provenance via a two-pane spatial link. The share surface, mobile-first
and read-only, cannot use that mechanism.

**Decision.** Every field row carries an inline §-citation ("from §3A") — always visible,
no tap required. Small and subordinate to the value; not hidden behind interaction.

**Consequences.** A seller who wants to trace a value sees exactly which section to look
for, without needing to know to ask. The citation maps directly to the static PDF equivalent
(printed inline) from the degradation matrix (handoff §3), making the future PDF path clean.
Options considered: tap-to-reveal (formally satisfies the guarantee only for sellers who
already know to tap) and a bottom-of-page "view source" link (buries it; most sellers won't
find it). Always-visible inline is the only form that delivers provenance to every seller.

---

## DEC-4 — Share surface high-stakes unknowns: elevated visual weight, not interaction

**Date:** 2026-06-29 · **Status:** DECIDED · **Lives in:** `07-screen-design/share-surface.md` §2, §6 fork 3

**Context.** The seller surface is read-only; the seller acknowledges nothing. The agent's
high-stakes gate (states §3) already fired upstream. How is an unreadable high-stakes field
— e.g., purchase price — rendered to the seller so it is unmissable and unmistakable without
an interaction?

**Decision.** High-stakes unreadable fields render with elevated visual weight in their row
(larger, higher-contrast, or higher hierarchy than low-stakes absences). When a high-stakes
field belongs in the offer headline, its absence state appears in the headline position with
headline prominence. A banner callout may be added above the offer content when a headline-
region field is unreadable.

**Consequences.** The seller cannot miss a high-stakes gap; the screen's only instrument is
presentation, and presentation must do the work the acknowledgment gate did for the agent.
Non-laundering (handoff §6) prohibits minimizing honest absences; this fork operationalizes
that at the design level.

---

## DEC-5 — Share surface glosses: always-on

**Date:** 2026-06-29 · **Status:** DECIDED · **Lives in:** `07-screen-design/share-surface.md` §3, §6 fork 4

**Context.** The verify workspace shows glosses on-demand — agents rarely need them. The
seller often doesn't know what a loan contingency is. What is the default gloss treatment
on the seller surface?

**Decision.** Glosses are always visible on the seller surface — inline, below each field
value, one sentence in Explanation voice.

**Consequences.** The seller doesn't need to know they should tap; the plain-English
explanation is just there. This is the mission functioning at its most literal:
"understand a real estate contract." The surface is not agent-dense; showing the gloss
is the right default. On-demand would help only sellers who already suspect they need it.

---

## DEC-6 — Share surface non-laundering: prohibition list as the enforcement mechanism

**Date:** 2026-06-29 · **Status:** DECIDED · **Lives in:** `07-screen-design/share-surface.md` §6 fork 5

**Context.** Handoff §6 (non-laundering): the share never strengthens a claim by dropping a
caveat. Without a concrete check, design iteration naturally drifts toward polish — gaps
soft-pedaled, corrections hidden, absence states greyed out. How is this discipline
enforced at the design level?

**Decision.** Two-part: (1) a naming rule as the principle ("no treatment that makes the
summary look more finished than the verified read"); (2) a prohibition list as the checklist.
Prohibition list: no "Summary complete" copy, no collapsible absence rows, no de-emphasized
correction markers, no absence states styled to blend with confident values, no promotional
copy editorializing the offer.

**Consequences.** Each item on the prohibition list names a specific drift pattern — polish
moves that look like UX improvements but are doctrine violations. The list makes "making it
look nicer" identifiable rather than gradual. Design review against this surface spec uses
the prohibition list as its non-laundering check.

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

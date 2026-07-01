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
for, without needing to know to ask. Options considered: tap-to-reveal (formally satisfies
the guarantee only for sellers who already know to tap) and a bottom-of-page "view source"
link (buries it; most sellers won't find it). Always-visible inline is the only form that
delivers provenance to every seller.

**What this resolves and what it doesn't.** This decision is for the **live-link surface
only**, which is the current form (DEC-1). Choosing always-visible inline rather than
hover-only means the citation *can* survive into print — it is a necessary precondition for
the static-provenance solution. It does **not** solve the hard column. The degradation matrix
(handoff §3, static PDF column) requires "§-citation printed inline + source appendix" — the
source appendix is undesigned and the hard column remains open. The choice made here removes
one blocker; it does not close the work. The static-provenance problem is deferred to the PDF
form spec (handoff §9).

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

## DEC-7 — Comparison-share access control: email-gated, expiring, agent-revocable

**Date:** 2026-06-30 · **Status:** DECIDED · **Lives in:** `06-handoff/handoff.md` §8 · `07-screen-design/comparison-view-plan.md` §8.3 (→ `comparison-share-surface.md`)

**Context.** A comparison share exposes multiple buyers' confidential terms (handoff §7),
and email makes forwarding the norm (DEC-1). A forwarded comparison link is therefore the
highest-confidentiality failure on any Docside surface — categorically worse than a
single-summary leak. handoff §8 had left the access model open ("Confirm before share
ships").

**Decision (Morris).** The comparison share is a **revocable, gated link**: **email-gated
recipient access with expiration and agent revocation.** The agent enters one or more
seller recipient emails; the recipient verifies access by email; the link can expire; the
agent can revoke it at any time; **a forwarded recipient does not automatically receive
access** (they meet the same email gate). It is **not** a fully public, freely forwardable
link.

**Options rejected.** Free-forward tokenized link (a forward exposes every buyer);
**PIN/passcode** (a PIN forwards as easily as the link); **per-view agent approval as the
default** (too much friction — breaks "open it cold on a phone"). Revocability and
expiration are adopted *with* email-gating, not as alternatives to it.

**Consequences.**
- *Scope:* this governs the **public share link**, not the authenticated agent workspace.
  `comparison-view.md`'s "Share comparison" affordance reflects it (enter recipient
  emails; the link is expiring + revocable); the recipient-verification / expiry /
  revocation flow belongs to `comparison-share-surface.md` and the main repo.
- *Single-summary* share links may stay lightweight for the alpha (handoff §8); the
  stronger gate is specific to the multi-buyer comparison.
- *Unblocks* the comparison-share spec, and partially resolves handoff §9's re-share /
  forwarding concern (the leak risk is addressed; the re-share UX is still downstream).

---

## DEC-8 — Default seller-priority dimensions and order

**Date:** 2026-06-30 · **Status:** DECIDED · **Lives in:** `02-information-architecture/information-architecture.md` §7 (seller-priority profile) · `07-screen-design/comparison-view-plan.md` §5, §10

**Context.** The comparison view ranks offers against a listing-scoped seller-priority
profile (IA §7), seeded from agent presets. The profile's *dimensions* and their default
priority order were not enumerated anywhere; the comparison matrix's columns are exactly
these dimensions, so the screen spec needed them fixed.

**Decision (Morris).** The default seller-priority dimensions, **in priority order**, are:
**(1) net to seller, (2) contingencies, (3) financing strength, (4) close speed.** They
are **user-controllable weights, not a fixed verdict** — the agent re-weights them to
reflect this seller's priorities (doctrine §4.2). If a field that feeds a dimension is
**unreadable or unverified, Docside suppresses that dimension rather than guessing**
(doctrine §5; comparison-view-plan §4c).

**Consequences.**
- The dimensions map to high-stakes vocabulary fields and `HIGH_STAKES_FIELD_KEYS`
  (cited, not forked — high-stakes-fields-pointer governance). "Net to seller" is an
  arithmetic of traceable components (price − seller-paid costs), suppressed if any
  component is unread (comparison-view-plan Fork I).
- The at-rest "Ranked by…" basis line renders in this order (comparison-view-plan §4b).
- To be formalized into IA §7 on the next IA bump.

---

## DEC-9 — Comparison layout: hybrid ranked spine + dimension matrix, offers as rows

**Date:** 2026-06-30 · **Status:** DECIDED (LOCK-pending-mockup) · **Lives in:** `07-screen-design/comparison-view.md` §1, §6 Forks C/D

**Context.** The comparison view's core layout is the cascading decision — every
downstream fork depends on it. A pure matrix (offers × dimensions) gives the strongest
cross-offer legibility but reads as a **scoreboard**, which implies scores (copy §2.2
hazard, forbidden). Ranked cards give the strongest per-offer atom and mobile ergonomics
but are weak at *relative* legibility at rest.

**Decision.** A **hybrid**: a ranked **spine** (positions + at-rest adjacent-order reason
previews) beside a **dimension matrix** (offers as rows, weighted dimensions as columns,
terms in cells, leading cell per weighted dimension marked). The scoreboard risk is
defused **structurally** — no total column, no per-offer number, ever; terms in cells,
position in the spine. Offers are rows because a ranking *is* a vertical list; it scales
in N and degrades cleanly to stacked mobile cards.

**Consequences.** Highest design complexity and the most cascading to reverse — so it is
**LOCK-pending-mockup**: the mockup must prove the matrix does not read as a scoreboard
before the lock is final. On reversal, §§1/2/3/5 of the spec and the mockup change
(rollback plan, comparison-view-plan §I). Anchors: doctrine §4.1 (legibility at rest);
copy §2.2 (no scores); NORTH-STAR depth loop.

---

## DEC-10 — Weighting visibility: basis line + compact weights at rest; Customize expands in place

**Date:** 2026-06-30 · **Status:** DECIDED · **Lives in:** `07-screen-design/comparison-view.md` §1, §3.4, §6 Fork F

**Context.** Resolves the doctrine §4.2 `TODO(design)`: how the weighting is shown *at
rest*, before the agent opens Customize. Doctrine §4.2 mandates visible weighting; copy
§2.2 forbids sub-scores. The two are not in tension — the **weighting** is the seller's
priorities; the **sub-score** is per-offer math that never appears.

**Decision.** The always-visible header is a term-based **"Ranked by:" basis line** (in the
DEC-8 default order) plus a **compact relative-weight indicator** (ordered bars/chips,
labeled by dimension, magnitude shown). **Customize** expands this header **in place** into
the free-slider / live-total editor — the same control at two widths (the verify-workspace
precedent). Weights are shown; sub-scores are never shown. The six things visible *instead
of* a sub-score are enumerated in the spec (§3.4): basis line, dimension columns, deciding
terms, leading-cell marks, relative-weight indicator, caveats.

**Consequences.** The order declares its own basis before the agent touches anything —
"legible without interaction" (§4.2). Never visible: a per-offer total, a 0–100, a "0.92
vs 0.78," a star rating, a "best offer" badge.

---

## DEC-11 — Inverted-ranking guarantee: three-tier suppression, withheld decisive order (runtime-dependent)

**Date:** 2026-06-30 · **Status:** DECIDED (runtime-dependent) · **Lives in:** `07-screen-design/comparison-view.md` §2.4, §2.5, §6 Obligation 3

**Context.** Renders doctrine §5 — *"If we cannot trace how a ranking was determined, we
will not present it"* — in pixels for the first time. When a comparison-affecting field is
unreadable, the screen must not fill the gap with a default that could quietly move an
offer up or down the list.

**Decision.** A **three-tier** treatment that degrades from cell to order: **(1) cell** —
"We couldn't read this field" (elevated weight if high-stakes), never blank/dash/default/
guess; **(2) position** — the dimension is suppressed for that offer, **visible-but-
excluded** ("partial — [dimension] unread"), never disappeared (a disappeared dimension
hides the gap — a non-laundering violation, handoff §6); **(3) order** — if the suppressed
dimension would be decisive between two offers, the pairwise order is **withheld** (a
bracketed "can't be separated until [field] is read for [buyer]" group). Every suppression
links back to that offer's verify workspace.

**Consequences.** **Runtime-dependent** (§2.5): tier 3 requires withhold-capable ranking
output from the main repo. Per doctrine §5's DEFER-LINE, the guarantee is generalized today
only for §3G(3); for fields the backend can only *flag* (not *withhold*) at alpha, **tier 3
degrades to tier 2** — a **doctrine-bound** divergence that must be recorded here and
escalated, not accepted silently in screen copy (CLAUDE.md cross-repo rule).

---

## DEC-12 — Net to seller: computed only from traceable components, else suppressed visible-but-excluded

**Date:** 2026-06-30 · **Status:** DECIDED (LOCK-pending-mockup) · **Lives in:** `07-screen-design/comparison-view.md` §2.2, §6 Fork I

**Context.** Net to seller is the top-weighted default dimension (DEC-8) and the §5 danger
in its commonest form: if any component (seller-paid buyer-broker comp `PCT-OR-FLAT`,
seller credits) is unread, a computed net can inherit a guess and **invert the ranking**.

**Decision.** Compute net **only when all components are confidently read**. If any
component is unread, net is **suppressed visible-but-excluded** ("net can't be determined:
[component] unread") — it does not disappear and is not ranked. Net is an **arithmetic of
traceable values**, never a model output — the §3G(3) `buyer_broker_comp` precedent
(domain-vocabulary §5) generalized. Absence states follow the aggregate-field participation
rules (spec §2.2): blank is never zeroed, structurally-null contributes only when both the
vocabulary and the formula define it so.

**Consequences.** **LOCK-pending-mockup:** validate on a real packet with an unread
buyer-broker comp (spec Appendix A-2). The net-to-seller **formula** (which seller-paid
costs feed net) is a main-repo concern the spec cites by name, not defines; if
unestablished, net falls back to components-only for alpha (Fork I fallback).

---

## DEC-13 — Legibility affordance: matrix at rest + adjacent-order preview + pairwise delta on demand

**Date:** 2026-06-30 · **Status:** DECIDED · **Lives in:** `07-screen-design/comparison-view.md` §3.3, §6 Fork G

**Context.** Resolves the doctrine §4.1 `TODO(design)`: the affordance for **relative**
position — "why is A above B?" — distinct from the §3.3 per-offer explanation, which
describes one offer alone.

**Decision.** **At rest:** the leading-cell marks (cross-offer legibility down each column)
plus a terse **adjacent-order reason preview** in the spine — "why does this neighbor sit
above that one?" answerable with no interaction. **On demand:** tapping an offer or the gap
between two adjacent offers yields the full **pairwise "why this order" delta** — pure
terms, signed by direction, scoped to the weighted dimensions. A difference on an unweighted
dimension is noted as "they also differ on X, which you didn't weight," never as a reason
for the order.

**Consequences.** The delta reflects the current weighting and composes with suppression
(DEC-11) — a delta that would rely on an unread dimension says so. Copy constraint (§2.2):
terms only, never scores or weights in the delta text.

---

## DEC-14 — Re-weighting feel: live re-ranking, degrading to apply-then on mobile

**Date:** 2026-06-30 · **Status:** DECIDED (LOCK-pending-mockup) · **Lives in:** `07-screen-design/comparison-view.md` §4, §5, §6 Fork E

**Context.** When the agent changes a weight in Customize, does the order re-rank **live**
(offers move as the weight moves) or **apply-then-reorder**? Seeing the order move when you
move a weight is the strongest proof it is not a black box (doctrine §4.2).

**Decision.** **Live re-ranking**, animated (offers move, don't jump). On mobile, live
re-rank **may fall back to apply-then-reorder** if motion/perf require it — the basis line
stays visible throughout, and the fallback is doctrine-neutral (it changes the feel, not
the guarantee).

**Consequences.** **LOCK-pending-mockup:** the mobile fallback is validated at the mockup /
interaction prototype. Behavior, not animation mechanics, is what this spec fixes (altitude
discipline).

---

## DEC-15 — Per-offer Clause-1 atom: inline expansion → side pane / drill-down, linked to verify

**Date:** 2026-06-30 · **Status:** DECIDED · **Lives in:** `07-screen-design/comparison-view.md` §1, §4, §6 Fork H

**Context.** The comparison inherits all of Clause 1 per offer (doctrine §4). Where does the
per-offer understanding-trust atom (provenance, the six-state grammar, term-based
explanation) live inside the comparison?

**Decision.** **Inline expansion into a side detail pane (desktop) / drill-down (mobile),
with a link back to the full verify workspace** for re-checking. The comparison **composes**
atoms; it never duplicates the verify document pane (source PDF + provenance scroll).

**Consequences.** Provenance is reachable from every matrix cell without leaving the
comparison; deep re-checking routes to the offer's verify workspace. Anchors: doctrine §4;
IA §4.

---

## DEC-16 — Free-text terms: a non-ranked "Other terms" section, quoted verbatim

**Date:** 2026-06-30 · **Status:** DECIDED · **Lives in:** `07-screen-design/comparison-view.md` §1, §6 Fork J

**Context.** `FREE-TEXT-VERBATIM` fields (§3R Other Terms; §3G(2)) are prose, not checkable
values. How do they appear in a matrix built from structured values without being scored
into the order?

**Decision.** A **non-ranked "Other terms" section** below/alongside the weighted matrix —
quoted verbatim in quotation marks, explicitly outside the weighting, present to read,
never scored into the order. A quoted field never enters the comparison as if it were a
verified value, even when the prose contains a number (doctrine §3.2 v0.3(a); copy §2.4).

**Consequences.** The screen "visibly leaves room for everything it can't see"
(seller-workflow §4). Provenance (§-citation) still applies to the quote.

---

## DEC-17 — Set provisionality: a provisional marker until the set is marked complete

**Date:** 2026-06-30 · **Status:** DECIDED · **Lives in:** `07-screen-design/comparison-view.md` §1, §2.3, §6 Fork K

**Context.** The set is open until the deadline (agent-workflow §2), so a comparison built
before the deadline is provisional and the product must not imply a finality the
transaction hasn't reached.

**Decision.** A **set-provisional marker** in the context bar — *"Comparison of [N] offers
in so far"* — until the agent marks the set complete. It is **distinct from** the per-offer
**not-yet-verified** marker (spec §2.3): set-provisional = *more offers may arrive*;
not-yet-verified = *this offer isn't vouched yet*. Both can be true at once and must look
different.

**Consequences.** The share-readiness matrix (spec §4.1) treats a provisional set as
"allowed with explicit disclosure" (the share surface must say "in so far" and imply no
finality), while a not-yet-verified offer is blocked by default.

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
| Comparison surface scope: two documents (agent workspace + comparison share surface), not one (Fork A) | comparison-view.md §6 Fork A · IA §3 |
| Reconciliation gate is a sibling upstream spec, not stage-0 of compare (Fork B) | comparison-view.md §6 Fork B · IA §2.1 · states §4.1 |

> These are not lesser decisions — they're simply already documented where they're
> used. The backfill is about giving each a stable handle and a one-place record, not
> about re-deciding anything.

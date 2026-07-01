# Screen — The Comparison View

> **Status:** v0.1 — screen spec. This specifies the layout, hierarchy, states,
> interactions, and mobile behavior of the agent-facing comparison workspace, and
> locks the design forks (§6) with `DEC-9`…`DEC-17`. It resolves all three
> `TODO(design)` markers the doctrine leaves for ranking-trust (§4.1, §4.2, §4.3/§5).
> The mockup follows once §6 is confirmed on a real packet.
> **Derives from:** `00-foundations/trust-doctrine.md` §2 (the two trust surfaces),
> §3.1–§3.3 (Clause 1, inherited per offer), §4.1–§4.3 (legibility, honest weighting,
> the guarantee), §5 (the inverted-ranking guarantee, full statement) ·
> `08-states-and-edge-cases.md` §1, §1.1 (field states; low-confidence resolution),
> §3, §3.1 (the stakes-weighted share gate; correction/append-only log), §4, §4.1
> (compare-stage edge cases; assembling the set), §6 (states ledger) ·
> `02-information-architecture/information-architecture.md` §2.1 (reconciliation gate;
> §1B auto-join; §1A buyer-name fallback), §3–§5 (two zones; navigation; route map),
> §7 (seller-priority profile, weighting) · `00-foundations/domain-vocabulary.md` §2
> (the five hazard tags), §4–§5 (high-stakes fields; the `PCT-OR-FLAT` / §3G(3)
> precedent) · `10-copy-guidelines/copy-guidelines.md` §1 (the registers), §2.1–§2.2
> (three-way grammar; terms-not-scores), §2.4 (free text verbatim) · `NORTH-STAR.md`
> (the compare row) · `06-handoff/handoff.md` §2, §6, §7–§8 · `04-agent-workflow.md`
> §2 · `05-seller-workflow.md` §4–§5 · `11-design-decisions/decisions.md` DEC-7, DEC-8.
> **Template:** `_templates/screen-spec-template.md`.
> **Plan:** `07-screen-design/comparison-view-plan.md` (v3.0, A–J) — the writing brief
> this spec executes. Worked fixtures and the comparison-share sibling brief that the
> plan carried forward from v2.1 are retained here as **Appendix A** and **Appendix B**.
> **Owns:** the agent-facing comparison workspace — the authenticated
> `/listings/[id]/compare` route. Ranked offer display, the weighting control, the
> legibility affordance, the suppression/withhold treatment, the revise-set re-entry,
> and the compare → share initiation affordance. Active only when **N > 1**.
> **Does NOT own** (each has a named home in §7): the reconciliation gate
> (`reconciliation-gate.md`), the comparison share recipient experience
> (`comparison-share-surface.md` — briefed in Appendix B), the net-to-seller formula
> (main repo), and visual tokens (brand adoption).

---

## 0. The one organizing idea: the order accounts for itself

The verify workspace makes a **value** traceable to the contract — *provenance made
spatial*. The share surface leads with what the offer **is** — *orient first*. The
comparison view is the only screen that carries **ranking-trust** (doctrine §2, Clause
2), and it makes a third thing physical:

> **Every rank is co-present with its basis: the weighting that produced the order and
> the terms that decide each position are visible alongside the order itself — so "why
> is this offer above that one?" is always answerable in plain terms, and the one thing
> the screen will never do is show a position it cannot account for.**

This is the constructive form of the doctrine's two prohibitions — *"An order Docside
cannot explain in plain terms is an order Docside does not present"* (§4.1) and *"If we
cannot trace how a ranking was determined, we will not present it"* (§5). Where verify
makes a value traceable to the contract, comparison makes the **order** traceable to the
weighting and the terms.

The sentence has to account for all three ranking-trust mechanisms at once, because the
screen renders all three for the first time:

| Mechanism (doctrine) | What the screen makes true |
|---|---|
| **Legibility** (§4.1) | The basis and the deciding terms sit next to the order; "why A above B" is answerable at rest and on demand, in terms, never numbers. |
| **Honest weighting** (§4.2) | The weighting that drives the order is visible before any interaction and user-controllable in place; the order is never a black box. |
| **The inverted-ranking guarantee** (§4.3, §5) | A dimension that can't be read is held out visibly; if it would decide an order, that order is withheld, not guessed. |

The comparison view **inherits all of Clause 1 per offer** (doctrine §4) — provenance,
honest uncertainty, term-based explanation recur inside the comparison, because the
per-offer explanation *is* the Clause 1 atom appearing again. Everything below serves the
organizing idea. If two people disagree about any component, this is the sentence they
return to first (template §0).

---

## 1. Layout — regions and hierarchy

Desktop-likely (the compare-and-share moment clusters at the deadline, more deliberate
than verify — agent-workflow §2), but not desktop-only: the Customize control must work
on a phone (§5). Offers are **rows**, weighted dimensions are **columns** (Fork D).

```
┌──────────────────────────────────────────────────────────────────────┐
│  CONTEXT BAR:  Listing · "Comparison of 3 offers in so far" (§K)      │
├──────────────────────────────────────────────────────────────────────┤
│  BASIS HEADER  (weighting, at rest — doctrine §4.2)                   │
│   "Ranked by:  net to seller ▸ contingencies ▸ financing ▸ close"     │
│   [▮▮▮▮ net] [▮▮▮ contingencies] [▮▮ financing] [▮ close]   Customize ▸│
├──────────────────────────────────────────────────────────────────────┤
│  RANKED BODY  (the order + the matrix, co-present)                    │
│                                                                       │
│   spine        │  net to seller │ contingencies │ financing │ close   │
│   ┌──────────┐ │                │               │           │         │
│   │ 1 Chen   │ │  $1,274,000 ◆  │  appraisal    │ no loan ◆ │ 30 days │
│   │  ▸ why ↑ │ │                │  contingency  │           │         │
│   ├──────────┤ │                │               │           │         │
│   │ 2 Reyes  │ │  $1,238,125    │  none ◆       │ 17-day    │ 21 days │
│   │  ▸ why ↑ │ │                │               │ loan cont.│         │
│   ├──────────┤ │                │               │           │         │
│   │ 3 Okafor │ │  $1,218,750    │  none ◆       │ all-cash ◆│ 14 d ◆  │
│   └──────────┘ │                │               │           │         │
│                                                                       │
│   ── Other terms (not ranked — quoted verbatim, §J) ──────────────    │
├──────────────────────────────────────────────────────────────────────┤
│  PER-OFFER DETAIL  (expansion / side pane — the Clause-1 atom, §H)    │
├──────────────────────────────────────────────────────────────────────┤
│  Share comparison ▸   (gated — see §4; DEC-7 email-gated recipients)  │
└──────────────────────────────────────────────────────────────────────┘
```

**Context bar.** Which listing, and the **set-provisional marker** — *"Comparison of
[N] offers in so far"* (Fork K) — so the screen never implies a finality the transaction
hasn't reached (the set is open until the deadline, agent-workflow §2). Minimal chrome,
consistent with verify.

**Basis header.** The always-visible answer to *"what is driving this order?"* — a
term-based **basis line** in the DEC-8 default order (*"Ranked by: net to seller,
contingencies, financing strength, close speed"*) plus a **compact relative-weight
indicator** (ordered bars/chips, labeled by dimension, magnitude shown). This is the
resolution of the §4.2 `TODO(design)`: weighting legible **without interaction**.
**Customize** expands this header **in place** into the free-slider / live-total editor —
the same control at two widths (verify's two-widths invariant). Its trust job: the order
declares its own basis before the agent touches anything.

**Ranked body.** The order and the matrix, co-present. A **ranked spine** down the left
holds positions (1, 2, 3…) and, under each offer, the **at-rest adjacent-order reason
preview** — a terse plain-terms reason for the neighbor relationship ("Above Reyes mainly
on higher net and stronger financing"). To its right, the **dimension matrix**: offers as
rows, the weighted dimensions as columns, each cell holding the offer's **term** in that
dimension (Explanation voice — "21-day close"), with the **leading offer per weighted
dimension marked** (◆). Down a column = "who leads this priority?"; across a row = the
Clause-1 atom for one offer. **Structurally, the body is not a scoreboard:** no total
column, no per-offer number, terms in cells, position in the spine (Fork C). Below the
matrix, a non-ranked **"Other terms"** section carries free-text fields verbatim (Fork J).

**Per-offer detail.** Expanding an offer opens its Clause-1 atom — provenance, the
six-state grammar, term-based explanation — in a side pane (desktop) or drill-down
(mobile), with a link back to the full verify workspace for re-checking (Fork H). The
comparison **composes** atoms; it does not duplicate the verify document pane.

**Share action.** Persistent, gated (§4). The workspace owns the **share-initiation** UI
only (the agent enters recipient emails; the link is expiring + revocable — DEC-7).

**Hierarchy principle.** The screen tells the agent what to read in an explicit order:
**basis (what drives the order) → order + deciding terms (the ranked matrix) → per-offer
detail on demand → share.** The ordering derives from the trust obligation: the agent
sees *why the order is what it is* before the order itself, so no rank ever arrives as an
unaccounted assertion. This is the compare-stage analogue of verify's *attention first,
reading second*.

---

## 2. The state grammar, on screen

This is the densest screen in the product, and density is where the grammar of absence is
likeliest to quietly collapse. The cardinal rule holds at the pixel level, **inside a
matrix cell**:

> **No two of these may look alike.** A shared dash, blank, or grey "N/A" across any two
> states is a defect the mockup must not introduce.

The spec fixes this **before** any individual cell is styled, in one consolidated table.

### 2.1 Consolidated matrix-cell field states

| Field state (states §1) | Matrix-cell treatment | Ranking participation | Provenance / trace | Action |
|---|---|---|---|---|
| **Verified present** (extracted-confident) | the term value, Explanation voice ("21-day close") | participates normally if the dimension is weighted | contract-location handle visible or one click away | open provenance / detail |
| **Agent-corrected** | the corrected term + a "corrected · original: X" marker; original traceable (doctrine §3.1 v0.5) | participates using the corrected value — a corrected value is a vouched value | shows the correction trail plus the original source location | open correction detail / verify |
| **Empty-on-form** | "Not specified on this form" | **never imputed** as zero, none, waived, or intentionally omitted; participation depends on the term and the aggregate rules (§2.2) | shows the form location where the blank occurred | open source / verify if needed |
| **Not-captured** | "Not captured on this form" | excluded from ranking-affecting computation until captured or verified (no value exists to rank) | shows the intake/system origin, not a contract citation | go to verify / capture |
| **Not-applicable / structurally-null** | "Not applicable — [reason]" ("all-cash purchase"), distinct treatment | may contribute to an aggregate **only** if domain-vocabulary and the formula both define it as structurally null | shows *why* it is structurally null, not merely missing | open explanation / source |
| **Unreadable / low-confidence** | "We couldn't read this field" — elevated weight for high-stakes fields (states §1.1 resolves low-confidence → unreadable at verify) | **suppressed** — excluded from that dimension; if decisive, the pairwise order is **withheld** (§2.4) | shows the attempted source location when available | **verify to resolve** |
| **Conflicting / incoherent** | "Conflicting values — needs resolution" | resolves to `null` → treated as unreadable (never a guess); may suppress an aggregate and trigger a withhold if decisive | shows both conflicting traces when available | resolve in verify workspace |

**The three rules the grammar enforces** (states §1; copy §2.1, §4):

- **(a) Blank is never "intentionally omitted."** Asserting the buyer *chose* to omit is
  inferred intent — a `DEFAULT-TRAP` violation (presence ≠ choice, copy §3; the §4
  "inferred intent" anti-pattern). The form shows blank; we show blank; we never narrate
  why.
- **(b) Blank ≠ zero for ranking.** A blank component never defaults to 0 in an aggregate
  (§2.2). Whether a specific blank field carries a contractual meaning (blank = none) is
  field-semantics owned by `domain-vocabulary.md` / the main repo, surfaced via the
  field's state — never guessed by the comparison.
- **(c) Not-applicable, unreadable, and empty are three different cells.** An all-cash
  offer's financing *detail* fields are *N/A* (not compared, not a gap); an unread
  financing field is *unreadable* (suppressed); a blank financing field is *empty* (not
  imputed). This is the single most common way this product would quietly lie; the three
  never share a treatment.

### 2.2 Aggregate-field participation rules (net to seller and any composed dimension)

Aggregates are the highest-risk place for silent lying, because an absence can be
accidentally converted into arithmetic. Net to seller is the primary case (Fork I). The
spec states these rules explicitly:

1. An aggregate may display **as computed** only when the formula is named and every
   required component is traceable as verified, agent-corrected, or explicitly
   structurally-null.
2. Verified and agent-corrected components participate normally, with each component's
   provenance reachable from the aggregate cell.
3. Empty-on-form and not-captured components are **never treated as zero by default.** The
   aggregate is **suppressed visible-but-excluded** unless the main-repo formula
   explicitly defines that absence state as non-participating for that field.
4. Not-applicable / structurally-null components may contribute a neutral value **only**
   when both `domain-vocabulary.md` and the formula identify that exact field state as
   structurally null. Otherwise the aggregate is suppressed.
5. Unreadable, low-confidence, conflicting, or incoherent components **suppress the
   aggregate visible-but-excluded.** If the aggregate would be decisive between adjacent
   offers, the pairwise order is **withheld** (§2.4).
6. Aggregate cells show the **component reason**, not just the value: *"Net can't be
   determined: buyer-broker comp unread"* or *"Net based on price, seller credit, and
   verified buyer-broker comp."*

Net to seller is therefore an **arithmetic of traceable values**, traceable to its
components — never a model output (doctrine §5; the §3G(3) `buyer_broker_comp` precedent,
domain-vocabulary §5, generalized).

### 2.3 The two offer-level states (the interruptible workflow adds these)

The set is open until the deadline and verify is interruptible (agent-workflow §2), so an
offer can sit in the set **before** it has completed verify. Field-level low-confidence is
already resolved at verify (states §1.1), so this is an *offer*-level distinction:

| Offer state | Trigger | Treatment |
|---|---|---|
| **Vouched** | passed the verify → share boundary — every field confirmed, corrected, or marked unreadable | ranks normally; no special marker beyond its position |
| **Not-yet-verified** | in the set, but verify is incomplete | flagged **"not yet verified"** on the row; held out of the asserted ranking (or shown provisionally with a **"verify to rank"** prompt); **never ranked as if vouched.** Visually distinct from the set-provisional marker |
| **Set-provisional** (set-level) | more offers may still arrive | header marker: *"Comparison of [N] offers in so far"* (Fork K). Describes the *set*, not an offer; must look different from not-yet-verified — both can be true at once |

### 2.4 Comparison-specific edge states (states §4) and the three-tier suppression

The inverted-ranking guarantee (doctrine §5) is rendered here as a **three-tier
treatment** that degrades from cell to order (Obligation 3 / DEC-11). Its worked
instances are Appendix A fixtures 2–3.

| State | Trigger | On-screen treatment | Fixture |
|---|---|---|---|
| **Unreadable dimension** | a ranking-feeding field is unreadable for one offer | **Tier 1 — cell:** "We couldn't read this field" (elevated weight if high-stakes). **Tier 2 — position:** the dimension is suppressed for that offer, **visible-but-excluded** ("partial — [dimension] unread") — it does *not* disappear (a disappeared dimension hides the gap — a non-laundering violation, handoff §6). **Tier 3 — order:** if the suppressed dimension would be decisive between two offers, the pairwise order is **withheld** — they render as a bracketed group, *"Can't be separated on your priorities until [field] is read for [buyer]."* Every suppression links back to that offer's verify workspace. | A-2, A-3 |
| **Asymmetric completeness** | offer A has a verified term; offer B left it blank | B's cell: "Not specified on this form" (empty-on-form — visually distinct from unreadable). B is **not imputed, not zeroed, not penalized**; the dimension's ◆ lead-mark excludes B. If the field feeds net, net for B follows §2.2 (suppressed-or-caveated, never silently zeroed). "Intentionally omitted" is never asserted. | (exercises §2.1 rules a/b) |
| **N = 1 degenerate** | dedup / exclusion / revision collapses the set to one | fall back to the **single-offer summary** with a note ("Only one offer is in this comparison"). **No ranking chrome, no weighting header asserting an order over one item.** | A-5 |
| **Tie / near-tie** | offers within a closeness band on the weighted priorities | a **near-tie band** — same visual position, or "Reyes and Chen are very close on your priorities." Pairwise delta: "Nearly even — [A] leads on [terms], [B] leads on [terms]; it's close." **No manufactured decisive order from rounding.** | A-4 |

**Gate-territory states** (states §4.1) belong to the reconciliation gate (§7); the
comparison view owns only its slice: an **unreadable buyer name** (§1A) shows the
**fallback handle** ("Offer 2") — never a guessed name (states §4.1 / IA §2.1); a
mid-compare **duplicate / withdrawn / backup** is handled by the "revise set" re-entry
(§4). The closeness-band width and the confidence threshold are **tuning parameters**
(main repo), not design decisions — the design provides the *states* and their
treatments (§2.5).

### 2.5 Runtime contract this state grammar assumes

The screen can only present these states truthfully if the main repo exposes the runtime
behaviors below. These are dependencies to **name**, not engines to define; what the spec
may **not** do is silently soften the guarantee in pixels. Any alpha degradation is
**doctrine-bound** — recorded in `decisions.md` as a deliberate divergence, not a
screen-level edit (§6, DEC-11; §7).

| Runtime contract | Target behavior | Alpha-degraded behavior, if missing | Required record |
|---|---|---|---|
| **Unknown propagation** for comparison-affecting fields | any unreadable / conflicting / low-confidence field degrades to *unknown*, never to a rank-moving default | the dimension is visible-but-excluded; a field that would be decisive is not shown as decisive | `decisions.md` divergence + main-repo task |
| **Withhold-capable ranking output** | runtime can tell when a suppressed dimension would decide two adjacent offers, so the screen renders a bracketed withheld group (tier 3) | if runtime can only *flag*, the screen shows tier-2 suppression but must not flatten the pair into a confident order | `decisions.md` divergence + doctrine-bound note |
| **Net-to-seller formula symbol** | the spec cites the main-repo formula by name; net is arithmetic of traceable components | if no formula is established, net falls back to components-only for alpha (Fork I fallback) | main-repo formula task + spec deferred note |
| **Closeness-band parameter** | runtime exposes a named parameter for tie/near-tie boundaries | tie/near-tie examples are illustrative only; the mockup must not imply exact boundaries | main-repo tuning task |

Per doctrine §5's `DEFER-LINE`, the guarantee is generalized today only for §3G(3)
(`buyer_broker_comp`, `PCT-OR-FLAT`). Before implementation or a guarantee-claiming
mockup, the main repo must confirm which comparison-affecting fields degrade to *unknown*
on a real packet. If some can only *flag* (not *withhold*) at alpha, **tier 3 degrades to
tier 2** for those fields — and that degradation escalates, doctrine-bound (§7, J-1).

---

## 3. Information design of an element

The screen has two nested repeating units: the **matrix cell** (a single offer × a single
dimension) and the **offer row** it lives in. Both must carry the Clause-1 grammar at the
smallest scale.

### 3.1 The matrix cell

Left-to-right / top-to-bottom, a cell carries:

- **Value or state** — the §2.1 treatment for this field's state. Explanation voice for
  confident values (the vocabulary `spoken`/gloss form — "21-day close"); System voice for
  every absence state. The value is the cell's headline.
- **Leading mark (◆)** — present only on the offer that leads this **weighted** dimension.
  A dimension the seller hasn't weighted carries no lead mark, because it must not read as
  a reason for the order (§3.3).
- **Provenance handle** — **required in every cell.** Clause 1 is inherited per offer even
  inside the dense matrix: the agent must be able to trace any value to its contract
  location without leaving the comparison. On desktop the handle drives the per-offer
  detail pane to the field's source; on the share surface it becomes the static inline
  §-citation (Appendix B). Omitting it is a Clause-1 failure.
- **Suppression caveat** (when applicable) — "partial — [dimension] unread" with a
  **"verify to resolve"** link, per §2.4 tier 2.

### 3.2 The offer row and its header

Each offer row is headed by:

- **Rank position** — the spine number (1, 2, 3…). For a **withheld** pair, the bracketed
  group replaces the two positions (§2.4 tier 3); for a **near-tie**, a shared band.
- **Buyer name** — the §1A name in System voice; unreadable → the **fallback handle**
  ("Offer 2"), never a guessed name (§2.4).
- **Offer-level marker** — "not yet verified" when the offer hasn't cleared verify (§2.3),
  visually distinct from the set-provisional header marker.
- **Adjacent-order reason preview** — the at-rest terse reason for the neighbor
  relationship ("▸ Above Reyes mainly on higher net and stronger financing"). This is the
  at-rest proof that the position has a traceable reason; it is *not* the full explanation.
- **Expand affordance** — opens the Clause-1 detail (§H / §4).

Glosses (vocabulary §1.2) are **on demand** here, as on the verify workspace — the agent
rarely needs them; the seller does, so the comparison *share* surface turns them always-on
(Appendix B). Same data, different default exposure per surface.

### 3.3 The legibility affordance — "why is A above B?" (Obligation 1 / DEC-13)

This resolves the doctrine §4.1 `TODO(design)`: the affordance for **relative** position,
distinct from the §3.3 per-offer explanation (which describes one offer alone). It has two
forms:

- **At rest** — the **leading-cell marks** (◆, cross-offer legibility down each column) plus
  the **adjacent-order reason preview** in the spine (§3.2). Together they let a reviewer
  answer "who leads this priority?" and "why does this neighbor sit above that one?" with
  **no interaction**.
- **On demand** — tapping/clicking an offer, or the gap between two adjacent offers, yields
  the full **pairwise "why this order" delta**: *"Ranked above Reyes on: higher net (+$36k),
  stronger financing (no loan contingency vs. a 17-day loan contingency); even on
  contingencies; Reyes leads on: faster close (21 vs 30 days)."*

Constraints the delta text must hold (copy §2.2): **pure terms, never scores or weights**;
**signed by direction** (who leads on what); **scoped to the weighted dimensions**. A
difference on an *unweighted* dimension is noted as *"they also differ on X, which you
didn't weight,"* never as a reason for the order. The delta reflects the **current**
weighting and composes with suppression — a delta that would rely on an unread dimension
says so rather than silently dropping it.

### 3.4 What is visible *instead of* a sub-score (Obligation 2 support)

The screen mandates visible weighting (doctrine §4.2) while forbidding sub-scores (copy
§2.2). These are not in tension: the **weighting** is the seller's priorities; the
**sub-score** is per-offer math and never appears. The six things visible in its place:

1. the **basis line** — "Ranked by: [priorities, in order]";
2. the **dimension columns** — each a term-bearing priority;
3. the **deciding terms** — the pairwise delta, in business language (§3.3);
4. the **leading-cell marks** — which offer leads each weighted dimension;
5. the **relative-weight indicator** — ordered bars/chips (priority magnitude);
6. the **caveats** — suppression / partial / withheld / tie / near-tie markers.

**Never visible:** a per-offer total, a 0–100, a "0.92 vs 0.78," a star rating, a "best
offer" badge.

---

## 4. Interactions & gates

Every user action and gate on this screen.

- **Customize the weighting** *(Obligation 2 control — Fork F / DEC-10; Fork E / DEC-14).*
  **Trigger:** tap "Customize" in the basis header. **Behavior:** the header expands **in
  place** into the free-slider / live-total editor; as the agent moves a weight, the order
  **re-ranks live** (offers move with an animated transition — the strongest proof the
  order is not a black box, doctrine §4.2). **Gate:** none. **Degraded path:** on mobile,
  live re-rank may fall back to **apply-then-reorder** (§5) — named, doctrine-neutral, and
  recorded (DEC-14 is LOCK-pending-mockup).
- **See "why above"** *(Obligation 1 — §3.3).* **Trigger:** tap an offer or the gap
  between two adjacent offers. **Behavior:** the pairwise delta appears (terms only, signed,
  scoped to weighted dimensions). **Gate:** none.
- **Expand an offer** *(Fork H / DEC-15).* **Trigger:** tap the expand affordance on a row.
  **Behavior:** the Clause-1 detail opens in a side pane (desktop) / drill-down (mobile),
  with a link to the **full verify workspace** for re-checking. The comparison never
  duplicates the verify document pane.
- **Resolve a suppression.** **Trigger:** tap "verify to resolve" on a suppressed cell.
  **Behavior:** jumps to that offer's verify workspace, focused on the unread field.
  Suppression is an honest hold **with a way forward**, never a dead end.
- **Revise the set.** **Trigger:** the agent drops a duplicate, a withdrawn offer, or a
  backup mid-compare. **Behavior:** the offer leaves the set and the order recomputes; the
  set-provisional marker persists. The reconciliation gate governs which offers *enter*
  (§7); the comparison owns only this **re-entry** affordance. If the set collapses to one,
  the N=1 fallback fires (§2.4).
- **Share the comparison** *(gated — DEC-7).* **Trigger:** tap "Share comparison."
  **Behavior:** the agent **enters one or more seller recipient emails**; the link created
  is **expiring and revocable** (the workspace owns the share-*initiation* UI only; the
  recipient-verification / expiry / revocation flow belongs to
  `comparison-share-surface.md`). **Gate:** the **share-readiness matrix** (§4.1). The
  compare → share boundary **inherits the per-offer high-stakes acknowledgment gate**
  (states §3) — it is not eliminated by the comparison; each offer's high-stakes unknowns
  are acknowledged exactly as at single-offer share.

**Zero-interaction facts.** The agent cannot *edit the contract* here (corrections happen
at verify; the contract is immutable, doctrine §3.1). The agent cannot manufacture a rank
for a withheld pair or a not-yet-verified offer — the screen has no affordance to override
the guarantee.

### 4.1 Share-readiness matrix

The workspace owns whether a comparison may be shared **at all** — it must not create a
link the share surface cannot represent honestly (non-laundering, handoff §6).

| Workspace state at share initiation | Outcome | Required workspace behavior |
|---|---|---|
| All included offers vouched; no suppressed decisive dimension; set marked complete | **Allowed** | agent enters recipient emails; link is expiring + revocable |
| A suppressed dimension exists but is **not** decisive | **Allowed with explicit disclosure** | the share preview names the suppressed dimension and confirms it stays visible on the share surface |
| A pairwise order is **withheld** (unread/conflicting field is decisive) | **Allowed only if the share surface preserves the withheld group** | preview shows the bracketed group + withhold reason; no flattened rank or "best" label is sent |
| Runtime can only *flag*, can't determine whether a withhold is required | **Blocked for decisive-looking shares** | agent must verify, remove the offer, or wait for the runtime contract (§2.5) |
| Any included offer is **not-yet-verified** | **Blocked by default** | agent must verify it, remove it, or (only if a later product decision creates that mode) share a clearly-marked draft |
| Set is **provisional** but all included offers are vouched | **Allowed with explicit disclosure** | the share surface must say "Comparison of [N] offers in so far" and imply no finality |
| **N collapses to 1** after exclusions/revisions | **Comparison share blocked; single-offer path used** | remove ranking chrome; route to the single-offer share model |
| Recipient emails missing or invalid | **Blocked** | DEC-7 email-gated access cannot be created until recipients are entered |

---

## 5. Mobile / degraded environment

Not an afterthought: the compare-and-share moment is desk-likely, but an agent may
re-prioritize from a phone at the deadline (agent-workflow §2). The matrix and the
Customize control — the two hardest devices — must survive a single column.

- **Viewport narrowing (mobile).** The **matrix collapses to ranked cards** — one card per
  offer, stacked in rank order, each carrying its per-dimension breakdown and a
  **tap-for-why-above** affordance. The **basis line is always visible** at the minimum
  collapsed state — it is the floor, not an optional element; losing it on mobile would
  hide what produced the order. The set-provisional marker and per-offer "not yet verified"
  markers persist.
- **Customize on mobile.** Opens as a **full-screen or bottom-sheet slider editor**, not a
  desktop-only control. **Live re-rank may fall back to apply-then-reorder** here
  (motion/perf — DEC-14 degraded path); the basis line stays visible while the editor is
  open.
- **No hover.** Nothing on this screen may rely on hover to carry meaning. The pairwise
  delta is a **tap** (on the offer or the gap); provenance is a **tap** (drives the detail
  pane / drill-down); the leading marks and adjacent-order previews are **always printed**,
  not hover-revealed.
- **Static PDF export.** Deferred (inherits handoff §3 / DEC-1). When it ships, every
  invariant needs a static form: leading marks and the basis line printed; the pairwise
  delta rendered as printed adjacent-order reasons; suppression and withheld groups printed
  in place; §-citations printed inline + source appendix (the undesigned hard column,
  DEC-3). Named here; not designed here (§7).
- **Accessibility baseline** (a full pass is deferred to screen design, but the baseline is
  never deferred): the **rank order must be conveyable without color or the ◆ glyph** —
  position is in the semantic order, not only the visual one; each **absence state** carries
  its meaning in **text**, color only reinforcing (states §1); the matrix uses a real table
  semantic (row = offer, column = dimension) so a screen reader can read "Chen, net to
  seller, $1,274,000, leads"; every tap target (why-above, provenance, Customize, verify-to-
  resolve) is keyboard-navigable and labeled; the withheld-group and suppression copy is
  read, not implied by layout alone.

---

## 6. Design forks (to confirm, then lock)

Forks A and B (surface scope; gate placement) are resolved as scope decisions (§0/§7 and
Appendix B). Forks C–K decide layout, components, and trust grammar. **Altitude
discipline:** every fork specifies **behavior and its trust purpose**, not implementation —
`HIGH_STAKES_FIELD_KEYS`, the scoring/weighting engine, and the net-to-seller formula are
**cited as dependencies by name, never redefined here** (high-stakes-fields-pointer
governance: cite, never fork).

### 6.0 DEC allocation and status

The source of truth for decision numbering. A fork may be behaviorally recommended below,
but it is not fully locked until its DEC entry exists with the status shown.

| Item | Decision | DEC | Status | Trigger / note |
|---|---|---:|---|---|
| Fork A | Two documents (workspace + share surface) | *backfill* | LOCKED | promote earlier scope decision without renumber collision |
| Fork B | Reconciliation gate as a sibling upstream spec | *backfill* | LOCKED | promote earlier scope decision without renumber collision |
| Fork C/D | Hybrid ranked spine + matrix; offers as rows | **DEC-9** | LOCK-pending-mockup | lock after the mockup proves the matrix does not read as a scoreboard |
| Fork F / Obl. 2 | At-rest basis line + compact weights; Customize expands in place | **DEC-10** | LOCKED | doctrine §4.2 TODO resolution |
| Obligation 3 | Visible suppression + withheld decisive order | **DEC-11** | LOCKED, runtime-dependent | depends on the withhold-capable runtime contract (§2.5) |
| Fork I | Net computed only from traceable components, else suppressed | **DEC-12** | LOCK-pending-mockup | validate on a real packet; cite the main-repo formula |
| Fork G / Obl. 1 | Matrix + adjacent preview + on-demand pairwise delta | **DEC-13** | LOCKED | doctrine §4.1 TODO resolution |
| Fork E | Live re-ranking while Customize changes weights | **DEC-14** | LOCK-pending-mockup | mobile may degrade to apply-then, with an explicit note |
| Fork H | Per-offer atom in expansion / side pane / drill-down | **DEC-15** | LOCKED | full verify workspace linked, not duplicated |
| Fork J | Free-text terms outside ranked weighting | **DEC-16** | LOCKED | quoted verbatim; never scored into the order |
| Fork K | Set-provisional marker until complete | **DEC-17** | LOCKED | distinct from offer-level not-yet-verified |

### Fork A — Surface scope *(LOCKED)*
**Question.** One combined spec, or two documents? **Locked: two documents** —
`comparison-view.md` (this) for the agent workspace; `comparison-share-surface.md` for the
seller surface. IA §3 forbids the merge ("two distinct information architectures —
conflating them is a category error"); share-surface §7 already defers "the comparison
surface — its own spec follows." **Anchor:** IA §3; share-surface §7; doctrine §2.
**DEC:** backfill (coordinate with the decisions.md backfill index).

### Fork B — Reconciliation gate placement *(LOCKED)*
**Question.** Gate as stage-0 of the comparison, or a separate upstream spec? **Locked:
separate upstream spec** (`reconciliation-gate.md`). Its trust job is *membership made
deliberate* — a precondition for ranking-trust, not ranking-trust itself; it fires at a
different nav location (listing → compare boundary, IA §5). **Anchor:** IA §2.1;
critical-path §3; doctrine §2. **DEC:** backfill.

### Fork C — Core layout model *(LOCK-pending-mockup)*
**Question.** Matrix vs. ranked cards vs. hybrid? **Options.** Matrix — strongest
cross-offer legibility, but reads as a scoreboard (implies scores, copy §2.2 hazard);
ranked cards — strong per-offer atom, mobile-friendly, weak at relative legibility at rest;
hybrid — ranked spine + dimension matrix, no total column, terms in cells. **Recommend:
hybrid.** Defuses the scoreboard risk **structurally**: no per-offer number, no total
column, terms in cells, position not points. **Trade-off:** highest design complexity, most
cascading if reversed — validate the matrix early in the mockup. **Anchor:** doctrine §4.1;
copy §2.2. **DEC-9.**

### Fork D — Orientation *(LOCKED)*
**Question.** Offers as rows or columns? **Locked: offers as rows, dimensions as columns.**
A ranking *is* a vertical list; it scales in N and degrades cleanly to stacked mobile
cards. **Anchor:** NORTH-STAR depth loop; agent-workflow §2. **DEC-9** (same decision as
Fork C).

### Fork E — Re-weighting feel *(LOCK-pending-mockup)*
**Question.** Live re-ranking vs. apply-then-reorder? **Recommend: live re-ranking,**
animated (offers move, don't jump) — the strongest proof the order responds to the agent's
priorities (doctrine §4.2). **Risk:** motion/perf on mobile may require scoping down to
apply-then for the mobile Customize experience (§5). **Anchor:** doctrine §4.2. **DEC-14.**

### Fork F — Customize at rest *(LOCKED)*
**Question.** Collapsed at rest or always open? **Locked: collapsed at rest** — basis line
+ compact weights visible; Customize expands in place. At-rest legibility without the
control's footprint (verify's two-widths precedent). **Anchor:** doctrine §4.2 TODO.
**DEC-10.**

### Fork G — Legibility affordance form *(LOCKED)*
**Question.** What is the UI form of the §4.1 "relative position" affordance? **Locked:
matrix at rest + adjacent-order reason preview + pairwise delta on demand** (§3.3). Pure
terms, signed by direction, scoped to weighted dimensions. **Anchor:** doctrine §4.1 TODO;
copy §2.2. **DEC-13.**

### Fork H — Per-offer Clause-1 atom location *(LOCKED)*
**Question.** Where does the per-offer understanding-trust atom live? **Locked: inline
expansion → side detail pane (desktop) / drill-down (mobile), with a link back to the full
verify workspace.** The comparison composes atoms; it never duplicates the verify document
pane. **Anchor:** doctrine §4 ("inherits all of Clause 1 per offer"); IA §4. **DEC-15.**

### Fork I — Net to seller *(LOCK-pending-mockup; trust-critical)*
**Question.** Compute net as a dimension, or show components only? **Options.** Computed
net — strongest legibility for the "highest net" priority, but if any component
(buyer-broker comp `PCT-OR-FLAT`, credits) is unread the net can inherit a guess and invert
the ranking (the §5 danger in its commonest form); components-only — no aggregation risk,
weakest legibility. **Recommend: compute net only when all components are confidently read;
if any is unread, net is suppressed visible-but-excluded** ("net can't be determined:
[component] unread"). Net = arithmetic of traceable values, never a model output; the
§3G(3) `PCT-OR-FLAT` precedent generalized. Absence states follow §2.2. **Validation:** run
on a real packet with an unread buyer-broker comp (Appendix A-2). **Anchor:** doctrine §5;
domain-vocabulary §5 `buyer_broker_comp`. **DEC-12.**

### Fork J — Free-text / unweightable terms *(LOCKED)*
**Question.** How do `FREE-TEXT-VERBATIM` fields appear in a structured matrix? **Locked: a
non-ranked "Other terms" section** — quoted verbatim, explicitly outside the weighting,
present to read, never scored into the order (a quoted field never enters the comparison as
if it were a verified value — doctrine §3.2 v0.3(a); copy §2.4). The screen "visibly leaves
room for everything it can't see" (seller-workflow §4). **DEC-16.**

### Fork K — Set provisionality *(LOCKED)*
**Question.** Show the comparison as provisional until the set is marked complete? **Locked:
provisional marker until complete** — *"Comparison of [N] offers in so far"* — never
implying a finality the transaction hasn't reached. **Distinct** from the per-offer
not-yet-verified marker (§2.3); both can show at once and must look different. **Anchor:**
agent-workflow §2. **DEC-17.**

---

## 7. Deferred

Everything not in this spec, each with a reason and a named home. Nothing that carries a
doctrine obligation is deferred without stating where that obligation is honored.

- **The comparison share surface spec** — the seller-facing multi-offer view. Fully briefed
  in **Appendix B**; the §5 guarantee and per-offer Clause-1 invariants are honored there,
  not dropped. → home: `07-screen-design/comparison-share-surface.md`.
- **The reconciliation gate spec** — *membership made deliberate*, the comparison's upstream
  dependency (Fork B). The comparison view consumes a curated set and owns only the
  revise-set re-entry. → home: `07-screen-design/reconciliation-gate.md`.
- **The comparison mockup** — built once §6 is confirmed; the Appendix A fixtures seed it,
  and the mockup is the LOCK-pending-mockup trigger for C/D, E, I. → home: screen-design,
  after brand adoption.
- **A comparison worked-specimen** — the natural sequel the Appendix A fixtures seed
  (worked-specimen §5). → home: `10-copy-guidelines/`.
- **Static PDF export** — awaits the static-provenance hard column (DEC-3; handoff §9). §5
  names the static forms; the source appendix is undesigned. → home: the future PDF-form
  spec.
- **Visual design tokens** — typography, color, spacing. This spec locks structure,
  hierarchy, and trust grammar only. → home: brand adoption (assets/README).
- **Agent-controlled buyer aliases** ("Offer A / B / C" instead of names) — a plausible
  later request; the default is to show buyer names to the seller (Appendix B). → home:
  `comparison-share-surface.md`.

### Runtime-contract dependencies (tracked, not blockers for this spec)

These do not block writing — the spec names the runtime contract (§2.5) — but they gate
implementation and any guarantee-claiming mockup:

- **J-1. §5 generalization coverage in the main repo.** The inverted-ranking guarantee is
  generalized today only for §3G(3) (doctrine §5 DEFER-LINE). Before a mockup claims it
  generally, the main repo must confirm which comparison-affecting fields degrade to
  *unknown* on a real packet. Fields that can only *flag* at alpha degrade tier 3 → tier 2,
  **doctrine-bound** (recorded in `decisions.md`, escalated — not silently accepted).
- **J-2. Net-to-seller formula.** Which seller-paid costs feed net is a main-repo concern;
  the spec cites it, does not define it (Fork I). If unestablished, net falls back to
  components-only for alpha. → home: `domain-vocabulary.md` / main repo.
- **J-3. Closeness-band width.** A main-repo tuning parameter; changing it shifts tie/near-
  tie boundaries without a spec revision (§2.5).

---

## Appendix A — Worked fixtures (definition of done)

Illustrative data echoing the worked-specimen's style (not the ground-truth fixture; no CAR
verbatim text). Three offers on one listing, ranked by the DEC-8 default order — **net to
seller ▸ contingencies ▸ financing strength ▸ close speed.** Illustrative net = price −
seller credit − seller-paid buyer-broker comp. The finished spec produces the correct
screen for each fixture.

**Cast.**
- **Reyes** — $1,275,000 · 21-day close · no appraisal contingency · 17-day loan contingency
  · $5,000 seller credit · buyer-broker comp 2.5%. Net = 1,275,000 − 5,000 − 31,875 =
  **$1,238,125**.
- **Chen** — $1,300,000 · 30-day close · appraisal contingency at price · no loan
  contingency · no credit · buyer-broker comp (varies per fixture).
- **Okafor** — $1,250,000 **all-cash** · 14-day close · no contingencies · no credit ·
  buyer-broker comp 2.5%. Net = 1,250,000 − 31,250 = **$1,218,750**.

**A-1 — Clean ranking.** Chen's comp reads as a flat $26,000 → Chen net = $1,274,000. With
net top-weighted, the order is **Chen ▸ Reyes ▸ Okafor.** Leading cells marked (Chen leads
net; Okafor leads contingencies, financing, close). Pairwise delta, Chen vs. Reyes:
*"Ranked above Reyes on: higher net (+$36k), stronger financing (no loan contingency vs. a
17-day loan contingency); even on contingencies; Reyes leads on: faster close (21 vs 30
days)."* No score anywhere. All-cash Okafor sweeps contingencies / financing / close but
trails on net — the top weight decides while the delta still names every dimension. (On the
*financing-strength dimension*, all-cash is the strongest value, not a gap; the financing
*detail* fields — loan amount, type — read *not-applicable* for an all-cash offer, §2.1.)

**A-2 — Suppressed dimension.** Chen's buyer-broker comp reads incoherently (`PCT-OR-FLAT`
conflict) → `null` → **unreadable.** Net depends on comp → Chen's **net cell shows "We
couldn't read this field — net can't be determined: buyer-broker comp unread,"**
visible-but-excluded; Chen is **not ranked on net** and carries a "partial — net unread"
caveat; a **"verify to resolve"** link points to Chen's verify workspace. Chen still ranks
on close and contingencies.

**A-3 — Withheld order.** As A-2, and Reyes and Chen are close enough that **net would
decide** between them. Because net is suppressed for Chen, the **Reyes-vs-Chen order is
withheld** — they render bracketed: *"Can't be separated on your priorities until
buyer-broker comp is read for Chen."* Okafor still ranks (below the bracket). This is the
inverted-ranking guarantee in pixels.

**A-4 — Tie / near-tie.** All fields read; Reyes and Chen land within the closeness band on
the weighted priorities. They render as a **near-tie band:** *"Reyes and Chen are very close
on your priorities."* Pairwise delta: *"Nearly even — Chen leads on net and financing, Reyes
leads on close, even on contingencies; it's close."* No manufactured decisive order.

**A-5 — N = 1.** The reconciliation gate flagged Chen's emailed copy as a duplicate of an
uploaded Chen; the agent dropped one, and Okafor was excluded as a backup → only Reyes
remains. The comparison view **falls back to Reyes's single-offer summary** with *"Only one
offer is in this comparison"* — no ranking chrome, no weighting header.

**A-6 — Forwarded seller share.** The agent shared the comparison to the seller's verified
email (DEC-7). The seller forwards the link to an adult child. Because access is
**email-gated**, the forwarded recipient **does not automatically get in** — opening the
link puts them against the same email gate; the agent can also **revoke** the link or let it
**expire.** The verified seller, on the seller surface, sees: **buyer names**
(Reyes/Chen/Okafor), the **"Ranked by…" basis line**, any **suppressed dimension
visible-but-excluded**, the **§5 guarantee in Principle voice**, **no scores, no "accept."**
This is the comparison-share spec's acceptance case (Appendix B).

---

## Appendix B — The comparison share (sibling brief)

The comparison share surface is the sibling spec (`comparison-share-surface.md`), **not**
part of this document. But `comparison-view.md` briefs it and owns the workspace's
share-initiation affordance. In one line, the comparison share is **N single-offer share
surfaces, ranked, with the basis shown and access tightened** — every Clause-1 invariant per
offer, plus a legible order presented as an **input** to the seller's decision, never the
decision.

### B.1 What it inherits vs. where it diverges (single-offer share → comparison share)

| Element / invariant | Single-offer share (`share-surface.md`) | Comparison share |
|---|---|---|
| Organizing idea | "orient first" — what this offer is | **DIVERGES** → "fit-to-priorities, an input not a verdict" (seller-workflow §4–§5) |
| Per-offer atom (provenance, six absence states distinct, term-based, corrections-as-corrected, glosses always-on, §-citation inline — DEC-3/4/5) | yes, for one offer | **INHERITS, per offer** — the comparison is N atoms |
| Top-of-screen | the one offer's headline terms | **DIVERGES** → the ordered set + the **"Ranked by…" basis line** |
| Weighting display | n/a (no order) | **NEW** → basis line always visible; magnitudes may be simplified for the seller, the basis never hidden (doctrine §4.2; handoff §2 invariant 5) |
| Suppressed dimension | n/a | **NEW** → shown **visible-but-excluded** to the seller ("we couldn't read [field] for [buyer], so this offer isn't ranked on [dimension]") |
| §5 guarantee, Principle voice | absent (single offer) | **NEW** → "If we cannot trace how a ranking was determined, we will not present it" |
| Buyer identity | one buyer (§1A) | **shows each buyer name (§1A)** to the seller; unreadable → fallback handle (states §4.1) |
| Read-only; no acknowledgment; `tel:` call prompt; non-laundering prohibition list (DEC-6) | yes | **INHERITS**; the prohibition list **extends to the order** (no false decisive order, no hidden suppression, no collapsed absence rows in the ranking) |
| Access control | lightweight link acceptable for alpha (handoff §8) | **DIVERGES** → email-gated recipient access, expiring + agent-revocable (DEC-7); a forward doesn't carry access |

### B.2 How ranking reaches the seller (governing principle)

**Ranking does reach the seller — as fit-to-priorities, never as a verdict.** The order
plus the visible "ranked by [their priorities]" basis, with the surface **visibly leaving
room for what it can't see** (a buyer's letter, gut feel — seller-workflow §4). **No "best
offer" verdict, no "accept" action, no score** ("the decision is never the algorithm's" —
seller-workflow §5). This is a stronger obligation than the single-offer surface, which had
no order to caveat.

### B.3 Access control (DEC-7, locked by Morris)

The agent workspace owns the **share-initiation UI only:** the agent enters one or more
seller recipient emails and sees that the link is expiring and revocable. The
recipient-verification flow, expiry handling, and revocation UI belong to
`comparison-share-surface.md` and the main repo. A forwarded recipient who opens the link
does **not** automatically receive access — they meet the same email gate. PIN was rejected
(a PIN forwards as easily as the link); per-view approval was rejected as the default (too
much friction for "open it cold on a phone").

### B.4 Resolved share questions (from the docs)

- **Buyer identity:** show each buyer's name (§1A) to the seller. The seller owns these
  offers on their own property; real-world offer presentation names buyers. Confidentiality
  (handoff §7) is about the link reaching outsiders — addressed by access control, not by
  hiding buyers from the legitimate seller. Unreadable §1A → fallback handle. Agent aliases
  are a possible later option, not the default.
- **Suppressed dimension visible to the seller?** Yes — visible-but-excluded. Omitting it
  would hide a gap to look cleaner — a non-laundering violation (handoff §6) and a DEC-6
  prohibition ("no collapsible absence rows").
- **Same weights as the workspace, or can the agent hide/simplify?** The basis (ordered
  priorities) is always shown; the agent sets the weights (that *is* the seller's priority
  profile) but cannot hide what produced the order. Display may simplify — omit precise bar
  magnitudes — but the basis is never hidden.

### B.5 Template mapping for the sibling spec

`comparison-share-surface.md` is a full screen spec on the same template as `share-surface.md`:
§0 organizing idea "fit-to-priorities, an input not a verdict" · §1 brand frame → ranked set
with "Ranked by…" basis → per-offer groups (N) → call prompt · §2 inherits the six absence
states from `share-surface.md`, adds suppressed-visible-but-excluded and withheld-order
states · §3 per-offer element inherited, buyer-name slot + basis-line element added · §4
zero interactions (read-only), no acknowledgment, `tel:` prompt inherited · §5 mobile-primary
inherited, ranked cards on narrow screens · §6 forks: access-control model (DEC-7 locked),
ranking-presentation principle, weighting-display simplification · §7 deferred: static PDF,
multi-viewer tracking, agent-alias system. **Starting point:** this appendix + `share-surface.md`
as the format model.

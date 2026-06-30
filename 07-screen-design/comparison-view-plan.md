# Plan — The Comparison View (screen-spec Plan 1.0)

> **Status:** v1.0 — plan. This is the plan for writing
> `07-screen-design/comparison-view.md`, not the spec. It resolves scope, names the
> organizing idea, proposes a resolution for every doctrine TODO that lands on this
> screen, lists every design fork with a recommended lock, maps the edge cases, and
> sequences the writing. It is written to be specific enough that the spec can be
> drafted from it without inventing scope or leaving a TODO undefined.
> **Derives from:** `NORTH-STAR.md` (the spine, the depth loop); `trust-doctrine.md`
> §2 (the two trust surfaces), §4 (Clause 2 — ranking-trust), §5 (the inverted-ranking
> guarantee); `information-architecture.md` §2.1 (reconciliation gate), §3 (two zones),
> §4–§5 (nav, routes); `critical-path.md` §3 (the Verify-each → Compare and Compare →
> Share seams); `states-and-edge-cases.md` §4, §4.1; `handoff.md` §7–§8;
> `verify-workspace.md` and `share-surface.md` (format, quality, and fork-discipline
> reference); `copy-guidelines.md`; `domain-vocabulary.md` (dimensions, hazards);
> `_templates/screen-spec-template.md` (the required section structure).
> **Produces:** a writing brief for `comparison-view.md` (the agent workspace), the
> obligations brief for a sibling `comparison-share-surface.md`, and the dependency
> note for a sibling `reconciliation-gate.md`.

---

## 0. Orientation — what this screen is, in one paragraph

The comparison view is the **compare** stage of the spine (`upload → verify →
[compare] → share`), active only when **N > 1**. It is the single screen in the
product that exercises **ranking-trust** (doctrine §2, Clause 2): the trust obligation
that appears when the agent evaluates several offers against a seller's priorities.
Every other screen lives on the *understanding-trust* surface — one offer, made clear.
This one inherits all of that **per offer** (the Clause-1 atom appears again inside the
comparison) and adds three mechanisms the single-offer view never needs: **legibility**
of relative order, **honest weighting**, and the **inverted-ranking guarantee**
(doctrine §4–§5). It is the retention engine (NORTH-STAR's depth loop) and the only
home of the most product-specific guarantee in the doctrine — a guarantee that has
never been rendered. This plan exists to render it correctly the first time.

---

## 1. The one organizing idea

**Handle: the order accounts for itself.**

> **One sentence:** the weighting that drives the order and the terms that decide
> each position are continuously visible and live alongside the order itself — so
> "why is this offer above that one?" is always answerable in plain terms, and the
> one thing the screen will never do is show a position it cannot account for.

This is the comparison stage's equivalent of verify's *provenance made spatial* and
share's *orient first*. It is derived from the trust obligation, not from what is
convenient:

| Screen | Stage trust obligation | Organizing idea | The move it makes physical |
|---|---|---|---|
| Verify | understanding-trust — a wrong *fact* | **provenance made spatial** | focus a value → the document moves to its source |
| Share | understanding-trust, for a vulnerable reader | **orient first** | lead with what the offer *is*, before any detail |
| **Compare** | **ranking-trust — a wrong *order*** | **the order accounts for itself** | every rank co-present with its basis; re-weight and watch the order respond; withhold any order that can't be traced |

The idea is the constructive form of the doctrine's two prohibitions — *"An order
Docside cannot explain in plain terms is an order Docside does not present"* (§4.1) and
*"If we cannot trace how a ranking was determined, we will not present it"* (§5). Where
verify makes a **value** traceable to the contract, comparison makes the **order**
traceable to the weighting and the terms. Provenance, lifted from the field to the
ranking. If two people disagree about any component below, this is the sentence they
return to first (template §0).

---

## 2. Surface scope — two documents, not one (resolves Fork A)

The spec must serve two surfaces:

- **The agent-facing comparison workspace** — authenticated, desktop-likely, rich,
  interactive (re-weight, expand, trace, revise the set).
- **The comparison share surface** — public `/share/[token]` (the N > 1 case),
  mobile-first, read-only, no login, possibly a static PDF later.

**Recommendation: two separate documents.** `comparison-view.md` (this plan's target)
specifies the **agent workspace**; a sibling `comparison-share-surface.md` specifies
the **seller surface**, written *after* this one — exactly as `share-surface.md`
followed `verify-workspace.md`.

**Rationale.**
- **Precedent is unambiguous.** The single-offer agent surface (verify) and seller
  surface (share) are already two documents, and `share-surface.md` §7 explicitly
  defers "the comparison surface… its own spec follows." This plan honors that promise
  rather than reopening it.
- **IA §3 forbids the merge.** "There are two distinct information architectures, not
  one… Conflating them is a category error." The two zones differ on who, device,
  contains, nav, provenance mechanism, and trust job. A comparison does not change
  that boundary; it raises the stakes on it (a comparison leak exposes *multiple*
  buyers — handoff §7).
- **Different organizing ideas.** The workspace idea is *the order accounts for
  itself* (the agent checks and re-weights). The share idea is the seller-facing one
  the sibling spec must derive — *fit-to-priorities, an input not a verdict*
  (seller-workflow §4–§5). One document cannot lead with two organizing ideas.
- **The share carries its own open decision** (access control, handoff §8) that the
  workspace does not. Bundling would stall the workspace spec behind an unrelated
  unresolved question.
- **Reviewability.** Two focused specs that each earn the rigor verify/share earned
  beat one sprawling document where neither surface gets it.

`comparison-view.md` will carry a short **"handoff to the comparison share"** pointer
section (parallel to verify §7 and share §7) that names what crosses to the seller and
defers the full treatment to the sibling. Requirement 7 of this plan (§7 below) writes
that obligations brief so the sibling can be drafted immediately after.

**Fallback (named, not recommended):** if the team insists on a single artifact, the
share surface becomes `comparison-view.md` §8, and §7 of this plan seeds that section
verbatim instead of a sibling. Rejected for the reasons above; recorded so the choice
is explicit, not silent.

---

## 3. The reconciliation gate — a sibling spec this one depends on (resolves Fork B)

The reconciliation gate (IA §2.1, states §4.1) is the moment the agent decides which
offers **enter** the comparison — assembling membership across the two intake channels
(upload + inbound email), with source visible, duplicates flagged, and per-offer
exclusion.

**Recommendation: its own spec (`reconciliation-gate.md`), not a section of the
comparison view.** `comparison-view.md` *depends on* it and owns only the parts that
are intrinsically comparison-internal.

**Rationale.**
- **Distinct trust surface.** The gate's trust job is *membership made deliberate*
  ("a comparison is only as trustworthy as its membership is deliberate," states §4.1)
  — a **precondition** for ranking-trust, not ranking-trust itself. The comparison
  view's job is *order made accountable*. One organizing idea per screen; the gate has
  its own.
- **Structurally upstream.** Critical-path §3 places it on the **Verify-each →
  Compare** seam: "the reconciliation gate has run, duplicates are resolved, each
  offer's inclusion is deliberate" is *what crosses into* compare. Its output is the
  comparison's input.
- **Different nav location.** It fires at the listing → compare boundary
  (`/listings/[id]` → `/listings/[id]/compare`, IA §5), and its trigger is
  listing-level (uploaded offers meeting already-present emailed offers), not
  compare-internal.
- **Already named as a separate deferred screen** in verify-workspace §7.

**What `comparison-view.md` must still own (the comparison-internal slice):**
- the **curated-set precondition** stated explicitly (the view renders a set the agent
  placed deliberately; it never assumes membership);
- the **"revise the set" re-entry** affordance — the agent realizes mid-compare they
  must drop the duplicate / withdrawn / backup, and jumps back to the gate;
- the **provisional-set state** — the set is open until the deadline (agent-workflow
  §2), so the view must not imply a finality the transaction hasn't reached;
- the **N collapses to 1** consequence (exclusion/dedup can drop the set to one →
  single-offer fallback, §6 below).

**Alternative considered:** make the gate "stage 0" of the comparison workspace
(reconcile → profile → compare reads as one flow near the deadline, agent-workflow
§4.2). Rejected: it would load the comparison view's organizing idea with a second,
different trust job, and the gate also governs the listing view, not just compare.
Continuity is preserved by the re-entry affordance, not by absorption.

---

## 4. The three doctrine TODOs that land here — proposed resolutions

These are the three `TODO(design)` markers in doctrine §4–§5. The spec must close all
three (no TODO for this screen may survive into the spec). Each resolution below is
concrete enough to draft and to lock as a DEC.

### 4a. Legibility of *relative* position (doctrine §4.1 TODO)

**The question.** "Why is offer A above offer B?" must be answerable in terms the
agent could repeat to a seller — and this is **distinct from** the per-offer
explanation of 3.3 (which describes one offer's terms). 4.1 is about the *delta*.

**Proposed resolution — a dimension matrix at rest, a pairwise delta on demand.**
- **At rest (the scaffold):** the comparison is a **dimension matrix** — offers in
  ranked order down the side, the **weighted dimensions** across the top (drawn from
  the seller-priority profile: net to seller, close speed, contingencies, financing
  strength, …). Each cell holds the offer's **term** in that dimension (Explanation
  voice — "21-day close," "no appraisal contingency"), and the **leading offer per
  weighted dimension is marked**. Reading **down a column** answers "who leads on this
  priority?"; reading **across a row** is the Clause-1 atom for one offer. The basis of
  the order is legible *without any interaction* — the matrix is the at-rest legibility.
- **On demand (the §4.1 affordance proper):** tapping an offer (or the gap between two
  adjacent offers) yields a **pairwise "why this order" delta** — "Ranked above
  [next] on: higher price, faster close; [next] leads on: lower buyer-broker comp."
  Pure terms, signed by direction, **scoped to the weighted dimensions** (a difference
  on a dimension the seller didn't prioritize is noted as "they also differ on X,
  which you didn't weight," never as a reason for the order).
- **Constraints it must honor:** terms only, never scores (copy §2.2); reflects the
  *current* weighting (re-weighting changes which deltas explain the order); composes
  with suppression (4c) — a delta that would rely on an unread dimension must say so,
  not silently drop it.

This gives the doctrine's literal question a literal UI answer, and keeps it separate
from 3.3: 3.3 is one row read aloud; 4.1 is the difference between two rows read aloud.

### 4b. The weighting display *at rest* (doctrine §4.2 TODO)

**The question.** The free-slider / live-total **Customize** model is the interactive
control. What does the weighting look like *before* Customize is opened? "The default
weighting must be legible without interaction."

**Proposed resolution — the "Ranked by" basis statement, with a compact relative-weight
indicator, as the always-visible header; Customize expands it in place.**
- **At rest:** a term-based, ordered **basis line** — *"Ranked by: highest net to
  seller, fastest close, fewest contingencies"* (the exact phrasing already used in
  handoff §7 and seller-workflow §4) — paired with a **compact relative-weight
  indicator** (ordered bars or chips, labeled by dimension, showing magnitude). This
  sits at the top of the comparison, above the matrix: the order's **declared basis**,
  legible at a glance.
- **Customize** expands the header **in place** into the free-slider / live-total
  editor (doctrine §4.2). At-rest and Customize are the **same control at two widths**
  — the same invariant verify used for its provenance link, and the same collapse
  discipline share used for its affordances.
- **Default source:** the listing-scoped seller-priority profile, seeded from
  agent-level presets (IA §7). "At rest" = the seeded or last-saved profile, shown
  legibly — never a hidden default.

**The subtle line the spec must hold (and the testing criteria must check):**
> **Weights are shown; sub-scores are not.** Doctrine §4.2 *mandates* that the
> weighting (seller priorities) be visible. Copy §2.2 *forbids* sub-scores from the
> copy. These are not in tension: the **weighting** is the seller's stated priorities,
> shown as ordered terms and relative magnitudes; the **sub-score** is the per-offer
> math that turns weights + terms into a position, and it never appears. The header
> shows priorities; the matrix shows terms; **no per-offer number and no total score
> ever renders.** This is the easiest place on the screen to violate the doctrine by
> accident — naming it here pre-empts it.

### 4c. The inverted-ranking guarantee, made visible (doctrine §5)

**The question.** When a comparison-affecting dimension is suppressed because a field
is unreadable, what does the agent see? The guarantee: *"marks it unknown and tells
you so — it does not fill the gap with a default that could quietly move an offer up or
down the list… If we cannot trace how a ranking was determined, we will not present
it."*

**Proposed resolution — a three-tier treatment that degrades from cell to order:**
1. **At the cell:** the unreadable comparison-affecting field renders with the standard
   **unreadable** absence treatment ("We couldn't read this field"), at elevated visual
   weight for high-stakes fields (consistent with states §1 and the share-surface
   DEC-4 logic). Never blank, never a dash, never a default, never a guess.
2. **At the offer's position:** the dimension that field feeds is **suppressed for that
   offer** — the offer is explicitly *not ranked on [dimension]*, and its position
   carries a visible **"partial — [dimension] unread"** caveat. The weighting header
   reflects that this offer's rank excludes that dimension.
3. **At the order (the §5 hard guarantee):** if the suppressed dimension would be
   **decisive** between two offers — the order between them flips on, or cannot be
   determined without, the unread value — the product **does not assert that pairwise
   order.** Those offers render as a **bracketed "can't be separated on your priorities
   until [field] is read"** group, with the field named. This is the one place in the
   product that visibly **withholds** an order rather than guess it — the inverted-
   ranking guarantee turned into pixels.

**The resolution path (a deliberate cross-screen tie):** because reads are resolved at
verify (states §1.1), every suppression treatment links **back to that offer's verify
workspace** for that field — "read it at verify to rank this dimension." The agent can
confirm/correct/mark-unreadable there, and the order updates. Suppression is never a
dead end; it is an honest hold with a way forward.

**Cross-repo caveat (flag in the spec, per CLAUDE.md's seam rule):** doctrine §5's
DEFER-LINE states this guarantee is honored today only in the §3G(3) buyer-broker-comp
field and is **not yet generalized**. Resolution 4c specifies the *design* of the
guarantee; the per-field runtime generalization (degrade-to-unknown rather than to a
ranking-moving default) is **tracked main-repo work**. The spec specifies what the
agent sees; it must not claim the system already keeps the guarantee for every field.

---

## 5. Design forks — every place two reasonable options decide the screen

Forks A (surface scope) and B (gate placement) are resolved in §2 and §3. The
remaining forks decide layout, components, and trust grammar. Each carries a
recommended lock with its anchor; the spec will record locks as DEC-7 onward
(coordinating numbers with any decisions-log backfill so they don't collide). Forks
flagged **LOCK-pending-mockup** are the high-risk ones the mockup must validate (§12).

### Fork C — Core layout: matrix vs. ranked cards vs. hybrid  *(the cascading fork)*
- **Matrix** (offers × dimensions): strongest cross-offer legibility (read down a
  column); supports legibility-at-rest (4a); scales in dimensions. Risk: reads as a
  **scoreboard**, and a scoreboard implies scores — a trust hazard (copy §2.2).
- **Ranked cards** (a stacked offer card per position): strongest per-offer Clause-1
  atom; mobile-friendly. Weak at *relative* legibility — "why A over B" by scrolling
  cards is hard.
- **Hybrid** (a ranked order + a dimension matrix as the comparison body): both the
  order and its basis co-present.
- **Recommend: hybrid — a ranked order spine + a dimension matrix as the primary
  comparison surface**, because the organizing idea (*the order accounts for itself*)
  requires the order **and** its basis in one view. Defuse the scoreboard risk
  structurally: **no total column, no per-offer score, ever** — cells hold terms, the
  spine holds positions. Anchor: doctrine §2 (compare inherits Clause 1 per offer *and*
  adds the relative surface); copy §2.2. **LOCK-pending-mockup.**

### Fork D — Orientation: offers-as-rows vs. offers-as-columns
- **Offers as rows** (dimension per column): a ranking *is* a vertical list; scales in
  N (more offers = vertical scroll, natural); degrades cleanly to mobile cards.
- **Offers as columns** (dimension per row): matches share's Money/Timing/Contingencies/
  Terms stacking; good for reading one offer top-to-bottom; breaks down at large N
  (horizontal scroll).
- **Recommend: offers as rows, dimensions as columns** for the agent workspace — the
  order is the spine and reads as a vertical list; N can be 5–7+. Anchor: NORTH-STAR
  (the depth loop is many offers); agent-workflow §2 (sets cluster near a deadline).
  **LOCKED.** (Mobile inverts this to per-offer cards — §10 phase 6.)

### Fork E — Re-weighting feel: live re-rank vs. apply-then-reorder
- **Live** (move a slider → the order re-orders immediately): makes the **causal link
  between weighting and order visible** — the core trust point of honest weighting.
- **Apply-then** (edit weights, press apply): calmer, less motion; hides the causal
  link behind a button.
- **Recommend: live re-ranking**, with a clear animated transition (offers move to new
  positions, they don't jump). Seeing the order move when you move a weight is the
  strongest possible proof the order is not a black box. Anchor: doctrine §4.2
  ("free-slider / live-total… see and change what's driving the order"). **LOCK-pending-
  mockup** (motion/perf is the validation risk; scope-reduction lever in §9).

### Fork F — Customize at rest: collapsed vs. always-open
- **Collapsed** (the "Ranked by" basis line + compact weights; Customize expands):
  keeps order/matrix primary; the weighting is the declared-basis header.
- **Always-open** (sliders always visible): the control is never hidden, but it
  competes with the order for space and attention.
- **Recommend: collapsed at rest** (per 4b) — at-rest legibility without the control's
  footprint; Customize expands the same object. Anchor: doctrine §4.2 TODO (legible at
  rest); the verify "same control at two widths" precedent. **LOCKED.**

### Fork G — The legibility affordance form
- **Pairwise "why A over B" delta** / **per-offer "what lifted this"** / **matrix-only
  (marked leading cells are the whole explanation)**.
- **Recommend: matrix at rest + pairwise delta on demand** (per 4a). The marked
  leading cells carry at-rest legibility; the pairwise delta answers the doctrine's
  literal *relative* question, distinct from 3.3. Anchor: doctrine §4.1. **LOCKED.**

### Fork H — Where the per-offer Clause-1 atom (the full verified summary) lives
- **Inline-expandable row** / **link out to that offer's verify-or-summary view** /
  **a side detail pane**.
- **Recommend: inline expansion into a side detail pane on desktop (drill-down on
  mobile), with a link to the full verify workspace** for re-checking/correcting. Keeps
  the agent in the comparison while honoring that the atom already has a home; the
  comparison *composes* atoms, it doesn't replace them. Anchor: doctrine §4 (the atom
  recurs inside the comparison); IA §4 (verify is the atom's canonical home).
  **LOCKED.**

### Fork I — "Net to seller": computed dimension vs. components only  *(trust-critical)*
- **Computed net** (price − seller-paid costs): directly serves the "highest net"
  priority (handoff §7, seller-workflow §4); but net depends on fields that can be
  unreadable (buyer-broker comp `PCT-OR-FLAT`, seller credits), so a naive net inherits
  a guess and can **invert the order** — the exact §5 danger.
- **Components only** (show price, credits, comp; let the reader assemble net): safest,
  least legible.
- **Recommend: show net to seller as a computed dimension, but only when all its
  components are confidently read; if any component is unread, net drops to the
  suppression treatment (4c) — "net can't be determined: [component] unread," never a
  partial-net guess.** Net is then an **arithmetic of traceable values**, traceable to
  its components — the same move the worked specimen already makes with *"$250,000
  down"* (derived from price − financing, both present and traceable) — **not** a model
  guess. Anchor: worked-specimen §1 (derivation from traceable values is allowed);
  doctrine §5 and the §3G(3) precedent (a guessed component must degrade to unknown).
  **LOCK-pending-mockup** (validate on a real packet with an unread component).

### Fork J — Free-text / unweightable terms in a dimension-organized matrix
- Free-text fields (`other_terms`, additional seller-credit terms) are
  `FREE-TEXT-VERBATIM`: doctrine §3.2 v0.3 forbids them from entering the comparison as
  if verified, even when the prose contains a number.
- **Recommend: a non-ranked "Other terms" section in the matrix, quoted verbatim,
  explicitly outside the weighting** — present to read, never scored into the order.
  This is also where the screen "visibly leaves room for everything it can't see"
  (seller-workflow §4). Anchor: doctrine §3.2 v0.3(a); copy §2.4. **LOCKED.**

### Fork K — Provisionality: provisional set vs. present-as-final
- The set is open until the deadline (agent-workflow §2); a comparison built early is
  provisional.
- **Recommend: a provisional marker until the agent marks the set complete** —
  *"Comparison of the 4 offers in so far"* — so the product never implies a finality
  the transaction hasn't reached. Anchor: agent-workflow §2. **LOCKED.**

---

## 6. Comparison-specific edge cases → screen treatments (states §4)

States §4.1 (assembling the set: cross-channel duplicate, unreadable buyer-name label,
source ambiguity, inclusion granularity) belongs to the **reconciliation-gate** spec
(§3); the comparison view inherits only the *result* (a curated set) and the re-entry
affordance. The four states §4 cases below are the **comparison view's own**:

| Edge case | Trigger | Screen treatment | Anchor |
|---|---|---|---|
| **Unreadable comparison-affecting field** | a ranking-feeding field is unreadable for one offer | the **three-tier suppression** of 4c: cell unreadable → dimension suppressed for that offer with a "partial" caveat → if decisive, the pairwise **order is withheld**; link back to verify to resolve | doctrine §5; states §4 |
| **Asymmetric completeness** | offer A specifies a term, offer B left it blank | B's cell shows **"Not specified on this form"** (empty-on-form — visually distinct from unreadable); B is **not imputed** a value, **not** defaulted, **not** silently penalized; the dimension's lead-marking simply excludes B | states §1, §4 |
| **N = 1 in the comparison** | dedup/exclusion (or only one offer in) collapses the set to one | **fall back to the single-offer summary** (the verify-derived summary / share preview) with a note ("Only one offer is in this comparison"); **no ranking chrome, no weighting header asserting an order over one item** | states §4 |
| **Tie / near-tie** | offers are within a closeness band on the weighted priorities | show them as a **tie / near-tie band** — same position or a visible "these two are very close on your priorities"; the pairwise delta reads "nearly even; they differ on [terms] but it's close"; **never a false decisive order from rounding** | states §4; copy (no false precision) |

Two notes for the spec:
- The **closeness band width** (what counts as a near-tie) and the **confidence
  threshold** are *tuning* questions for extraction/scoring, not design questions — the
  design provides the **states** (tie/near-tie, suppressed) and their treatments; it
  does not set the numbers (mirrors states §1.1's handling of the confidence
  threshold).
- The dangerous collapses from states §1 must hold at the pixel level **inside the
  matrix**, where density makes them likeliest to fail: *empty-on-form vs. unreadable*
  (a blank cell from "they didn't specify" must not look like "we couldn't read it"),
  and *agent-corrected vs. present-confident* (a corrected cell wears its marker even
  in a dense grid).

---

## 7. The comparison share obligations (the brief for `comparison-share-surface.md`)

The sibling seller surface inherits **every single-offer share invariant per offer**
(handoff §2; critical-path Verify-each → Compare): provenance reaches the seller
without hover, corrected values shown as corrected, the six absence states distinct,
term-based with no scores, non-laundering. It then **adds** what the single-offer
surface never carried:

- **The order, ranked by the seller's own priorities.** The at-rest **"Ranked by:
  highest net, fastest close, fewest contingencies"** basis statement (4b) crosses to
  the seller — the order is legible because the basis is shown, not because a number
  declares a winner (handoff §7).
- **Ranking as input, not verdict** — the governing decision for how ranking reaches
  the seller. **Ranking does reach the seller**, but as **fit-to-priorities**, with the
  surface *visibly leaving room for what it can't see* (a buyer's letter, gut feel —
  seller-workflow §4). **No "best offer" verdict, no "accept" action, no score.** The
  seller "must never feel a score decided for them" (seller-workflow §5). This is a
  stronger obligation than the single-offer surface, which had no order to caveat.
- **The §5 guarantee, surfaced in Principle voice.** The public statement — *"If we
  cannot trace how a ranking was determined, we will not present it"* — belongs on this
  surface (worked-specimen §2 places the ranking guarantee on the comparison view, not
  the single offer). The suppression / withheld-order honesty (4c) crosses too, degraded
  for read-only / mobile / no-hover.
- **Stronger access control.** A comparison share exposes **multiple buyers'**
  confidential terms; a forwarded comparison link is a multi-buyer breach (handoff §7).
  The comparison-share spec must adopt **stronger access control than the single-summary
  share** — handoff §8 recommends revocable links, comparison links email-gated or
  expiring. This is an **open decision** (handoff §8, DEC-1's raised concern); the
  sibling spec resolves or inherits it. **This plan does not resolve it** —
  `DEFER-LINE:` access-control model → home: handoff §8 / the comparison-share spec.

> **In sum:** the comparison share is *N single-offer share surfaces, ranked, with the
> basis shown and access tightened* — every Clause-1 invariant per offer, plus a legible
> order presented as an input to the seller's decision, never as the decision.

---

## 8. Assumptions (things this plan depends on that the docs don't settle)

- **The seller-priority dimension set is small and named.** IA §7 locks that the
  profile is listing-scoped and preset-seeded, but the **actual dimensions** (net,
  close speed, contingencies, financing strength, …) and their mapping to vocabulary
  fields are enumerated nowhere. The matrix columns = these dimensions. *The spec will
  likely have to propose the default dimension set*, grounded in the high-stakes
  vocabulary fields and `HIGH_STAKES_FIELD_KEYS` (not invented metrics). Flag as the
  first thing to confirm.
- **The main repo can support legible, accountable ranking.** Specifically that it can
  (a) produce an order from a weighting, (b) expose **which terms drove each position**
  (for 4a), and (c) **suppress a dimension / withhold an order** when a field is unread
  (for 4c). Per doctrine §5's DEFER-LINE, (c) is **not yet generalized** — a real
  dependency, not a given.
- **Net to seller is computable from traceable components** (Fork I) — net = price −
  traceable seller-paid costs, suppressible when any component is unread. The formula
  and component list are main-repo concerns; the spec assumes net is *arithmetic of
  traceable values*, not a model output.
- **"Comparison-affecting field" has a definition.** 4c needs to know which fields are
  comparison-affecting. Assume it = the active weighting's source fields ⊇
  `HIGH_STAKES_FIELD_KEYS`, **single-sourced from the main repo, not forked here**
  (high-stakes-fields-pointer governance).
- **`reconciliation-gate.md` will exist** (or its precondition is stubbed) before this
  spec is "complete," since comparison-view depends on a curated set (§3).
- **The agent workspace is desktop-primary for compare**, mobile-capable. Unlike verify
  (explicitly "offer 3 of 7 on a phone between showings"), the **compare-and-share
  moment clusters at the deadline** (agent-workflow §2) — more deliberate, more
  desk-likely. The matrix needs width; mobile is a real but secondary case.
- **Visual tokens are deferred** to brand adoption (assets/README, verify §7, share §7).
  The spec locks structure, hierarchy, and trust grammar — not color, type, or spacing.

---

## 9. Risks (and the scope-reduction lever for each)

- **The scoreboard trap.** A matrix naturally reads as a scorecard, and the product
  forbids score narration (copy §2.2) and forbids the order feeling like a verdict
  (seller-workflow §5). *Lever:* no total column, no per-offer number, terms-in-cells,
  position-not-points — a permanent design constraint, restated in the testing criteria.
- **The inverted-ranking guarantee isn't generalized in the backend** (doctrine §5
  DEFER-LINE). The screen's signature feature (4c) depends on un-built runtime
  behavior. *Lever:* spec the *design* and name the cross-repo dependency; if the
  backend can only *flag* (not *withhold*) for some fields at alpha, 4c degrades from
  "withhold the order" to "flag the order as partial" — **but that degradation touches
  the doctrine and must be reconciled up, not silently** (see §12).
- **Net-to-seller is a ranking-moving number** (Fork I) — exactly the §5 danger zone.
  *Lever:* net suppresses whenever any component is unread; if even that is too risky
  for alpha, fall back to components-only (lose legibility, keep safety).
- **The dimension set is unspecified** (§8). *Lever:* propose a fixed small default set
  grounded in vocabulary + HIGH_STAKES, mark "to confirm," and keep the matrix
  dimension-agnostic (it renders whatever the profile defines).
- **Live re-ranking is heavy to specify and build** (Fork E). *Lever:* fall back to
  apply-then-reorder for alpha (lose some "see what drives the order" value, keep the
  control visible).
- **Three specs of scope** (workspace + share + gate). *Lever:* the §2/§3 splits are
  themselves risk control — write `comparison-view.md` first and fully; defer share and
  gate to their own specs, exactly as share followed verify.
- **Access control is an open decision** (handoff §8) — the comparison share can't be
  fully specified until it closes. *Lever:* single-summary shares ship first; the
  comparison share waits on access control (already the handoff §8 posture).
- **The mobile matrix.** The core legibility device is hardest exactly where width is
  scarce. *Lever:* mobile degrades to ranked cards + per-card dimension breakdown +
  tap-for-why-above; severity is reduced because compare is more desk-likely than
  verify.

---

## 10. Phases for writing the spec (dependency-ordered)

The template's section order is the *output* order; the *writing* order front-loads the
decisions everything else hangs on (the same sequence verify/share followed: surface
the forks, lock them, then mockup).

- **Phase 0 — Settle meta-scope (Forks A, B).** Decide two-docs (§2) and gate-as-sibling
  (§3). Determines what `comparison-view.md` even contains. Everything assumes it.
- **Phase 1 — Lock the organizing idea (template §0) and the core layout (Forks C, D).**
  The matrix + ranked-spine hybrid, offers-as-rows. Every downstream section hangs on
  the layout; this is the return-to anchor.
- **Phase 2 — Resolve the three doctrine TODOs (4a, 4b, 4c) and their forks (E, F, G, I,
  J).** This is the screen's reason to exist (ranking-trust). The element and
  interaction detail are *expressions* of these; design them before the detail.
- **Phase 3 — Layout/regions (template §1) and the core repeating unit (template §3).**
  Regions: weighting header, ranked matrix body, per-offer expansion/detail pane, order
  spine. Decompose the core unit (offer row / matrix cell): label · value-or-state ·
  provenance handle · action, per surface, citing the state grammar.
- **Phase 4 — State grammar on screen (template §2) + edge cases (§6 of this plan /
  states §4).** Map the six field states + comparison states (asymmetric, N=1,
  tie/near-tie, suppressed/withheld) to distinct treatments. Depends on Phase 3 and 4c.
- **Phase 5 — Interactions & gates (template §4).** Live re-weight, expand offer,
  why-above delta, revise-set re-entry (to the gate), provisional-set, jump-back-to-
  verify for suppressed fields. Note the **compare → share** boundary inherits the
  per-offer high-stakes acknowledgment gate (states §3); the comparison view itself
  gates nothing for the agent.
- **Phase 6 — Mobile / degraded (template §5).** Matrix → ranked cards + per-card
  breakdown + tap-for-why-above; no hover; static export deferred (inherits handoff §3,
  the comparison row of the degradation matrix). Accessibility baseline: the order must
  be conveyable without color; screen-reader semantics for rank and for each absence
  state.
- **Phase 7 — Forks (template §6) + deferred (template §7) + DEC entries.** Lock every
  fork as LOCKED (DEC-7 onward) or DEFER (reason + home). Deferred list: comparison
  share surface → sibling spec; reconciliation gate → sibling spec; static PDF; access
  control; dimension-set confirmation; visual tokens.
- **Phase 8 — Follow-ons (not this spec).** Then, in order: `comparison-share-surface.md`
  (seeded by §7 here), `reconciliation-gate.md`, the comparison **mockup**, and a
  **comparison worked-specimen** (worked-specimen §5 names it "the natural sequel").

---

## 11. Testing criteria (spec-quality, not code)

A reviewer runs the finished spec against this checklist:

**Forks & TODOs**
- [ ] Every fork (A–K) is **LOCKED** (with a DEC-n entry in `decisions.md`) or **DEFER**
      (named reason + named home). No "we haven't decided" (template §6 rule).
- [ ] All three doctrine TODOs are closed: §4.1 legibility (4a), §4.2 weighting-at-rest
      (4b), §5 inverted-ranking (4c). **No `TODO(design)` for this screen survives.**

**Doctrine obligations have a named screen home**
- [ ] Clause 1 is shown to be **inherited per offer** (provenance, honest uncertainty,
      term-based) inside the comparison.
- [ ] **Legibility (§4.1):** "why is A above B?" has a concrete UI answer in terms a
      seller would accept. Pick any adjacent pair; confirm the spec produces a
      plain-terms explanation.
- [ ] **Honest weighting (§4.2):** the weighting is legible at rest *and* user-
      controllable; **weights shown, sub-scores never** — no per-offer number, no total
      column anywhere (the 4b line).
- [ ] **Inverted-ranking (§5):** there is a specified state that **withholds** an order
      rather than guesses, and a suppressed dimension never silently becomes a default.
      Trace one unreadable comparison-affecting field through the screen and confirm it
      **never moves the order**.

**State grammar & edge cases**
- [ ] The six field states + comparison states (asymmetric, N=1, tie/near-tie,
      suppressed) each render **distinctly**; no two collapse to a shared dash, blank,
      or "N/A" — checked **inside the dense matrix**, including the dangerous collapses
      (empty-on-form vs. unreadable; agent-corrected vs. present-confident).
- [ ] **Asymmetric completeness never imputes** — an empty-on-form is shown as empty,
      never defaulted, never silently penalized.
- [ ] **N = 1 falls back** to the single-offer summary; no ranking-of-one.

**The two governing tests**
- [ ] **Doctrine §7 test:** does the screen make the comparison more *trustworthy*
      (legible order, honest weighting, honest gaps) — not just more *finished*? In
      particular, does **non-laundering** hold for the **order** — nothing makes the
      ranking look more decided or cleaner than the reads support (handoff §6 applied to
      rank)?
- [ ] **NORTH-STAR test:** does the screen move the agent toward a comparison they're
      **proud to share** — by being trustworthy, not impressive? Comparison is the
      retention depth; it earns retention by honesty.

**Cross-repo seams (CLAUDE.md)**
- [ ] `HIGH_STAKES_FIELD_KEYS` is **cited, not forked**; "comparison-affecting field" is
      single-sourced from the main repo; the §5 generalization is flagged as tracked
      main-repo work; the §1B/§1A and correction/audit-log dependencies are noted.

**The organizing idea is actually delivered**
- [ ] Every position is traceable to weighting + terms (provenance lifted to the
      order); the reconciliation-gate **precondition and re-entry** are explicit; the
      spec never silently assumes membership.

---

## 12. Rollback / revision plan

**Forks are kept separable so a wrong call is local.** Each fork → a DEC-n entry that
"lives in" a named spec section. Reversing a fork means writing a **new DEC-n′ that
supersedes DEC-n** (both left in place — `decisions.md` convention: "entries are never
deleted; a reversal is a new entry that supersedes an old one"), **bumping
`comparison-view.md`'s status/version line**, and revising only the sections that cite
the reversed fork. The plan's separability (layout C/D ≠ legibility G ≠ suppression 4c ≠
net I) is what keeps one reversal from cascading.

**The mockup is the trigger.** As with verify (mockup follows the §6 lock) and share,
the mockup is where a resolution proves right or wrong. Sequence: lock forks → mockup →
if a fork fails, supersede its DEC and revise. The mockup review uses §11 as its
checklist.

**Severity tiers (which reversal costs what):**
- **Cosmetic** (e.g., Fork F collapsed-vs-open weighting): revise template §§2/4,
  supersede the DEC, no cascade.
- **Structural** (e.g., Fork C matrix → cards): revise template §§1/2/3/5, supersede the
  DEC, **re-mockup**. The most expensive reversal — which is why C and D are validated
  earliest (Phase 1) and C is marked **LOCK-pending-mockup**.
- **Trust-grammar / doctrine-bound** (e.g., 4c can't be built generally, or net I must
  stop computing): **this is not a free screen-level choice.** Softening how §5 is
  honored, or letting a guessed number into the order, changes how the **doctrine** is
  kept. It **escalates**: reconcile with doctrine §5 — version-bump the doctrine or
  record a deliberate divergence in `decisions.md` (CLAUDE.md cross-repo rule) — rather
  than quietly revising the screen spec. The screen may *render* a degraded guarantee
  only after the doctrine has acknowledged the degradation.

**Highest-risk forks to watch at mockup** (the ones most likely to need a superseding
DEC): **C/D** (layout — most cascading; prototype the matrix early), **I** (net-to-seller
— validate suppression on a real packet with an unread component), **4c** (suppression /
withheld order — depends on main-repo generalization; may need to soften to "flag,"
which is doctrine-bound per above), **E** (live re-rank — may scope-reduce to apply-then).

**Numbering & propagation:** comparison-view locks become **DEC-7 onward** (coordinate
with any `decisions.md` backfill promotions so numbers don't collide); a later reversal
is the next DEC "supersedes DEC-x." On any lock or reversal, update **`STATUS.md`** (the
screens row and the decisions-logged list) and the **`decisions.md`** log.

---

## 13. Out of scope for this plan (named, with homes)

- **The spec prose, layout sketches, and DEC text themselves** — this is the plan;
  the spec is Phase 1–7 output → home: `07-screen-design/comparison-view.md`.
- **The comparison share surface spec** — obligations briefed in §7 → home:
  `07-screen-design/comparison-share-surface.md`.
- **The reconciliation gate spec** — dependency named in §3 → home:
  `07-screen-design/reconciliation-gate.md`.
- **The comparison mockup and worked-specimen** → home: Phase 8.
- **Link access-control model** → home: handoff §8 (open decision).
- **The default dimension set's final membership** → home: confirm against IA §7 +
  vocabulary at spec Phase 2.
- **Visual design tokens** → home: brand adoption (assets/README).

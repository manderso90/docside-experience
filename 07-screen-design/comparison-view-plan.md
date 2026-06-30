# Plan — The Comparison View (screen-spec Plan 3.0, A–J restructure)

> **Status:** v3.0 — plan. This version replaces the v2.1 numeric structure with the
> A–J framework requested for `07-screen-design/comparison-view-plan.md`.
> It synthesizes v2.1's resolved forks, fixtures, comparison-share brief, and
> data-state taxonomy, and incorporates six review-driven hardening changes.
>
> **What this file is:** the writing guide for `comparison-view.md` (the
> comparison-view screen spec). The plan is the brief; the spec is the artifact.
>
> **Does not replace:** `comparison-view.md` (the actual spec, not yet written).

---

## Context

The comparison view is the only screen in the product that exercises **ranking-trust**
(doctrine §2, Clause 2). Every other screen lives on the understanding-trust surface —
one offer, made clear. This screen inherits all of that per offer and adds three
mechanisms the single-offer view never needs: legibility, honest weighting, and the
inverted-ranking guarantee. All three have outstanding `TODO(design)` markers in
`trust-doctrine.md` §4.1, §4.2, and §4.3/§5. This spec resolves all three for the
first time.

The comparison-view-plan.md v2.1 has done substantial work: it resolved the surface-scope
fork (two documents), placed the reconciliation gate as a sibling dependency, proposed
resolutions to the three doctrine TODOs, built a full data-state taxonomy, wrote the
comparison-share brief (§8), produced six worked fixtures (§9), and incorporated
Morris's decisions (DEC-7 access control, DEC-8 dimension defaults). The A–J structure
reorganizes that content into a reference the spec author can work from section by section.

This revision incorporates six review-driven hardening changes:
1. At-rest adjacent-order reason preview, so the matrix does not merely show dimension
   leaders but also gives a terse reason for each neighboring rank relationship.
2. A DEC allocation/status table, so fork status and decision numbering do not drift.
3. A runtime contract, so target behavior is separated from alpha degradations.
4. A consolidated field-state matrix for all matrix-cell states.
5. Explicit aggregate-field participation rules, especially for net-to-seller.
6. A share-readiness matrix for withheld, provisional, and not-yet-verified states.

---

## A. Scope Statement

The comparison view work spans **two surfaces** and one **sibling dependency**:

**Surface 1 — Agent workspace** (`/listings/[id]/compare`): Authenticated,
desktop-likely (more deliberate than verify; agents cluster compare/share near
deadlines), interactive. Active when N > 1. The primary target of `comparison-view.md`.

Owns:
- Ranked offer display (dimension matrix + ranked spine)
- Weighting control (basis-line header + Customize expanding in place)
- Legibility affordance (matrix at rest; pairwise "why above" delta on demand)
- At-rest adjacent-order reason preview in the ranked spine
- Suppression/withhold states for unreadable dimensions
- Compare → share boundary (the agent enters recipient emails; link is expiring + revocable per DEC-7)
- Revise-set re-entry (drop/swap mid-compare)
- Set-provisional and offer-not-yet-verified markers

Does NOT own:
- The reconciliation gate itself (which offers enter the set) → sibling `reconciliation-gate.md`
- The comparison share recipient experience → sibling `comparison-share-surface.md`
- The net-to-seller formula (main repo arithmetic; the spec cites, does not define)
- Visual design tokens (deferred to brand adoption)

**Surface 2 — Comparison share surface** (`/share/[token]` for N > 1): Public,
mobile-first, read-only. The seller-facing multi-offer view. **IN SCOPE for this
plan as a brief (see §G); OUT OF SCOPE as a full spec.** The comparison share gets its
own document (`comparison-share-surface.md`); the plan for that spec lives in §G of
this plan (the full sibling brief is in v2.1 §8).

**Sibling dependency — Reconciliation gate** (`reconciliation-gate.md`): Governs
which offers enter the comparison. The comparison view depends on its output (a curated
set) but does not re-specify it. The comparison view owns only: (a) the curated-set
precondition stated explicitly, (b) the "revise set" re-entry affordance, (c) the
set-provisional marker, and (d) the N → 1 collapse consequence.

**Why this scope:** The two surfaces serve different audiences (agent vs. seller) with
different organizing ideas, interaction models, and access-control obligations. IA §3
forbids merging them ("two distinct information architectures — conflating them is a
category error"). `share-surface.md` §7 already defers "the comparison surface — its
own spec follows." The reconciliation gate's trust job is *membership made deliberate*,
not ranking-trust — a distinct problem that would dilute the comparison view's
organizing idea if merged.

---

## B. Relevant Files and Sections

### Direct sources (the sections this spec derives from)

| File | Section | What it contributes |
|---|---|---|
| `00-foundations/trust-doctrine.md` | §4.1 | Legibility obligation + `TODO(design)` for the relative-position affordance |
| `00-foundations/trust-doctrine.md` | §4.2 | Honest weighting obligation + `TODO(design)` for the at-rest weighting display |
| `00-foundations/trust-doctrine.md` | §4.3 + §5 | Inverted-ranking guarantee (full user-facing statement; §3G(3) precedent; DEFER-LINE on generalization) |
| `00-foundations/trust-doctrine.md` | §3.1, §3.2, §3.3 | Clause 1 obligations inherited per offer: provenance, honest uncertainty, term-based explanation |
| `00-foundations/trust-doctrine.md` | §2 | The two trust surfaces table: understanding-trust vs. ranking-trust |
| `08-states-and-edge-cases/states-and-edge-cases.md` | §4 | Compare-stage edge cases: unreadable-dimension, asymmetric-completeness, N=1, tie/near-tie |
| `08-states-and-edge-cases/states-and-edge-cases.md` | §4.1 | Assembling the comparison set: cross-channel duplicate, unreadable buyer-name, source-ambiguity, inclusion-granularity |
| `08-states-and-edge-cases/states-and-edge-cases.md` | §1, §1.1, §6 | Field states (three-way grammar), low-confidence resolution, states ledger |
| `02-information-architecture/information-architecture.md` | §2.1 | Reconciliation gate; two intake channels; §1B auto-join key; buyer-name fallback handle |
| `02-information-architecture/information-architecture.md` | §3, §4, §5 | Two zones; navigation hierarchy; route map (`/listings/[id]/compare`, `/share/[token]`) |
| `02-information-architecture/information-architecture.md` | §1, §7 | Object model (seller-priority profile, weighting); locked IA decisions |
| `00-foundations/domain-vocabulary.md` | §2, §4, §5 | Five hazard tags; high-stakes seed entries; `PCT-OR-FLAT` worked entry for the §5 precedent |
| `10-copy-guidelines/copy-guidelines.md` | §1.1, §1.3 | Principle voice; System voice ("An unreadable field is a fact, not a crisis") |
| `10-copy-guidelines/copy-guidelines.md` | §2.1, §2.2 | Three-way grammar of knowing (present/empty-on-form/unreadable); no score narration |
| `11-design-decisions/decisions.md` | DEC-7 | Access control: email-gated recipient access, expiring + agent-revocable (Morris) |
| `11-design-decisions/decisions.md` | DEC-8 | Default seller-priority dimensions and order: net to seller ▸ contingencies ▸ financing strength ▸ close speed (Morris) |

### Quality references (format and rigor to match)

| File | What to take from it |
|---|---|
| `_templates/screen-spec-template.md` | The mandatory seven-section structure all screen specs follow (§0 organizing idea → §7 deferred); the cardinal rule (no two states look alike); accessibility baseline is never deferred |
| `07-screen-design/verify-workspace.md` | Format rigor: one organizing idea derived from the trust obligation, then layout → states → element → interactions → mobile → forks → deferred. The two-widths precedent for Customize. |
| `07-screen-design/share-surface.md` | Format for the public share surface spec; how DEC entries are embedded inline; how the prohibition list is handled; §7 already defers "the comparison surface — its own spec follows" |

### Cross-reference obligations (sections in other docs that promise something this spec must deliver)

| Promise located in | Section | What the spec must deliver |
|---|---|---|
| `trust-doctrine.md` | §4.1 `TODO(design)` | The legibility affordance for *relative* position — the "why A above B" delta, distinct from the per-offer explanation of §3.3 |
| `trust-doctrine.md` | §4.2 `TODO(design)` | How weighting is shown at rest before Customize opens; the default weighting must be legible without interaction |
| `trust-doctrine.md` | §3.1 `TODO(design)` | Provenance in the comparison share surface (partially resolved in share-surface.md; comparison share must extend it to N offers and to the ranked display) |
| `trust-doctrine.md` | §3.2 `TODO(design)` | Three-way visual grammar (present/empty-on-form/unreadable) inside the dense comparison matrix — the place trust is most often quietly lost |
| `share-surface.md` | §7 Deferred | "The comparison surface — its own spec follows" — the comparison-share spec must be briefed here and written as a sibling |
| `states-and-edge-cases.md` | §6 States ledger | All comparison-stage states must appear in the spec's §2 with visually distinct treatments before the ledger is complete |
| `information-architecture.md` | §7 Locked decisions | DEC-8 dimension set and order must formalize into IA §7 on the next IA bump; the spec is the trigger |
| `NORTH-STAR.md` | Compare stage row | "Legible order, honest user-controllable weighting, no ranking from a guessed number" must each have a named screen home in the spec |

---

## C. The Trust Obligations This Spec Must Render

The comparison screen is the only home for Clause 2 (ranking-trust). All three
obligations below have outstanding `TODO(design)` markers or must be rendered for the
first time. No `TODO(design)` for this screen survives into the spec.

---

### Obligation 1: Legibility (doctrine §4.1)

**What the doctrine says:**
> "The user can always answer 'why is this offer ranked above that one?' in terms they
> could repeat to a seller. An order Docside cannot explain in plain terms is an order
> Docside does not present."
> `TODO(design):` "the legibility affordance for *relative* position, distinct from the
> per-offer explanation in 3.3."

**What the spec must specify:**
A UI mechanism that answers "why is offer A above offer B?" in plain terms — at rest
(no interaction required) and on demand (pairwise). The affordance must be *relative*
(comparing two offers on their delta) and *distinct* from the §3.3 per-offer explanation
(which describes one offer in isolation). Copy constraint: terms only, never scores
(copy §2.2: "explain rank with terms... never with numbers"). A dimension that is
unweighted by the seller's profile must not appear as a reason for the order even if it
differs between offers.

**Proposed resolution (from v2.1 §4a):**
- **At rest:** A dimension matrix where offers are rows, weighted dimensions are columns,
  cells hold terms (Explanation voice — "21-day close"), and the leading offer per
  dimension is marked. Down a column = "who leads this priority?" Cross-offer legibility
  without interaction. The ranked spine also includes a terse adjacent-order reason preview
  for each neighboring relationship: "Above Chen mainly on higher net and faster close."
  The preview is not the full explanation; it is the at-rest proof that the position has
  a traceable reason.
- **On demand:** Tapping/clicking an offer (or the gap between two adjacent offers) yields
  a pairwise "why this order" delta: *"Ranked above [next] on: higher net, faster close;
  [next] leads on: lower buyer-broker comp."* Scoped to the weighted dimensions. If an
  unweighted dimension also differs, it is noted as "they also differ on X, which you
  didn't weight" — never as a reason for the order.

**Which doctrine TODO this resolves:** `TODO(design)` in §4.1.
**Resolution statement to lock:** "The legibility affordance for relative position is
the at-rest leading-cell matrix plus an adjacent-order reason preview, with the full
pairwise delta available on demand. The delta is stated in terms, scoped to weighted
dimensions, and signed by direction." → DEC-13.

---

### Obligation 2: Honest Weighting (doctrine §4.2)

**What the doctrine says:**
> "The ranking reflects **seller priorities**, and the weighting is **visible and
> user-controllable.** The free-slider / live-total Customize model is a *trust
> mechanism*, not a UX convenience: it lets the agent see and change what's driving
> the order, which means the order is never a black box asserting authority it can't
> account for."
> `TODO(design):` "how weighting state is shown at rest (before the user opens
> Customize) — the default weighting must be legible without interaction."

**What the spec must specify:**
- The at-rest weighting display (the "before Customize" state), legible without
  interaction: a basis line showing the priorities in order + a compact relative-weight
  indicator (ordered bars or chips, labeled by dimension, magnitude shown, not per-offer scores)
- Customize expands the header in place (same two-widths principle as verify-workspace)
- What is **never** visible: per-offer sub-scores, totals, 0–100 numbers, star ratings,
  "best offer" badges (copy §2.2)
- What is **visible instead** of a sub-score (the positive enumeration, v2.1 §4b):
  1. The basis line — "Ranked by: [priorities in order]"
  2. The dimension columns — each a term-bearing priority
  3. The deciding terms — the pairwise delta, in business language
  4. The leading-cell marks — which offer leads each weighted dimension
  5. The relative-weight indicator — ordered bars/chips (priority magnitude)
  6. The caveats — suppression / partial / withheld / tie / near-tie markers

**Proposed resolution (from v2.1 §4b):**
A "Ranked by" basis statement + compact relative-weight indicator as the always-visible
header above the matrix (DEC-8 default order: *"Ranked by: highest net to seller,
fewest contingencies, stronger financing, faster close"*). Customize expands this header
in place into the free-slider / live-total editor.

**Which doctrine TODO this resolves:** `TODO(design)` in §4.2.
**Resolution statement to lock:** "Weighting at rest is a basis line ('Ranked by:
[priorities in order]') plus a compact relative-weight indicator. Customize expands
the header in place. Weights are shown; sub-scores are never shown." → DEC-10.

---

### Obligation 3: Inverted-Ranking Guarantee (doctrine §4.3 + §5)

**What the doctrine says:**
> "Docside will never rank one offer above another on the strength of a number it
> guessed. When a term that affects the comparison can't be read with confidence,
> Docside marks it unknown and tells you so — it does not fill the gap with a default
> that could quietly move an offer up or down the list. **If we cannot trace how a
> ranking was determined, we will not present it.**"
> `DEFER-LINE:` "the guarantee is honored in §3G(3) today. It is **not yet
> generalized** across every comparison-affecting field."

**What the spec must specify:**
A three-tier treatment that degrades from cell to order when a comparison-affecting
dimension is unreadable:
1. **At the cell:** "We couldn't read this field" — elevated visual weight for
   high-stakes fields. Never blank, never a dash, never a default, never a guess.
2. **At the offer's position in the dimension:** The dimension is suppressed for that
   offer — explicitly **visible-but-excluded** ("partial — [dimension] unread"). The
   suppressed dimension does NOT disappear (disappearing hides the gap; that is a
   non-laundering violation, handoff §6).
3. **At the pairwise order:** If the suppressed dimension would be decisive between
   two offers, the order between those two offers is **withheld** — they render as a
   bracketed group: "Can't be separated on your priorities until [field] is read for
   [buyer]." The one place the product explicitly withholds an order rather than
   assert one it can't trace.

Every suppression links back to that offer's verify workspace: "verify to resolve."
Suppression is an honest hold with a way forward, not a dead end.

**Cross-repo caveat the spec must name:** The spec specifies the design; the per-field
runtime generalization (degrade-to-unknown, not to a ranking-moving default) is tracked
main-repo work. If the backend can only *flag* (not *withhold*) at alpha, tier 3 degrades
to tier 2 — but that degradation is **doctrine-bound** (must be recorded in decisions.md
as a deliberate divergence, not a silent screen-level edit).

**Which doctrine obligation this resolves:** §4.3 / §5 — not a TODO but a guarantee
rendered for the first time in pixels.
**Resolution statement to lock:** "Unreadable comparison-affecting fields suppress the
dimension visible-but-excluded; if decisive, the pairwise order is withheld, not guessed."
→ DEC-11.

### Runtime contract this spec assumes

This plan specifies the target design behavior. The implementation can only honor that
behavior if the main repo exposes a few explicit runtime contracts. These are not visual
details; they determine whether the screen can truthfully present an order.

| Runtime contract | Target behavior in the spec | Alpha-degraded behavior, if missing | Required record |
|---|---|---|---|
| **Unknown propagation for comparison-affecting fields** | Any unreadable, conflicting, or low-confidence comparison-affecting field degrades to unknown, never to a default that can move rank | The affected dimension is visible-but-excluded. If the field would be decisive and the runtime cannot decide this, the pairwise order is not shown as decisive | decisions.md divergence + main-repo task |
| **Withhold-capable ranking output** | Runtime can identify when a suppressed dimension would be decisive between adjacent offers, allowing the screen to render a bracketed withheld group | If runtime can only flag uncertainty, the screen may show suppressed-visible-but-excluded but must not flatten the pair into a confident order | decisions.md divergence + doctrine-bound note |
| **Net-to-seller formula symbol** | Spec cites the main-repo formula by symbol/name and treats net as arithmetic of traceable components | If no formula is established, net-to-seller falls back to components-only for alpha | main-repo formula task + spec deferred note |
| **Closeness-band parameter** | Runtime exposes a named parameter for tie/near-tie state boundaries | If not exposed, tie/near-tie examples are illustrative only and mockup must not imply exact boundaries | main-repo tuning task |

The spec may name these as dependencies without defining the engine. What it may not do
is silently soften the guarantee in pixels.

---

## D. Implementation Sequence

The spec is written in template order (§0 → §7), but decisions are made in dependency
order. Below: what to write, what to read first, what can go wrong, and the trust test
that section must pass before moving on.

### Step 0 — Organizing idea (template §0)

**What:** One sentence that the spec returns to when any design question is disputed.
**Read first:** doctrine §4–§5 (the trust obligation); NORTH-STAR.md compare row ("legible
order, honest user-controllable weighting, no ranking from a guessed number"); verify-workspace.md
§0 and share-surface.md §0 as format patterns — each derives the idea from the trust
obligation, not from convenience or feature description.
**Could go wrong:** Choosing an idea that describes a layout ("ranked cards with a
weighting panel") rather than the trust claim. The organizing idea must answer "why
this, not something cleaner that would hide the gaps?"
**Trust test:** Does the sentence account for all three ranking-trust mechanisms (legibility,
honest weighting, inverted guarantee)? If it only covers one, it is not the organizing idea.
**From v2.1:** "The order accounts for itself" — confirmed by external review as 5/5.

---

### Step 1 — Core layout decision (template §1, Forks C/D)

**What:** Lock the layout model (matrix vs. cards vs. hybrid; offers-as-rows vs. columns).
This is the cascading fork; everything downstream depends on it.
**Read first:** doctrine §4.1 (legibility requires cross-offer visibility at rest); copy §2.2
(matrix hazard: must not read as a scoreboard implying scores); verify-workspace.md §1 for
the layout-region pattern; NORTH-STAR compare row.
**Could go wrong:** The matrix reads as a scoreboard (implies numeric totals), which is
forbidden. Ranked cards are clean but fail relative legibility at rest. A matrix with
only leading-cell marks can show who leads each priority without explaining why one
adjacent offer sits above another. The hybrid must *structurally* defuse the scoreboard —
no total column, no per-offer number, terms in cells — while the ranked spine carries a
terse adjacent-order reason preview.
**Trust test:** Can a reviewer see "why is A above B?" without opening any interaction,
including a plain-language adjacent-order reason? If not, the layout fails legibility at
rest and the §4.1 TODO is not resolved.

---

### Step 2 — Data-state taxonomy (template §2 foundation)

**What:** Map every field/offer state to ranking participation and disclosure treatment.
This is the foundation for every matrix cell. Fix it early because the matrix is dense —
the dangerous collapses are likeliest to fail here. The spec must include one consolidated
field-state matrix before it writes any cell UI.
**Read first:** states §1 (the six field states: verified, agent-corrected, empty-on-form,
not-captured, not-applicable, unreadable/conflicting); states §4 (comparison states);
domain-vocabulary.md §2 (hazard tags — `FREE-TEXT-VERBATIM`, `PCT-OR-FLAT`, `STRUCTURALLY-NULL`,
`DEFAULT-TRAP`, `FORM-LITERAL`); copy §2.1 (three-way grammar). From v2.1: the taxonomy
in §5 (field-level states × ranking participation × disclosure) and §5.2 (offer-level
not-yet-verified state).
**Could go wrong:** Collapsing empty-on-form and unreadable (copy §2.1 single-biggest
trust failure: "the single most common way this product would lie"); asserting "intentionally
omitted" (a `DEFAULT-TRAP` violation — presence ≠ intent); imputing a zero for a blank
aggregate component; treating a structurally null component the same as an unread component.
**Trust test:** Are all seven field states (including conflicting/incoherent → null) and
both offer states (vouched / not-yet-verified) rendered distinctly? Run the dangerous-collapse
check: empty-on-form ≠ unreadable ≠ not-applicable ≠ not-captured, in the same matrix.
For any aggregate field, can the reviewer tell which component states suppress the aggregate,
which are allowed as structurally null, and which require a caveat?

---

### Step 3 — Doctrine TODO resolutions (4a, 4b, 4c)

**What:** Write the concrete UI specifications for legibility (§4.1), at-rest weighting
(§4.2), and the three-tier suppression/withhold (§5). These are the spec's reason to exist.
**Read first:** doctrine §4 (the three TODOs verbatim); copy §2.2 (terms-only, no sub-scores);
worked fixtures from v2.1 §9 (concrete instances of all three tiers across six scenarios).
**Could go wrong:**
- Legibility affordance restates per-offer terms (the §3.3 per-offer explanation) rather
  than expressing the *delta* between two offers in a relative sense
- Weighting display shows sub-scores or per-offer totals while claiming to show weights
- Suppression makes a dimension *disappear* rather than keeping it visible-but-excluded
  (disappearing hides the gap — a non-laundering violation identical to the DEC-6 prohibition)
**Trust test:** Run v2.1 fixture 3 (withheld order) from §9. Does the spec produce a
screen where: Chen's buyer-broker comp is unreadable → net is suppressed visible-but-excluded
→ Chen's net dimension is present in the matrix but marked excluded → the Reyes-vs-Chen order
is genuinely withheld (not just caveated)? If the spec passes fixture 3, it passes all three
doctrine TODOs.

---

### Step 4 — Element information design (template §3)

**What:** Decompose the offer row and matrix cell: label · value-or-state · provenance
handle · action per surface. Define the offer-header (buyer name, offer-level state,
"not yet verified" flag). Define the pairwise delta affordance form.
**Read first:** verify-workspace.md §3 (field row decomposition — the four-part anatomy);
share-surface.md §3 (seller-facing adaptation of the same anatomy); domain-vocabulary.md §4
(label/spoken/gloss/hazards for each high-stakes field — the cell's label and Explanation-
voice spoken value come from here).
**Could go wrong:** Omitting the provenance handle from the matrix cell. Clause 1 must be
inherited per offer even inside the dense matrix — the agent must be able to trace any value
to its contract location without leaving the comparison view.
**Trust test:** Pick any cell in the worked fixture 1 matrix. Can the agent trace the value
("21-day close") to its form location (§3B → ¶33A) without a round-trip to verify? If not,
provenance is not present in the element design.

---

### Step 5 — Interactions and gates (template §4)

**What:** Live re-weight (Customize in place); expand-offer → side pane/drill-down → link
to verify workspace; pairwise delta affordance trigger; revise-set re-entry; offer-not-yet-
verified prompt; compare → share boundary (agent enters recipient emails; link is expiring
+ revocable per DEC-7); share-readiness outcomes for withheld order, suppressed dimensions,
set-provisionality, and not-yet-verified offers.
**Read first:** states §3 (compare→share boundary inherits the per-offer high-stakes
acknowledgment gate — this gate is not eliminated by the comparison view); IA §2.1
(the set composition mechanics — what "revise set" means); decisions.md DEC-7 (the
access model the share-initiation UI must reflect).
**Could go wrong:** Treating the compare→share boundary as a button-press rather than
a gate that inherits states §3. Not speccing the share-initiation UI (agent enters emails;
link is expiring+revocable) — that belongs to comparison-view.md even though the
recipient experience belongs to the share spec. Leaving ambiguous whether a withheld order,
set-provisional comparison, or not-yet-verified offer may be shared.
**Trust test:** At the compare → share boundary, does the spec require the agent to
explicitly enter recipient emails before a comparison link is created? If not, DEC-7 is
not reflected in the workspace. Does the boundary also say whether each ranking state is
allowed, blocked, or allowed only with explicit disclosure?

---

### Step 6 — Mobile and degraded (template §5)

**What:** Matrix → ranked cards on narrow screens; Customize → full-screen or bottom-
sheet slider editor; basis line always visible at minimum collapsed state; accessibility
baseline.
**Read first:** verify-workspace.md §5 (mobile strategy: summary-primary + provenance
drill-down) for the precedent pattern; v2.1 §12 phase 6 (mobile Customize requirements).
**Could go wrong:** Treating the Customize control as desktop-only when agents may re-
prioritize from a phone. Losing the basis line on mobile when Customize is closed — the
basis line is the minimum state, not an optional element.
**Trust test:** On a narrow screen, before any interaction: is the basis line ("Ranked
by: [priorities]") visible? Is there a path to the per-offer detail without horizontal
scrolling through a matrix?

---

### Step 7 — Design forks and DEC entries (template §6)

**What:** Lock or explicitly defer every fork from §E below. Write DEC-9 through DEC-17
(and any additional entries that surface during writing). LOCK-pending-mockup forks get
a "pending" status and name the mockup as the trigger. Preserve the DEC allocation table
in §E so numbering, status, and triggers remain auditable.
**Read first:** decisions.md DEC-1 through DEC-8 (the existing log; DEC-9 onward continues
the numbering without collision); template §6 (every fork must be LOCKED with a DEC entry
or DEFER with a reason and named home — never "we haven't decided").
**Could go wrong:** A LOCK-pending-mockup fork being written as LOCKED; a fork that
silently resolves a doctrine question without creating a DEC entry; a DEC number being
claimed in prose but not in the allocation table.
**Trust test:** Does every fork resolution in the spec have a DEC entry? Is any DEC entry
missing from decisions.md? Does the DEC allocation table match the fork list exactly?

---

### Step 8 — Deferred (template §7)

**What:** Explicitly name everything not in this spec — comparison share surface spec,
reconciliation gate spec, comparison mockup, static PDF, visual tokens, agent-alias
system — each with a reason and a named home.
**Read first:** v2.1 §16 (out-of-scope list); share-surface.md §7 (the pattern for an
explicit deferred section — reason + home for each item, no orphans).
**Could go wrong:** A deferred item with no named home (orphaned); a trust obligation
deferred as if it were polish (a guarantee cannot be deferred, only a UX affordance for
a guarantee that already has a home elsewhere).
**Trust test:** Every deferred item has a named home. Nothing that carries a doctrine
obligation is deferred without an explicit statement of where that obligation is being honored.

---

### Step 9 — Follow-on specs (not this spec, but brief them here)

Comparison share surface: brief it (see §G of this plan; full brief is v2.1 §8). Home:
`comparison-share-surface.md`.
Reconciliation gate: name the dependency (see §A). Home: `reconciliation-gate.md`.
Comparison mockup: seed the fixtures from v2.1 §9. Home: Phase 8 of v2.1 §12.

---

## E. Design Forks

**Altitude discipline (inherited from v2.1 §6):** Every fork specifies behavior and its
trust purpose, not implementation. `HIGH_STAKES_FIELD_KEYS`, the scoring engine, and the
net-to-seller formula are **cited as dependencies by name, never redefined here.**

### DEC allocation and status table

This table is the source of truth for decision numbering during spec-writing. A fork may
be behaviorally recommended below, but it is not fully locked until its DEC entry exists
with the status shown here.

| Item | Decision | DEC | Status | Trigger / note |
|---|---|---:|---|---|
| Fork A | Two separate documents for workspace and share surface | Backfill | LOCKED | Promote earlier scope decision without renumber collision |
| Fork B | Reconciliation gate as sibling upstream spec | Backfill | LOCKED | Promote earlier scope decision without renumber collision |
| Fork C/D | Hybrid ranked spine + matrix; offers as rows | DEC-9 | LOCK-pending-mockup | Lock after mockup proves matrix does not read as scoreboard |
| Obligation 2 / Fork F | At-rest weighting basis line + compact weights; Customize expands in place | DEC-10 | LOCKED | Doctrine §4.2 TODO resolution |
| Obligation 3 | Visible suppression + withheld decisive order | DEC-11 | LOCKED, runtime-dependent | Depends on runtime contract for withhold-capable ranking |
| Fork I | Net-to-seller computed only from traceable components | DEC-12 | LOCK-pending-mockup | Validate on real packet and cite main-repo formula |
| Obligation 1 / Fork G | Matrix + adjacent preview + on-demand pairwise delta | DEC-13 | LOCKED | Doctrine §4.1 TODO resolution |
| Fork E | Live re-ranking while Customize changes weights | DEC-14 | LOCK-pending-mockup | Mobile may degrade to apply-then with explicit note |
| Fork H | Per-offer atom in expansion / side pane / mobile drill-down | DEC-15 | LOCKED | Full verify workspace linked, not duplicated |
| Fork J | Free-text terms outside ranked weighting | DEC-16 | LOCKED | Quoted verbatim; never scored into order |
| Fork K | Set-provisional marker until complete | DEC-17 | LOCKED | Distinct from offer-level not-yet-verified |

### Fork A — Surface scope *(LOCKED)*
**Question:** One combined spec or two separate documents?
**Options:** Single doc / Two docs (workspace + share surface)
**Recommendation:** **Two separate documents.** `comparison-view.md` for the agent
workspace; `comparison-share-surface.md` for the seller surface. Precedent:
verify-workspace.md + share-surface.md. IA §3 forbids the merge. share-surface.md §7
already defers "the comparison surface — its own spec follows."
**Anchor:** IA §3; share-surface.md §7; doctrine §2 (two distinct trust surfaces)
**DEC:** Backfill candidate (no DEC number yet; coordinate with decisions.md backfill index)

### Fork B — Reconciliation gate placement *(LOCKED)*
**Question:** Gate as stage-0 of the comparison view, or as a separate upstream spec?
**Options:** Gate-as-compare-preamble / Gate-as-sibling (`reconciliation-gate.md`)
**Recommendation:** **Separate upstream spec.** The gate's trust job is *membership made
deliberate*, not ranking-trust. It fires at a different nav location (listing → compare
boundary, IA §5). Verify-workspace.md §7 already names it as a deferred screen.
**Anchor:** IA §2.1; critical-path §3; doctrine §2 (one trust job per surface)
**DEC:** Backfill candidate

### Fork C — Core layout model *(LOCK-pending-mockup)*
**Question:** Matrix (offers × dimensions) vs. ranked cards vs. hybrid?
**Options:**
- Matrix: strongest cross-offer legibility; hazard: reads as a scoreboard (implies scores)
- Ranked cards: strong per-offer atom, mobile-friendly; weak at relative legibility at rest
- Hybrid: ranked spine + dimension matrix, no total column, terms in cells
**Recommendation:** **Hybrid.** Defuses scoreboard risk structurally. No per-offer number,
no total column, terms in cells, position not points.
**Trade-off:** Highest design complexity; most cascading if reversed. Validate the matrix
early in the mockup.
**Anchor:** doctrine §4.1 (legibility at rest); copy §2.2 (no scores)
**DEC:** DEC-9

### Fork D — Orientation *(LOCKED)*
**Question:** Offers as rows or offers as columns?
**Recommendation:** **Offers as rows, dimensions as columns.** A ranking is a vertical
list; scales in N; degrades cleanly to mobile cards (one card per offer, stacked).
**Anchor:** NORTH-STAR depth loop; agent-workflow §2
**DEC:** DEC-9 (same decision as Fork C)

### Fork E — Re-weighting feel *(LOCK-pending-mockup)*
**Question:** Live re-ranking (order moves as weights move) vs. apply-then-reorder?
**Options:**
- Live re-ranking: strongest proof that the order is not a black box; the order responds visibly to the agent's priorities
- Apply-then-reorder: lower motion/perf cost; less "magic" but more predictable
**Recommendation:** **Live re-ranking**, animated transition (offers move, don't jump).
**Risk:** Motion/perf on mobile may require scoping-down to apply-then for the mobile
Customize experience.
**Anchor:** doctrine §4.2 ("the order is never a black box asserting authority it can't
account for")
**DEC:** DEC-14

### Fork F — Customize at rest *(LOCKED)*
**Question:** Collapsed at rest or always open?
**Recommendation:** **Collapsed at rest** — basis line + compact weights visible; Customize
expands in place. At-rest legibility without the control's footprint.
**Anchor:** doctrine §4.2 TODO ("legible without interaction"); verify-workspace.md
two-widths precedent
**DEC:** DEC-10

### Fork G — Legibility affordance form *(LOCKED)*
**Question:** What is the UI form of the §4.1 "relative position" affordance?
**Recommendation:** **Matrix at rest + adjacent-order reason preview + pairwise delta on
demand.** Leading cells give at-rest legibility across offers; the ranked spine gives a
terse adjacent-order reason for each neighbor relationship; tapping/clicking the offer
or the gap between two adjacent offers yields the full pairwise "why this order" delta.
Pure terms, signed by direction, scoped to weighted dimensions.
**Anchor:** doctrine §4.1 TODO; copy §2.2 (terms only, never scores or weights in the
delta text)
**DEC:** DEC-13

### Fork H — Per-offer Clause-1 atom location *(LOCKED)*
**Question:** Where does the per-offer understanding-trust atom live inside the comparison?
**Recommendation:** **Inline expansion → side detail pane (desktop) / drill-down (mobile)**,
with a link back to the full verify workspace for re-checking.
**Why:** The comparison composes atoms; it does not replace them. The full verify-workspace
detail (document pane + provenance scroll) should never be duplicated inside the comparison.
**Anchor:** doctrine §4 ("inherits all of Clause 1 per offer"); IA §4
**DEC:** DEC-15

### Fork I — Net to seller *(LOCK-pending-mockup; trust-critical)*
**Question:** Compute net to seller as a comparison dimension, or show components only?
**Options:**
- Computed net: strongest legibility for the "highest net" priority; hazard: if any
  component (buyer-broker comp `PCT-OR-FLAT`, seller credits) is unread, the net value
  can inherit a guess and invert the ranking — the §5 danger in its most common form
- Components only: no aggregation risk; weakest legibility (agents must do the math)
**Recommendation:** **Compute net only when all components are confidently read. If any
component is unread, net is suppressed visible-but-excluded** ("net can't be determined:
[component] unread"). Net = arithmetic of traceable values, never a model output. The
§3G(3) `PCT-OR-FLAT` precedent (domain-vocabulary.md §5 worked entry) generalized. If a
component is empty-on-form, not-captured, or not-applicable, the aggregate-field
participation rules in §F decide whether net is suppressed, caveated, or allowed as
structurally null; the spec never silently treats absence as zero.
**Validation:** Run on a real packet with an unread buyer-broker comp (v2.1 fixture 2).
**Anchor:** doctrine §5; domain-vocabulary.md §5 buyer_broker_comp entry; v2.1 §4c
**DEC:** DEC-12

### Fork J — Free-text / unweightable terms in the matrix *(LOCKED)*
**Question:** How do `FREE-TEXT-VERBATIM` fields (§3R other terms; §3G(2)) appear in
a dimension matrix built from structured values?
**Recommendation:** **A non-ranked "Other terms" section** below or alongside the
weighted matrix — quoted verbatim, explicitly outside the weighting, present to read,
never scored into the order. The screen "visibly leaves room for everything it can't see"
(seller-workflow §4).
**Anchor:** doctrine §3.2 v0.3(a) ("a quoted field never enters the comparison as if it
were a verified value"); copy §2.4
**DEC:** DEC-16

### Fork K — Set provisionality *(LOCKED)*
**Question:** Show the comparison as provisional until the agent marks the set complete?
**Recommendation:** **Provisional marker until complete** — header reads "Comparison of
[N] offers in so far" — never implying finality the transaction hasn't reached.
**Note:** Distinct from the per-offer not-yet-verified marker (§5.2 of v2.1). Both are
shown simultaneously when an unverified offer is also in an open set. They are different
markers and must look different.
**Anchor:** agent-workflow §2 (the set is open until the deadline)
**DEC:** DEC-17

---

## F. Field and Comparison-Specific States

Each state must be visually distinct from every other state. "No two states look alike"
is the template's cardinal rule; in the dense comparison matrix, it is also the trust proof.

### Consolidated matrix-cell field states

The spec must include this table, or a stricter version of it, before defining individual
matrix cells. It is the practical answer to doctrine §3.2 inside the densest screen in
the product.

| Field state | Matrix-cell treatment | Ranking participation | Provenance / trace | Action |
|---|---|---|---|---|
| **Verified present** | Term value in Explanation voice, e.g., "21-day close" | Participates normally if the dimension is weighted | Contract location handle visible or one click away | Open provenance / detail |
| **Agent-corrected** | Corrected term value with correction marker; original value traceable | Participates using corrected value | Shows correction trail plus original source location | Open correction detail / verify |
| **Empty-on-form** | "Not specified on this form" | Never imputed as zero, none, waived, or intentionally omitted; participation depends on the term and aggregate rules below | Shows form location where the blank/absence occurred | Open source / verify if needed |
| **Not-captured** | "Not captured" or "Not captured in intake" | Excluded from ranking-affecting computation until captured or verified | Shows intake/system origin, not a contract citation | Go to verify / capture |
| **Not-applicable / structurally null** | "Does not apply" with distinct visual treatment | May contribute to an aggregate only if domain vocabulary and formula both define it as structurally null | Shows why it is structurally null, not merely missing | Open explanation / source |
| **Unreadable / low-confidence** | "We couldn't read this field" with elevated weight for high-stakes fields | Excluded from that dimension; if decisive, pairwise order is withheld | Shows attempted source location when available | Verify to resolve |
| **Conflicting / incoherent** | "Conflicting values" or "Needs resolution" | Excluded until resolved; may suppress aggregate and trigger withhold if decisive | Shows both conflicting traces when available | Resolve in verify workspace |

### Aggregate-field participation rules

Aggregates such as net-to-seller are the highest-risk place for silent lying because an
absence can be accidentally converted into arithmetic. The spec must state these rules:

1. An aggregate may display as computed only when the formula is named and every required
   component is traceable as verified, agent-corrected, or explicitly structurally null.
2. Verified and agent-corrected components participate normally, with the component
   provenance visible from the aggregate cell.
3. Empty-on-form and not-captured components are never treated as zero by default. The
   aggregate is suppressed visible-but-excluded unless the main-repo formula explicitly
   defines that absence state as non-participating for that field.
4. Not-applicable / structurally-null components may contribute a neutral value only when
   both domain-vocabulary.md and the formula identify that exact field state as structurally
   null. Otherwise, the aggregate is suppressed.
5. Unreadable, low-confidence, conflicting, or incoherent components suppress the aggregate
   visible-but-excluded. If the aggregate would be decisive between adjacent offers, the
   pairwise order is withheld.
6. Aggregate cells show the component reason, not just the aggregate value: "Net can't be
   determined: buyer-broker comp unread" or "Net based on price, seller credit, and verified
   buyer-broker comp."

### States from states §4 (comparison-view's own edge cases)

| State | Trigger | Proposed on-screen treatment | Fixture in v2.1 §9 |
|---|---|---|---|
| **Unreadable-dimension** | A ranking-feeding field is unreadable for one offer | Three-tier (doctrine §5): (1) cell: "We couldn't read this field" — elevated weight if high-stakes; (2) dimension suppressed for that offer — **visible-but-excluded** ("partial — [dimension] unread"); (3) if decisive pairwise: order **withheld** — "Can't be separated on your priorities until [field] is read for [buyer]." Link to verify for each suppression. | Fixtures 2 and 3 |
| **Asymmetric-completeness** | Offer A has a verified term; offer B left it blank | B's cell: "Not specified on this form" (empty-on-form — visually distinct from unreadable). B not imputed, not zeroed, not penalized. The dimension's leading-cell mark excludes B. If the field feeds net, net is suppressed-or-caveated for B, never silently zeroed. "Intentionally omitted" is never asserted. | Not a separate fixture; exercises §5.1 rules |
| **N=1 degenerate** | After reconciliation or exclusion, only one offer remains | Fall back to the single-offer summary with a note ("Only one offer is in this comparison"). No ranking chrome. No weighting header asserting an order over one item. | Fixture 5 |
| **Tie / near-tie** | Two or more offers land within a closeness band on weighted priorities | A tie/near-tie band: same visual position, or labeled "Reyes and Chen are very close on your priorities." Pairwise delta: "Nearly even — [A] leads on [terms], [B] leads on [terms]; it's close." No manufactured decisive order from rounding. | Fixture 4 |

### States from states §4.1 (gate territory; comparison-view's slice)

| State | Trigger | Comparison-view treatment |
|---|---|---|
| **Cross-channel duplicate** | Same offer via upload AND email | The gate resolves this before the comparison view receives the set. The comparison view owns only: the "revise set" re-entry affordance when the agent wants to drop a copy mid-compare. |
| **Unreadable buyer-name** | §1A buyer name can't be read | Show the fallback handle (states §4.1 / IA §2.1 — a system-generated label, e.g., "Offer 2"). Never assert a guessed name. The agent can assign a label at the gate; if no label was assigned, the fallback shows in the buyer-name slot throughout. |
| **Source-ambiguity** | Channel of intake unclear | The gate resolves this. If source is still ambiguous after the gate (unlikely), show source as "Unknown" rather than asserting a channel. |
| **Inclusion-granularity** | Which version of an offer enters when a buyer submitted revisions | The gate decides which version enters. The comparison view receives the curated set; "revise set" re-entry handles swaps mid-compare. |

### Offer-level states (from v2.1 §5.2; the interruptible-workflow distinction)

| State | Trigger | Treatment |
|---|---|---|
| **Not-yet-verified** | Offer is in the set but verify is incomplete | Flagged "not yet verified" on the offer's row/card. Held out of the asserted ranking, or shown provisionally with a "verify to rank" prompt. **Never ranked as if vouched.** Visually distinct from the set-provisional marker. |
| **Vouched** | Offer passed the verify → share boundary (all fields confirmed, corrected, or marked unreadable) | Ranks normally. No special marker needed beyond the standard ranking position. |
| **Set-provisional** | The comparison set may still grow (deadline not yet reached) | Header marker: "Comparison of [N] offers in so far." Distinct from not-yet-verified — this describes the set, not an individual offer. |

---

## G. Comparison Share Obligations

The comparison share surface is the sibling spec (`comparison-share-surface.md`), not
part of `comparison-view.md`. But `comparison-view.md` must brief it and own the
workspace's share-initiation affordance. The full sibling brief lives in v2.1 §8 and
serves as the first draft of the comparison-share spec.

### What the comparison share adds beyond the single-offer share surface

| Element | Single-offer share (share-surface.md) | Comparison share |
|---|---|---|
| Organizing idea | "orient first" — what this offer is | **"fit-to-priorities, an input not a verdict"** — the order plus the visible basis, leaving room for what can't be seen (buyer letter, gut feel) |
| Per-offer atom | Yes: provenance, six absence states, term-based, corrections-as-corrected, glosses, §-citation (DEC-3/4/5) | **Inherited per offer** — the comparison is N atoms |
| Top-of-screen | The one offer's headline terms | **The ordered set + "Ranked by…" basis line** |
| Ranking visible to seller | N/A | **Yes — as fit-to-priorities, never as a verdict.** No "best offer" badge, no "accept" action, no scores. |
| Weighting display | N/A | **Basis line always visible.** Agent cannot hide what produced the order (doctrine §4.2; handoff invariant 5). Display may simplify — omit precise bar magnitudes — but the basis is never hidden. |
| Suppressed dimension | N/A | **Visible-but-excluded** — "We couldn't read [field] for [buyer], so this offer isn't ranked on [dimension]." Hiding it makes the ranking look cleaner than the reads support — a non-laundering violation. |
| §5 inverted-ranking guarantee | Absent (single offer; no ranking to guarantee) | **Shown in Principle voice:** "If we cannot trace how a ranking was determined, we will not present it." |
| Buyer identity | One buyer (§1A) | **Each buyer's name (§1A) shown to the seller.** The seller owns these offers on their property; real-world offer presentations name buyers. Confidentiality concerns are about link access, not buyer-name display. Unreadable §1A → fallback handle. |
| Access control | Lightweight link acceptable for alpha (handoff §8) | **Email-gated recipient access, expiring + agent-revocable (DEC-7, locked by Morris).** A forwarded link does not carry access — the forward recipient meets the same email gate. Specific to multi-buyer comparison (multi-buyer exposure risk, handoff §7). |
| Non-laundering + prohibition list | DEC-6 prohibition list | **Inherited; extended to the order** — no false decisive order, no hidden suppression, no collapsed absence rows in the ranking display. |

### Ranking presentation to the seller: governing principle

**Ranking does reach the seller — as fit-to-priorities, never as a verdict.** The
surface leaves room for what it can't see (seller-workflow §4). "The decision is never
the algorithm's" (seller-workflow §5). This is a stronger obligation than the single-
offer surface, which had no order to caveat.

### Access control (DEC-7, locked)

The agent workspace owns the **share-initiation UI only**: the agent enters one or more
seller recipient emails and sees the link is expiring and revocable. The recipient-verification
flow, expiry handling, and revocation UI belong to the comparison-share spec and the main repo.

A forwarded recipient who opens the link does not automatically receive access — they
meet the same email gate. The PIN option was considered and rejected (a PIN forwards as
easily as the link). Per-view approval was considered and rejected as the default (too
much friction for "open cold on a phone").

### Workspace share-readiness matrix

The comparison workspace owns whether a comparison can be shared at all. The recipient
experience belongs to `comparison-share-surface.md`, but the workspace must not create a
share link that the share surface cannot represent honestly.

| Workspace state at share initiation | Outcome | Required workspace behavior |
|---|---|---|
| All included offers vouched; no suppressed decisive dimension; set marked complete | **Allowed** | Agent enters recipient emails; link is expiring and revocable |
| Suppressed dimension exists but is not decisive | **Allowed with explicit disclosure** | Share preview names the suppressed dimension and confirms it will remain visible on the share surface |
| Pairwise order is withheld because an unread/conflicting field is decisive | **Allowed only if the share surface preserves the withheld group** | Preview shows the bracketed group and withhold reason; no flattened rank or "best" label may be sent |
| Runtime can only flag uncertainty and cannot determine whether withhold is required | **Blocked for decisive-looking shares** | Agent must verify, remove the affected offer, or share only after the runtime contract is available |
| Any included offer is not-yet-verified | **Blocked by default** | Agent must verify the offer, remove it from the shared set, or intentionally share a clearly marked draft if a later product decision creates that mode |
| Set is provisional but all included offers are vouched | **Allowed with explicit disclosure** | Share surface must say "Comparison of [N] offers in so far" and must not imply finality |
| N collapses to 1 after exclusions or revisions | **Comparison share blocked; single-offer share path used** | Remove ranking chrome and route to the single-offer share model |
| Recipient emails missing or invalid | **Blocked** | Email-gated DEC-7 access cannot be created until recipients are entered |

### How the comparison share surface uses the screen-spec-template

The comparison-share surface is a full screen spec using the same template as share-surface.md:
- §0 Organizing idea: "fit-to-priorities, an input not a verdict"
- §1 Layout: brand frame → ranked set with "Ranked by…" basis → per-offer groups (N) → call prompt
- §2 State grammar: inherits the six absence states from share-surface.md; adds suppressed-visible-but-excluded and withheld-order states
- §3 Information design: per-offer element design inherited from share-surface.md; buyer-name slot added; basis-line element new
- §4 Interactions: zero interactions intentional (read-only); no acknowledgment action; `tel:` call prompt inherited
- §5 Mobile: mobile-primary inherited; ranked cards on narrow screens
- §6 Design forks: access-control model (DEC-7 locked); ranking-presentation principle; weighting display simplification
- §7 Deferred: static PDF; multi-viewer tracking; agent-alias system (possible later option)

**Starting point for the spec author:** v2.1 §8 (the full sibling brief), plus the inheritance
table above, plus share-surface.md as the format model.

---

## H. Verification Steps

A reviewer runs these checks against the completed `comparison-view.md`.

### 1. Every doctrine obligation has a named screen home

- [ ] **Legibility (§4.1):** "Why is A above B?" has a concrete answer in plain terms — at
  rest (leading cells in the matrix plus adjacent-order reason preview) and on demand
  (pairwise delta). The delta is relative (A vs. B), not absolute (description of A alone).
  The delta is scoped to weighted dimensions.
- [ ] **Honest weighting (§4.2):** The basis line and compact weights are legible at rest
  before Customize opens. Customize expands in place. The six-item "what is visible instead
  of sub-scores" list from §C above is fully satisfied. No per-offer number, no total column,
  no star rating, no "best offer" badge.
- [ ] **Inverted-ranking guarantee (§5):** A specified state explicitly *withholds* an order
  (not just warns). A suppressed dimension is *visible-but-excluded* (not disappeared, not
  silently dropped). Trace v2.1 fixture 3 through the spec: buyer-broker comp unread → net
  suppressed visible-but-excluded (net column present, marked excluded for Chen) → Reyes-vs-Chen
  order genuinely withheld (they appear in a bracketed group with the withhold reason stated).
- [ ] **Runtime contract:** The spec names the runtime dependencies for unknown propagation,
  withhold-capable ranking, net-to-seller formula, and closeness-band parameter. Any alpha
  degradation is doctrine-bound and recorded, not hidden in screen copy.
- [ ] **Clause 1 inherited per offer:** The per-offer provenance handle, the three-way
  field-state distinction, and term-based explanation (Explanation voice from domain-vocabulary.md)
  are all present in the matrix cell and/or the per-offer expansion.

### 2. Every state has a visually distinct treatment named

- [ ] All states from §F have a named visual treatment in the spec's §2
- [ ] The consolidated field-state matrix appears before individual matrix-cell designs
- [ ] The dangerous collapses do not occur: empty-on-form ≠ unreadable ≠ not-applicable ≠
  not-captured — each is visually distinct inside the dense matrix
- [ ] Agent-corrected ≠ present-confident: the corrected marker and the original value are
  traceable even inside a small matrix cell
- [ ] Blank is never imputed, never zeroed, never labeled "intentionally omitted"
- [ ] Aggregate-field participation rules are explicit: verified/corrected, empty-on-form,
  not-captured, structurally-null, unreadable, and conflicting components have distinct effects
- [ ] Not-yet-verified (offer-level) is visually distinct from set-provisional (set-level)
- [ ] Tie/near-tie renders distinctly from a decisive single-position rank

### 3. Every fork is either locked (with DEC entry) or explicitly deferred (with reason + home)

- [ ] Fork C (layout model): LOCKED DEC-9 or LOCK-pending-mockup named
- [ ] Fork D (orientation): LOCKED DEC-9
- [ ] Fork E (re-weighting): LOCK-pending-mockup DEC-14 with degraded path named (mobile → apply-then)
- [ ] Fork F (Customize at rest): LOCKED DEC-10
- [ ] Fork G (legibility affordance): LOCKED DEC-13
- [ ] Fork H (atom location): LOCKED DEC-15
- [ ] Fork I (net to seller): LOCK-pending-mockup with suppressed path confirmed and DEC-12 entry
- [ ] Fork J (free-text): LOCKED DEC-16
- [ ] Fork K (set-provisional): LOCKED DEC-17
- [ ] No fork reads "to be decided" without a named home and expected resolution trigger
- [ ] The DEC allocation table matches the fork list and decisions.md entries exactly

### 4. The spec passes the doctrine §7 test

> "Does this make the contract more trustworthy to understand — by provenance, honest
> uncertainty, or term-based explanation — or does it only make it look more finished?"

- [ ] The suppression/withhold treatment makes the comparison *more trustworthy*
- [ ] The non-laundering obligation holds for the order: nothing makes the ranking look more
  decided or cleaner than the reads support (no gap disappears, no suppressed dimension hides)
- [ ] Polish that hides uncertainty fails this test — check every "cleaner" design choice

### 5. The spec passes the NORTH-STAR test

> "Does this move the agent toward a comparison they're proud to put their brand on — through
> upload, verify, compare, or share — or does it sit outside that path?"

- [ ] The comparison view lands the agent on a ranked view they can send to the seller
  with confidence that the order is traceable
- [ ] The compare → share path is explicit: the share-initiation UI is specced
- [ ] The share-readiness matrix is present: withheld order, suppressed dimensions,
  not-yet-verified offers, set-provisionality, N=1 collapse, and invalid recipients are
  each allowed, blocked, or allowed only with explicit disclosure
- [ ] The spec is on the spine, not a detour

### 6. STATUS.md and decisions.md are updated (post-write checklist)

- [ ] STATUS.md: comparison row updated from "⛔ not started" to reflect the spec's state
- [ ] decisions.md: DEC-9 through DEC-17 (and any additional entries locked during
  spec-writing) added as full entries following the DEC-1–DEC-8 format
- [ ] decisions.md backfill index: note comparison-view decisions that came from earlier
  docs and need promotion to full entries (Forks A, B in particular)
- [ ] IA §7: DEC-8 dimension set and order formally incorporated on the next IA version bump

---

## I. Rollback Plan

### DEC entries are superseded, never deleted

The decisions.md convention: a wrong decision gets a **new DEC-n′ entry** that explicitly
cites the superseded DEC-n. The old entry remains, annotated "Superseded by DEC-n′ —
[date] — [reason]." This creates an auditable trail of *why* decisions changed — more
valuable than a clean log.

Example: if Fork C (layout model) is reversed after mockup review, the new entry reads:
"DEC-9′ — [date] — Layout model revised: ranked cards replace the matrix hybrid (DEC-9)
because [reason from mockup]. Sections §1, §2, §3, §5 of comparison-view.md revised."

### Which sections change, by fork severity

| Fork | Severity | Sections of comparison-view.md that change | Re-mockup required? |
|---|---|---|---|
| C (layout model) | **Structural** | §0 (organizing idea may need revision), §1 (layout regions), §2 (state grammar in new layout), §3 (element in new layout), §5 (mobile adaptation) | Yes — most cascading; this is why C is LOCK-pending-mockup |
| D (orientation) | **Structural** | §1, §3, §5 | Likely yes, but less cascading than C |
| E (re-weighting) | **Behavioral** | §4 (interactions: Customize feel), §5 (mobile: live vs. apply-then) | Interaction prototype, not full re-mockup |
| F (Customize at rest) | **Cosmetic** | §2 (state: weighting at rest), §4 (interactions: Customize expand) | No |
| G (legibility affordance) | **Trust-grammar** | §4 (pairwise delta trigger), §3 (leading-cell marks) | No, but must re-verify the §4.1 TODO is still resolved by the replacement |
| H (atom location) | **Behavioral** | §4 (expansion/drill-down), §5 (mobile drill-down) | No |
| I (net to seller) | **Trust-grammar** | §3 (net cell element design), §2 (suppressed-net state) | Validate on a real packet; not a full re-mockup |
| J (free-text) | **Cosmetic** | §3 (other-terms section placement) | No |
| K (set-provisional) | **Cosmetic** | §2 (state grammar for provisional marker), §4 (set-state marker timing) | No |

### Trust-grammar reversals require doctrine reconciliation

If a fork reversal weakens a trust guarantee (e.g., "the backend can't build the withhold
tier; we'll show a caveat instead of withholding"), that is **not a free screen-level
edit.** The path is:
1. Record the deliberate divergence in decisions.md per CLAUDE.md cross-repo rules
2. Bump the trust-doctrine.md version to acknowledge the weaker guarantee, OR
3. Note it as a bounded exception with the named technical constraint and escalation path

The screen may render a degraded guarantee only after the doctrine acknowledges it.

### How to communicate a change to the main repo

1. Update decisions.md with the superseding DEC entry (visible to both repos)
2. Update comparison-view.md with the revised section + status/version bump
3. Update STATUS.md
4. If the reversal affects a CLAUDE.md cross-repo seam (e.g., `HIGH_STAKES_FIELD_KEYS`,
   the inverted-ranking generalization, the net-to-seller formula): note which main-repo
   implementation is now misaligned, and create a reconciliation task in the main repo

---

## J. Unresolved Questions

This planning pass could not answer these from the existing docs. They must be resolved
before or during spec-writing.

### Blockers for writing comparison-view.md

None. The two former blockers are resolved (Morris decisions DEC-7 and DEC-8). The items
below are cross-repo dependencies that do not block writing as long as the spec names the
runtime contract from §C. They do affect implementation and any mockup that claims the
runtime guarantee is already available.

### Runtime-contract dependencies to confirm before implementation or guarantee-claiming mockup

**J-1. §5 generalization coverage in the main repo.**
Doctrine §5's DEFER-LINE: the inverted-ranking guarantee is generalized only for §3G(3)
(`buyer_broker_comp`, `PCT-OR-FLAT`) today. The spec specifies the target design and names
the runtime contract; the per-field runtime generalization is tracked main-repo work.
Before implementation or a mockup that claims the guarantee generally, the main repo must
confirm which comparison-affecting fields degrade to *unknown* (not to a ranking-moving
default) on a real packet. If the backend can only *flag* (not *withhold*) for some fields
at alpha: tier 3 (withheld order) degrades to tier 2 (suppressed-visible-but-not-withheld)
for those fields. The spec must name the degraded path and make it doctrine-bound
(escalate, not silently accept).

**J-2. Net-to-seller formula established in the main repo.**
Fork I recommends computing net as arithmetic of traceable components. The formula (which
seller-paid costs feed net) is a main-repo concern; the spec cites it, does not define it.
Before implementation or a mockup that shows computed net, confirm: which components?
which main-repo symbol to cite? If the formula isn't established, the net dimension falls
back to components-only for alpha (Fork I fallback).

**J-3. Closeness-band width for tie/near-tie.**
States §4 names the tie/near-tie state but does not define "close." The spec must state that
the closeness-band width is a **main-repo tuning parameter** (not a spec decision), name
where it lives, and note that changing it shifts state boundaries without requiring a spec
revision. This is a two-sentence clarification, not a blocker.

### Must resolve before comparison-share-surface.md (not a blocker for comparison-view.md)

**J-4. Comparison share mobile layout.**
share-surface.md is explicitly mobile-primary. The comparison share adds a ranked list and
N offers, which is harder on mobile than one offer. Must the comparison-share spec define a
distinct mobile layout (ranked cards, one per offer, stacked)? Or does the desktop layout
translate reasonably to mobile via responsive width? The comparison-share spec resolves this.

**J-5. Agent-alias system for buyer names.**
The plan resolves buyer identity (§8.4 Q2 of v2.1: show buyer names to the seller). A
future request for agent aliases ("Offer A / B / C") is plausible and is explicitly deferred
in v2.1 §8.4 Q2. The comparison-share spec must name this deferral with a home. Not a blocker.

**J-6. Comparison share recipient-side UX for the email gate (DEC-7).**
DEC-7 specifies email-gated recipient access with expiration and agent revocation. The
workspace spec owns the share-initiation UI. The recipient experience — what the seller sees
when they click the link, how the email gate is presented, how expiry is communicated — belongs
to the comparison-share spec and the main repo. The comparison-view spec does not need to
resolve this, but it must *not* spec the recipient experience.

### Inherited from doctrine (confirmed as tracked, not newly unresolved)

**J-7. The three-way visual grammar (doctrine §3.2 TODO).**
This TODO is partially resolved in verify-workspace.md (for the verify surface) and in
share-surface.md (for the single-offer share). The comparison view must extend it to the
dense matrix — the most challenging environment. The grammar itself is settled (present /
empty-on-form / unreadable must never look alike); the *pixel treatment inside a matrix cell*
is the spec's decision to make. Not unresolved at the principle level; unresolved at the
element-design level, which Step 4 of §D resolves.

---

## Execution Notes

When writing `07-screen-design/comparison-view.md` from this plan:
1. Use sections A–J as the working sequence and map them into the screen-spec template
   (§0 through §7) during spec-writing.
2. Retain the v2.1 worked fixtures (§9 of v2.1) as an appendix or inline in §F.
3. Retain the comparison-share sibling brief (§8 of v2.1) as §G or an appendix.
4. Carry forward all locked forks and their DEC entries from v2.1.
5. Treat the at-rest adjacent-order reason preview, DEC allocation table, runtime contract,
   consolidated field-state matrix, aggregate-field participation rules, and share-readiness
   matrix as first-class plan requirements.
6. Do not duplicate verification that has already been done; the v2.1 external review and
   Morris decisions are settled inputs, not items to re-open.

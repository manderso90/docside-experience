# Plan — The Comparison View (screen-spec Plan 2.0)

> **Status:** v2.0 — plan. Revises v1.0 in response to an external review (ChatGPT)
> of v1.0. This is the plan for writing `07-screen-design/comparison-view.md`, not the
> spec. It is a **revision, not a rewrite**: every v1.0 section the review did not
> challenge is retained (some renumbered); the additions are the data-state taxonomy
> (§5), the expanded comparison-share plan with access control (§8), worked example
> fixtures (§9), an open-questions-for-Morris section (§15), and a disposition +
> changelog (§17). The whole remains specific enough to write the spec from without
> further guidance.
> **What changed and why:** see §17 (per-concern disposition + changelog). One-line
> summary: v2.0 resolves comparison-share access control, plans the share surface as a
> sibling with an inheritance table, tightens the data-state distinctions, adds mobile
> Customize behavior and concrete fixtures, and separates what blocks `comparison-view.md`
> (nothing — write it now) from what blocks the sibling share spec (access control —
> Morris).
> **Derives from:** `NORTH-STAR.md`; `trust-doctrine.md` §2, §4, §5; `information-
> architecture.md` §1, §2.1, §3–§5, §7; `critical-path.md` §3; `states-and-edge-cases.md`
> §1, §3, §4, §4.1; `handoff.md` §2, §6, §7–§8; `verify-workspace.md` and
> `share-surface.md` (format, quality, fork discipline); `copy-guidelines.md`;
> `domain-vocabulary.md`; `_templates/screen-spec-template.md`.
> **Produces:** the writing brief for `comparison-view.md` (agent workspace), a full
> sibling brief for `comparison-share-surface.md` (§8), and the dependency note for
> `reconciliation-gate.md` (§3).

---

## 0. Orientation — what this screen is, in one paragraph

The comparison view is the **compare** stage of the spine (`upload → verify →
[compare] → share`), active only when **N > 1**. It is the single screen that
exercises **ranking-trust** (doctrine §2, Clause 2): legible order, honest weighting,
and the inverted-ranking guarantee. Every other screen lives on the *understanding-
trust* surface (one offer, made clear). This one inherits all of that **per offer**
(the Clause-1 atom recurs inside the comparison) and adds three mechanisms the single-
offer view never needs (doctrine §4–§5). It is the retention engine (NORTH-STAR's depth
loop) and the only home of the most product-specific guarantee in the doctrine — a
guarantee that has never been rendered. This plan exists to render it correctly the
first time.

---

## 1. The one organizing idea

**Handle: the order accounts for itself.**

> **One sentence:** the weighting that drives the order and the terms that decide each
> position are continuously visible and live alongside the order itself — so "why is
> this offer above that one?" is always answerable in plain terms, and the one thing
> the screen will never do is show a position it cannot account for.

The comparison stage's equivalent of verify's *provenance made spatial* and share's
*orient first*, derived from the trust obligation, not from convenience:

| Screen | Stage trust obligation | Organizing idea | The move it makes physical |
|---|---|---|---|
| Verify | understanding-trust — a wrong *fact* | **provenance made spatial** | focus a value → the document moves to its source |
| Share | understanding-trust, for a vulnerable reader | **orient first** | lead with what the offer *is*, before any detail |
| **Compare** | **ranking-trust — a wrong *order*** | **the order accounts for itself** | every rank co-present with its basis; re-weight and watch the order respond; withhold any order that can't be traced |

This is the constructive form of the doctrine's two prohibitions — *"An order Docside
cannot explain in plain terms is an order Docside does not present"* (§4.1) and *"If we
cannot trace how a ranking was determined, we will not present it"* (§5). Where verify
makes a **value** traceable to the contract, comparison makes the **order** traceable
to the weighting and the terms. If two people disagree about any component below, this
is the sentence they return to first (template §0). *(The review scored this dimension
5/5; it is retained unchanged.)*

---

## 2. Surface scope — two documents, not one (resolves Fork A)

The work spans two surfaces: the **agent-facing comparison workspace** (authenticated,
desktop-likely, interactive) and the **comparison share surface** (public
`/share/[token]` for N > 1, mobile-first, read-only).

**Recommendation: two separate documents.** `comparison-view.md` (this plan's target)
specifies the **agent workspace**; a sibling `comparison-share-surface.md` specifies
the **seller surface** — exactly as `share-surface.md` followed `verify-workspace.md`.

**Rationale.** Precedent is unambiguous (share-surface §7 already defers "the comparison
surface… its own spec follows"); IA §3 forbids the merge ("two distinct information
architectures… conflating them is a category error"); the two surfaces carry different
organizing ideas (workspace: *the order accounts for itself*; share: *fit-to-priorities,
an input not a verdict*); and the share carries its own open access-control decision
(handoff §8). Two focused specs each earn the rigor verify/share earned.

**What changed in v2.0:** the review (Major 2) asked that the share be *planned*, not
just deferred. It now is — **§8 is a full sibling brief** (inheritance table, divergences,
access control, resolved questions), not a list of obligations. `comparison-view.md`
still carries only a short "handoff to the comparison share" pointer to §8.

**Fallback (named, not recommended):** if the team insists on a single artifact, §8
becomes `comparison-view.md` §8 verbatim. Rejected for the reasons above; recorded so
the choice is explicit.

---

## 3. The reconciliation gate — a sibling spec this one depends on (resolves Fork B)

The reconciliation gate (IA §2.1, states §4.1) is where the agent decides which offers
**enter** the comparison — assembling membership across the two intake channels, with
source visible, duplicates flagged, per-offer exclusion.

**Recommendation: its own spec (`reconciliation-gate.md`).** Its trust job is
*membership made deliberate* — a **precondition** for ranking-trust, not ranking-trust
itself. It is structurally upstream (critical-path §3 places it on the Verify-each →
Compare seam; its output is the comparison's input), it fires at a different nav
location (listing → compare boundary, IA §5), and verify-workspace §7 already names it
as a separate deferred screen.

**What `comparison-view.md` still owns (the comparison-internal slice):** the
**curated-set precondition** stated explicitly; the **"revise the set" re-entry** (drop
the duplicate / withdrawn / backup mid-compare); the **set-provisional state** (the set
is open until the deadline, agent-workflow §2); and the **N→1 collapse** consequence
(§7). *Alternative considered and rejected:* gate-as-stage-0-of-compare (would load the
comparison view's organizing idea with a second trust job; the gate also governs the
listing view). Retained unchanged from v1.0.

---

## 4. The three doctrine TODOs that land here — proposed resolutions

The three `TODO(design)` markers in doctrine §4–§5. The spec must close all three (no
TODO for this screen survives into the spec). Each resolution is concrete enough to draft
and to lock as a DEC.

### 4a. Legibility of *relative* position (doctrine §4.1 TODO)

"Why is offer A above offer B?" must be answerable in terms the agent could repeat to a
seller — and **distinct from** the per-offer explanation of 3.3 (which describes one
offer). 4.1 is about the *delta*.

**Resolution — a dimension matrix at rest, a pairwise delta on demand.**
- **At rest (the scaffold):** the comparison is a **dimension matrix** — offers in
  ranked order down the side, the **weighted dimensions** across the top (from the
  seller-priority profile). Each cell holds the offer's **term** in that dimension
  (Explanation voice — "21-day close"), and the **leading offer per weighted dimension
  is marked**. Down a column = "who leads on this priority?"; across a row = the Clause-1
  atom for one offer. The basis is legible without interaction.
- **On demand (the §4.1 affordance proper):** tapping an offer (or the gap between two
  adjacent offers) yields a **pairwise "why this order" delta** — "Ranked above [next]
  on: higher price, faster close; [next] leads on: lower buyer-broker comp." Pure terms,
  signed by direction, **scoped to the weighted dimensions** (a difference on an
  unweighted dimension is noted as "they also differ on X, which you didn't weight,"
  never as a reason for the order).
- **Constraints:** terms only, never scores (copy §2.2); reflects the *current*
  weighting; composes with suppression (4c) — a delta that would rely on an unread
  dimension says so, never silently drops it.

### 4b. The weighting display *at rest* (doctrine §4.2 TODO)

The free-slider / live-total **Customize** model is the interactive control. The TODO:
what does the weighting look like *before* Customize is opened? "Legible without
interaction."

**Resolution — the "Ranked by" basis statement + a compact relative-weight indicator
as the always-visible header; Customize expands it in place.**
- **At rest:** a term-based, ordered **basis line** — *"Ranked by: highest net to
  seller, fastest close, fewest contingencies"* (the phrasing already in handoff §7 and
  seller-workflow §4) — paired with a **compact relative-weight indicator** (ordered
  bars/chips, labeled by dimension, magnitude shown). It sits above the matrix as the
  order's **declared basis**.
- **Customize** expands the header **in place** into the free-slider / live-total editor
  (doctrine §4.2) — the **same control at two widths** (verify's invariant).
- **Default source:** the listing-scoped seller-priority profile, seeded from agent
  presets (IA §7). "At rest" = the seeded/last-saved profile, shown legibly.

**The line the spec must hold — weights shown, sub-scores never.** Doctrine §4.2
*mandates* visible weighting; copy §2.2 *forbids* sub-scores. Not in tension: the
**weighting** is the seller's priorities (ordered terms + relative magnitudes); the
**sub-score** is the per-offer math, and it never appears.

**What is visible *instead of* a sub-score** *(added in v2.0, review Minor 3 / Suggested
Change 3 — the positive enumeration):*
1. the **basis line** — "Ranked by: [priorities, in order]";
2. the **dimensions** — the matrix columns, each a term-bearing priority;
3. the **deciding terms** — the pairwise "why A over B" delta, in business language;
4. the **leading-cell marks** — which offer leads each weighted dimension;
5. the **relative-weight indicator** — ordered bars/chips (priority magnitude, *not* a
   per-offer score);
6. the **caveats** — suppression / partial / withheld / tie / near-tie markers.

**Never visible:** a per-offer total, a 0–100, a "0.92 vs 0.78," a star rating, a "best
offer" badge.

### 4c. The inverted-ranking guarantee, made visible (doctrine §5)

When a comparison-affecting dimension is suppressed because a field is unreadable, what
does the agent see? The guarantee: *"marks it unknown and tells you so… does not fill
the gap with a default… If we cannot trace how a ranking was determined, we will not
present it."*

**Resolution — a three-tier treatment that degrades from cell to order:**
1. **At the cell:** the unreadable comparison-affecting field renders with the standard
   **unreadable** treatment ("We couldn't read this field"), at elevated weight for
   high-stakes fields (states §1; share-surface DEC-4 logic). Never blank, never a dash,
   never a default, never a guess.
2. **At the offer's position:** the dimension that field feeds is **suppressed for that
   offer** — the offer is explicitly *not ranked on [dimension]*, with a visible
   **"partial — [dimension] unread"** caveat. **The suppressed dimension does not
   disappear; it remains visible-but-excluded** *(clarified in v2.0, review Minor 4 / Q3
   — a disappeared dimension would hide a gap, violating non-laundering, handoff §6)*.
3. **At the order (the §5 hard guarantee):** if the suppressed dimension would be
   **decisive** between two offers, the product **does not assert that pairwise order** —
   the offers render as a **bracketed "can't be separated on your priorities until
   [field] is read"** group, with the field named. The one place the product visibly
   **withholds** an order rather than guess it.

**Resolution path (cross-screen tie):** every suppression treatment links **back to that
offer's verify workspace** for that field — "read it at verify to rank this dimension."
Suppression is an honest hold with a way forward, never a dead end.

Worked instances of all three tiers are in §9 (fixtures 2–3) — *added in v2.0 (review
Minor 2) so the tiers stay concrete behavior, not abstract doctrine prose.*

**Cross-repo caveat (CLAUDE.md seam):** doctrine §5's DEFER-LINE states this guarantee
is honored today only in the §3G(3) buyer-broker-comp field and is **not yet
generalized**. 4c specifies the *design*; the per-field runtime generalization
(degrade-to-unknown, not to a ranking-moving default) is **tracked main-repo work**. If
the backend can only *flag* (not *withhold*) for some fields at alpha, tier 3 degrades —
but that degradation is **doctrine-bound** and escalates (§14), it is not a free
screen-level edit.

---

## 5. The data-state taxonomy — how each state affects ranking and disclosure *(new in v2.0)*

*Added in response to review Major 3 / Suggested Change 3 and Questions 5. The six states
already live in states §1; what was missing is their effect on **ranking participation**
and **disclosure**, plus one offer-level distinction the interruptible workflow
introduces. This taxonomy is the single reference the spec's §2 (state grammar) and §6
(forks) build on.*

### 5.1 Field-level states

| Field state | Means (states §1) | Ranking participation | Disclosure |
|---|---|---|---|
| **Verified value** (extracted-confident) | read, stood behind at verify | ranks normally | the value, Explanation voice; §-citation |
| **Agent-corrected** | agent fixed a misread at verify (vouched) | ranks normally — a corrected value is a vouched value | the value + "corrected by agent · original: X," original traceable (doctrine §3.1 v0.5) |
| **Empty-on-form** (blank) | field exists on the form; left blank | **not imputed**; excluded from that dimension's lead-marking for this offer; if it feeds an aggregate (net), the aggregate is suppressed-or-caveated, **never defaulted to 0** | "Not specified on this form." **Not** labeled "intentionally omitted" — see rule (a) |
| **Not-captured** (structurally-null) | the form never records this value | never a ranking input (no value exists to rank) | "Not captured on this form." |
| **Not-applicable** | excluded by another answer (e.g., financing rows when all-cash) | the dimension is **N/A for this offer** — shown as N/A, not as a gap and not as a zero | "Not applicable — [reason]." |
| **Unreadable** | OCR/parse failure, or low-confidence resolved to unreadable at verify (states §1.1) | **suppressed (4c)** — never ranks on it; if decisive, order withheld | "We couldn't read this field." Elevated weight if high-stakes |
| **Conflicting / incoherent** | e.g., `PCT-OR-FLAT` contradictory read | resolves to `null` → treated as **unreadable** (never a guess) | "We couldn't read this field." (copy §3 `PCT-OR-FLAT` rule) |

**Three rules the taxonomy enforces:**
- **(a) We do not distinguish "blank" from "intentionally omitted."** Asserting the
  buyer *chose* to omit is inferred intent — forbidden (copy §4; `DEFAULT-TRAP`, presence
  ≠ choice). The form shows blank; we show blank; we never narrate why. *(This partially
  rejects a sub-item of review Major 3 — "intentionally omitted" is not a state we may
  claim — with a doctrine-grounded reason.)*
- **(b) Blank ≠ zero for ranking.** A blank component never defaults to 0 in an
  aggregate. Whether a specific blank field carries a contractual meaning (blank = none)
  is **field-semantics owned by `domain-vocabulary.md` / the main repo**, surfaced via
  the field's state — never guessed by the comparison.
- **(c) Not-applicable, unreadable, and empty are three different cells.** An all-cash
  offer's financing dimension is *N/A* (not compared, not a gap); an unread financing
  field is *unreadable* (suppressed); a blank financing field is *empty* (not imputed).
  The grammar of absence holds inside the matrix at the pixel level (states §1; DEC-6
  prohibition list).

### 5.2 Offer-level verification state *(the distinction the interruptible workflow adds)*

The workflow is interruptible and the set is open until the deadline (agent-workflow §2),
so an offer can sit in the set **before** it has completed verify. Field-level
low-confidence is already resolved-at-verify (states §1.1), so this is an *offer*-level
distinction, not a field one:

| Offer state | Means | Treatment |
|---|---|---|
| **Vouched** | passed the verify → share boundary — every field confirmed, corrected, or marked unreadable (critical-path §3) | ranks normally |
| **Not-yet-verified** (provisional) | in the set, but verify is incomplete | flagged **"not yet verified"**; held out of the asserted ranking (or shown provisionally with a **"verify to rank"** prompt); **never ranked as if vouched** |

This is the review's "extracted-but-not-verified / provisional" concern, placed at the
correct level. **Distinguish from set-provisionality (Fork K):** set-provisional = *more
offers may arrive*; offer-provisional = *this offer isn't vouched yet*. Both are real and
both are shown; they are different markers.

---

## 6. Design forks — every place two reasonable options decide the screen

**Altitude discipline (the spec stays at design/behavior level).** *Added in v2.0
(review Overengineering 3/5).* The forks below specify **behavior and its trust purpose**,
not implementation. The spec references implementation constants and engines **as
dependencies, by name** — `HIGH_STAKES_FIELD_KEYS`, the scoring/weighting engine, the
net-to-seller formula — and **does not redefine them** (high-stakes-fields-pointer
governance: cite, never fork). Live re-ranking is specified as *"the order re-orders when
a weight changes, for this trust reason,"* not as animation/perf mechanics. Suppression
tiers describe *what the agent sees*, not how it is computed.

Forks A (surface scope) and B (gate placement) are resolved in §2–§3. The rest decide
layout, components, and trust grammar. Each carries a recommended lock with its anchor;
**LOCK-pending-mockup** marks the high-risk ones the mockup must validate (§14).

### Fork C — Core layout: matrix vs. ranked cards vs. hybrid  *(the cascading fork)*
- **Matrix** (offers × dimensions): strongest cross-offer legibility; but reads as a
  **scoreboard**, which implies scores (copy §2.2 hazard). **Ranked cards**: strongest
  per-offer atom, mobile-friendly; weak at *relative* legibility. **Hybrid**: order +
  basis co-present.
- **Recommend: hybrid — a ranked order spine + a dimension matrix as the comparison
  body.** Defuse the scoreboard risk structurally: **no total column, no per-offer score,
  ever**; cells hold terms, the spine holds positions. Anchor: doctrine §2; copy §2.2.
  **LOCK-pending-mockup.** → **DEC-7** (§14).

### Fork D — Orientation: offers-as-rows vs. offers-as-columns
- **Recommend: offers as rows, dimensions as columns.** A ranking *is* a vertical list;
  scales in N; degrades to mobile cards cleanly. Anchor: NORTH-STAR depth loop;
  agent-workflow §2. **LOCKED.** (Mobile inverts to per-offer cards — §12 phase 6.)

### Fork E — Re-weighting feel: live re-rank vs. apply-then-reorder
- **Recommend: live re-ranking**, animated transition (offers move, don't jump). Seeing
  the order move when you move a weight is the strongest proof it is not a black box.
  Anchor: doctrine §4.2. **LOCK-pending-mockup** (motion/perf risk; mobile may fall back
  to apply-then — §12, Fork-E scope lever in §11).

### Fork F — Customize at rest: collapsed vs. always-open
- **Recommend: collapsed at rest** (the basis line + compact weights; Customize expands)
  — at-rest legibility without the control's footprint. Anchor: doctrine §4.2 TODO; the
  verify two-widths precedent. **LOCKED.** → **DEC-8** (§14).

### Fork G — The legibility affordance form
- **Recommend: matrix at rest + pairwise delta on demand** (per 4a). Marked leading
  cells carry at-rest legibility; the pairwise delta answers the doctrine's *relative*
  question, distinct from 3.3. Anchor: doctrine §4.1. **LOCKED.**

### Fork H — Where the per-offer Clause-1 atom lives
- **Recommend: inline expansion into a side detail pane (desktop) / drill-down (mobile),
  with a link to the full verify workspace** for re-checking. The comparison composes
  atoms; it doesn't replace them. Anchor: doctrine §4; IA §4. **LOCKED.**

### Fork I — "Net to seller": computed dimension vs. components only  *(trust-critical)*
- **Computed net** serves the "highest net" priority but can inherit a guess from an
  unread component (buyer-broker comp `PCT-OR-FLAT`, credits) and **invert the order** —
  the §5 danger. **Components only** is safest, least legible.
- **Recommend: compute net to seller only when all components are confidently read; if
  any component is unread, net drops to the suppression treatment (4c) — and, per the
  v2.0 clarification, the net dimension stays *visible-but-excluded* ("net can't be
  determined: [component] unread"), it does not disappear and is not ranked.** Net is
  then an **arithmetic of traceable values**, traceable to its components — the move the
  worked specimen already makes with *"$250,000 down"* (price − financing, both present
  and traceable) — never a model guess. Anchor: worked-specimen §1; doctrine §5; the
  §3G(3) precedent. **LOCK-pending-mockup** (validate on a real packet with an unread
  component — fixture 2, §9). → **DEC-10** (§14).

### Fork J — Free-text / unweightable terms in a dimension matrix
- **Recommend: a non-ranked "Other terms" section, quoted verbatim, explicitly outside
  the weighting** — present to read, never scored into the order; the screen "visibly
  leaves room for everything it can't see" (seller-workflow §4). Anchor: doctrine §3.2
  v0.3(a); copy §2.4. **LOCKED.**

### Fork K — Set provisionality: provisional vs. present-as-final
- **Recommend: a provisional marker until the agent marks the set complete** —
  *"Comparison of the 4 offers in so far"* — never implying a finality the transaction
  hasn't reached. Anchor: agent-workflow §2. **LOCKED.** *(Distinct from the offer-level
  not-yet-verified marker, §5.2.)*

---

## 7. Comparison-specific edge cases → screen treatments (states §4)

States §4.1 (assembling the set) belongs to the **reconciliation-gate** spec (§3); the
comparison view inherits the curated set + the re-entry affordance. The four states §4
cases below are the comparison view's own. Each maps to a data-state from §5.

| Edge case | Trigger | Screen treatment | Anchor |
|---|---|---|---|
| **Unreadable comparison-affecting field** | a ranking-feeding field is unreadable for one offer | the **three-tier suppression** of 4c: cell unreadable → dimension suppressed, **visible-but-excluded** → if decisive, **order withheld**; link back to verify (fixtures 2–3) | doctrine §5; states §4; §5.1 |
| **Asymmetric completeness** | offer A has a verified term; offer B left it blank (Q5) | B's cell shows **"Not specified on this form"** (empty-on-form, visually distinct from unreadable); B is **not imputed, not defaulted to 0, not penalized**; the dimension's lead-marking excludes B; if the field feeds an aggregate, the aggregate is suppressed-or-caveated for B, never silently zeroed | states §4; §5.1 rules (a)/(b) |
| **N = 1 in the comparison** | dedup/exclusion (or only one offer in) collapses the set to one | **fall back to the single-offer summary** with a note ("Only one offer is in this comparison"); **no ranking chrome, no weighting header asserting an order over one item** (fixture 5) | states §4 |
| **Tie / near-tie** | offers within a closeness band on the weighted priorities | a **tie / near-tie band** — same position or "these two are very close on your priorities"; the pairwise delta reads "nearly even; they differ on [terms] but it's close"; **never a false decisive order from rounding** (fixture 4) | states §4; copy (no false precision) |

Two notes for the spec: the **closeness-band width** and the **confidence threshold** are
*tuning* questions (extraction/scoring), not design questions — the design provides the
*states* (tie/near-tie, suppressed) and their treatments. And the dangerous collapses
(empty-on-form vs. unreadable; agent-corrected vs. present-confident) must hold **inside
the dense matrix**, where they are likeliest to fail.

---

## 8. The comparison share — inheritance, divergence, and access control *(expanded in v2.0)*

*Rewritten from v1.0's obligations list into a full sibling brief, in response to review
Major 1 (access control), Major 2 (share inheritance), and Questions 1–4. This section
is the brief for `comparison-share-surface.md`. The comparison share is, in one line, **N
single-offer share surfaces, ranked, with the basis shown and access tightened** — every
Clause-1 invariant per offer, plus a legible order presented as an input to the seller's
decision, never the decision.*

### 8.1 What it inherits vs. where it diverges (single-offer share → comparison share)

| Element / invariant | Single-offer share (`share-surface.md`) | Comparison share |
|---|---|---|
| Organizing idea | "orient first" — what this offer is | **DIVERGES** → "fit-to-priorities, an input not a verdict" (seller-workflow §4–§5) |
| Per-offer atom: provenance to seller, the six absence states distinct, term-based, corrections-as-corrected, glosses always-on, §-citation inline (DEC-3/4/5) | yes, for one offer | **INHERITS, per offer** — the comparison is N atoms |
| Top-of-screen | the one offer's headline terms | **DIVERGES** → the ordered set + the **"Ranked by…" basis line** |
| Weighting display | n/a (no order) | **NEW** → basis line always visible (Q4); magnitudes may be simplified for the seller, basis never hidden |
| Suppressed dimension | n/a | **NEW** → shown **visible-but-excluded** to the seller (Q3) |
| §5 guarantee, Principle voice | absent (single offer; worked-specimen §2) | **NEW** → "If we cannot trace how a ranking was determined, we will not present it" |
| Buyer identity | the one buyer (§1A) | **shows each buyer name (§1A)** to the seller (Q2); unreadable → fallback handle (states §4.1) |
| Read-only; no acknowledgment; `tel:` call prompt; non-laundering prohibition list (DEC-6) | yes | **INHERITS**; the prohibition list **extends to the order** (no false decisive order, no hidden suppression) |
| Access control | lightweight link acceptable for alpha (handoff §8) | **DIVERGES** → stronger; multi-buyer confidential (§8.3) |

### 8.2 How ranking reaches the seller (the governing decision)

**Ranking does reach the seller — as fit-to-priorities, never as a verdict.** The order
plus the visible "ranked by [their priorities]" basis, with the surface **visibly leaving
room for what it can't see** (a buyer's letter, gut feel — seller-workflow §4). **No
"best offer" verdict, no "accept" action, no score** (seller-workflow §5: "the decision
is never the algorithm's"). This is a stronger obligation than the single-offer surface,
which had no order to caveat.

### 8.3 The access-control open decision *(review Major 1)*

**The decision.** How a comparison share link is protected. A forwarded comparison link
exposes **every competing buyer's price and terms** (handoff §7) — categorically worse
than a single-summary leak, and email makes forwarding the norm (DEC-1 consequence).

**Options** (the space from review Q1 + handoff §8):

| Option | What it does | Trade-off |
|---|---|---|
| Free-forward tokenized link | anyone holding the link views it | **rejected** — multi-buyer confidentiality breach |
| Revocable link | agent can kill the link later | handoff §8 baseline; doesn't stop a forward before revocation |
| Expiring link | link dies after a window | limits exposure; seller may lose access mid-decision |
| Email-gated / recipient-bound | viewer must verify the intended email | strongest forwarding resistance; adds seller friction |
| PIN / passcode | shared secret to open | simple; the secret forwards with the link |
| Per-view agent approval | agent approves each open | maximal control; maximal friction, breaks "open it cold on a phone" |

**Risk.** A leaked comparison link is the highest-confidentiality failure on any Docside
surface. It deserves the strongest treatment, balanced against the seller's "open it cold
on a phone, no login" need (seller-workflow §0).

**Working assumption (so dependent specs are unblocked).** Comparison links are **not
freely forwardable**: at minimum **revocable and gated** (email-gated or expiring), per
handoff §8's recommendation. Single-summary links may stay lightweight for the alpha.

**Critical scoping — this does NOT block `comparison-view.md`.** The agent workspace is
**authenticated**; access control governs the **public share link**, i.e. the sibling
`comparison-share-surface.md`. The workspace only needs to **reflect** the chosen posture
in its "Share comparison" affordance (a placeholder: "this link applies the comparison-
share access posture — see handoff §8"). So **`comparison-view.md` is unblocked; the
comparison-share spec waits on the access mechanism.**

**Home + Morris-flag.** The final mechanism choice is **Morris's** (handoff §8: "Confirm
before share ships"), recorded in handoff §8 and a comparison-share DEC (anticipated
**DEC-12**, §14). Carried to §15.

### 8.4 Resolved share questions (from the docs)

- **Q2 — buyer identity:** **show each buyer's name (§1A) to the seller.** The seller
  owns these offers on their own property; real-world offer presentation names buyers.
  Confidentiality (handoff §7) is about the link reaching **outsiders** — addressed by
  access control (§8.3), **not** by hiding buyers from the legitimate seller.
  Unreadable §1A → the fallback handle (states §4.1). Agent-controlled aliases are a
  possible later option, not the default. *Resolved from docs.*
- **Q3 — suppressed dimension visible to the seller?** **Yes — visible-but-excluded.**
  Omitting it would hide a gap to look cleaner — a non-laundering violation (handoff §6)
  and a DEC-6 prohibition ("no collapsible absence rows"). The seller sees "we couldn't
  read [field] for [buyer], so this offer isn't ranked on [dimension]." *Resolved from
  docs.*
- **Q4 — same weights as the workspace, or can the agent hide/simplify?** **The basis
  (ordered priorities) is always shown; the agent sets the weights (that *is* the
  seller's priority profile) but cannot hide what produced the order** (doctrine §4.2:
  never a black box; handoff §2 invariant 5: weighting visible). **Display may simplify**
  — the seller surface may show the basis line and omit precise bar magnitudes — but the
  basis is never hidden. *Resolved from docs.*

---

## 9. Worked example fixtures *(new in v2.0)*

*Added in response to review Minor 2 and Suggested Change 5, and to serve Testing/DoD
(§13). Illustrative data echoing the worked-specimen's style (not the ground-truth
fixture); no CAR verbatim text. Three offers on one listing, ranked by: **highest net to
seller, fastest close, fewest contingencies.** Net to seller (illustrative) = price −
seller credit − seller-paid buyer-broker comp.*

**Cast.**
- **Reyes** — $1,275,000 · 21-day close · no appraisal contingency · 17-day loan
  contingency · $5,000 seller credit · buyer-broker comp 2.5%. Net = 1,275,000 − 5,000 −
  31,875 = **$1,238,125**.
- **Chen** — $1,300,000 · 30-day close · appraisal contingency at price · no loan
  contingency · no credit · buyer-broker comp (varies per fixture).
- **Okafor** — $1,250,000 **all-cash** · 14-day close · no contingencies · no credit ·
  buyer-broker comp 2.5%. Net = 1,250,000 − 31,250 = **$1,218,750**.

**Fixture 1 — Clean ranking.** Chen's comp reads as a flat $26,000 → Chen net =
$1,274,000. On the weighted basis the order is **Chen ▸ Reyes ▸ Okafor**. The matrix
shows each term per dimension; leading cells marked (Chen leads net; Okafor leads close
and contingencies). Pairwise delta on Chen vs. Reyes: *"Ranked above Reyes on: higher net
(+$36k), no loan contingency; Reyes leads on: faster close (21 vs 30 days)."* No score
anywhere; financing dimension is **N/A** for all-cash Okafor (shown N/A, not a gap).

**Fixture 2 — Suppressed dimension.** Chen's buyer-broker comp reads incoherently
(`PCT-OR-FLAT` conflict) → `null` → **unreadable**. Net depends on comp → Chen's **net
cell shows "We couldn't read this field — net can't be determined: buyer-broker comp
unread,"** visible-but-excluded; Chen is **not ranked on net** and carries a "partial —
net unread" caveat; a **"verify to resolve"** link points to Chen's verify workspace.
Chen still ranks on close and contingencies.

**Fixture 3 — Withheld order.** As fixture 2, and Reyes and Chen are close enough that
**net would decide** between them. Because net is suppressed for Chen, the **Reyes-vs-Chen
order is withheld** — they render bracketed: *"Can't be separated on your priorities until
buyer-broker comp is read for Chen."* Okafor still ranks (below the bracket). This is the
inverted-ranking guarantee in pixels.

**Fixture 4 — Tie / near-tie.** All fields read; Reyes and Chen land within the closeness
band on the weighted priorities. They render as a **near-tie band**: *"Reyes and Chen are
very close on your priorities."* Pairwise delta: *"Nearly even — Reyes leads on close,
Chen leads on net; it's close."* No manufactured decisive order.

**Fixture 5 — N = 1.** The reconciliation gate flagged Chen's emailed copy as a duplicate
of an uploaded Chen; the agent dropped one, and Okafor was excluded as a backup → only
Reyes remains. The comparison view **falls back to Reyes's single-offer summary** with
*"Only one offer is in this comparison"* — no ranking chrome, no weighting header.

**Fixture 6 — Forwarded seller share.** The seller forwards the comparison link to an
adult child. Under the **working assumption** (§8.3 — revocable + gated), the forward
either prompts recipient verification or honors the chosen posture; an over-shared link
the agent can **revoke**. What the recipient sees on the seller surface: **buyer names**
(Reyes/Chen/Okafor), the **"Ranked by…" basis line**, any **suppressed dimension
visible-but-excluded**, the **§5 guarantee in Principle voice**, **no scores, no
"accept."** This fixture exercises Q1–Q4 together and is the comparison-share spec's
acceptance case.

---

## 10. Assumptions (things this plan depends on that the docs don't settle)

- **The seller-priority dimension set is small and named.** IA §7 locks that the profile
  is listing-scoped and preset-seeded, but the **actual dimensions** (net, close speed,
  contingencies, financing strength, …) and their mapping to vocabulary fields are
  enumerated nowhere. The matrix columns *are* these dimensions. *The spec will likely
  propose a default set* grounded in the high-stakes vocabulary fields and
  `HIGH_STAKES_FIELD_KEYS` (not invented metrics), marked "to confirm" — see §15.
- **The main repo can support accountable ranking:** produce an order from a weighting,
  expose **which terms drove each position** (4a), and **suppress / withhold** when a
  field is unread (4c). Per doctrine §5's DEFER-LINE, the last is **not yet generalized** —
  a real dependency (§15).
- **Net to seller is computable from traceable components** (Fork I), suppressible when
  any component is unread. The formula/component list is a main-repo concern; the spec
  assumes net is *arithmetic of traceable values*, not a model output.
- **"Comparison-affecting field" = the active weighting's source fields ⊇
  `HIGH_STAKES_FIELD_KEYS`**, single-sourced from the main repo, not forked
  (high-stakes-fields-pointer governance).
- **`reconciliation-gate.md` will exist** (or its precondition is stubbed) — the
  comparison view depends on a curated set (§3).
- **The agent workspace is desktop-likely but not desktop-only for compare.** The
  compare-and-share moment clusters at the deadline (agent-workflow §2 — more deliberate,
  more desk-likely than verify). *Adjusted in v2.0 (review Minor 1):* the **weighting /
  Customize control must still work on mobile** — an agent may re-prioritize from a
  phone. See §12 phase 6.
- **Visual tokens are deferred** to brand adoption (assets/README; verify §7; share §7).
  The spec locks structure, hierarchy, and trust grammar — not color, type, or spacing.

---

## 11. Risks (and the scope-reduction lever for each)

- **The scoreboard trap.** A matrix reads as a scorecard; scores are forbidden (copy
  §2.2) and the order must not feel like a verdict (seller-workflow §5). *Lever:* no
  total column, no per-offer number, terms-in-cells, position-not-points — a permanent
  constraint, restated in §13.
- **The inverted-ranking guarantee isn't generalized in the backend** (doctrine §5
  DEFER-LINE). 4c depends on un-built runtime behavior. *Lever:* spec the *design* and
  name the dependency; if the backend can only *flag* (not *withhold*) at alpha, tier 3
  degrades from "withhold" to "flag as partial" — **doctrine-bound, escalate** (§14), not
  a silent edit.
- **Access-control under-resolution** *(strengthened in v2.0, review Operational Risk).*
  A leaked comparison link is the product's highest-confidentiality failure (multi-buyer
  exposure, handoff §7). *Lever:* the working assumption (§8.3 — not freely forwardable,
  revocable + gated) lets dependent specs proceed; the **comparison-share spec does not
  ship until Morris locks the mechanism** (§15). `comparison-view.md` is unaffected
  (authenticated).
- **Net-to-seller is a ranking-moving number** (Fork I) — the §5 danger zone. *Lever:*
  net suppresses (visible-but-excluded) whenever any component is unread; if even that is
  too risky for alpha, fall back to components-only (lose legibility, keep safety).
- **The dimension set is unspecified** (§10, §15). *Lever:* propose a fixed small default
  set, mark "to confirm," keep the matrix dimension-agnostic (renders whatever the profile
  defines).
- **Live re-ranking is heavy** (Fork E), especially on mobile. *Lever:* fall back to
  apply-then-reorder (keep the control visible; lose some "see what drives the order").
- **Three specs of scope** (workspace + share + gate). *Lever:* the §2/§3 splits are
  themselves risk control — write `comparison-view.md` first and fully; defer share and
  gate to their own specs.
- **The mobile matrix + mobile Customize.** The core legibility device and the weighting
  control are hardest where width is scarce. *Lever:* matrix → ranked cards + per-card
  breakdown + tap-for-why-above; Customize → full-screen / bottom-sheet editor with the
  basis line always visible (§12 phase 6). Severity reduced because compare is more
  desk-likely than verify.

---

## 12. Phases for writing the spec (dependency-ordered)

The template's section order is the *output* order; the *writing* order front-loads the
decisions everything hangs on (the sequence verify/share followed: surface forks, lock,
then mockup).

- **Phase 0 — Meta-scope (Forks A, B).** Two docs (§2); gate-as-sibling (§3).
- **Phase 1 — Organizing idea (template §0) + core layout (Forks C, D).** The matrix +
  ranked-spine hybrid, offers-as-rows. The return-to anchor.
- **Phase 2 — The data-state taxonomy (§5).** *New early task in v2.0:* fix how each
  field/offer state affects ranking and disclosure **before** the element and interaction
  detail, since the matrix cell and the suppression behavior are expressions of it.
- **Phase 3 — The three doctrine TODOs (4a, 4b, 4c) and their forks (E, F, G, I, J).**
  The screen's reason to exist; design before detail.
- **Phase 4 — Layout/regions (template §1) + core repeating unit (template §3).**
  Regions: weighting header, ranked matrix body, per-offer expansion/detail pane, order
  spine. Decompose the offer row / matrix cell: label · value-or-state · provenance
  handle · action, per surface, citing §5.
- **Phase 5 — State grammar on screen (template §2) + edge cases (§7).** Map §5's states
  + comparison states (asymmetric, N=1, tie/near-tie, suppressed/withheld) to distinct
  treatments.
- **Phase 6 — Interactions & gates (template §4) + mobile (template §5).** Live
  re-weight, expand offer, why-above delta, revise-set re-entry, set-provisional and
  offer-not-yet-verified markers, jump-back-to-verify. **Mobile Customize** *(new in
  v2.0):* the basis line is always visible (minimum collapsed state); Customize opens as
  a full-screen / bottom-sheet slider editor; live re-rank may fall back to apply-then on
  mobile. Matrix → ranked cards + per-card breakdown + tap-for-why-above; no hover; static
  export deferred (inherits handoff §3). Accessibility: order conveyable without color;
  screen-reader semantics for rank and for each absence state. Note the **compare → share**
  boundary inherits the per-offer high-stakes acknowledgment gate (states §3).
- **Phase 7 — Forks (template §6) + deferred (template §7) + DEC entries (§14).** Lock
  every fork as LOCKED (DEC-7 onward) or DEFER (reason + home).
- **Phase 8 — Follow-ons (not this spec), in order:** `comparison-share-surface.md`
  (briefed in §8), `reconciliation-gate.md`, the comparison **mockup**, and a comparison
  **worked-specimen** (worked-specimen §5 names it "the natural sequel"; the §9 fixtures
  seed it).

---

## 13. Testing criteria (spec-quality, not code)

A reviewer runs the finished spec against this checklist.

**Forks & TODOs**
- [ ] Every fork (A–K) is **LOCKED** (with a DEC entry) or **DEFER** (reason + home). No
      "we haven't decided" (template §6).
- [ ] All three doctrine TODOs closed (4a, 4b, 4c). **No `TODO(design)` for this screen
      survives.**

**Doctrine obligations have a named screen home**
- [ ] Clause 1 **inherited per offer** (provenance, honest uncertainty, term-based).
- [ ] **Legibility (§4.1):** "why is A above B?" has a concrete plain-terms UI answer.
- [ ] **Honest weighting (§4.2):** legible at rest *and* controllable; **weights shown,
      sub-scores never** — the §4b "what's visible instead" list is satisfied; no
      per-offer number, no total column.
- [ ] **Inverted-ranking (§5):** a specified state **withholds** an order rather than
      guesses; a suppressed dimension is **visible-but-excluded**, never disappeared,
      never defaulted. Trace one unreadable comparison-affecting field through the screen
      and confirm it **never moves the order**.

**Data-state grammar** *(new in v2.0)*
- [ ] All §5.1 field states render **distinctly** inside the dense matrix; the dangerous
      collapses hold (empty-on-form vs. unreadable; not-applicable vs. unreadable vs.
      empty; agent-corrected vs. present-confident).
- [ ] **Blank is never imputed or zeroed** (asymmetric completeness, Q5); "intentionally
      omitted" is never asserted (rule a).
- [ ] **Offer not-yet-verified** (§5.2) is flagged and never ranked as if vouched;
      distinct from set-provisional (Fork K).

**Fixture-based definition of done** *(new in v2.0 — review Testing)*
- [ ] The spec produces the correct screen for each §9 fixture: clean ranking,
      suppressed dimension, withheld order, tie/near-tie, N=1, forwarded seller share.

**The comparison share** *(new in v2.0)*
- [ ] The §8.1 inheritance table is honored: per-offer invariants inherited; divergences
      (organizing idea, weighting, suppression-to-seller, §5 guarantee, access) present.
- [ ] Ranking reaches the seller **as input, not verdict** (no "best offer," no "accept,"
      no score); the basis line is shown; suppression is visible to the seller.
- [ ] Access posture reflected in the workspace's share affordance; the mechanism is
      flagged for Morris (§15), not silently assumed.

**The two governing tests**
- [ ] **Doctrine §7:** more *trustworthy* (legible order, honest weighting, honest gaps),
      not just more *finished* — **non-laundering holds for the order** (nothing makes the
      ranking look more decided or cleaner than the reads support, handoff §6).
- [ ] **NORTH-STAR:** moves the agent toward a comparison they're **proud to share** by
      being trustworthy, not impressive.

**Cross-repo seams (CLAUDE.md)**
- [ ] `HIGH_STAKES_FIELD_KEYS` **cited, not forked**; "comparison-affecting field"
      single-sourced; the §5 generalization flagged as main-repo work; §1B/§1A and
      correction/audit-log dependencies noted; the net-to-seller formula referenced as a
      dependency, not redefined (altitude discipline, §6).

---

## 14. Rollback / revision plan

**Forks are separable so a wrong call is local.** Each fork → a DEC-n entry that "lives
in" a named spec section. Reversing a fork = a **new DEC-n′ superseding DEC-n** (both
left in place — `decisions.md` convention), a **status/version bump** on
`comparison-view.md`, and revision of only the citing sections. Separability (layout C/D
≠ legibility G ≠ suppression 4c ≠ net I) keeps one reversal from cascading.

**First DEC entries expected when the spec is drafted** *(added in v2.0 — review Minor 5 /
Suggested Change 7; numbers coordinate with any `decisions.md` backfill so they don't
collide):*

| DEC | Decision | Fork / §  |
|---|---|---|
| **DEC-7** | Comparison layout model — matrix + ranked spine, offers-as-rows | C, D |
| **DEC-8** | Weighting visibility — basis line + compact weights at rest; Customize expands; weights-shown/sub-scores-never | F, 4b |
| **DEC-9** | Suppression / inverted-ranking behavior — cell → position (visible-but-excluded) → withheld order | 4c |
| **DEC-10** | Net to seller — computed when all components traceable, else suppressed visible-but-excluded | I |
| **DEC-11** | Legibility affordance — matrix at rest + pairwise delta | G, 4a |
| **DEC-12** | Comparison-share access posture — *in the comparison-share spec, once Morris decides* | §8.3 |

**The mockup is the revision trigger.** Lock forks → mockup → if a fork fails, supersede
its DEC and revise; the mockup review uses §13 as its checklist.

**Severity tiers.** *Cosmetic* (Fork F): revise template §§2/4, supersede the DEC.
*Structural* (Fork C): revise §§1/2/3/5, **re-mockup** — the most expensive reversal,
which is why C/D are validated earliest and C is LOCK-pending-mockup. *Trust-grammar /
doctrine-bound* (4c can't be built generally; net I must stop computing): **not a free
screen-level choice** — reconcile with doctrine §5 (version-bump the doctrine or record a
deliberate divergence in `decisions.md`, CLAUDE.md cross-repo rule); the screen may render
a degraded guarantee only after the doctrine acknowledges it.

**Highest-risk forks to watch at mockup:** C/D (layout — most cascading; prototype the
matrix early), I (net — validate suppression on a real packet, fixture 2), 4c (suppression
/ withheld — depends on main-repo generalization), E (live re-rank — may scope-reduce to
apply-then, esp. mobile). On any lock/reversal, update **`STATUS.md`** and **`decisions.md`**.

---

## 15. Open questions that must be resolved before / alongside the spec

Separating what blocks **`comparison-view.md`** from what blocks the **sibling specs**:

**Hard blockers for `comparison-view.md` (the agent workspace): none.** With the working
assumptions and the proposed dimension set below, the spec can be written now. The items
below are confirmations and sibling-spec blockers.

1. **Comparison-share access-control mechanism** *(Morris — blocks the comparison-SHARE
   spec, not `comparison-view.md`).* Working assumption: not freely forwardable; revocable
   + gated (email-gated or expiring), per handoff §8. Morris picks the mechanism
   (email-gate / expiry / recipient-bind / PIN / approval). **Home:** handoff §8 →
   comparison-share DEC-12. The workspace proceeds with a placeholder share affordance.
2. **The default seller-priority dimension set** *(confirm — soft, not a hard block).* The
   spec **proposes** a small default set (net to seller, close speed, contingencies,
   financing strength) grounded in `domain-vocabulary.md` + `HIGH_STAKES_FIELD_KEYS`,
   marked "to confirm." Morris/IA confirms or amends. **Home:** IA §7 / spec Phase 1.
3. **The §5 generalization state in the main repo** *(cross-repo dependency, not a design
   decision).* 4c assumes the read-failure path degrades to *unknown* (suppress/withhold),
   not to a ranking-moving default, for comparison-affecting fields. Today only §3G(3) is
   confirmed (doctrine §5 DEFER-LINE). Confirm coverage before the mockup claims the
   guarantee generally; if absent, tier 3 degrades to "flag" (doctrine-bound, §14).
   **Home:** the cross-repo seam (CLAUDE.md) / main repo.
4. **Net-to-seller component formula** *(implementation dependency, not a blocker).* Which
   seller-paid costs feed net. The screen specifies behavior (net = arithmetic of
   traceable components; suppress if any unread); the formula is the main repo's. **Home:**
   `domain-vocabulary.md` / main repo.

---

## 16. Out of scope for this plan (named, with homes)

- **The spec prose, layout sketches, and DEC text** — Phase 1–7 output → home:
  `07-screen-design/comparison-view.md`.
- **The comparison share surface spec** — fully briefed in §8 → home:
  `07-screen-design/comparison-share-surface.md`.
- **The reconciliation gate spec** — dependency named in §3 → home:
  `07-screen-design/reconciliation-gate.md`.
- **The comparison mockup and worked-specimen** (the §9 fixtures seed the latter) → home:
  Phase 8.
- **Link access-control mechanism** → home: handoff §8 / Morris (§15).
- **The default dimension set's final membership** → home: IA §7 / spec Phase 1 (§15).
- **Visual design tokens** → home: brand adoption (assets/README).

---

## 17. Response to the v1.0 review (disposition) + changelog

### 17.1 Disposition of every review item

**Major concerns (blocking) — all incorporated.**

| # | Concern | Disposition | Where addressed |
|---|---|---|---|
| 1 | Access control under-resolved | **Accept** | §8.3 (options, risk, working assumption, home), §11 (strengthened risk), §15 #1 (Morris-flag). Correctly scoped: blocks the share sibling, **not** `comparison-view.md`. |
| 2 | Share surface seeded but under-planned | **Accept** | §8 rewritten as a full sibling brief with the §8.1 inheritance/divergence table. |
| 3 | Data-state distinctions need tightening | **Accept** (with one grounded partial-reject) | §5 taxonomy (field-level × ranking/disclosure; offer-level verification state). **Partial reject:** "intentionally omitted" is not a claimable state — asserting intent violates copy §4 / `DEFAULT-TRAP` (§5.1 rule a). |

**Minor concerns — disposition.**

| # | Concern | Disposition | Where |
|---|---|---|---|
| 1 | Mobile Customize missing | **Accept** | §10 (assumption adjusted), §12 phase 6 (mobile Customize + minimum collapsed state), §11. |
| 2 | Suppression needs examples | **Accept** | §9 fixtures 2–3; referenced from 4c. |
| 3 | Define what's visible instead of sub-scores | **Accept** | §4b "what is visible instead of a sub-score" (6-item list). |
| 4 | Net suppression display behavior | **Accept** | §4c + Fork I: **visible-but-excluded, never disappears**; generalized as a rule. |
| 5 | Which decisions become DEC entries | **Accept** | §14 "first DEC entries" table (DEC-7…DEC-12). |

**Suggested changes** map onto the above: 1→§8.3; 2→§8.1; 3→§5; 4→§12; 5→§9; 6→§6
altitude discipline + §13 cross-repo check; 7→§14. **All accepted.**

**Questions — resolution.**

| # | Question | Resolution |
|---|---|---|
| 1 | Can the share link be forwarded freely? | **Morris decision** (§8.3, §15 #1). Working assumption: no — revocable + gated. |
| 2 | Buyer identities / aliases? | **Resolved from docs** (§8.4): show buyer names (§1A) to the seller; confidentiality is an access-control concern, not a display one. |
| 3 | Suppressed dimension visible to seller? | **Resolved from docs** (§8.4): yes, visible-but-excluded (non-laundering, handoff §6; DEC-6). |
| 4 | Same weights as workspace, or simplify/hide? | **Resolved from docs** (§8.4): basis always shown; agent sets weights, cannot hide; display may simplify magnitudes. |
| 5 | Blank term vs. verified term across offers? | **Resolved from docs** (§5.1, §7): the blank is empty-on-form, not imputed/zeroed/penalized; aggregates suppress-or-caveat, never default. |

### 17.2 Changelog: v1.0 → v2.0

**Added**
- **§5 Data-state taxonomy** — field-level states mapped to ranking participation +
  disclosure, plus the offer-level not-yet-verified distinction. *(Major 3, Q5.)*
- **§9 Worked example fixtures** — six concrete scenarios doubling as DoD. *(Minor 2,
  Suggested Change 5, Testing.)*
- **§8.3 access-control subsection** and **§8.1 inheritance table** inside a rewritten,
  full comparison-share brief. *(Major 1, Major 2.)*
- **§15 Open-questions-for-Morris** — separating `comparison-view.md` blockers (none) from
  sibling-spec blockers (access control). *(Requirement 6.)*
- **§6 altitude-discipline note**; **§4b "what's visible instead of sub-scores" list**;
  **§14 "first DEC entries" table**; mobile-Customize requirements (§10, §12). *(Overengineering,
  Minor 1/3/5, Suggested Changes 6/7.)*
- **§17** itself (this disposition + changelog). *(Requirement 5.)*

**Modified**
- **§4c / Fork I** — suppressed dimensions/net are now explicitly **visible-but-excluded,
  never disappeared**. *(Minor 4, Q3.)*
- **§7 asymmetric completeness** — sharpened to the canonical no-impute/no-zero behavior
  and cross-linked to §5. *(Q5.)*
- **§8** — from an obligations list to a full sibling brief. *(Major 2.)*
- **§10 assumptions** — desktop-likely softened to desktop-likely-not-only; data-state and
  access-control assumptions added. *(Minor 1.)*
- **§11 risks** — access-control risk strengthened and correctly scoped. *(Operational
  Risk.)*
- Section numbering shifted to accommodate new §5, §8 expansion, §9, §15, §17.

**Removed**
- Nothing of substance. No v1.0 decision was reversed; every unchallenged section is
  retained (the organizing idea, the two-doc split, the gate-as-sibling decision, all
  fork resolutions, the doctrine-TODO resolutions, the §7/NORTH-STAR tests). This is a
  revision, not a rewrite. *(Requirement 4.)*

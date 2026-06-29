# Screen — The Share Surface

> **Status:** v0.1 — screen spec
> **Derives from:** `05-seller-workflow/seller-workflow.md` §3 (trust arc — the
> organizing idea), §0 (who the seller is), §4 (the journey), §5 (duties to a
> vulnerable reader), §6 (call prompt); `06-handoff/handoff.md` §2 (invariants) ·
> §3 (degradation matrix and the live-link column) · §4 (brand as messenger) · §6
> (non-laundering); `08-states-and-edge-cases.md` §1 (the six absence states) · §3
> (stakes-weighted gate — the agent's, upstream); `00-foundations/trust-doctrine.md`
> §3.1 (provenance reaches the seller) · §3.2 (honest uncertainty) · §3.3
> (term-based); `10-copy-guidelines/copy-guidelines.md` §1 (registers) · §2
> (three-way grammar) · §2.4 (free text verbatim).
> **Template:** `_templates/screen-spec-template.md`
> **Owns:** the seller-facing share surface — the public `/share/[token]` route.
> Visual layout, state rendering, and the provenance affordance for the seller zone.
> **Relationship to handoff.md:** this file specifies the *screen*; handoff §2–§6
> specifies the *seam*. They are the same moment, different levels. If they diverge,
> handoff.md governs the trust principle and this file's §6 forks govern the visual
> form it takes.

---

## 0. The one organizing idea: orient first

The seller opens this surface **overwhelmed** — a 17-page contract compressed into
one screen, arriving on their phone. Their trust arc (seller-workflow §3) is:

```
overwhelmed  ──►  oriented  ──►  understanding  ──►  confident to decide
```

The screen's entire job is to move the seller from the first state to the last, in
one sitting, without the seller having to log in, know the tool, or ask the agent
what anything means.

> **The one thing the seller must grasp on open: what this offer is.**

That is the organizing principle. Not provenance (that's the agent's arc). Not
scores (forbidden). Not urgency (explicitly prohibited — seller-workflow §5).

**What "orient first" means structurally:** the screen leads with the offer's
headline terms — price, close, cash or financed — before any detail. A seller who
has opened the link and read the first three lines should be able to say: "Okay, I
understand what they're offering." Every element below serves that moment, not the
agent's workflow. The verify workspace is built around *provenance made spatial* for
a checking agent; this screen is built around *the offer stated plainly* for a
decision-making seller.

Everything below serves this idea.

---

## 1. Layout — regions and hierarchy

Mobile-primary. This is not the verify workspace at a smaller size — it is a
different surface for a different person.

```
┌─────────────────────────────────────┐
│  BRAND FRAME                         │
│  [Agent name · Brokerage]            │
│  [Short agent-voiced framing line]   │
├─────────────────────────────────────┤
│  OFFER HEADLINE                      │
│  [Buyer name — §1A] · [Property]     │
│  [Purchase price] · [Close] ·        │
│  [Cash / Financed]                   │
├─────────────────────────────────────┤
│  THE OFFER                           │
│  ── Money                            │
│  ── Timing                           │
│  ── Contingencies                    │
│  ── Terms                            │
│  (each: label · value · §-cite)      │
│                                      │
│  Absence states visible, distinct    │
├─────────────────────────────────────┤
│  CALL PROMPT                         │
│  "Whenever you're ready, call me     │
│   to discuss — [tel: link]"          │
│  Agent-voiced (copy §1.4)            │
└─────────────────────────────────────┘
```

**Brand frame.** The agent's name, brokerage, and optional logo, followed by their
short framing line ("Here is my summary of [Buyer]'s offer on [Address]"). This copy
is **Docside-defaulted and agent-owned** (copy §1.4): Docside seeds a sensible
draft; the agent sees and can edit it before sending. The brand frames; it does not
author contract facts. A claim about the contract in the brand frame is a doctrine
violation (handoff §4 · copy §1.4 seam rule).

**Offer headline.** Three to five orientation terms — price, close date, cash or
financing type — the *one thing the seller must grasp on open*. Explanation voice
(copy §1.2). These are not a scored summary; they are the terms that let the seller
place the offer. They carry provenance handles (the §-citation, §6 fork 2) exactly
as the detail rows do. If any is unreadable, it renders as its absence state — a
missing purchase price is "We couldn't read this field" in the headline, never a
blank or a dash. See §2 and §6 fork 3.

**The offer.** The full extracted and verified reading, grouped for comprehension —
**Money, Timing, Contingencies, Terms** — not in raw form order. This mirrors the
grouping from the verify workspace (verify-workspace §1), because the same grouping
that helps an agent confirm a read helps a seller understand one. Glosses are
always-on here (see §3 and §6 fork 4) — the seller, unlike the agent, often doesn't
know what a loan contingency is.

**Call prompt.** The agent-voiced sign-off — "Whenever you're ready, call me to
discuss — (310) 555-1212" — rendered as a `tel:` link (seller-workflow §6 locked
decision). It is the last element, not an interstitial. It models the no-pressure
duty to a vulnerable reader: "whenever you're ready" is the copy enacting §5.

**Hierarchy principle.** The screen tells the seller what to read in an explicit
order: brand (who sent this) → headline (what is being offered) → detail (the full
terms) → action (talk to the agent). The hierarchy derives from the trust arc: orient
before understand, understand before act. No element competes with the headline at
the moment of open.

---

## 2. The state grammar, on screen

All six absence states from states §1 must render **visibly
distinct** on this surface. The cardinal rule holds at the seller's pixel level: no
two may look alike. The seller has no correction affordance and no verify step; they
read what they see. A collapsed distinction here is a permanent lie.

| State | On-screen treatment |
|---|---|
| Present — confident | the value, Explanation voice; §-citation inline (§6 fork 2) |
| Present — agent-corrected | the value + a quiet "corrected by agent · original: [X]" System-voice label below it — visible, not hidden; the correction is a trust signal (doctrine §3.1 v0.5) |
| Empty-on-form | "Not specified on this form." System voice; visually unlike a value and unlike an error — lighter weight, no alarm |
| Not-captured | "Not captured on this form." System voice; visually distinct from empty-on-form — the phrasing difference carries the semantic difference |
| Not-applicable | "Not applicable — [reason]." System voice; tied to its cause ("all-cash purchase") |
| Unreadable | "We couldn't read this field." System voice; clearly our limitation, not the deal's; for high-stakes fields, rendered with elevated visual weight (§6 fork 3) |

**The dangerous collapses on this surface** (states §1):
- *unreadable* vs *empty-on-form* — "we failed" vs "the buyer didn't specify." They
  must be visually apart. A seller who sees a blank purchase price must know whether
  the field wasn't filled in (a deal question) or we couldn't read it (a tool
  question).
- *agent-corrected* vs *present-confident* — the seller must be able to tell a
  corrected value from an extracted one. The correction marker is not a blemish; it
  is provenance class 2 (doctrine §3.1 v0.5). Hiding it would violate non-laundering
  (handoff §6).

**Low-confidence is not a state on this surface.** By the time a summary reaches
the seller, every field is binary: a trusted value or an honest absence (states
§1.1). The verify step resolved it. This is not a surface that hedges.

**Free-text fields.** Rendered verbatim, in quotation marks, attributed as the
buyer's words — not normalized, not paraphrased, never a number lifted from the
prose (doctrine §3.2 v0.3 · copy §2.4). The quotes are the trust signal: they mark
the text as *passed through*, not verified. The §-citation still applies (provenance
is traceable; the form section is still identifiable).

---

## 3. Information design of a field row

The repeating unit. The seller reads dozens of these; the design must carry the
trust grammar at the smallest scale.

Left-to-right (mobile: top-to-bottom):

- **Label** — System voice; the vocabulary `label` verbatim (e.g., "Earnest money
  deposit"). Consistent, scannable, never a paraphrase.
- **Value or state** — the §2 treatment for this field's state. Explanation voice
  for confident values; System voice for all absence states.
- **Gloss** — always on. Seller-workflow §3: "glosses earn their existence here."
  The seller often doesn't know what a loan contingency is; the gloss turns a term
  of art into understanding. The agent rarely needs them on the verify workspace;
  here they default visible. One sentence, Explanation voice, may name the
  trade-off honestly (copy §1.2 example).
- **Provenance handle** — the §-citation (§6 fork 2, locked). On this surface it
  appears as an inline label: "from §3A" or "§3G(3)" — always visible, not hidden
  behind a tap. The seller who wants to verify opens the contract and finds the
  section. The seller who doesn't is not burdened with interactive chrome.

**No action.** The seller cannot correct, confirm, or mark unreadable. These are
the agent's affordances, already exercised upstream. The seller's affordance set is:
read, trace (via §-citation), call the agent.

**Corrected-value row.** A corrected field adds a second line below the value:
"Corrected by agent · original read: [X]" — System voice, quiet weight, always
present. The correction is information, not a blemish. The seller can see the
original extraction and know the agent vouched for the current value. This is
provenance carried to its logical end.

---

## 4. Interactions & gates

This surface is **read-only**. The seller cannot edit, correct, confirm, or
acknowledge anything. That is a design decision, not an omission.

The only interactions:

- **Tap a §-citation handle** — opens (or scrolls to) the relevant section of the
  contract, if the surface is a live link. On a static PDF, the §-citation is the
  affordance; tapping does nothing, because it is already printed.
- **Tap a gloss** — no tap needed; glosses are always visible. (§6 fork 4.)
- **Tap the `tel:` call prompt** — initiates a phone call. Native OS action; no
  Docside logic.

**Gates that already fired upstream:** the high-stakes acknowledgment gate (states
§3) was the **agent's** at verify/share time. By the time this surface is live, the
agent has already acknowledged any high-stakes unknown. The seller sees the honest
display of that unknown (§2, unreadable treatment); they do not re-acknowledge it.
The gate is not on this surface; it was upstream.

**What the seller cannot do:** accept the offer, acknowledge terms, add comments,
share the link onward within the product, or indicate a decision. These actions are
outside Docside's scope for the seller (seller-workflow §4 · §5 "inform, never
advise").

---

## 5. Mobile / degraded environment

The share surface is mobile-primary by assumption — the seller opens a text or email
link on their phone (seller-workflow §0). Desktop is a real secondary case; it
degrades upward (more space, same hierarchy).

**Mobile (primary).**
Single-column layout as specified in §1. Brand frame → headline → grouped offer →
call prompt. No two-pane; the seller is not a checker. Tap targets sized for thumb
use. No hover anywhere — provenance is inline (§-citation always visible). Glosses
always on — no tap needed. The call prompt is a native `tel:` link, large enough for
a confident tap.

**No hover.** The verify workspace's provenance affordance relies on focus and the
document pane responding. That mechanism doesn't exist here. The §-citation printed
inline (§6 fork 2) is the replacement: it doesn't require interaction, it is always
present, it survives the transition to static. No element on this surface should
rely on hover to carry meaning; hover may enhance (tooltip with the full citation
text) but must not be the only form.

**Static PDF export.** The live link is the current form (DEC-1). The PDF is deferred
(handoff §3 · §9). This section states what the static equivalents *would be* when
that form ships, following the degradation matrix (handoff §3, static PDF column):

| Invariant | Live link (this surface) | Static PDF (deferred) |
|---|---|---|
| Provenance | §-citation inline, always visible; tap to view source | §-citation printed inline + source appendix |
| Corrections | "corrected by agent · original: X" below each corrected field | same, printed |
| Uncertainty | six absence states, visually distinct, always visible | same, printed; never collapsed to a dash |
| Term-based | terms + glosses always on | terms + glosses printed inline or footnoted |

The live link already satisfies every invariant without requiring the seller to do
anything. The PDF form must satisfy the same table before it ships; this surface
spec is its model.

**Accessibility baseline.** The seller population skews older than the agent
population and is more likely to include screen-reader users (seller-workflow §7
deferred accessibility pass). Minimum for this spec:
- Semantic HTML: headings for each section group, `<dl>` or equivalent for label/
  value pairs.
- Color is never the only signal for an absence state — the phrasing carries the
  meaning; color reinforces.
- The call prompt `tel:` link is keyboard-navigable and screen-reader-labeled.
- A dedicated accessibility pass is deferred to screen design and is more important
  here than anywhere else in the product (seller-workflow §7).

---

## 6. Design forks (locked)

All five confirmed and locked. Recorded in `11-design-decisions/decisions.md`
(DEC-2 through DEC-6).

### Fork 1 — Organizing idea: what is the one thing the seller must grasp on open?

**Question.** The seller's trust arc is *overwhelmed → oriented → understanding →
confident.* The screen must move them from the first to the second in the first
screenful. What anchors that moment?

**Options.**
- A: The offer's headline terms in plain Explanation voice (price, close, cash/
  financed) — the deal stated as a fact, immediately.
- B: The agent's framing copy — a personal introduction before the terms.

**Locked: A, with B above it.** The brand frame (B) comes first but is brief — it
establishes who sent this and provides the agent's framing sentence. Immediately
below, without a visible break in attention, the offer headline (A) states the
terms. The headline is what orients; the brand frame is what establishes trust in
the source. Neither replaces the other. The headline is the larger, more prominent
element — "orient first" means the terms, not a personal introduction.

**Rationale.** The seller's first question on opening is "what are they offering?" —
not "who built this tool." The agent's brand frame establishes context; the offer
headline answers the question. Seller-workflow §3's arc starts with *overwhelmed*;
the antidote is clarity about what is being offered, not warmth.

**→ Recorded as DEC-2.**

---

### Fork 2 — Provenance without hover: what is the static form of the provenance handle?

**Question.** Provenance must reach the seller (doctrine §3.1 v0.2) without hover.
The verify workspace achieves it via a two-pane spatial link. This surface can't do
that. The degradation matrix (handoff §3, live-link column) specifies the end state;
this fork locks the visual form.

**Options.**
- A: §-citation inline and always visible ("from §3A"), no tap required — provenance
  is present without interaction.
- B: §-citation behind a tap-to-reveal — provenance available on demand.
- C: No §-citation on screen; a "view source" link at the bottom goes to the full
  contract.

**Locked: A.** The inline §-citation is always visible — a small, quiet System-voice
label attached to each field row. The seller who wants to trace a value sees exactly
which section of the contract to look at, without a tap. The seller who doesn't need
it is not burdened — the citation is small and subordinate to the value.

**Rationale.** Option B makes provenance conditional on the seller knowing to look
for it — a seller who doesn't tap never gets provenance, which means doctrine §3.1
v0.2 is only formally satisfied. Option C buries provenance in a secondary action;
a seller who doesn't find it experiences the same trust gap. Always-visible inline
citation is the form that actually carries the guarantee to every seller, without
requiring them to know what they're looking for. It also maps directly to the static
PDF equivalent (printed inline), which makes the degradation path clean.

**→ Recorded as DEC-3.**

---

### Fork 3 — High-stakes unknowns on the seller surface: how are they rendered?

**Question.** The seller surface is read-only; the seller does not acknowledge
anything. The acknowledgment *gate* is the **agent's**, upstream at verify/share
time (states §3). So how is a high-stakes unknown (e.g., unreadable purchase price)
**rendered to the seller** — so it is unmissable and unmistakable, but not an
interaction?

**Options.**
- A: Same visual treatment as low-stakes unknowns — all unreadable fields render
  identically, via their absence state copy.
- B: Elevated visual weight for high-stakes unreadable fields — same absence-state
  copy ("We couldn't read this field."), but rendered at a prominence that reflects
  the stakes: larger, higher-contrast, or higher in the hierarchy.
- C: A banner or callout at the top of the surface: "Note: the purchase price could
  not be read from this document."

**Locked: B, with C as a composable addition for the offer headline region.**
High-stakes fields that are unreadable render with elevated visual weight in their
row (option B). When the unreadable field is one that belongs in the offer headline
(purchase price, close date, financing type), the headline renders the absence state
in the headline position, with headline prominence — the absence is as prominent as
a confident value would have been.

Option C (a banner) is a composable addition *only* when a high-stakes field is
absent from the headline region — it makes the gap unmissable for a seller who
starts reading the detail before the headline. It is not a replacement for rendering
the absence in context.

**Rationale.** The seller cannot check, cannot acknowledge, and cannot ask the tool
for clarification. The screen's only instrument is presentation. A high-stakes gap
that blends into the background fails doctrine §3.2 — honest uncertainty must be
surfaced, not present in the data but invisible in the UI. States §1.1 established
that no caveated number reaches the seller; this fork establishes that an honest
absence reaches them with proportionate prominence. Non-laundering (handoff §6)
prohibits cleaning up; this fork makes honest gaps unmissable rather than quietly
present.

**→ Recorded as DEC-4.**

---

### Fork 4 — Glosses: always-on or on-demand?

**Question.** On the verify workspace, glosses are on-demand — the agent rarely
needs them (verify-workspace §3). The seller often does. What is the default on this
surface?

**Options.**
- A: Always-on — every field row shows its gloss inline, below the value.
- B: On-demand — a tap reveals the gloss; hidden by default.
- C: Hybrid — headline fields always show their gloss; detail fields reveal on tap.

**Locked: A (always-on).** Glosses are always visible on the seller surface.

**Rationale.** Seller-workflow §3: "glosses earn their existence here." The seller
is the reader for whom the gloss was built — they often don't know what a loan
contingency is, and a gloss that's hidden behind a tap helps only the seller who
already suspects they need it. The verify workspace hides glosses because agents
don't need them and the screen is dense; this surface is not agent-dense, it is
seller-readable. Showing the gloss is the mission functioning at its most literal:
"understand a real estate contract." Hiding it requires an explanation. It also
matches the always-on provenance (fork 2) — the seller surface makes the trust layer
visible, not hidden.

**→ Recorded as DEC-5.**

---

### Fork 5 — Non-laundering enforcement: what prevents the surface from looking "cleaner" than the truth?

**Question.** The non-laundering principle (handoff §6) holds that the handoff never
strengthens a claim by dropping a caveat. Concretely: what stops the surface design
from treating gaps, correction markers, and absence states as clutter to minimize?

**Options.**
- A: A naming rule in the spec — "the surface may not introduce any treatment that
  makes the summary look more finished than the verified read" — enforced at design
  review.
- B: A specific prohibition list — no "Summary complete," no collapsible absence
  rows, no de-emphasis of correction markers, no greying-out of unreadable fields to
  the point of invisibility.
- C: Both: the naming rule as the principle; the prohibition list as the checklist.

**Locked: C (both).** The naming rule is the principle; the prohibition list is the
practical test.

**Prohibition list (the non-laundering check for this surface):**
- No "Summary complete" or "All fields verified" language — honesty about what was
  and wasn't readable is the product's job.
- No collapsible absence rows — a seller shouldn't need to expand a row to discover
  that a field was unreadable.
- No de-emphasis of correction markers — "corrected by agent · original: X" must
  render at a weight the seller will see, not in 10px grey that disappears at a
  glance.
- No visual treatment that makes an unreadable or empty field blend with surrounding
  confident values. Absence states use their §2 treatments; they do not inherit the
  confident-value style.
- No promotional copy — no "Great news: this offer has no contingencies!" Nothing
  that editorializes the deal (seller-workflow §5 · copy §1.1 no-marketing rule).

**Rationale.** Non-laundering is the defining discipline of the handoff seam
(handoff §6). Without a named check, design iteration naturally drifts toward
polish: gaps get soft-pedaled, corrections get hidden to look cleaner, absence states
get greyed out to avoid visual noise. Each small polish step is a doctrine violation.
The prohibition list makes the pattern explicit so "making it look nicer" is
identifiable rather than gradual.

**→ Recorded as DEC-6.**

---

## 7. Deferred

- **Comparison surface.** The share surface for N > 1 offers. This spec covers the
  single-offer case. The comparison share inherits these invariants and adds the
  ranking-trust surface (doctrine §4–§5) — stronger access control (handoff §7–§8),
  visible weighting, and per-offer term explanation. Its own spec follows.
- **Static PDF export.** §5's table is the model; the full spec waits on the
  static-provenance work (handoff §9 deferred · DEC-1 consequences).
- **Seller-side accessibility pass.** Named in §5 as the highest-priority
  accessibility work in the product. A dedicated pass belongs with screen design.
  More important here than anywhere else in the product (seller-workflow §7).
- **Multi-viewer / co-owner experience.** A shared reference for a family
  conversation (seller-workflow §0 · §7 deferred). The alpha serves a single reader;
  structured co-viewing is post-alpha.
- **Link access-control model.** Revocable links, comparison-link expiry or
  email-gating (handoff §8 · DEC-1 raised concern). This spec doesn't design the
  access model; it is an open decision in handoff §8.
- **Evolving-comparison freshness.** When the agent re-shares after a new offer
  arrives, the seller's view updates (handoff §5). The experience of *receiving* that
  update is not scoped here.
- **Visual design tokens.** Typography, color, spacing — the brand adoption defer
  (assets/README, verify-workspace §7) holds here too. This spec locks structure and
  hierarchy; the visual design layer follows brand adoption.

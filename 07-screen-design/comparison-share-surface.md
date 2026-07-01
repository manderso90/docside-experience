# Screen — The Comparison Share Surface

> **Status:** v0.1 — screen spec
> **Derives from:** `07-screen-design/share-surface.md` (the single-offer template this
> inherits — per-offer atom, six absence states, read-only, `tel:` prompt, DEC-6
> prohibition list); `07-screen-design/comparison-view.md` **Appendix B** (the sibling
> brief, B.1–B.5) · §2.3–§2.4 (order-integrity treatments) · §4 (share-initiation, DEC-7);
> `05-seller-workflow/seller-workflow.md` §4 (the journey — fit-to-priorities) · §5
> (duties to a vulnerable reader — inform never advise, the decision is never the
> algorithm's) · §6 (call prompt); `08-states-and-edge-cases/states-and-edge-cases.md`
> §1 (the six absence states) · §3 (stakes-weighted gate — the agent's, upstream) · §4.1
> (buyer-name fallback handle); `06-handoff/handoff.md` §5 (freshness) · §6
> (non-laundering) · §8 (access
> control — DEC-7) · §9 (static PDF deferral); `00-foundations/trust-doctrine.md` §4.2
> (honest weighting) · §5 (the inverted-ranking guarantee);
> `10-copy-guidelines/copy-guidelines.md` §1 (registers) · §2.2 (no score narration).
> **Template:** `_templates/screen-spec-template.md` — mirrors `share-surface.md` §0–§7.
> **Owns:** the seller-facing comparison share — the public, **email-gated**
> `/share/[token]` route for N > 1 offers. Visual layout, the two-layer state grammar,
> the ranked set with its basis line, per-offer term explanation, and the four
> recipient-access surface states.
> **Relationship to comparison-view.md:** that file specifies the *workspace* and owns
> share-*initiation* (§4 · the share-readiness matrix §4.1); this file specifies the
> *seller's screen*. Appendix B briefs this spec. Where they diverge, Appendix B and
> `share-surface.md` are the parents this file reconciles against; the recipient
> verification, expiry, and revocation *mechanics* are the main repo's (§4, cross-repo seam).

---

## 0. The one organizing idea: fit-to-priorities, an input not a verdict

The seller opens this surface **overwhelmed** — now not one contract but several, each a
17-page document, all arriving at once, on their phone. The single-offer share answered
*"what is this offer?"* (share-surface §0). The comparison share answers a harder
question: *"how do these offers fit my priorities — and the fit is an **input** to my
decision, never the decision."* The seller's trust arc (seller-workflow §4) extends by one
job:

```
overwhelmed  ──►  oriented  ──►  understanding  ──►  confident to decide
                                     (+ grasp the order and why, free to overrule it)
```

The screen's job is to move the seller across that arc in one sitting — and to hand them a
legible order **they can set aside.** The ranking reaches the seller as *fit-to-priorities,
never as a verdict*: the order plus its visible basis, with the surface **visibly leaving
room for what it can't see** — a buyer's letter, keeping the house in reach of a family
they like, gut feel (seller-workflow §4). This is the section's thesis:

> **The seller must grasp the order and its basis — never be handed a winner.** No "best
> offer," no "accept," no score. The decision is never the algorithm's (seller-workflow §5).

This is a stronger obligation than the single-offer surface, which had no order to caveat.
Where the single-offer surface leads with one offer's headline terms, this surface leads
with the **ranked set and its "Ranked by…" basis line** — the order stated as an input, its
reasons co-present, its blind spots admitted. In one line: **N single-offer share surfaces,
ranked, with the basis shown and access tightened.**

**The inherit-vs-diverge spine (Appendix B.1).** The backbone of this doc: what the
comparison share inherits from the single-offer surface, and where it diverges.

| Element / invariant | Single-offer share (`share-surface.md`) | Comparison share (this spec) |
|---|---|---|
| Organizing idea | "orient first" — what this offer is | **DIVERGES** → "fit-to-priorities, an input not a verdict" (seller-workflow §4–§5) — §0 |
| Per-offer atom (provenance, six absence states distinct, term-based, corrections-as-corrected, glosses always-on, §-citation inline — DEC-3/4/5) | yes, for one offer | **INHERITS, per offer** — the comparison is N atoms — §2 Layer 1, §3 |
| Top-of-screen | the one offer's headline terms | **DIVERGES** → the ordered set + the **"Ranked by…" basis line** — §1, §3 |
| Weighting display | n/a (no order) | **NEW** → basis line always visible; magnitudes may simplify, the basis never hidden (doctrine §4.2; DEC-10; Appendix B.4) — §3 |
| Suppressed dimension | n/a | **NEW** → shown **visible-but-excluded** to the seller — §2 Layer 2 |
| Withheld order | n/a | **NEW** → a decisive-but-unread pair rendered as a bracketed group, never flattened — §2 Layer 2 |
| Doctrine §5 guarantee, Principle voice | absent (single offer) | **NEW** → "If we cannot trace how a ranking was determined, we will not present it" — §2 Layer 2 |
| Buyer identity | one buyer (§1A) | **shows each buyer name (§1A)**; unreadable → fallback handle (states §4.1 · IA §2.1) — §1, §3 |
| Read-only; no acknowledgment; `tel:` prompt; DEC-6 prohibition list | yes | **INHERITS**; the prohibition list **extends to the order** — §4 |
| Access control | lightweight link acceptable for alpha (handoff §8) | **DIVERGES** → email-gated, expiring, agent-revocable (DEC-7); a forward doesn't carry access — §4 |

Everything below serves this idea.

---

## 1. Layout — regions and hierarchy

Mobile-primary, single column. This is not the comparison *workspace* at a smaller size —
it is a different surface for a different person. The workspace is a matrix built for a
checking agent who re-weights; this surface is a **ranked reading** built for a
decision-making seller who cannot log in, does not know the tool, and will not customize.

```
┌─────────────────────────────────────┐
│  BRAND FRAME                         │
│  [Agent name · Brokerage]            │
│  [Short agent-voiced framing line]   │
├─────────────────────────────────────┤
│  THE RANKED SET                      │
│  ── "Ranked by: [priorities, in      │
│      order]" — basis line, always    │
│      visible                         │
│  ── the order (1..N), as an input    │
│      not a verdict — no score,       │
│      no "best"                       │
├─────────────────────────────────────┤
│  PER-OFFER GROUPS (N)                │
│  ┌───────────────────────────────┐   │
│  │ [Buyer name — §1A / fallback] │   │
│  │  ── Money                     │   │
│  │  ── Timing                    │   │
│  │  ── Contingencies             │   │
│  │  ── Terms                     │   │
│  │  (each: label · value · gloss │   │
│  │   · §-cite)                   │   │
│  └───────────────────────────────┘   │
│  … one atom per offer, in rank order │
│                                      │
│  Absence states + suppressed/        │
│  withheld treatments visible,        │
│  distinct                            │
├─────────────────────────────────────┤
│  CALL PROMPT                         │
│  "Whenever you're ready, call me     │
│   to discuss — [tel: link]"          │
│  Agent-voiced (copy §1.4)            │
└─────────────────────────────────────┘
```

**Brand frame.** The agent's name, brokerage, optional logo, and their short framing line
("Here is my summary of the offers on [Address]"). **Docside-defaulted and agent-owned**
(copy §1.4): Docside seeds a draft; the agent edits before sending. The brand *frames*; it
asserts **no contract fact and no claim about the order** — a claim about the deal or the
ranking in the brand frame is a doctrine violation (handoff §6 · copy §1.4 seam rule).

**The ranked set.** The top of the screen — replacing the single offer's headline. It
carries two things, in this order: the **"Ranked by…" basis line** (the seller's priorities,
in order — see §3) and the **order itself** (1..N). The order is presented as an input the
seller weighs, not a result they accept: no per-offer score, no total, no "best offer"
badge (copy §2.2 · §4 prohibition list). When an order cannot be traced it is not shown as
an order — it degrades to the Layer-2 treatments (§2).

**Per-offer groups.** N single-offer atoms, one per offer, in rank order. Each atom is the
inherited Clause-1 unit (share-surface §3), grouped for comprehension — **Money · Timing ·
Contingencies · Terms** — not in raw form order. Glosses are always-on (DEC-5). Each group
is **headed by its buyer's name (§1A)**; the seller owns these offers on their own property
and real-world offer presentation names buyers (Appendix B.4).

**Buyer name and its fallback.** When §1A is unreadable, the group heads with a **fallback
handle** — "Emailed offer, received Tue 2 PM" — shown as *buyer name unreadable*, never
blank, never a guessed or fabricated name (states §4.1 · IA §2.1). A high-stakes unreadable
field that belongs in a headline region (a purchase price, a close date) renders its absence
state at **headline prominence**, with an optional banner callout when the gap sits outside
the region a scanning seller reads first (DEC-4).

**Call prompt.** The agent-voiced sign-off — "Whenever you're ready, call me to discuss —
(310) 555-1212" — rendered as a `tel:` link (seller-workflow §6). Last element, never an
interstitial. "Whenever you're ready" is the copy enacting the no-pressure duty
(seller-workflow §5).

**Hierarchy principle.** The screen tells the seller what to read, in order: brand (who sent
this) → the order + its basis (how these fit your priorities) → each offer's terms → call
(talk to the agent). Orient before understand, understand before act, grasp the order before
overruling it. No element competes with the ranked set at the moment of open, and the ranked
set never competes with the seller's own judgment.

---

## 2. The state grammar, on screen — two layers, kept separate

This surface carries **two distinct taxonomies**, and the spec keeps them apart so the
multi-offer view does not corrupt the inherited field-state set.

- **Layer 1 — the six per-field states.** Inherited verbatim from share-surface §2 /
  states §1. They describe **one cell**: a single field of a single offer.
- **Layer 2 — two order-integrity treatments.** New with the comparison. They describe the
  **ranking**, not a field. They are *not* field-row states and must never be described as
  one.

### 2.1 Layer 1 — the six per-field states (inherited, per offer)

Each **visibly distinct** — the cardinal rule holds at the seller's pixel level: no two may
look alike. System voice for every absence; §-citation inline, always on.

| State | On-screen treatment |
|---|---|
| Present — confident | the value, Explanation voice; §-citation inline (§3) |
| Present — agent-corrected | the value + a quiet "corrected by agent · original: [X]" System-voice label below it — visible, not hidden; the correction is a trust signal (doctrine §3.1) |
| Empty-on-form | "Not specified on this form." System voice; lighter weight, no alarm — unlike a value, unlike an error |
| Not-captured | "Not captured on this form." System voice; visually distinct from empty-on-form — the phrasing carries the semantic difference |
| Not-applicable | "Not applicable — [reason]." System voice; tied to its cause ("all-cash purchase") |
| Unreadable | "We couldn't read this field." System voice; clearly our limitation, not the deal's; high-stakes fields get elevated weight (DEC-4) |

**Free-text fields** render verbatim, in quotation marks, attributed as the buyer's words —
never normalized, never a number lifted from the prose (doctrine §3.2 · copy §2.4). The
§-citation still applies.

### 2.2 Layer 2 — two order-integrity treatments (operate on the ranking, not a field)

These render the inverted-ranking guarantee (doctrine §5) as the seller meets it. They are
the seller-facing face of the workspace's three-tier suppression (comparison-view §2.4 ·
DEC-11). The guarantee itself is stated in Principle voice — the one promise the ranking
makes to the seller:

> **If we cannot trace how a ranking was determined, we will not present it** (doctrine §5).

The two treatments below are how that promise is kept when a field can't be read.

| Treatment | Trigger | On-screen treatment |
|---|---|---|
| **Suppressed dimension** (visible-but-excluded) | a ranking-feeding field is unreadable for one offer | "We couldn't read [field] for [buyer], so this offer isn't ranked on [dimension]." The dimension is **shown, never dropped** — a disappeared dimension hides the gap, a non-laundering violation (handoff §6 · DEC-6). Links back to that offer's provenance. |
| **Withheld order** (bracketed pair) | a suppressed dimension would be decisive between two offers | the two offers render as a **bracketed group** with the reason: "Can't be separated on your priorities until [field] is read for [buyer]." Never flattened into a confident rank; the runtime withholds rather than guesses (DEC-11). |

**The dangerous collapses — spanning both layers.** Each pair below must stay visibly apart;
collapsing any one is a doctrine failure, not a polish choice.

- *unreadable* vs *empty-on-form* (Layer 1) — "we failed" vs "the buyer didn't specify." A
  seller who sees a blank purchase price must know which.
- *agent-corrected* vs *present-confident* (Layer 1) — the correction marker is provenance,
  not a blemish; hiding it violates non-laundering (handoff §6).
- *suppressed dimension* vs *not-applicable field* (Layer 2 vs Layer 1) — "we couldn't rank
  this offer on close speed" is **not** "close speed doesn't apply." One is our gap; the
  other is the deal's shape.
- *withheld order* vs *near-tie* (Layer 2) — "we won't separate these until a field is read"
  is **not** "these are close on your priorities." A withhold is an admission of missing
  data; a near-tie is a finding. Neither is manufactured from the other.
- A suppressed dimension is **never silently removed.** Hiding the gap to look cleaner is a
  non-laundering violation (handoff §6) and a DEC-6 prohibition.

---

## 3. Information design of a field row — plus two new elements

The repeating unit is the **per-offer field row**, inherited whole from share-surface §3.
The comparison adds two elements above it: the **buyer-name slot** and the **basis line**.

**The inherited field row.** Left-to-right (mobile: top-to-bottom):

- **Label** — System voice; the vocabulary `label` verbatim ("Earnest money deposit").
  Consistent, scannable, never a paraphrase.
- **Value or state** — the §2.1 treatment for this field's state. Explanation voice for
  confident values; System voice for every absence.
- **Gloss** — **always on** (DEC-5). One sentence, Explanation voice; the seller often
  doesn't know what a loan contingency is, and the gloss turns a term of art into
  understanding. May name a trade-off honestly.
- **Provenance handle** — the §-citation, **always visible**, inline (DEC-3): "from §3A",
  "§3G(3)". Not behind a tap. The seller who wants to trace opens the contract to that
  section; the seller who doesn't is not burdened with chrome.
- **Corrected-value row** — a corrected field carries a second line, "corrected by agent ·
  original: [X]", System voice, at **readable weight** — never 10px grey (DEC-6). The seller
  sees the original extraction and that the agent vouched for the current value.

**New element — the buyer-name slot.** Each per-offer group is headed by its buyer's name
(§1A), Explanation voice. Unreadable → the **fallback handle** ("Emailed offer, received Tue
2 PM"), shown *buyer name unreadable*, never blank, never fabricated (states §4.1 · IA
§2.1). Agent-controlled aliases ("Offer A / B / C") are a later option, not the default
(Appendix B.4 · §7).

**New element — the basis line.** A single always-visible line at the top of the ranked set:
**"Ranked by: [priorities, in order]"** — e.g., "Ranked by: net to seller, fewest
contingencies, financing strength, fastest close." System-voice label; the priorities named
in plain terms. The **basis is never hidden** (doctrine §4.2 · DEC-10 · Appendix B.4);
magnitudes *may* be simplified for the seller — the surface need not print precise weight
bars — but what produced the order is always legible. The basis line is the seller-facing
form of the workspace's weighting header; the seller does not re-weight here (§4).

**No per-offer score, ever.** No cell, header, or badge shows a sub-score, a total, or a
percentage. Rank is explained in terms — "higher price, faster close" — never in numbers
("scored 0.92 vs 0.78"). A sub-score may decide *which term to surface*; it must never
appear in the copy (copy §2.2).

---

## 4. Interactions & gates

This surface is **read-only**. The seller cannot edit, correct, confirm, acknowledge,
comment, decide, re-weight, or forward-in-product. That is a design decision, not an
omission (seller-workflow §5, "inform, never advise").

The only interactions:

- **Tap a §-citation handle** — opens (or scrolls to) the relevant contract section, if the
  surface is a live link. On a static PDF the §-citation is already printed; tapping does
  nothing (§5).
- **Tap the `tel:` call prompt** — initiates a phone call. Native OS action; no Docside
  logic.

Glosses need no tap (always on, DEC-5). There is **no "accept," no "customize," no "best
offer," no comment field** — the workspace's re-weighting and share-initiation controls
(comparison-view §4) do not exist on the seller's screen.

**Gates that already fired upstream.** The **high-stakes acknowledgment gate** (states §3,
which reuses `HIGH_STAKES_FIELD_KEYS`, not a forked list) was the **agent's**, at
verify/share time — one per offer, inherited by the compare→share boundary and *not*
eliminated by the comparison (comparison-view §4). By the time this surface is live, the
agent has acknowledged every high-stakes unknown; the seller sees the honest display (§2),
and does **not** re-acknowledge it. The gate is not on this surface.

**Access-control — the four recipient surface states (DEC-7).** The link is **email-gated,
expiring, and agent-revocable**. This spec specifies the seller-facing *states*, not the
mechanism: recipient verification, expiry handling, and revocation are the **main repo's**,
and the workspace owns share-*initiation* only (comparison-view §4 · Appendix B.3 — the
cross-repo seam). The four states a recipient can meet, each with an honest System-voice
message:

| State | What the recipient meets | System-voice message |
|---|---|---|
| **Allowed recipient** | a verified email on the share list | the comparison, in full |
| **Expired link** | the link's window has passed | "This shared comparison has expired. Ask [agent] to send a new link." — no terms shown |
| **Revoked link** | the agent revoked access | "This link is no longer active. Please contact [agent]." — no terms shown |
| **Forwarded / unrecognized recipient** | opened by someone not on the list | meets the **same email gate**; does **not** auto-enter. "This comparison was shared with a specific person. If it was meant for you, ask [agent] to add your email." |

A forward does not carry access (Appendix B.3): PIN was rejected (a PIN forwards as easily as
the link), and per-view approval was rejected as the default (too much friction for opening
cold on a phone).

**The non-laundering prohibition list (DEC-6), extended to the order.** This surface inherits
the five single-offer prohibitions and adds four for the ranking:

- *(inherited)* No "Summary complete" / "All fields verified" language.
- *(inherited)* No collapsible absence rows — no expanding to discover a field was unreadable.
- *(inherited)* No de-emphasis of correction markers.
- *(inherited)* No visual treatment that blends an unreadable or empty field with confident
  values.
- *(inherited)* No promotional copy — nothing that editorializes the deal.
- **No false decisive order** — a withheld pair is never flattened into a confident rank.
- **No hidden suppression** — a suppressed dimension is shown visible-but-excluded, never
  dropped.
- **No collapsed absence rows in the ranking** — the order never buries a gap to look
  cleaner.
- **No "best offer" label, no score, no total, no "accept"** — the order is an input, never a
  verdict (copy §2.2 · seller-workflow §5).

---

## 5. Mobile / degraded environment

Mobile-primary by assumption — the seller opens a text or email link on their phone
(seller-workflow §4). Desktop degrades upward (more space, same hierarchy).

**Mobile (primary).** Single column, in the §1 order: brand → **basis line** → **ranked
cards** (one per offer, in rank order, each an atom with its per-dimension terms) → call
prompt. No two-pane; the seller is not a checker. The **basis line is the floor — always
visible** at the minimum collapsed state; losing it on mobile would hide what produced the
order. Suppressed dimensions and withheld groups persist on the cards. Tap targets sized for
thumb use.

**No hover carries meaning.** Provenance is inline (§-citation always visible) and glosses
are always on — nothing on this surface relies on hover. Hover may enhance (a tooltip with
the full citation) but must never be the only form.

**Static PDF export (deferred).** The live link is the current form; the PDF awaits the
static-provenance hard column (DEC-3 · handoff §9). This section states what the static
equivalents *would be*, extending the single-offer degradation matrix with **two comparison
rows**:

| Invariant | Live link (this surface) | Static PDF (deferred) |
|---|---|---|
| Provenance | §-citation inline, always visible; tap to view source | §-citation printed inline + source appendix |
| Corrections | "corrected by agent · original: X" below each corrected field | same, printed |
| Uncertainty | six absence states, visually distinct, always visible | same, printed; never collapsed to a dash |
| Term-based | terms + glosses always on | terms + glosses printed inline or footnoted |
| Basis line | "Ranked by…" always visible; the order as an input | printed at the head of the ranked set; the order printed with its basis, never a bare list |
| **Suppressed dimension** | shown visible-but-excluded | **printed visible-but-excluded, never collapsed** — the gap is on the page |
| **Withheld order** | bracketed group + withhold reason | **the bracketed group printed in place** with its reason; no flattened rank, no "best" label |

**Accessibility baseline.** The seller population skews older than the agent population and is
more likely to include screen-reader users — this is the **highest-priority accessibility
pass in the product** (a full pass is deferred to screen design; the baseline is never
deferred):

- **Rank order is conveyed in the semantic order, not by color or any glyph** — a screen
  reader reads the offers in rank sequence.
- Every **absence state** and **the withhold** carries its meaning in **text**; color only
  reinforces (states §1).
- The `tel:` call prompt is keyboard-navigable and screen-reader-labeled.
- The withheld-group and suppressed-dimension copy is **read aloud**, never implied by layout
  alone.

---

## 6. Design forks (locked)

Locked as **records**, not new decisions. `decisions.md` runs through DEC-17, and Appendix
B.4 already resolves buyer identity, suppression visibility, and basis visibility; this doc
mints no new DEC. Each fork is in the `share-surface.md` form — Question · Options · Locked ·
Rationale — and its recording line **cites an existing decision**.

### Fork 1 — Access-control model: how does the comparison reach only its intended reader?

**Question.** The single-offer link could stay lightweight for the alpha (handoff §8). The
comparison exposes N offers and a ranking across them — more to protect (Appendix B.1 ·
handoff §7). What access model reaches the intended seller without letting a forward carry
access?

**Options.**
- A: Email-gated, expiring, agent-revocable — the recipient verifies against an email on the
  share list; a forward meets the same gate.
- B: A free-forwarding token link — anyone with the URL sees the comparison.
- C: A PIN, or per-view agent approval on every open.

**Locked: A.** Email-gated recipient access, with expiration and agent revocation; a
forwarded recipient does not auto-enter (§4, the four states).

**Rationale.** Option B lets a link reach outsiders — the exact confidentiality risk (handoff
§7). Option C's PIN forwards as easily as the link, and per-view approval is too much friction
for a seller opening cold on a phone (Appendix B.3). Email-gating carries the guarantee
without the friction. The verification / expiry / revocation *mechanics* are main-repo; this
surface owns only their honest states (§4, cross-repo seam).

**→ Recorded as DEC-7** (locked by Morris; not re-litigated here).

---

### Fork 2 — Ranking presentation: does the order reach the seller as a verdict or an input?

**Question.** The comparison view is the only screen carrying ranking-trust (doctrine §5).
When that order reaches the seller, is it a result they accept, or an input they weigh?

**Options.**
- A: An input — the order plus its visible basis, with room left for what the form can't see;
  no score, no "accept," no "best offer."
- B: A verdict — a highlighted winner, an "accept" action, a confidence score.

**Locked: A.** Fit-to-priorities, an input not a verdict. The order and the "Ranked by…"
basis are shown; the surface visibly leaves room for a buyer's letter and gut feel
(seller-workflow §4). No "best offer," no "accept," no score (copy §2.2).

**Rationale.** "Inform, never advise" — Docside shows what the offers *are* and how they fit
the stated priorities; it never tells the seller what they *should do*. "The decision is
never the algorithm's" (seller-workflow §5). A verdict would make a seller feel a score
decided for them — the precise harm the no-score discipline exists to prevent. This is the
surface's spine, resolved at seller-workflow §5 and Appendix B.2 — **cited, not a new DEC.**

**→ Recorded at seller-workflow §5 · Appendix B.2** (the surface's governing principle).

---

### Fork 3 — Weighting display to the seller: how much of the basis is shown?

**Question.** The workspace shows the agent full weights and a live re-rank (DEC-10). The
seller does not re-weight. How much of what produced the order does the seller see?

**Options.**
- A: The basis (ordered priorities) always shown in terms; precise magnitudes may be
  simplified; the basis never hidden.
- B: Full numeric weights and bar magnitudes, as in the workspace.
- C: No basis — just the order.

**Locked: A.** The "Ranked by…" basis line is always visible, in plain terms; display may omit
precise magnitudes, but the basis is never hidden (§3).

**Rationale.** Option C makes the order a black box — a doctrine §4.2 violation. Option B
imports workspace density the seller doesn't need and edges toward score-narration (copy
§2.2). The agent sets the weights — that *is* the seller's priority profile — but cannot hide
what produced the order (Appendix B.4). Basis-always-shown is the form that keeps the order
accountable without turning it into math. Resolved at DEC-10 and Appendix B.4 — **cited, not
a new DEC.**

**→ Recorded at DEC-10 · Appendix B.4.**

---

**Ranking mechanics inherited (no fork).** The order's construction is fixed upstream and
consumed here as-is — not re-decided on the seller surface: default seller-priority
dimensions and order (**DEC-8**); the three-tier suppression / withheld-order guarantee
(**DEC-11**, rendered in §2 Layer 2); net-to-seller computed only from traceable components,
else suppressed visible-but-excluded (**DEC-12**); the set-provisional marker — "Comparison of
[N] offers in so far" — when more offers may still arrive (**DEC-17**). Suppressed and
withheld reaching the seller is specified in §2 Layer 2, not a separate fork (Appendix B.4).

---

## 7. Deferred

Each with a reason and a named home (defer-line discipline).

- **Static PDF export.** §5's extended matrix is the model; the full spec awaits the
  static-provenance hard column (DEC-3 · handoff §9). → home: the future PDF-form spec.
- **Multi-viewer / co-owner tracking.** A shared reference for a family conversation — who
  opened it, co-owner access. The alpha serves a single verified reader; structured
  co-viewing is post-alpha. → home: this file / screen design.
- **Agent-controlled buyer aliases** ("Offer A / B / C" instead of names). The default is
  buyer names (Appendix B.4); an alias mode is a plausible later request, not the default. →
  home: this file.
- **Seller-side accessibility pass.** Named in §5 as the highest-priority accessibility work
  in the product. A dedicated pass belongs with screen design. → home: screen design.
- **Evolving-comparison freshness.** When the agent re-shares after a new offer arrives, the
  seller's view updates (handoff §5). The experience of *receiving* that update is not scoped
  here. → home: this file / handoff §5.
- **Visual design tokens.** Typography, color, spacing. This spec locks structure, hierarchy,
  and the two-layer trust grammar only. → home: brand adoption (assets/README).

---

## Voice map (copy §1)

- **Principle** — §0's organizing idea; the doctrine §5 guarantee ("If we cannot trace how a
  ranking was determined, we will not present it").
- **Explanation** — offer headline terms, confident values, glosses, buyer names.
- **System** — every absence state, the two Layer-2 treatments, correction markers,
  §-citations, the "Ranked by…" basis line, the four access-state messages.
- **Agent voice** (brand-frame copy, copy §1.4) — the brand frame and the call prompt only.
  It *frames*; it never asserts a contract fact or a claim about the order. Agent voice
  frames; Docside voice asserts; provenance governs only the second.

# Domain Vocabulary

> **Status:** v0.2 — seed. The governing principles and the entry schema are
> complete. The entry set is seeded with the high-stakes fields only; the long tail
> is deferred (see §6). Grow it as fields enter scope, not pre-emptively.
> **Derives from:** `trust-doctrine.md` §3.3 (term-based explanation) and §3.1
> (provenance).
> **Feeds:** `10-copy-guidelines/` — copy renders *these* phrasings; it does not
> invent its own and never narrates a score.

---

## 0. What this file is

"Understand a real estate contract" is, mechanically, a **translation** task. The
contract speaks in form sections, cross-references, and term-of-art shorthand
(EMD, COE, §8A loan contingency). The agent and the seller need to read the same
deal in the same plain words and trust that the words are faithful to the form.

This file is the single canonical map for that translation:

> **contract term → the words Docside uses → where it lives on the form → how it
> can mislead.**

It is core IP, not a glossary. Every phrase the product shows a user should be
traceable to a row here, and every row here is traceable to a place on the form.

---

## 1. Governing principles

**1.1 One phrasing, two audiences.** The mission is singular — *the* most
trustworthy way to understand the contract — so the agent and the seller read the
**same words**, not a pro version and a dumbed-down version. The term is never
softened in a way that loses the precision an agent relies on.

**1.2 The gloss bridges expertise without altering the term.** A seller may not
know what a loan contingency *is*; an agent does. We reconcile 1.1 with that gap
through an optional **gloss** — a plain expansion the UI can surface for the
non-expert — that *explains* the term without *replacing* it. "Loan contingency"
stays "loan contingency"; the gloss says what it does. The term is the fact; the
gloss is the courtesy.
> `DECIDED (v0.2):` the same-term-plus-optional-gloss model is adopted, over the
> alternatives (one phrasing only / separate agent & seller phrasings). It keeps
> faith with the singular mission and still serves the seller. Copy-guidelines
> builds on it.

**1.3 Conference-table voice.** Phrasings read the way a listing agent would say
the term at the table — "all-cash purchase," "21-day close," "$5,000 seller
credit" — per doctrine §3.3. Phrasings are built from the *term*, never from a
sub-score or weight.

**1.4 Every entry carries its provenance.** Each row names its form location
(§ row + ¶ cross-reference). That location is what powers the provenance
affordance (doctrine §3.1) in both the verify view and the shared summary.

**1.5 Hazards are first-class.** The ways a term can be mistranslated are named,
not folded into prose (§2). A field's hazard tag is how copy and the
states/edge-cases work know *not* to assert something the form doesn't support.

---

## 2. Translation hazards (controlled vocabulary)

A small fixed set of tags. Copy-guidelines and `08-states-and-edge-cases/` key off
these names, so they are stable identifiers, not descriptions.

| Tag | Meaning | Canonical instance |
|---|---|---|
| `STRUCTURALLY-NULL` | The form never captures this as the value you'd expect. Do not fabricate or derive it; show *not-on-this-form*. | `down_payment_pct` — the RPA captures deposit and balance of down payment separately, never a down-payment percentage. §3D(1) even prints that its percentage "is not a contractual term." |
| `FORM-LITERAL` | The form may print a *relative anchor* instead of an absolute value. Render the literal; never compute an absolute (e.g. an ISO date from signing). | `offer_expiration` — §3C prints "3 calendar days after all Buyer Signature(s)" unless an absolute date is filled. |
| `DEFAULT-TRAP` | A filled slot reads as a deviation even when its value equals the printed default. Presence ≠ deviation; observe, don't infer. | `is_default` on §3L(1) loan contingency — a filled "17 days" is not evidence the buyer chose something non-standard. |
| `FREE-TEXT-VERBATIM` | Prose, not a checkable value. Quote verbatim in quotation marks; never assert as a verified value; never score a number out of the prose (doctrine §3.2). | §3R Other Terms; §3G(2) additional seller credit terms. |
| `PCT-OR-FLAT` | Value may be a percentage, a flat amount, or both. Resolve on the ratified gate order — *incoherent → null, absent → 0, pct → derived, flat → flat*; an incoherent read becomes `null`, never a guess that could move a ranking (doctrine §5). | §3G(3) seller-paid buyer-broker compensation. |

---

## 3. Entry schema

Each vocabulary entry carries:

- **`key`** — the schema field name (aligns with `car-rpa.ts` where one exists).
- **`form`** — provenance: the §-row of the RPA terms table **and** the ¶
  cross-reference it points to, plus the label as printed.
- **`label`** — the canonical noun Docside uses in UI chrome.
- **`spoken`** — how the term reads inside a conference-table explanation sentence.
- **`gloss`** *(optional)* — plain expansion for the non-expert reader (§1.2). Does
  not replace `spoken`.
- **`hazards`** — zero or more tags from §2.

---

## 4. Seed entries (high-stakes set)

Pinned to **C.A.R. Form RPA, Revised 6/25**. Section letters are the §3 "Terms of
Purchase and Allocation of Costs" rows; ¶ numbers are that row's cross-reference
into the body.

| `key` | `form` (§ row → ¶) | `label` | `spoken` | `hazards` |
|---|---|---|---|---|
| `purchase_price` | §3A → ¶5, 5B | Purchase price | "$1,200,000 purchase price" / "all-cash purchase" | — |
| `all_cash` | §3A / §3H(1) → ¶5B | All-cash | "all-cash purchase" | when set, financing rows are *not-on-this-form*, not missing |
| `close_of_escrow` | §3B | Close of escrow | "21-day close" | `FORM-LITERAL` (days-after-acceptance vs. absolute date) |
| `offer_expiration` | §3C → ¶33A | Offer expiration | "offer expires 3 days after signing" | `FORM-LITERAL` |
| `initial_deposit` | §3D(1) → ¶5A(1) | Earnest money deposit | "$36,000 earnest money deposit" | `STRUCTURALLY-NULL` for any deposit-% contractual claim |
| `financing` | §3E(1) → ¶5C(1) | Financing | "conventional financing, $960,000 first loan" | carries loan type: Conventional / FHA / VA / Seller / Other |
| `down_payment` | §3F → ¶5D (+ §3D(1)) | Down payment | "$240,000 down" | `STRUCTURALLY-NULL` for `down_payment_pct` |
| `occupancy_type` | §3E(3) → ¶7A | Occupancy | "buyer-occupied / primary residence" | — |
| `seller_credit` | §3G(1) → ¶5E | Seller credit | "$5,000 seller credit toward closing costs" | — |
| `seller_credit_terms` | §3G(2) | Additional seller credit terms | quoted verbatim | `FREE-TEXT-VERBATIM` |
| `buyer_broker_comp` | §3G(3) → ¶18A | Seller-paid buyer-broker compensation | "seller pays buyer's broker 2.5%" | `PCT-OR-FLAT` |
| `loan_contingency` | §3L(1) → ¶8A | Loan contingency | "17-day loan contingency" / "no loan contingency" | `DEFAULT-TRAP` |
| `appraisal_contingency` | §3L(2) → ¶8B | Appraisal contingency | "no appraisal contingency" / "appraisal contingency at purchase price" | — |
| `other_terms` | §3R | Other terms | quoted verbatim | `FREE-TEXT-VERBATIM` |

---

## 5. Worked entries (showing the full schema + gloss)

Three entries written out, to set the pattern for the rest.

**`loan_contingency`**
- `form`: §3L(1) → ¶8A — printed "Loan(s) … 17 (or ___) Days after Acceptance / No loan contingency"
- `label`: Loan contingency
- `spoken`: "17-day loan contingency" — or, when removed, "no loan contingency"
- `gloss`: "The buyer can cancel and keep their deposit if their financing falls
  through within this window. *Waiving it strengthens the offer for the seller and
  raises the buyer's risk.*"
- `hazards`: `DEFAULT-TRAP` — a filled "17 days" equals the form's printed default;
  it is **not** evidence the buyer deviated. Surface the value, not an inference
  about choice.

**`buyer_broker_comp`**
- `form`: §3G(3) → ¶18A — printed "Seller agrees to pay Buyer's Broker, out of
  transaction proceeds, ___% of the final purchase price AND, if applicable $___
  OR, if checked $___"
- `label`: Seller-paid buyer-broker compensation
- `spoken`: "seller pays the buyer's broker 2.5%" (or the flat amount, or both)
- `gloss`: "Money the seller agrees to pay the buyer's agent out of proceeds —
  it reduces the seller's net, so it belongs in any honest comparison of offers."
- `hazards`: `PCT-OR-FLAT` — resolve on the ratified gate order; an incoherent read
  is `null`, never a guess. This field is the doctrine §5 precedent: a wrong value
  here can invert the seller's net and therefore the ranking.

**`offer_expiration`**
- `form`: §3C → ¶33A — printed "3 calendar days after all Buyer Signature(s) or
  ___ (date), at ___ AM/PM"
- `label`: Offer expiration
- `spoken`: "offer expires 3 days after signing" — *only when the form prints the
  relative anchor*
- `gloss`: "How long the seller has to accept before the offer lapses."
- `hazards`: `FORM-LITERAL` — if no absolute date is filled, render the relative
  phrase the form prints. Never compute an ISO datetime from the signing date.

---

## 6. Source and versioning

- **Source form:** C.A.R. Form RPA, Revised **6/25** (17-page agreement; the §3
  terms table spans RPA pages 1–3). Section letters and ¶ cross-references in this
  file are **pinned to that revision.**
- **A form revision can move section letters.** When C.A.R. revises the RPA, this
  file's `form` column must be re-grounded against the new form before any copy
  that cites a section is trusted. Section numbers from memory are not authority;
  the form is.
- **Verified against the canonical form, not reconstructed.** The §3 rows above
  were read from the actual 6/25 form, including the §3D(1) printed disclaimer that
  the deposit percentage "is for calculation purposes and is not a contractual
  term" — the form itself confirming the `down_payment_pct` `STRUCTURALLY-NULL`
  hazard.

---

## 7. Deferred (explicit, not open-ended)

Not seeded yet, by intent — added when the field enters product scope:

- Full §3L contingency set L(3)–L(9) — investigation, insurance, seller-document
  review, title, common-interest disclosures, leased/liened items, sale-of-buyer's-property.
- Full §3Q Allocation of Costs Q(1)–Q(18) — already a documented schema deferral
  in POLISH-BACKLOG; vocabulary follows the schema, not ahead of it.
- §3P items included/excluded.
- Body-paragraph terms not surfaced in the §3 table.
- Verification/POF rows §3H(1)–(3); possession §3M; documents/fees §3N.

> The list above is a **boundary**, not a backlog to burn down. A term earns a row
> when the product surfaces it to a user — no sooner.

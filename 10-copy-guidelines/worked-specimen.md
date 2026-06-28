# Worked Specimen — Conventional 80/20 Offer

> **Status:** v0.1 — reference specimen.
> **Derives from:** `copy-guidelines.md` (the three registers, the cross-cutting
> disciplines, the hazard-rendering rules) and `domain-vocabulary.md` (phrasings,
> hazard tags, glosses). Grounded in **C.A.R. Form RPA, Revised 6/25**.
> **Purpose:** the guide is rules; this is the rules *fired on a real offer*. It is
> the artifact copy gets checked against. If a future string disagrees with this
> specimen, one of them is wrong — resolve it, don't ship both.

This is an **illustrative** specimen built to exercise every register and every
hazard. It echoes the `Conventional_80_20` ground-truth fixture by design but is
not that fixture.

---

## 0. The offer (input — what the form says)

Source data, each row carrying its provenance and any hazard it triggers. This is
the *input*; everything below is how Docside renders it.

| Field | Form (§ → ¶) | Value on the form | Hazard |
|---|---|---|---|
| Purchase price | §3A → ¶5 | $1,250,000 | — |
| Initial deposit (EMD) | §3D(1) → ¶5A(1) | $37,500 | `STRUCTURALLY-NULL` (deposit % not contractual) |
| First loan | §3E(1) → ¶5C(1) | $1,000,000, Conventional | — |
| Loan rate cap | §3E(1) "not to exceed __%" | *illegible on scan* | → **unreadable** |
| Balance of down payment | §3F → ¶5D | $212,500 | — |
| Occupancy | §3E(3) → ¶7A | Primary | — |
| Close of escrow | §3B | 21 days after Acceptance | `FORM-LITERAL` |
| Offer expiration | §3C → ¶33A | 3 days after signing (no absolute date filled) | `FORM-LITERAL` |
| Loan contingency | §3L(1) → ¶8A | 17 days (the printed default) | `DEFAULT-TRAP` |
| Appraisal contingency | §3L(2) → ¶8B | "No appraisal contingency" **checked** | — (affirmative signal) |
| Seller credit | §3G(1) → ¶5E | $5,000 toward closing costs | — |
| Additional seller credit terms | §3G(2) | *blank* | → **empty-on-form** |
| Seller-paid buyer-broker comp | §3G(3) → ¶18A | 2.5% of purchase price | `PCT-OR-FLAT` |
| Other terms | §3R | "Seller to leave the patio furniture and two kayaks." | `FREE-TEXT-VERBATIM` |

Arithmetic check (for the reader, never shown in product): $37,500 + $1,000,000 +
$212,500 = $1,250,000. Down payment = price − financing = $250,000.

---

## 1. The summary, rendered — Explanation voice

This is the branded summary an agent would send. Conference-table voice, built from
terms, no scores. (Output strings are in **bold**; everything else is annotation.)

**Headline (the one-glance line):**
> **Conventional financing · $1,250,000 · 21-day close · no appraisal contingency ·
> $5,000 seller credit**

**The terms:**

- **Purchase price — $1,250,000**
- **Financing — Conventional. $1,000,000 first loan, $250,000 down.**
  - down payment is shown as a dollar figure (price − financing, both present and
    traceable). The **percentage is never printed** — the form does not capture
    down payment as a percent (`STRUCTURALLY-NULL`).
  - **Rate cap — We couldn't read this field.** *(System voice intruding into the
    summary: the loan amount read fine; the "not to exceed __%" cap did not. We say
    so rather than leave a gap that reads as "no cap.")*
- **Earnest money deposit — $37,500**
- **Close of escrow — 21 days after acceptance** *(`FORM-LITERAL` — the relative
  phrase the form prints; no calendar date is computed)*
- **Offer expires — 3 days after signing** *(`FORM-LITERAL` — relative anchor, no
  ISO datetime)*
- **Loan contingency — 17-day loan contingency**
  - *(`DEFAULT-TRAP`: 17 days is the form's printed default. We state the value. We
    do **not** say the buyer "chose" or "kept a standard" timeline — a filled
    default is not a signal of choice.)*
  - gloss: **"The buyer can cancel and keep their deposit if financing falls
    through within this window."**
- **Appraisal contingency — None. The buyer removed the appraisal contingency.**
  - *(Contrast the line above: here a checkbox was affirmatively checked. That **is**
    a signal, so describing the removal is honest.)*
  - gloss: **"The buyer won't renegotiate or cancel if the home appraises below the
    price — a stronger position for the seller."**
- **Seller credit — $5,000 toward closing costs**
- **Additional seller credit terms — Not specified on this form.** *(empty-on-form,
  distinct from unreadable above)*
- **Seller-paid buyer-broker compensation — Seller pays the buyer's broker 2.5%**
  - *(`PCT-OR-FLAT`, percentage branch. Had this field been contradictory, it would
    read "We couldn't read this field," never a guessed number — doctrine §5.)*
  - gloss: **"This comes out of the seller's proceeds, so it belongs in any honest
    comparison of net offers."**
- **Occupancy — Buyer's primary residence**
- **Other terms — "Seller to leave the patio furniture and two kayaks."** *(quoted
  verbatim, presented as the buyer's words — `FREE-TEXT-VERBATIM`)*

---

## 2. The frame — Principle voice & System voice

**Principle voice** (the trust commitment around the summary, not on every line):
> **Every value in this summary can be traced to the contract.**

In a single-offer summary that is the whole principle surface. The ranking
guarantee — *"If we cannot trace how a ranking was determined, we will not present
it"* — belongs to the comparison view (N > 1) and is cited there, not forced into a
single offer.

**System voice** (chrome and states, neutral and calm):
- Field labels are the vocabulary `label` strings verbatim ("Earnest money
  deposit," not "EMD"; "Seller-paid buyer-broker compensation").
- The two non-value states are worded to be unmistakably different:
  **"We couldn't read this field."** (unreadable) vs. **"Not specified on this
  form."** (empty-on-form). A reader can tell, at a glance, which is which.
- The provenance affordance reads plainly, e.g. **"From §3G(3) of the purchase
  agreement"** — and it reaches the shared summary, not just the verify view
  (doctrine §3.1).

---

## 3. Hazard ledger (the checkable part)

Every hazard tag, where it fires in this specimen, and the rule it obeys. This is
the table a reviewer runs the specimen against.

| Hazard | Fires on | What the specimen does | What would break it |
|---|---|---|---|
| `STRUCTURALLY-NULL` | down payment | shows "$250,000 down" (derived, traceable); omits a percent | printing "20% down" |
| `FORM-LITERAL` | close of escrow; offer expiration | renders the relative phrase | computing "Aug 14, 2025 5:00 PM" |
| `DEFAULT-TRAP` | loan contingency | states "17-day loan contingency" only | "buyer kept the standard 17 days" |
| `FREE-TEXT-VERBATIM` | other terms | verbatim, quoted, attributed | paraphrasing "some outdoor items" |
| `PCT-OR-FLAT` | buyer-broker comp | renders the percentage as read | guessing when illegible |
| *(three-way grammar)* | rate cap vs. seller-credit terms | "couldn't read" vs. "not specified" rendered differently | one blank/"N/A" for both |

---

## 4. Anti-specimen (the same offer, written wrong)

The forbidden moves from `copy-guidelines.md` §4, made concrete. Left is what
fails; right is the specimen.

| ❌ Breaks trust | ✅ Specimen | Rule |
|---|---|---|
| "20% down" | "$250,000 down" | §3 `STRUCTURALLY-NULL` |
| "Offer expires Aug 14, 2025, 5:00 PM" | "Offer expires 3 days after signing" | §3 `FORM-LITERAL` |
| "Buyer chose a standard 17-day loan contingency" | "17-day loan contingency" | §3 `DEFAULT-TRAP` |
| "Seller including some outdoor items" | "Seller to leave the patio furniture and two kayaks." | §2.4 free text |
| Rate cap shown as "—" | "We couldn't read this field." | §2.1 three-way grammar |
| "A strong, competitive offer (87/100)" | *(terms only; no score, no adjective)* | §1.1, §2.2 |

---

## 5. What this specimen covers — and doesn't

**Covers:** all three registers; the three-way grammar (present / empty-on-form /
unreadable) with a real instance of each; all five hazard tags firing; the
default-trap-vs-affirmative-signal contrast (loan vs. appraisal); free-text
verbatim; provenance reaching the shared summary; the no-score discipline.

**Deferred, by intent:**
- A **comparison specimen** (N > 1) showing the ranking guarantee and ranking-trust
  in Principle voice — needs the comparison view's copy, which doesn't exist yet.
  This is the natural sequel.
- An **all-cash specimen**, to show the financing rows rendering as *not-on-this-form*
  rather than empty or unreadable — a different, instructive null case.
- Specimens for the `FHA`/`VA` fixtures, where the lender-required-repairs and
  FVAC paths add terms not exercised here.

> One specimen is a proof of voice. The set above is what turns it into coverage —
> add them as the views they depend on come into being, not before.

# Trust Doctrine

> **Status:** v0.5 — skeleton. Load-bearing sections are written; sections marked
> `TODO(design)` require actual design work and should not be filled with prose
> that stands in for that work.
> **Governs:** every screen, component, copy decision, and error state in
> `docside-experience`.
> **Relationship to the mission:** subordinate and explanatory. This document never
> rewrites the mission; it states the method beneath it.

---

## 0. Why this document exists

The mission gives Docside its **unit**:

> Design the world's most trustworthy way to understand a real estate contract.

The mission does not, on its own, say *how* trust is earned, or what happens to
trust when there is more than one contract on the table. This doctrine supplies
both.

**Binding principle:**

> **The mission governs the unit. The doctrine governs every multiple of it.**

The mission sentence is fixed. It will not be stretched to mention comparison.
Comparison is fully in scope — but it enters through this doctrine, *beneath* the
sentence, not by editing the sentence. Single-offer understanding is the **atom**;
multi-offer comparison is a **composition of atoms plus one added trust surface**
(§2). Comparison is not a second mission and does not get its own north star.

---

## 1. The word that has to be load-bearing

"Trustworthy" is the only word in the mission that the rest of the product can
fail to honor while still appearing to work. An extraction can be wrong and look
clean. A ranking can be misleading and look authoritative. The whole risk surface
of Docside is **confident output that hasn't earned its confidence** — the false-green
problem, surfaced to the user.

So trust is not a tone, a color, or a badge. It is a set of structural
guarantees the interface must keep even when keeping them is uglier than not.
The doctrine names those guarantees and treats every one of them as a feature with
a home, not an implicit hope.

---

## 2. The two trust surfaces

Understanding a single offer and comparing several offers are **not the same trust
problem.** Comparison inherits the first problem and then adds a second one that
the single-offer view never has. Stating both explicitly is the point of this
document, because the word "understand" honestly covers the first and does *not*
natively cover the second.

| | Surface | Failure looks like | Trust mechanism |
|---|---|---|---|
| **Clause 1** | Understanding-trust (per offer) | A wrong **fact** | Provenance · honest uncertainty · term-based explanation |
| **Clause 2** | Ranking-trust (across offers) | A wrong **order** | Legibility · honest weighting · the inverted-ranking guarantee |

A wrong fact is contained — it misstates one number in one summary. A wrong
*order* is not contained: the agent acts on the order and the seller chooses on
it. That is why Clause 2 exists as its own surface and not as a footnote to
Clause 1.

---

## 3. Clause 1 — Understanding-trust (per offer)

The trust unit. The branded summary is this atom *made shareable* — which means
every guarantee below has to survive being put on the agent's brand and sent to a
client.

**3.1 Provenance.** Every value Docside surfaces is traceable to where it came
from in the contract. The user can always answer "where did this number come
from?" without leaving the product. A number with no traceable origin is a number
Docside does not assert.

**Decision (v0.2):** provenance reaches into the *shared* branded summary — not
just the agent's verify view. The seller can trace a value to its origin in the
contract, exactly as the agent can. This is the stronger of the two guarantees:
the brand the agent puts their name on carries the same traceability the agent
relied on. A summary the agent can trace but the seller cannot is explicitly
**not** sufficient.
`TODO(design):` the provenance affordance — inline source reference, hover-to-form,
section citation — *and* its form in the shared summary, which will differ from the
verify view: the seller is not logged in, is likely on mobile, and may be reading a
static PDF export where hover doesn't exist. Specify the mechanism for **both**
surfaces. Saying "yes" here is only real once the shared-summary affordance is
designed, not just the verify-view one.

**Decision (v0.5) — provenance has classes; agent correction is one.** The agent
can correct a misread at verify (states §3). That introduces a second way a value
can originate, so a surfaced value now carries not only a *location* but a *class*:
it was **extracted** from the contract, or it was **agent-corrected** over an
extraction. These are different trust claims and stay distinguishable end-to-end.
Three rules hold the line:
- **The contract is immutable.** An agent never edits the contract; they edit
  Docside's *reading* of it. The source document remains the canonical ground truth
  every value traces back to. Correction restores or asserts a reading; it cannot
  alter the thing being read.
- **Every correction is logged, append-only.** Field, original extracted value,
  corrected value, agent identity, timestamp, and the contract location it applies
  to — written immutably, never overwritten.
- **A correction is visible, not an erasure.** Because provenance reaches the seller
  (the v0.2 decision above), a corrected value is shown *as* corrected, with its
  original read traceable, in the shared summary too. The system cannot know whether
  an edit restores fidelity (fixing OCR) or asserts an override — so it treats every
  edit identically and lets the transparent record speak. Shown honestly, a
  correction reads as the agent vouching for the contract, which is a trust signal,
  not a blemish.

**3.2 Honest uncertainty.** Nulls, low-confidence reads, and `ocr_no_text`
failures are **surfaced, never hidden.** A blank is a claim ("this field is empty
on the form"); an unknown is a different claim ("we could not read this"); the two
must never render identically. Structurally-null fields (e.g. `down_payment_pct`,
which the CAR RPA never captures as a number) are shown as *not-on-this-form*, not
as missing data — absence by form design is not the same as absence by failure.

**Decision (v0.3) — free-text fields.** `other_terms`, `seller_credits_notes`, and
any field that holds prose rather than a checkable value are shown **verbatim, in
quotation marks.** The quotes are the trust signal: they mark the text as *the
person's own words, passed through* — not a value Docside read, normalized, or
verified. Verbatim means verbatim: no cleanup, no paraphrase, no meaning-changing
truncation. Two consequences follow: **(a)** a quoted field never enters the
comparison as if it were a verified value, even when the prose contains a number
("seller to credit $5,000") — if a term inside free text should affect ranking, it
must first be captured as a structured field, never scored out of the quote;
**(b)** provenance (§3.1) still applies — the quote stays traceable to where it
appears on the form.
`TODO(design):` the three-way visual grammar — present value / empty-on-form /
unreadable — plus the quoted-prose treatment above. This is where trust is most
often quietly lost.

**3.3 Term-based explanation.** Every explanation is built from the **offer's
terms, in business language** — "All-cash purchase," "21-day close," "seller
credit of $5,000" — the way a listing agent would say it at the conference table.
Explanations are **never** built from sub-scores, weights, or numbers. Sub-scores
may decide *which* terms are worth surfacing; the text the user reads is always
the term, never the score.

---

## 4. Clause 2 — Ranking-trust (across offers)

Active when N > 1. **Inherits all of Clause 1 per offer** — the per-offer
explanation inside the comparison *is* the Clause 1 atom appearing again, which is
exactly why "built from terms, never sub-scores" holds at both levels — and then
adds three mechanisms the single-offer view has no need for.

**4.1 Legibility.** The user can always answer "why is this offer ranked above
that one?" in terms they could repeat to a seller. An order Docside cannot explain
in plain terms is an order Docside does not present.
`TODO(design):` the legibility affordance for *relative* position, distinct from
the per-offer explanation in 3.3.

**4.2 Honest weighting.** The ranking reflects **seller priorities**, and the
weighting is **visible and user-controllable.** The free-slider / live-total
Customize model is a *trust mechanism*, not a UX convenience: it lets the agent
see and change what's driving the order, which means the order is never a black
box asserting authority it can't account for.
`TODO(design):` how weighting state is shown at rest (before the user opens
Customize) — the default weighting must be legible without interaction.

**4.3 The inverted-ranking guarantee.** Stated in full in §5, because it is the
single guarantee most specific to this product and the one with a known failure
class behind it.

---

## 5. The inverted-ranking guarantee

**User-facing statement:**

> Docside will never rank one offer above another on the strength of a number it
> guessed. When a term that affects the comparison can't be read with confidence,
> Docside marks it unknown and tells you so — it does not fill the gap with a
> default that could quietly move an offer up or down the list. **If we cannot trace
> how a ranking was determined, we will not present it.**

**Why this guarantee specifically.** At the single-offer level, a misread term is
a wrong fact in one summary. At the comparison level, the same misread term can
**invert the order** — making a worse offer for the seller appear to be the better
one. The agent acts on that order; the seller chooses on it. The cost of a silent
guess is therefore categorically higher in comparison than in understanding, and
the guarantee has to be stated at the *relative* level, not just the field level.

**Implementation anchor (internal — not user-facing).** This guarantee is already
honored, structurally, in one place: the §3G(3) seller-paid buyer-broker
compensation field. Its `buyerBrokerCompAmount` helper resolves on a ratified gate
order — *incoherent → null, absent → 0, percentage → derived, flat → flat* — so an
incoherent read becomes an honest `null` (honest uncertainty, §3.2) rather than a
fabricated number that could move the seller's net and therefore the ranking. That
field is the **precedent**, not the proof of generality.

> `DEFER-LINE:` the guarantee is honored in §3G(3) today. It is **not yet
> generalized** across every comparison-affecting field. Schema presence is not
> runtime behavior; this guarantee is only real for a field once that field's
> read-failure path has been shown to degrade to *unknown* rather than to a
> ranking-moving default, on a real packet. Generalization is tracked work, not a
> claim this document gets to make on the system's behalf.

---

## 6. What the doctrine derives

The downstream artifacts do not invent their own trust posture. They inherit it
from here.

- **`10-copy-guidelines/`** derives from §3.3 and `00-foundations/domain-vocabulary.md`:
  copy renders terms in business language; it never narrates a score.
- **`08-states-and-edge-cases/`** derives from §3.2 and §5: the failure states
  *are* the trust proof. Unsupported form version, OCR failure, incoherent field,
  missing data, and the three-way present/empty/unreadable grammar live here as
  first-class screens, not as afterthoughts inside happy-path design.
- **`09-component-library/`** must provide, as named primitives: a provenance
  reference, an uncertainty marker (three-way), and a weighting control. If a
  guarantee in this doctrine has no corresponding component, the guarantee is not
  yet real in the UI.

---

## 7. The one-sentence test (experience-repo version)

Mirrors §17 in the main repo. Before any screen, component, or copy change ships:

> **Does this make the contract more trustworthy to understand — by provenance,
> honest uncertainty, or term-based explanation — or does it only make it look
> more finished?**

"Looks more finished" is not a passing answer. Polish that hides uncertainty
fails this test even when it is beautiful.

---

## Open questions

_None currently open at the doctrine level. The remaining `TODO(design)` markers
in §§3–4 are design obligations, not unresolved questions — the principle is
decided; the affordance is not yet built._

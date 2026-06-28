# Copy Guidelines

> **Status:** v0.2 — foundational. The registers, the cross-cutting disciplines,
> and the hazard-rendering rules are complete and usable. Component-level
> microcopy (specific button labels, specific error strings) is deferred to the
> screens and component work that will cite this file.
> **Derives from:** `trust-doctrine.md` (§3.1 provenance, §3.2 honest uncertainty,
> §3.3 term-based explanation, §5 the guarantee) and `domain-vocabulary.md` (the
> phrasings, the gloss model §1.2, the hazard tags §2).
> **Relationship:** vocabulary decides **what words** name a term; this file decides
> **how we write** with them. It does not re-list phrasings — it cites vocabulary.

---

## 0. The one rule everything else serves

Copy is where trust is delivered or quietly broken. A number can be correct and
still mislead in how it's phrased; an unknown can be honest in the data and a lie
in the UI if it's rendered to look like a value. So the governing instruction is
narrow:

> **Write what the form supports, in the voice the moment calls for, and never let
> the phrasing claim more certainty or more judgment than we actually have.**

The rest of this file is that instruction made specific.

---

## 1. Register discipline (the spine)

Docside speaks in **three registers**. Most copy mistakes are register mistakes —
the right fact in the wrong voice. Before writing any string, name its register.

### 1.1 Principle voice — *the product stating its commitments*
Where trust is asserted: guarantees, trust statements, the doctrine surfaced to
the user, consequential confirmations.

- Formal, precise, declarative. Reads like a product principle, not a tagline.
- Present tense, plain verbs, no hedging and no marketing adjectives.
- "We" is the product keeping a promise.

> ✅ "If we cannot trace how a ranking was determined, we will not present it."
> ✅ "Every value here can be traced to the contract it came from."
> ❌ "Docside is the most trustworthy way to understand offers!" (marketing)
> ❌ "We try our best to keep rankings accurate." (hedged — a principle doesn't beg)

This is the **only** register the §5 guarantee belongs to. Do not let its formality
leak into the explanation layer.

### 1.2 Explanation voice — *the deal, in an agent's plain spoken language*
The conference-table voice of doctrine §3.3. Where offer terms are described to a
human.

- Built from the **term**, never from a sub-score, weight, or number-as-judgment.
- Plain, spoken, the way a listing agent narrates an offer at the table.
- Concrete and short. Strings of terms, not sentences about quality.

> ✅ "All-cash purchase, 21-day close, no appraisal contingency."
> ✅ "Seller credit of $5,000 toward closing costs."
> ❌ "This offer scored 87/100 on price." (narrates a score — forbidden, §3)
> ❌ "A very strong, highly competitive offer." (judgment adjectives, not terms)

Glosses (vocabulary §1.2) live in this register: one plain sentence that *explains*
a term without *replacing* it, and may name the trade-off honestly.

> ✅ Loan contingency → "The buyer can cancel and keep their deposit if financing
> falls through within this window. Waiving it strengthens the offer for the seller
> and raises the buyer's risk."

### 1.3 System voice — *labels, controls, and state messages*
UI chrome and the honest-uncertainty surface. Where the product names fields and
reports what it does and doesn't know.

- Minimal and neutral. Canonical labels come straight from vocabulary `label`.
- Calm, never alarming, never cute. An unreadable field is a fact, not a crisis.
- Honest about absence (§2 below is mostly this register's job).

> ✅ "Not specified on this form." / "We couldn't read this field."
> ❌ "Oops! Something went wrong 😬" (alarming, cute, uninformative)
> ❌ "N/A" used for both empty and unreadable (collapses a distinction — see §2.1)

### 1.4 The fourth speaker — brand-frame copy (the agent's voice)

The three registers above are all **Docside's** voice. There is one more speaker on
the artifact, and it is **not Docside**: the **agent**, addressing their client
directly. *"Whenever you're ready, call me to discuss"* (seller-workflow §6) is the
agent talking, not the product.

This copy is **Docside-defaulted but agent-owned:**

- Docside may seed a sensible default, but the agent must be able to **see and edit**
  it — they are putting their name on it (handoff §4: the brand frames, never
  authors).
- Docside never finalizes words spoken *as the agent* without the agent reviewing
  them. Putting words in the agent's mouth they can't review is a trust breach, not a
  convenience.
- It is the agent-voice analogue of free text (§2.4): a human's own words, carried,
  not authored by Docside — except here Docside seeds the draft the human then owns.

**The seam is strict.** The agent's voice **frames** — warmth, a personal sign-off, a
call-to-discuss. Docside's voice **asserts** — every claim about the contract. A
claim about the contract must never appear in the agent's voice (that would let
framing masquerade as verified content), and Docside's registers must never fake
personal warmth. Agent voice frames; Docside voice asserts; provenance governs only
the second.

---

## 2. Cross-cutting disciplines (apply in every register)

### 2.1 The three-way grammar of knowing
Doctrine §3.2 in words. These three states must **never** render identically. A
reader has to be able to tell them apart at a glance.

| State | Means | Phrasing pattern |
|---|---|---|
| **Present** | We read a value and stand behind it | the value, in its register |
| **Empty-on-form** | The form has this field; it was left blank | "Not specified on this form." |
| **Unreadable** | We could not read it (OCR failure, low confidence) | "We couldn't read this field." |

Collapsing empty and unreadable into one blank, dash, or "N/A" is the single most
common way this product would lie. They are different claims; they get different
words.

### 2.2 No score narration — ever
A sub-score may *decide which term to surface*; it must never *appear in the
copy*. The reader sees the term, never the math. This holds in the comparison view
as much as the single summary: explain rank with terms ("higher price, faster
close"), never with numbers ("scored 0.92 vs 0.78").

### 2.3 Provenance-friendliness
Copy never obstructs the source. A value is written so its form origin (vocabulary
`form`) stays attachable — no rephrasing that detaches a number from where it came
from, no merging two form fields into one sentence that can't be traced back to
either.

### 2.4 Free text is quoted, never paraphrased
For any `FREE-TEXT-VERBATIM` field: reproduce the person's words verbatim, in
quotation marks, presented as theirs. Never paraphrase, summarize, normalize, or
lift a number out of the prose into a structured claim (doctrine §3.2).

---

## 3. Rendering the hazards in words

The bridge from `domain-vocabulary.md` §2. Each hazard tag has one copy rule. This
is how a writer turns a tagged field into trustworthy text.

**`STRUCTURALLY-NULL`** — the form never captures this. Write *not-on-this-form*
(System voice), never a fabricated or back-computed value.
> ✅ Down payment %: "Not captured on this form." ❌ "≈20% down" (computed — the
> form's own §3D(1) says its percentage is not a contractual term)

**`FORM-LITERAL`** — render the relative phrase the form prints; never compute an
absolute.
> ✅ "Offer expires 3 days after signing." ❌ "Offer expires Aug 14, 2025, 5:00 PM"
> (an ISO datetime the form did not state)

**`DEFAULT-TRAP`** — describe the value; never assert the buyer *chose*, *waived*,
or *deviated* unless the form actually shows a deviation.
> ✅ "17-day loan contingency." ❌ "Buyer waived the standard timeline." (a filled
> default is not a deviation; presence ≠ choice)

**`FREE-TEXT-VERBATIM`** — quotation marks, verbatim, attributed as their words.
> ✅ Other terms: "Seller to leave the patio furniture and two kayaks."
> ❌ Other terms: "Seller including some outdoor items." (paraphrase)

**`PCT-OR-FLAT`** — render whichever the form gives (or both). If the read is
incoherent, drop to System voice ("We couldn't read this field") — never a guessed
number, because here a guess can invert the ranking (doctrine §5).
> ✅ "Seller pays buyer's broker 2.5%." / "Seller pays buyer's broker $20,000."
> ❌ a number assembled from an unreadable or contradictory field

---

## 4. Anti-patterns (the forbidden moves)

A quick-reference of what breaks trust, each tied to its rule:

- **Marketing superlatives** in any register — "best," "unbeatable," "perfect
  offer." (§1.1)
- **Score narration** — any number, weight, or sub-score appearing as the *reason*
  for anything. (§2.2)
- **False precision** — computing an absolute the form left relative; deriving a
  value the form never captured. (§3 · `FORM-LITERAL`, `STRUCTURALLY-NULL`)
- **Collapsed unknowns** — empty and unreadable rendered the same. (§2.1)
- **Paraphrased free text** — summarizing what should be quoted. (§2.4)
- **Inferred intent** — "chose," "waived," "prioritized" asserted from a value the
  form doesn't mark as a deviation. (§3 · `DEFAULT-TRAP`)
- **Alarming or cute system copy** — error states written to spike anxiety or to
  charm. Failure is reported plainly. (§1.3)

---

## 5. The one-line test for any string

Before a string ships:

> **Is it in the right register, does it claim only what the form supports, and
> could the reader trace it back to the contract?**

If a string narrates a score, computes what the form left blank, or makes an
unknown look like a value, it fails — regardless of how good it reads.

---

## 6. Deferred (explicit)

- Component-level microcopy — exact button text, toast strings, tooltip wording —
  is written *against* this file by the component and screen work, not pre-specified
  here.
- The shared-summary vs. verify-view copy split: the seller-facing summary may need
  more gloss and more System-voice scaffolding than the agent's verify view (the
  seller isn't logged in, is likely on mobile, may hold a static export — doctrine
  §3.1). Register rules are the same; density differs. Tracked, undesigned.
- Localization / Spanish-language phrasing of terms and glosses — out of scope until
  a term set is stable; flagged because California's agent and seller population
  makes it foreseeable, not because it's near.

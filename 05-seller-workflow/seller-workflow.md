# Seller Workflow

> **Status:** v0.2 — journey. Deliberately shorter than the agent workflow — the
> seller's journey *is* shorter, and the doc honors that rather than padding it.
> **Derives from:** `handoff.md` (the surface the seller receives), `trust-doctrine.md`
> §3.1–§3.3, §4 (what reaches the seller), `domain-vocabulary.md` §1.2 (the gloss),
> `agent-workflow.md` (the journey this one mirrors).
> **Relationship:** the agent workflow is a skeptic-to-reliant arc across days; this
> is a single sitting whose whole job is *understand and trust in one pass.* The
> asymmetry is the point.

---

## 0. Who the seller is

A homeowner, usually **not** a real estate professional, selling what is likely their
largest asset — and often under a stressful life event (relocation, divorce, a death,
financial pressure). They will eventually **sign** this contract, so understanding it
isn't academic; they're being asked to commit. They trust their **agent**, and they
receive the summary *as their agent's* — on their phone, from a text or email link.
They are frequently not one person but a few: spouses, co-owners, a trustee, heirs,
reaching a decision together. The surface is often a **shared reference for a family
conversation**, not a lone reader's screen.

---

## 1. The asymmetry

Everything that gives the agent workflow its shape is absent here:

| Agent | Seller |
|---|---|
| uploads, accumulates over days | receives once, reads in one sitting |
| authenticated workspace | public link, no login |
| can correct, mark, confirm | read-only — can only read and trace |
| two-pane, desktop-likely | single surface, mobile-likely |
| skeptic of the *tool* | doesn't know there's a tool — trusts the *agent* |
| arc ends in *reliance* (returns) | arc ends in a *decision* (one transaction) |

So this workflow is not a smaller agent workflow. It is a different act with a
different job.

---

## 2. Where the mission actually lands

The mission is to make a real estate contract *understood.* The agent already
understands contracts — they're a pro; for them the product is about trust and time.
The **seller** is the one for whom understanding a 17-page RPA is genuinely hard and
genuinely valuable. So in the most literal sense, **the seller surface is where the
mission is fulfilled.** "Understand a real estate contract" beats hardest here.

And the two ahas are linked by cause:

> **The seller understanding the offer is what makes the agent proud to have sent
> it.** Seller comprehension → agent pride.

The agent looks competent and caring *because* their seller finally gets it. Which
means designing for the seller's comprehension is not charity to a non-paying
beneficiary — it is how the paying customer's aha gets earned. The two workflows are
one causal chain, and this is its far end.

---

## 3. The seller's trust arc

The mirror of the agent's, and shorter:

```
overwhelmed ──► oriented ──► understanding ──► confident to decide
```

- The conversion is **comprehension, not tool-trust.** The seller doesn't start
  skeptical of an AI; they start *swamped by a contract.* The win is the moment the
  opaque becomes clear — "okay: all-cash, 21-day close, they waived the appraisal —
  I get it now."
- **Glosses earn their existence here.** The same-term-plus-plain-expansion model
  (vocabulary §1.2) was built for exactly this reader: the agent knows what a loan
  contingency is; the seller often doesn't. The gloss is what turns a term of art
  into understanding without dumbing the term down.
- **Provenance is comprehension and ownership, not audit.** For the seller, tracing a
  value to the contract isn't about catching the agent lying — it's "I can see the
  21-day close is right there," which lets the seller *own* the decision instead of
  merely being told. It also protects the agent: nothing was fudged, and it shows.

---

## 4. The journey

Short, because it is:

```
open the link ──► read ──► understand (glosses, plain terms) ──► trace anything (optional)
              ──► form a view ──► talk to the agent
```

- **Single offer:** the seller reads a branded summary and understands the offer.
- **Comparison (N>1):** the seller sees the offers ranked **by their own stated
  priorities** — "ranked by: fastest close, highest net, fewest contingencies." The
  order is legible because its basis is shown (doctrine §4). Crucially, the ranking
  is an **input to the seller's decision, not the decision** — the seller may weigh
  things the form never captured (a buyer's letter, keeping the house in reach of a
  family they like, gut feel). The surface presents fit-to-priorities and visibly
  leaves room for everything it can't see.

The journey **ends in a conversation with the agent**, not a transaction inside
Docside. The summary is a conversation aid that makes the seller a more informed
partner in the discussion they were always going to have with the person they hired.

---

## 5. Duties to a vulnerable reader

This surface meets someone emotionally activated, possibly stressed, holding a big
decision. That imposes obligations the agent surface doesn't carry as sharply:

- **Inform, never advise.** Docside shows what the offer **is**; it never tells the
  seller what they **should do.** The recommendation is the agent's licensed,
  fiduciary role; the decision is the seller's. Docside occupies only the *understand*
  slot — which is exactly the mission's scope, held honestly. No "accept" button, no
  "best offer" verdict; a ranking is fit-to-priorities, not a should.
- **No pressure, no manufactured urgency, no dark patterns.** Calm, plain, unhurried
  (copy §1.1's no-marketing rule, the handoff's non-laundering principle). A seller
  deciding the fate of their home is owed honesty without nudging.
- **The decision is never the algorithm's.** A seller must never feel a score decided
  for them. The no-score discipline (copy §2.2) protects this directly: they see
  terms and their own priorities, never a number rendering a verdict.

---

## 6. Decisions (locked)

- ✅ **End with a light, agent-voiced prompt to call** — e.g. *"Whenever you're
  ready, call me to discuss — (310) 555-1212"* rendered as a `tel:` link. It honors
  §4's ending (the journey returns to the agent) and **needs no new infrastructure**:
  it surfaces the agent's existing contact as a native phone action, not a Docside
  messaging path. Three things it gets right, and a fallback:
  - **It's the agent's voice, not Docside's.** "Call *me*" is the agent speaking to
    their client — brand-frame copy (handoff §4), a different speaker from Docside's
    own three registers. Docside provides a sensible default; the agent can edit it,
    because they're the one putting their name on it.
  - **The number is brand/profile data, not a contract value.** It comes from the
    agent's Docside profile, cleanly separate from the contract's traceable values —
    no confusion with provenance.
  - **The tone models §5.** "Whenever you're ready" is the opposite of manufactured
    urgency — the copy itself enacts the no-pressure duty to a vulnerable reader.
  - *Fallback:* if the agent has no contact on file, the prompt degrades to whatever
    contact the brand carries, or is omitted — never a broken or empty `tel:` link.

---

## 7. Deferred (explicit)

- **Multi-viewer alignment** — co-owners reaching a decision together (§0): shared
  view is enough for the alpha; structured collaboration is post-alpha.
- **Seller-side accessibility** — this is the surface most likely to meet an
  older, less technical, or screen-reader-dependent reader; a dedicated accessibility
  pass belongs with screen design and matters disproportionately here.
- **Evolving-comparison shares** — when a new offer arrives mid-window and the agent
  re-shares, the seller receives an updated picture (handoff §5 freshness); the
  experience of *that* update is not scoped here.

# Critical Path — Spine Index

> **Status:** v0.1 — spine index
> **What this is:** wiring, not exposition. The NORTH-STAR trust-obligation table,
> `04-agent-workflow/agent-workflow.md` §4, `02-information-architecture/
> information-architecture.md`, and `06-handoff/handoff.md` already walk the spine
> stage-by-stage. This index names what each stage hands to the next, and which trust
> invariants thread across the entire chain. It does not re-state what those docs say.
> **If they disagree with this file, they win** — go fix the wiring here, not there.

---

## The spine

```
upload  →  verify  →  [compare]  →  share
```

Single-offer activation: upload → verify → share.
Multi-offer depth: upload 1…N → verify each → compare → share (the same spine,
fanning out and converging).

**Canonical stage-by-stage reference:** NORTH-STAR.md trust-obligation table.

---

## Stage handoffs — what crosses each boundary

### Upload → Verify

**What crosses:** a successfully ingested Offer — an immutable source Document, an
extracted field set with per-field confidence scores, and an auto-join to a Listing
by §1B identity (IA §2).

**What does not cross:** any judgment, summary, or confidence-smoothing. The raw
read arrives at verify intact, including every low-confidence flag and every
unreadable field. The agent is not pre-filtered; they see the real extraction.

**Trust invariant that threads forward:** the source Document is immutable from this
point. An agent correction at verify changes the *reading*, never the document
(doctrine §3.1 v0.5). The document is the canonical ground truth every downstream
value traces back to.

**Where failures surface:** upload-stage failures are defined in
`08-states-and-edge-cases.md` §2. They are named and actionable before anything
reaches the agent — an upload failure is a trust moment, not an error to suppress.

---

### Verify → Share (single offer)

**What crosses:** the agent's *vouched* reading — every field either confirmed,
corrected (with its append-only log entry), or marked unreadable. Plus: any
high-stakes acknowledgment the agent gave before share could proceed (states §3).

**What does not cross:** the low-confidence category. By the time the share is
authorized, every field is binary — a trusted value (read or agent-corrected) or an
honest "We couldn't read this field" — per the resolve-at-verify decision (states
§1.1). A caveated number never reaches the seller.

**Trust invariants that thread forward** (from handoff §2):
1. Provenance reaches the seller — every value traceable to the contract, without
   hover (handoff §3 · doctrine §3.1 v0.2).
2. Corrected values shown as corrected, with the original read visible (doctrine
   §3.1 v0.5 · states §3.1).
3. Honest uncertainty preserved — all six absence states arrive on the seller
   surface as distinct, named, unmistakable (states §1 · handoff §2 invariant 3).
4. Term-based, no scores — the seller sees terms and glosses, never a weight or a
   sub-score (doctrine §3.3 · copy §2.2).
5. Non-laundering — the crossing never strengthens a claim by dropping a caveat
   (handoff §6). The seller surface may not look "cleaner" than the agent's verified
   read.

**Canonical reference for the crossing mechanics:** handoff §2–§6.

---

### Verify each → Compare (N > 1)

**What crosses:** N individually vouched readings, each having passed the
verify → share boundary above. Plus: the agent's comparison-set curation — the
reconciliation gate has run, duplicates are resolved, each offer's inclusion is
deliberate (IA §2.1 · states §4.1).

**What does not cross:** the comparison membership decision itself — no offer enters
a ranking the agent didn't see and place there. The reconciliation gate is the proof
of deliberateness.

**Trust invariants that thread forward** (beyond those already above):
5. Ranking legible and guaranteed — the order is explained in terms, the weighting
   (seller-priority profile) is visible, and an unreadable comparison-affecting field
   suppresses that dimension rather than guessing (doctrine §4–§5 · states §4).

**What the compare stage adds:** ranking-trust (doctrine §2, Clause 2). It inherits
all of Clause 1 per offer and adds legibility, honest weighting, and the
inverted-ranking guarantee.

**Canonical reference for the comparison trust surface:** doctrine §4–§5 and
states §4.

---

### Compare → Share (N > 1)

Same invariants as verify → share, with the additional access-control obligation:
a comparison share exposes multiple buyers' confidential terms, warranting stronger
link access control than a single-summary share (handoff §7–§8 · decisions.md
DEC-1's raised concern). This is an active open decision (handoff §8); the spine
index flags it; handoff §8 owns it.

---

## The invariants that thread the whole chain

These are not stage-specific; they hold from upload through share and must be
preserved at every seam:

| Invariant | Anchored in | The failure if it breaks |
|---|---|---|
| Source Document is immutable | doctrine §3.1 v0.5 | a correction rewrites the contract instead of annotating a reading |
| Provenance is traceable end-to-end | doctrine §3.1 v0.2 | the seller (or the agent) can't verify a number — trust becomes assertion |
| Absence has six named states, not one | states §1 · copy §2.1 | "empty" and "unreadable" collapse — two opposite claims look identical |
| Correction is logged, append-only | states §3.1 · doctrine §3.1 v0.5 | an edit can cover its tracks — the audit is gone |
| No caveat is dropped at share | handoff §6 (non-laundering) | the summary looks cleaner than the truth; the first time a seller finds the gap, trust is gone |

---

## The two-zone boundary (IA §3)

The spine's most consequential seam is not between stages — it is between the two
zones: the **authenticated agent workspace** and the **public share surface**. The
handoff is the crossing (folder 06). Everything upstream is the agent's world; the
share surface is the seller's.

The trust invariants above all have a "what crosses intact" requirement precisely
because this zone boundary strips interactive affordances. A provenance system that
works only inside the agent workspace has not fulfilled doctrine §3.1 v0.2. The
degradation matrix (handoff §3) is the build gate: no form ships until every
invariant has a named static equivalent.

**Canonical reference for the zone boundary:** IA §3 and handoff §1–§3.

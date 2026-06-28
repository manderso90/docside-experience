# States & Edge Cases

> **Status:** v0.3 — spec. The state taxonomy and the per-stage catalogs are
> complete and checkable. Per-state visual mockups are deferred to the screen and
> component work that will cite this file.
> **Derives from:** `trust-doctrine.md` §3.2 (honest uncertainty), §5 (the
> guarantee); `NORTH-STAR.md` (the upload and verify obligations);
> `copy-guidelines.md` §2.1 (the grammar) and §3 (hazard rendering).
> **Refines:** copy-guidelines §2.1 — the three-way grammar there was the minimum
> viable distinction; §1 below is its full resolution. copy §2.1 should point here.

---

## 0. Why this folder carries weight

For most products, edge cases are where polish goes to die — designed last, last to
matter. For *this* mission they are inverted: trust is won or lost in failure. A
product that produces a beautiful summary when the scan is clean and a confident
**wrong** summary when it isn't has not earned "the world's most trustworthy way to
understand a real estate contract." It has earned the opposite.

So the states below are not the afterthought to the happy path. They **are** the
proof. The happy path is what the product does; these are what the product *is*.

---

## 1. The grammar of what we don't show (centerpiece)

When the product does not show a normal value, there is always a reason — and there
are **at least six distinct reasons**. Conflating any two of them is a lie told by
omission. Each gets its own words, and they must be tellable apart at a glance.

| State | Means | Copy (System voice) | Register note |
|---|---|---|---|
| **Present — confident** | read it, stand behind it | the value | Explanation voice |
| **Present — low-confidence** | read *something*, not sure | *see §1.1 — resolved at verify, never shown to the seller as a caveated number* | — |
| **Empty-on-form** | the field exists on the form; left blank | "Not specified on this form." | the buyer/seller didn't fill it |
| **Not captured** *(structurally-null)* | the form never records this value | "Not captured on this form." | e.g. down payment %; §3D(1) disclaims its own percentage |
| **Not applicable** | excluded by another answer | "Not applicable — all-cash purchase." | financing rows when §3A all-cash |
| **Unreadable** | OCR/parse failure on this field | "We couldn't read this field." | the document, not the deal, is the problem |

**The dangerous collapses** — pairs that look similar and must never render the same:

- *empty-on-form* vs *unreadable* — "the buyer didn't specify" vs "we failed to
  read." Opposite meanings; the first is about the deal, the second about us. This
  is the §2.1 pair and the one most often gotten wrong.
- *empty-on-form* vs *not-captured* — "left blank" vs "the form has no such field."
  One invites a follow-up ("why didn't they fill it?"); the other forecloses it.
- *not-captured* vs *not-applicable* — both are about form structure, but one is
  always true and the other depends on this offer's other answers.

> **Rule:** every absence names its cause. A blank cell, a dash, or "N/A" that
> stands for more than one of the above is a defect, not a style choice.

### 1.1 Low-confidence is resolved at verify, never punted to the seller

A read can land below the confidence threshold — present, but not trusted. The
question is what to do with it, and the answer uses the spine.

- **In the verify view (agent only):** show it as **"Low confidence — please
  confirm,"** with the value and its provenance. The agent is the human in the
  loop; verify exists precisely to resolve marginal reads. The agent has three
  resolutions, all available: **confirm** the value as read, **correct** a misread
  (logged — see §3), or **mark it unreadable.**
- **In the shared summary (seller):** there is **no** caveated-number state. By the
  time something is shared it is either a **confident value** (read or corrected),
  or an honest **"We couldn't read this field."** A "here's a number but it might be
  wrong" never reaches a seller — a flagged-but-wrong figure can still mislead, and
  the seller has no way to check it.

> `DECIDED:` threshold-below ⇒ unreadable, with a verify-only confirm/correct/mark
> band at the margin. This makes the verify step do real work instead of being a
> rubber stamp, and keeps the shared artifact binary: a trusted value (read or
> agent-corrected) or an honest blank. The threshold value itself is a tuning
> question for extraction, not a design question.

---

## 2. Upload-stage states (ingestion)

The upload obligation from `NORTH-STAR.md`: **don't silently mangle the input.**
Every ingestion failure becomes a specific, named, legible state — never a silent
degradation into a confident-looking but wrong summary. The `ocr_no_text` guard is
the precedent: it turned a silent failure into a caught, auditable one.

| Failure | What actually happens | What the agent sees | What they can do |
|---|---|---|---|
| **Not a PDF** | the file is something else wearing a `.pdf` name (a real export was a ZIP) | "This file isn't a readable PDF." | re-export / re-save as PDF |
| **Encrypted PDF** | zipForm/Lone Wolf RC4 export; `pdf-lib`'s `ignoreEncryption` would emit ciphertext | "This PDF is locked. Re-export it without security, or print-to-PDF." | re-export unlocked |
| **No text, OCR empty** | image-only scan, OCR yields nothing (`ocr_no_text`) | "We couldn't read any text in this document." | rescan at higher quality |
| **Wrong document** | not a purchase agreement at all | "This doesn't look like a California Residential Purchase Agreement." | upload the RPA |
| **Unsupported form version** | an RPA revision other than the one we're calibrated to | "This looks like a different version of the RPA than we currently support." | flagged; see note |
| **Incomplete packet** | the RPA is present but pages are missing | "Some pages of the agreement appear to be missing." | re-upload the full packet |

**Two principles run through this table:**

1. **Fail loud, fail specific, fail early.** An upload failure is *better* than a
   wrong summary, and it should be framed that way to the agent: we caught this
   before it could mislead you. That is a trust-building moment, not an error.
   Hence: calm System voice, never alarming, always with the next action.
2. **Version is pinned, and the form says so.** The vocabulary is calibrated to RPA
   **6/25**; section letters move across revisions. An unrecognized version is a
   named state, not a silent mis-parse against the wrong section map.

---

## 3. Verify-stage states (the human-in-the-loop)

Verify is where the agent earns the right to put their brand on the summary
(`NORTH-STAR.md`: *won at share, earned at verify*). The states are about how much
checking the read demands.

- **Clean read** — all high-stakes fields confident. Verify is a fast confirm.
- **Read with minor unknowns** — unreadable/empty in low-stakes fields. Surfaced,
  but verify stays light.
- **Read with high-stakes uncertainty** — an unreadable or low-confidence read in a
  `HIGH_STAKES_FIELD_KEY` (purchase price, financing, close date, contingencies,
  buyer-broker comp). This is not a footnote.

**Stakes-weighted verification.** Not all unknowns are equal. An unreadable
purchase price and an unreadable HOA certification fee are both "unknowns," but one
can mislead a seller about the whole offer and the other cannot. The verify step
should weight its friction by stakes: a high-stakes unknown gets a stronger,
explicit acknowledgment before the summary can be shared; a low-stakes one rides
along as a visible footnote.

> `DECIDED:` a high-stakes unreadable requires an explicit agent acknowledgment at
> verify before share ("This summary couldn't read the purchase price — share
> anyway?"). Low-stakes unknowns do not gate share. This keeps the verify step
> proportionate instead of either rubber-stamping everything or nagging on trivia.
> The field-to-stakes mapping reuses `HIGH_STAKES_FIELD_KEYS`, not a new list.

### 3.1 Correction & audit

The agent can **fix a misread**, and can also **confirm a value is unreadable** —
both paths exist. Correction is what makes verify a real review step rather than a
checkbox. It is also the riskiest affordance in the product, because a careless
version lets an agent's keystrokes masquerade as the contract's text. The doctrine
holds the line (§3.1, v0.5 decision); here is what that means in this stage:

- **The agent edits the *reading*, never the contract.** The source document is
  immutable ground truth. A correction changes Docside's recorded value, not the
  PDF — and the original extracted value is preserved beneath it.
- **Every correction is logged, append-only:** field, original read, corrected
  value, agent identity, **timestamp**, and the contract location it applies to. The
  log is never overwritten; a correction of a correction is a new entry.
- **A corrected value is shown *as* corrected, through to the shared summary.**
  Because provenance reaches the seller, the seller can tell a corrected value from
  an extracted one and trace the original read. This is entailed by the v0.2
  provenance decision, not a new choice: if the seller can trace origin, and a
  corrected value has a different origin, the seller must be able to see it.
- **Framing matters.** A visible correction is a *trust signal* — the agent vouching
  for the contract — not a blemish. The treatment should read that way: quiet,
  System voice, "corrected by agent · original read: $X," never an alarm.

> `TODO(design):` the *treatment* of the corrected-value marker (how prominent, how
> it renders on a static shared PDF where there's no hover) and the correction input
> itself. The log schema and its storage are the **main repo's** job (likely an
> append-only Supabase table); this file specifies that the log must exist, what it
> must capture, and that its result is surfaced — a cross-repo requirement for
> `CLAUDE.md` to track.

---

## 4. Compare-stage edge cases (N > 1)

The ranking obligation: **if we cannot trace how a ranking was determined, we will
not present it** (doctrine §5). The edge cases are the cases that test it.

- **Unreadable comparison-affecting field.** A field that feeds the ranking is
  unreadable in one offer. The dimension it feeds is **suppressed or flagged for
  that offer** — never guessed to keep the ranking tidy. A partial ranking honestly
  labeled beats a complete ranking quietly fabricated.
- **Asymmetric completeness.** Offer A specifies a term, Offer B left it blank. The
  comparison shows the asymmetry (empty-on-form on B), it does not impute B's value
  from A or from a default.
- **N = 1 in the comparison view.** A degenerate comparison. Don't render a
  ranking of one as if it were a contest; fall back to the single-offer summary.
- **Tie / near-tie.** When offers are close on the weighted priorities, say so
  plainly rather than manufacturing a decisive order from rounding. A near-tie is
  information the seller wants, not a flaw to hide.

### 4.1 Assembling the comparison set (two-channel reconciliation)

Before a comparison can be trusted, its **membership** has to be. Offers reach a
listing by two channels — agent upload and inbound email (IA §2.1) — and the agent
controls which enter the comparison at the reconciliation gate. Each edge below is a
comparison-integrity failure if missed.

| State | Trigger | Surface | Why it matters |
|---|---|---|---|
| **Cross-channel duplicate** | same offer arrives by upload *and* email (match: buyer §1A + property §1B + price §3A) | flagged in the list — "Possible duplicate"; agent drops one | a duplicate ranks an offer against a copy of itself — doctrine §5 |
| **Unreadable buyer-name label** | §1A buyer name unreadable / low-confidence | fallback handle ("Emailed offer, received Tue 2 PM"), shown *buyer name unreadable* — never blank | the agent can't curate offers they can't tell apart |
| **Source ambiguity** | which channel an offer came from is unclear | list always shows uploaded vs. emailed per offer | reconciling two channels means seeing the seam |
| **Inclusion granularity** | "use both sets," but one offer is a duplicate / withdrawn / backup | set-level toggle by default; per-offer exclusion available (entailed by dedup) | the comparison shows only what the agent vouched for |

**Principle:** a comparison is only as trustworthy as its membership is deliberate.
No offer enters a ranking by default, by duplication, or through a channel the agent
didn't see.

---

## 5. Share-stage edge cases

- **Sharing with gaps.** Allowed. A summary with an honest "We couldn't read this
  field" is more trustworthy than one with the gap papered over — and provenance
  reaches the seller (doctrine §3.1), so the seller sees the same gap the agent
  did. We never hide a gap to make the share look complete.
- **High-stakes gap at share.** Gated by §3's acknowledgment, not by hiding it.
- **Stale share.** If the underlying offer is later re-read or corrected, a
  previously shared summary can drift from current data. Flagged as a real concern;
  out of scope for the alpha.

---

## 6. States ledger (the checkable master)

The table a reviewer runs a screen against — every state, its trigger, its surface.

| Stage | State | Trigger | Surface |
|---|---|---|---|
| field | present-confident | confident read | the value, Explanation voice |
| field | agent-corrected | agent fixed a misread | the value, marked "corrected by agent · original: X", logged |
| field | low-confidence | below threshold | verify: confirm/correct/mark; share: value or unreadable |
| field | empty-on-form | blank field on form | "Not specified on this form." |
| field | not-captured | structurally-null | "Not captured on this form." |
| field | not-applicable | excluded by another answer | "Not applicable — [reason]." |
| field | unreadable | OCR/parse failure | "We couldn't read this field." |
| upload | not-a-PDF / encrypted / no-text / wrong-doc / bad-version / incomplete | §2 | named, calm, actionable |
| verify | clean / minor-unknown / high-stakes-unknown | §3 | proportionate friction |
| intake | cross-channel duplicate / unreadable-label / source-ambiguity / inclusion | §4.1 | comparison membership is deliberate, never default |
| compare | unreadable-dimension / asymmetric / N=1 / tie | §4 | honest partial, never fabricated |
| share | share-with-gaps / high-stakes-gap / stale | §5 | gaps visible, gated, never hidden |

---

## 7. Decisions (locked)

1. **Low-confidence ⇒ unreadable, with a verify-only confirm/correct/mark band**
   (§1.1). ✅ locked.
2. **High-stakes unreadable gates share via agent acknowledgment; low-stakes does
   not** (§3), reusing `HIGH_STAKES_FIELD_KEYS`. ✅ locked.
3. **Correction path exists** alongside confirm-unreadable, with an **append-only,
   timestamped audit log** and the corrected value surfaced *as* corrected through
   to the shared summary (§3.1). ✅ locked; doctrine §3.1 (v0.5) updated to carry it.

Open at the design level (not the principle level): the *treatment* of the
corrected-value marker on the shared surface, and the correction input UI (§3.1
TODO). The audit log's storage is the main repo's to implement.

---

## 8. Deferred (explicit)

- Per-state **visual mockups** — how each state *looks*, not just reads — belong to
  the screen/component work and will cite this file.
- The **corrected-value marker treatment** and **correction input UI** (§3.1 TODO) —
  the principle is locked; the visual treatment is downstream design.
- **Stale-share** invalidation (§5) — out of scope for the alpha.
- Localized failure/state copy — follows the copy-guidelines localization defer.

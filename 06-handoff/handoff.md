# Handoff — the Agent → Seller Seam

> **Status:** v0.1 — spec. The trust-fidelity framing, the invariant set, the
> degradation matrix, and the share-form sequencing are complete. Visual layout of
> the share surface belongs to screen design.
> **Derives from:** `information-architecture.md` §3 (the two zones), `trust-doctrine.md`
> §3.1 (provenance reaches the seller; corrections shown as corrected), §3.2 (gaps
> visible), §3.3 (term-based), §4–§5 (ranking-trust & the guarantee), `NORTH-STAR.md`
> (*won at share, earned at verify*), `states-and-edge-cases.md` §5 (share states).
> **Owns:** the moment the branded artifact leaves the agent's hands. This is folder
> 06, the seam between IA's two zones.

---

## 0. What the handoff is

The handoff is the crossing of a **Summary** (one offer) or a **Comparison** (N > 1)
from the authenticated agent workspace into the public seller surface. It is where
the aha is *won* — the agent puts their brand on it and sends it — and it is the
single point where everything the doctrine promised gets stress-tested in front of
the one person the agent is trying to earn trust with.

The seller cannot edit, cannot re-extract, cannot log in. They can only **read and
trace.** So the seller's trust is entirely *inherited* — from the agent's
verification, and from what survives the crossing.

---

## 1. The central problem: trust-fidelity across a degrading channel

Trust is built in a **rich** environment: the agent's desktop verify workspace —
interactive, two-pane, hover-to-source, authenticated, correctable. It is consumed
in a **poor** one: the seller's share surface — mobile-likely, read-only, no login,
possibly a static PDF with no interactivity at all.

> **Every affordance the doctrine leaned on in the rich zone must have a
> degraded-but-faithful equivalent in the poor zone — or the guarantee silently
> weakens at exactly the moment it matters most: when it leaves the agent's hands.**

That is the whole job of this seam. A summary that's trustworthy on the agent's
screen and hollow on the seller's phone has failed the mission precisely where the
mission is judged.

---

## 2. The invariants — what must cross intact

Pulled from the doctrine. These are not re-decided here; they are the carry-over
set, and the rest of this file is about keeping them alive across degradation.

1. **Provenance reaches the seller** — every value traceable to the contract
   (doctrine §3.1). The hard part: *without hover.*
2. **Corrected values shown as corrected** — the agent's edits carry their marker
   and original read into the seller's view (doctrine §3.1, v0.5).
3. **Honest uncertainty preserved** — "We couldn't read this field" and "Not
   specified on this form" survive intact and distinct; gaps stay visible (§3.2).
4. **Term-based, no scores** — Explanation voice carries over; no sub-score ever
   surfaces (§3.3, copy §2.2).
5. **Ranking legible and guaranteed** *(comparison only)* — the order is explained
   in terms, the weighting (the listing's seller-priority profile) is visible, and
   *if we cannot trace how a ranking was determined, we will not present it* (§4–§5).

---

## 3. The degradation matrix (centerpiece)

How each invariant survives each share form. The **static PDF column is the hard
one** — no interactivity, so anything that relied on a tap or hover must become
*printed*.

| Invariant | Interactive link (`/share/[token]`) | Static PDF export | Email |
|---|---|---|---|
| **Provenance** | tap/expand a value → its §-citation and source snippet | §-citation printed inline ("from §3G(3)") + a source appendix | preview + link; provenance lives in the link |
| **Corrections** | marker + tap to see original read | "corrected by agent · original: $X" printed beside the value | carried by the link/PDF, not the email body |
| **Uncertainty** | "couldn't read" / "not specified" rendered distinctly | same two phrasings, printed distinctly — never collapsed to a dash | summarized honestly; detail in link/PDF |
| **Term-based** | terms, glosses on tap | terms; glosses printed inline or footnoted | terms in preview |
| **Ranking** *(N>1)* | order + "ranked by: [seller priorities]" + per-offer term explanation | the same, printed; weighting stated, not interactive | order + link to the live comparison |

The matrix is also a **build gate**: a share form may not ship until *every*
invariant has a real cell in its column. A PDF that can't print provenance is not a
smaller version of the share — it's a doctrine violation wearing the agent's brand.

---

## 4. The brand: messenger, not author

The aha is "a summary the agent is proud to put their **brand** on." Branding
applies here — agent name, brokerage, logo, contact frame the artifact. But the
brand **frames** the content; it does not **author** it. The seller should read the
artifact as *[Agent]'s summary of the contract*, with the contract as the traceable
source underneath.

This is why branding and trust are not in tension: **provenance is what reconciles
them.** The agent can put their name on it *because* every value traces to the
contract, and the seller can trust the agent's brand *because* they can check it
against the source. Remove provenance and the brand becomes an unverifiable
assertion; keep it and the brand becomes a vouching, backed by a checkable record.

> **Rule:** branding may style the frame — never the facts. A brand treatment that
> obscures a gap, a correction marker, or a provenance citation fails §6.

---

## 5. Freshness: live link vs. snapshot

A correction or re-read can change the underlying data *after* a share goes out
(states §5, stale-share).

- **The interactive link is live.** It reflects current data, so a correction the
  agent makes later propagates to what the seller sees. This is the safer default
  and the reason link-share leads.
- **A PDF is a snapshot.** It is point-in-time and *will* go stale if data changes.
  So an exported PDF must be **dated and version-stamped** ("Prepared June 27, 2026,
  3:14 PM"), making a stale copy identifiable rather than silently wrong.

> A share is not fire-and-forget. Live shares stay honest by staying current;
> snapshots stay honest by being dated.

---

## 6. The non-laundering principle

The defining discipline of this seam:

> **The handoff never strengthens a claim by dropping a caveat.**

At share, the temptation is to *clean up* — drop the "we couldn't read this" so the
branded summary looks polished, thin out provenance to reduce clutter, round a
near-tie into a decisive winner. Every one of those makes the share *look* more
trustworthy while making it *less* so. The handoff transmits the verified truth
**including its imperfections.** It does not launder them on the way out the door.

A summary that admits one unreadable field is more credible than one that hides it —
and the first time a seller catches a hidden gap, every other number on the page
loses its authority.

---

## 7. Comparison handoff specifics (N > 1)

A shared comparison carries more than a shared summary, and more risk:

- **Ranked by the seller's own priorities.** The artifact states the weighting
  plainly — "ranked by: fastest close, highest net, fewest contingencies" — drawn
  from the listing-scoped seller-priority profile (IA §1). The order is legible
  because the basis is visible, not because a number declares a winner.
- **It holds multiple buyers' confidential terms.** A comparison exposes every
  competing offer's price and terms. If a comparison link leaks, it exposes more
  than one buyer's sensitive position — so comparison shares warrant **stronger
  access control** than single-summary shares (§8).

---

## 8. Open decisions

- `DECIDE — recommended:` **ship the interactive link first; defer the PDF export**
  until static-provenance (§3, the hard column) is designed. Rationale: the link
  preserves every invariant with the least effort and stays current; a PDF cannot
  ship until it can print provenance without violating the doctrine. The link is
  also the form the doctrine §3.1 TODO has been waiting on.
- `DECIDE:` **the link access model.** Tokenized links are viewable by anyone who
  holds them. Recommend **revocable** links, **comparison links optionally
  email-gated or expiring** given they carry multiple buyers' terms (§7).
  Single-summary links can stay lightweight for the alpha. Confirm before share ships.

---

## 9. Deferred (explicit)

- **Visual layout** of the share surface — screen design, citing this file.
- **PDF export** — deferred until the static-provenance treatment exists (§8).
- **Seller-side interaction** beyond read/trace (questions back to the agent,
  acknowledgments) — post-alpha; the seller zone is read-only for now.
- **Re-share / forwarding** controls — what happens when a seller forwards the link
  onward. Real, given §7's leak concern; not scoped here.

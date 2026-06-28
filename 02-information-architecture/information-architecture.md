# Information Architecture

> **Status:** v0.2 — structure. The object model, the central organizing decision,
> the zones, and the route map are complete. Visual nav treatment (sidebar width,
> hover-expand) and screen layouts are *not* here — they belong to screen design.
> **Derives from:** `NORTH-STAR.md` (the spine), `trust-doctrine.md` (provenance
> zones, the shared-summary surface), `states-and-edge-cases.md` (the uncertainty
> that IA must route around).
> **Relationship:** this is the **map** — the nouns and how they nest. The agent and
> seller **workflows** (04, 05) are the journeys across it. IA defines the space;
> workflows define movement through it.

---

## 1. The object model

The core nouns and how they relate. Keep this small — the alpha needs five real
objects, not a schema.

```
Agent
  └── owns ──> Listing            (a property the agent is selling)
                 ├── identified by ──> Property identity   (§1B: APN, address)
                 ├── receives ──> Offer ──> has source ──> Document  (the RPA PDF, immutable)
                 │                  └── renders to ──> Summary        (the branded, shareable view)
                 └── has ──> Comparison   (over its Offers, scored against…)
                              └── uses ──> Seller-priority profile    (weighting; preset + customized)

Share        — a public, read-only emission of a Summary or a Comparison
Correction log — append-only record attached to an Offer's Document (states §3.1)
```

The relationships that matter most:

- **A Listing has many Offers; an Offer belongs to exactly one Listing.** This is
  the spine of the whole structure (see §2).
- **An Offer has one immutable source Document.** Corrections attach to the Offer's
  reading, never to the Document (doctrine §3.1, v0.5).
- **A Comparison is Listing-scoped** — it ranks *this listing's* offers, using *this
  listing's* seller-priority profile. There is no cross-listing comparison; offers
  on different properties are not comparable.
- **A Share is an emission, not a place** — a Summary or Comparison sent outward,
  read-only, to the public zone (§3).

---

## 2. The central decision: listing-scoped, offer-entered, address-joined

This is the IA decision everything else hangs on, and it sits directly on the
mission-scope resolution: *the mission governs the unit (the offer); comparison is a
multiple of it (the listing).* The IA has to hold both — and they pull in opposite
directions.

**The tension.** The agent's mental model is **listing-first**: "1517 Harvard St has
five offers." Comparison only has a home in a listing. But the **aha is
offer-first**: *upload one document → summary.* If the product makes the agent
create or pick a listing *before* they can upload, it puts a setup chore in front
of the magic moment and the aha dies on the doorstep.

**The resolution — don't choose; derive.** Organize the workspace around Listings
(matches the mental model, gives comparison its scope), but make the **entry action
a bare offer upload that requires no prior setup.** The Listing is *derived from the
contract*, not built before it:

- The RPA carries the property's identity in **§1B** — including the **Assessor's
  Parcel Number**, a unique parcel ID, plus the street address.
- On upload, extract that identity and **join the offer to a listing automatically**:
  on **APN when present** (canonical, no formatting drift), falling back to a
  **normalized address**, falling back to **agent confirmation**.
- The agent uploads offers; the offers *self-organize into listings underneath
  them.* The aha stays immediate; the listing structure forms for free.

**Why not the alternatives:**
- *Offer-flat (no listings):* comparison has nowhere to live, and the agent's
  property-centric mental model has no home. Rejected.
- *Listing-first (setup before upload):* a speed bump before the aha. Rejected.

**The edge this introduces** (and it's real): the join key can be uncertain. APN
blank or unreadable, address ambiguous, two offers on one property formatted
differently. This routes straight into the states grammar — an **unreadable** or
**low-confidence** property identity becomes an agent-confirm step ("Is this offer
for 1517 Harvard St?"), never a silent mis-file. A misrouted offer corrupts a
comparison, so this join is a high-stakes read, not a convenience.

### 2.1 Two intake channels, one reconciliation gate

Offers reach a listing two ways: the agent **uploads** them, or a buyer's agent
**emails** them in (the Postmark inbound path). Both auto-join to a listing by §1B
identity (§2). But the two channels must never silently merge into a comparison —
the agent decides what gets compared.

**The reconciliation gate.** When the agent uploads offers and inbound-email offers
are already present on the same listing, Docside presents **both sets as a list,
each offer labeled by buyer name (§1A)**, and asks whether to include both sets in
the comparison. Offers are ingested either way; the gate governs *comparison
participation*, not existence. Nothing enters a ranking the agent didn't put there.

Three things make this trustworthy, two of them entailed by the decision rather than
added to it:

- **Source is visible.** The list shows which set each offer came from (uploaded vs.
  emailed). Reconciling two channels is the whole point — the agent is deciding
  across a seam they need to see.
- **Duplicates are detected, not compared.** The same offer can arrive by *both*
  channels (the agent uploads a PDF that was also emailed). A duplicate slipping into
  a comparison would rank an offer against a copy of itself and corrupt the result —
  a doctrine §5 violation. Likely duplicates (same buyer §1A + same property §1B +
  same price §3A) are flagged in the list for the agent to resolve.
- **Per-offer control is entailed by dedup.** A set-level "use both sets?" is the
  headline action — but the moment Docside flags a duplicate, the agent must be able
  to drop *one specific offer.* So per-offer exclusion isn't an optional refinement;
  resolving a flagged duplicate *is* per-offer control. Set-level toggle by default;
  per-offer exclusion available for the duplicate, the withdrawn, the backup.

**The label's edge.** Buyer name (§1A) is an extracted field and can be unreadable
(states grammar). When it is, the offer carries a fallback handle — price + receipt
time, or source + sequence ("Emailed offer, received Tue 2 PM") — shown as *buyer
name unreadable*, never blank, never fabricated. The agent always gets something
recognizable to decide on.

---

## 3. The two zones

There are **two distinct information architectures**, not one, because they serve
different people under different constraints. Conflating them is a category error.

| | **Agent workspace** | **Share surface** |
|---|---|---|
| Who | the agent (authenticated) | the seller / co-op agent (public, no login) |
| Device | desktop-likely, rich | mobile-likely; may be a static PDF export |
| Contains | listings, offers, verify, compare, correction, manage | one Summary or one Comparison, read-only |
| Nav | full hierarchy (§4) | none — self-contained, no app chrome |
| Provenance | interactive (hover-to-source, two-pane) | must work **without** hover (doctrine §3.1 TODO) |
| Trust job | let the agent *check and vouch* | let the seller *understand and trace* |

The boundary between them **is the handoff seam** (folder 06). A Share crosses from
the authenticated zone into the public one — and everything the doctrine says about
provenance-reaching-the-seller, corrected-values-shown-as-corrected, and gaps-stay-
visible is enforced *at this crossing*. The share surface is where the trust doctrine
faces its hardest test, because it has the fewest affordances to lean on.

---

## 4. Navigation hierarchy

The agent-workspace structure. Each level maps to a spine stage.

```
Listings  (home — the agent's properties)
  └── Listing
        ├── Offers            (the offers on this property)          ── upload lands here
        │     └── Offer
        │           └── Verify workspace   (two-pane: Document | Summary)   ── verify
        │                 └── Share         ── share
        └── Comparison        (when N > 1, scored vs seller profile)  ── compare → share
```

**The two-pane verify workspace** is the one layout-adjacent thing IA must fix,
because it's structural, not cosmetic: the source **Document** on one side, the
extracted **Summary** on the other. This is **provenance made spatial** — the agent
checks the read against the contract without leaving the view, which is exactly what
"the agent earns the right to put their brand on it" (NORTH-STAR) requires. The
correction affordance (states §3.1) lives in this pane. How wide, how it collapses
on mobile — screen design's call; *that it is two panes* — IA's call.

---

## 5. Route map

Rough routes, pinned to the two zones. The public share route is the one that must
survive being opened cold, on a phone, by someone with no account.

| Route | Zone | Renders |
|---|---|---|
| `/` or `/listings` | agent | the agent's listings |
| `/listings/[id]` | agent | one listing: its offers + comparison entry |
| `/listings/[id]/compare` | agent | the comparison view (N > 1) |
| `/offers/[id]` | agent | the verify workspace (two-pane) for one offer |
| `/upload` | agent | the bare entry action; resolves to an offer + auto-joined listing |
| `/share/[token]` | **public** | a read-only Summary or Comparison — no chrome, no login |

The `/share/[token]` route is its own world: unauthenticated, tokenized,
mobile-first, and possibly mirrored as a static PDF. It is the share surface (§3) as
a URL.

---

## 6. Build-sequencing note

The IA is designed listing-scoped, but it can be *built* in the spine's own order,
and the address-join is what makes that clean:

1. **Activation IA first:** `/upload → /offers/[id] (verify) → /share`. A single
   offer needs no listing layer to deliver the aha. Offers still carry their §1B
   identity from day one.
2. **Retention IA second:** switch on the Listing grouping and `/compare`. Because
   offers already carry APN/address, the listing layer groups *existing* offers
   retroactively — no migration, no re-upload.

This matches NORTH-STAR (single-offer cycle = activation; comparison = retention)
and lets the alpha ship the activation spine without the comparison structure
blocking it — while never painting into a corner, because the join key was captured
all along.

---

## 7. Decisions (locked)

- ✅ **Inbound + uploaded offers reconcile at an agent-controlled gate** (§2.1).
  Inbound-email offers auto-join by §1B and are ingested, but on upload both sets
  are listed by buyer name (§1A) and the agent chooses whether both sets enter the
  comparison. Source visibility, cross-channel dedup, and per-offer exclusion are
  entailed; the unreadable-buyer-name fallback follows the states grammar.
- ✅ **The seller-priority profile is listing-scoped, seeded from agent-level
  presets** (§1). Each seller's priorities differ; agents have a default posture the
  presets capture.

Both feed the comparison screen directly, so they're locked before that work begins.

---

## 8. Deferred (explicit)

- **Visual nav treatment** — sidebar icon-rail width, hover-expand vs. icons-only —
  is screen design, not IA. IA fixes *what's in the nav*, not how it looks.
- **Team / TC multi-user** — multiple people on one listing, role separation. The
  alpha is single-agent; the object model has room for it (Agent → Listing) but it
  is not specified.
- **Listing lifecycle** — archived / closed / withdrawn states for a listing once a
  deal is done. Real, post-alpha.
- **Cross-device continuity** of the verify workspace (start on desktop, glance on
  mobile). Noted; follows screen design.

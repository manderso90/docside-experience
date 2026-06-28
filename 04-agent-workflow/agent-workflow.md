# Agent Workflow

> **Status:** v0.2 — journey. The modes, the temporal shape, the trust arc, the two
> loops, and the entry points are complete. This integrates prior specs into the
> agent's lived path; it does not re-decide them.
> **Derives from:** `NORTH-STAR.md` (the spine), `information-architecture.md` (the
> map, the two channels, the two zones), `states-and-edge-cases.md` (what happens
> when a step fails), `handoff.md` (the share crossing).
> **Relationship:** IA is the **map**; this is the **journey** across it. Where the
> spine is abstract (`upload → verify → share`), this is what the agent actually
> does, decides, and feels, in the order and at the pace it really happens.

---

## 0. Who the agent is

A listing agent or transaction coordinator representing a seller. High-stakes
context: their license, their client's biggest asset, a contract they're legally
responsible for understanding. Time-pressured, mobile half the time, and — this is
the load-bearing fact — **skeptical by default.** They have been handed slick tools
that quietly got things wrong, and a tool that misreads a purchase contract is worse
than no tool. The workflow does not get to assume trust. It has to earn it, in order,
on the way through.

---

## 1. Two modes — and real intake is reactive

The spine implies the agent *uploads*. In real life, the agent mostly *receives*.

- **Onboarding mode (active).** The agent tries Docside by uploading one offer they
  have in hand. Single offer, deliberate, low-commitment — "let me see if this thing
  is any good." This is the **aha** and the activation metric.
- **Operational mode (reactive).** In practice, offers arrive *to* the listing
  agent — a buyer's agent emails the RPA PDF, often several offers over a few days
  against an offer-review deadline. The agent's sustained life is processing offers
  that land, not hunting for files to upload.

These are not in tension; they're front door and house, the same shape as the
mission scope. The **upload aha is the front door** — the deliberate first taste of
the magic. The **reactive inbound flow is the house** — where the agent lives once
Docside is wired into how offers actually reach them (IA §2.1's two channels, with
*email as the dominant one*). That reframes the inbound path: it isn't an edge case
the reconciliation gate occasionally handles — it's the main way offers arrive, which
is exactly why the gate matters.

---

## 2. The temporal shape

The journey is **not one sitting.** It is stretched across the offer window and
paced by a deadline the agent doesn't control:

```
listing live ──► offers trickle in (days) ──► offer-review deadline ──► compare ──► present to seller
```

Offers accumulate over time, mostly by email, sometimes uploaded. The agent verifies
each as it lands (or batches near the deadline). The **compare-and-share moment
clusters at the deadline**, when the full set is finally in hand. This has three
design consequences the workflow must respect:

- **Verify is interruptible and resumable.** An agent verifies offer 3 of a possible
  7 on their phone between showings; offers 4–7 aren't here yet. State persists; the
  journey pauses and resumes without loss.
- **The set is open until the deadline.** "All offers in" is a moment, not an
  assumption — a comparison built before the deadline is provisional, and the product
  shouldn't imply finality the transaction hasn't reached.
- **Notification is an entry point** (§5). A new inbound offer pulls the agent back
  in; the workflow is re-entered, not restarted.

---

## 3. The trust arc

The emotional spine, because the whole product is a trust instrument and the agent's
trust is *built by the workflow*, not granted to it.

```
skeptic ──► checker ──► convinced ──► proud ──► reliant
```

- **Skeptic** (arrival): "An AI read my contract? I'll believe it when I've caught
  it lying."
- **Checker → convinced** (verify): the conversion point. The two-pane workspace
  lets the agent check the read against the contract, and the honest signals do the
  converting — provenance they can trace, an upfront "we couldn't read this,"
  corrections they can make. **The counterintuitive engine: honesty converts a
  skeptic faster than apparent perfection does.** A flawless-looking summary makes a
  professional ask "what's it hiding?"; a summary that admits its one gap earns the
  benefit of the doubt on everything else. This is *why* NORTH-STAR says the aha is
  earned at verify.
- **Proud** (share): the agent puts their brand on it and sends it. Looking good to
  their client *is* the aha landing.
- **Reliant** (return): offers arrive, the agent routes them through Docside without
  thinking about it. Trust has become habit.

The arc is the reason verify must not be streamlined into invisibility (states §3,
NORTH-STAR): skip the checking and you skip the conversion, and an unconverted agent
shares once and never returns.

---

## 4. The two loops

### 4.1 Activation loop — single offer (the aha)

1. **Intake.** Agent uploads an offer (onboarding) or forwards one in.
2. **Ingest.** Docside extracts and auto-joins it to a listing by §1B identity —
   silently if confident, with a confirm step if the property read is uncertain
   (IA §2). An ingestion failure surfaces here, named and actionable (states §2).
3. **Verify.** Agent lands in the two-pane workspace (contract | summary). Per field:
   **confirm**, **correct** (logged), or **mark unreadable** (states §1.1, §3.1).
   Low-confidence reads are resolved here. *This is the conversion.*
4. **Share-gate.** A high-stakes unreadable requires explicit acknowledgment before
   share; low-stakes rides along visibly (states §3).
5. **Share.** Agent sends the branded summary as a live link (handoff §8). The seller
   gets a clean, traceable summary; the agent looks good. **Aha.**

### 4.2 Depth loop — multiple offers (the retention engine)

1. **Accumulate.** Offers arrive across the window, mostly by email, some uploaded.
2. **Verify each** as they land or in a batch near the deadline (§2). Each offer
   passes through the activation loop's verify step.
3. **Reconcile** (at/near deadline). If offers came by both channels, the
   reconciliation gate lists both sets by buyer name, flags duplicates, and the agent
   chooses what enters the comparison (IA §2.1, states §4.1).
4. **Profile.** Agent selects and customizes the listing-scoped seller-priority
   profile — the weighting that reflects *this* seller's priorities (IA §1).
5. **Compare.** Offers rank against those priorities; the agent reviews a legible,
   term-based order (doctrine §4–§5). Near-ties are shown as near-ties (states §4).
6. **Share the comparison** with the seller, under stronger access control than a
   single summary (handoff §7). The seller chooses; the agent advises.

**The branch between the loops is N.** One offer → activation loop, share a summary.
Several → depth loop, share a comparison. The agent never declares which; it follows
from how many offers the listing holds.

---

## 5. Entry points

The workflow is a map with several doors, not a single track. Each re-enters the
journey at the right place rather than restarting it.

| Entry | Trigger | Lands at |
|---|---|---|
| **First-time** | new agent, onboarding | upload → activation loop |
| **New inbound offer** | an offer emails in; agent notified | verify the new offer; or reconcile if a set exists |
| **Returning to a listing** | agent opens a listing in progress | its offers + comparison entry (IA §4 nav) |
| **Deadline approaching** | the set is (nearly) complete | reconcile → compare → share |
| **Re-share** | seller asks again, or data changed | the live link is already current (handoff §5) |

---

## 6. The retention moment

Activation is one completed `upload → verify → share` cycle. **Retention is a
different act: the agent wires Docside into how offers actually reach them** — routing
their inbound offers in, so the reactive operational mode (§1) takes over. That
transition, from "I tried it once" to "this is where my offers go," is the real
retention event, and it is more about *intake habit* than about any single feature.
The depth loop is what makes that habit worth forming; the inbound path is what makes
it frictionless. The alpha tests activation; this is the line it has to cross to
matter beyond it.

---

## 7. Decisions (locked)

- ✅ **Inbound routing: agent forwards to a per-agent Docside address** for the alpha
  (simplest, no buyer-agent behavior change); auto-join (IA §2) sorts forwarded
  offers into the right listing by §1B. Build the inbound flow past the current
  Postmark hook on this basis. *Note: forwarding strips the buyer's-agent sender
  identity, but offer identity and labels come from RPA **content** (§1A buyer, §1B
  property), not the email envelope — so auto-join and buyer-name labeling are
  unaffected by who forwarded it.*
- ✅ **Verify confirm: one-tap confirm for a fully-clean read** (all high-stakes
  fields confident), **field-by-field whenever anything is flagged** — preserves the
  conversion where it matters without taxing the easy case.

---

## 8. Deferred (explicit)

- **Onboarding sequence** — the very first-run experience (first upload, first aha)
  as a designed flow, vs. just the activation loop. Belongs with screen design and
  user-research.
- **Notification design** — channel and content of the "new offer" nudge (§5). Real,
  not scoped here.
- **Team / TC handoffs** — when an agent and a coordinator share a listing's workflow.
  Follows the IA multi-user defer.
- **Post-share follow-through** — the agent advising the seller after the comparison
  goes out. Beyond the product's current surface.

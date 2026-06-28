# Screen — The Verify Workspace

> **Status:** v0.2 — screen spec. This specifies the layout, hierarchy, states, and
> interactions; it surfaces the design forks (§6) that should be settled before a
> built mockup. The mockup follows once §6 is confirmed.
> **Derives from:** essentially everything — `information-architecture.md` §4 (the
> two-pane structure), `trust-doctrine.md` §3.1–§3.2 (provenance, honest uncertainty,
> correction), `states-and-edge-cases.md` §1, §3, §3.1 (the state grammar, stakes-
> weighting, correction), `copy-guidelines.md` (the registers), `agent-workflow.md`
> §2–§3 (mobile, interruptible, the trust conversion).
> **Why this screen first:** every thread in the repo converged here. Verify is where
> the agent's skepticism turns to confidence (NORTH-STAR: *earned at verify*), so it
> is where the accumulated doctrine has to become pixels first.

---

## 0. The one organizing idea: provenance made spatial

The verify workspace is **two panes** — the source **Document** on one side, the
extracted **Summary** on the other — and the whole screen exists to make one
relationship physical:

> **Focus a value in the Summary, and the Document moves to where it came from.**

Provenance here is not a hover tooltip. It is the document pane *responding*. Tap
"Seller-paid buyer-broker comp" and the contract scrolls to §3G(3) and highlights it.
The agent checks the reading against the source without leaving the screen — which is
exactly what "the agent earns the right to put their brand on it" requires. The link
is **bidirectional**: tapping a clause in the document can surface the field it feeds.

Everything below serves this idea.

---

## 1. Layout — regions and hierarchy

```
┌─────────────────────────────────────────────────────────────┐
│  Context bar:  Listing · Buyer (§1A) · "Offer 2 of 5"        │
├──────────────────────────────┬──────────────────────────────┤
│                              │  NEEDS YOUR ATTENTION          │
│                              │   • unreadable / low-conf /    │
│      DOCUMENT (source)       │     high-stakes-unknown rows   │
│   the RPA, page images,      │                                │
│   scrolls + highlights to    │  ───────────────────────────   │
│   the focused field's source │  THE READING (grouped)         │
│                              │   Money · Timing · Contingency │
│                              │   · Terms                      │
│                              │                                │
├──────────────────────────────┴──────────────────────────────┤
│  Share ▸  (gated — see §4)                                   │
└─────────────────────────────────────────────────────────────┘
```

- **Context bar.** Which listing, which buyer (§1A), and progress through the set —
  grounding the agent in a workflow that spans days and many offers (agent-workflow
  §2). Minimal; not app-wide chrome (§6).
- **Document pane.** The immutable source (doctrine §3.1). Full RPA, scrollable, but
  it *follows the agent's focus* — auto-scrolling and highlighting the source of
  whatever Summary field is active.
- **Summary pane**, two stacked zones:
  - **Needs your attention** (top). Everything flagged — unreadable, low-confidence,
    high-stakes-unknown — rises here. This *is* stakes-weighted verify (states §3)
    made visual: the agent's eye lands first on what actually needs a human.
  - **The reading** (below). The full extracted summary, grouped for comprehension —
    **Money, Timing, Contingencies, Terms** — not in raw form order. Confident fields
    live here, scannable and mostly confirmable in bulk.
- **Share action.** Persistent, gated (§4).

The hierarchy inverts the usual "show everything equally": **attention first, clean
reading second.** The screen tells the agent where to look.

---

## 2. The state grammar, on screen

Every field state from states §1 must render **visibly distinct** — this screen is
where the grammar of absence either holds or collapses. Each gets its own visual
treatment (exact styling is the mockup's job; the *distinctions* are fixed here):

| State | On-screen treatment |
|---|---|
| Present — confident | the value, plain, in the reading zone |
| Present — agent-corrected | the value + a quiet "corrected · original: X" marker (doctrine §3.1 v0.5) |
| Low-confidence | in *Needs your attention*; value shown with a confirm/correct/mark control |
| Empty-on-form | "Not specified on this form" — visually unlike a value and unlike an error |
| Not-captured | "Not captured on this form" — visually unlike empty-on-form |
| Not-applicable | "Not applicable — all-cash purchase" — tied to its cause |
| Unreadable | "We couldn't read this field" — clearly *our* limitation, in the attention zone if high-stakes |

The cardinal rule from states §1 holds at the pixel level: **no two of these may look
alike.** A shared dash, blank, or grey "N/A" across any two is a defect the mockup
must not introduce.

---

## 3. Information design of a field row

Each Summary row carries, left to right (conceptually):

- **Label** — System voice, the vocabulary `label` verbatim ("Earnest money deposit").
- **Value or state** — Explanation voice for values; the §2 treatment for non-values.
- **Provenance handle** — the affordance that drives the document pane (§0); on the
  shared surface this becomes the static citation (handoff §3), but here it's live.
- **Action** — for flagged rows: confirm / correct / mark unreadable, inline.

Glosses (vocabulary §1.2) are available on demand, not always-on — the agent rarely
needs them; the seller will (seller-workflow §3). Same data, different default
exposure per surface.

---

## 4. Interactions

- **Confirm a clean read in one tap.** When no field is flagged, the whole reading is
  confirmable at once (agent-workflow §7). The screen doesn't force field-by-field
  busywork on a clean offer.
- **Resolve a flagged field inline.** Confirm the value as read, **correct** it (opens
  a small editor; the change is logged append-only, the original preserved — doctrine
  §3.1 v0.5, states §3.1), or **mark unreadable.** No modal detour; resolution happens
  in place.
- **Correction shows its work.** A corrected field immediately wears its "corrected ·
  original: X" marker, here and onward to the share (handoff §3).
- **The document follows focus.** Selecting any field drives the document pane (§0).
- **Share is gated.** Tapping Share with an unacknowledged high-stakes unknown raises
  the acknowledgment ("This summary couldn't read the purchase price — share
  anyway?") before proceeding (states §3). Low-stakes unknowns don't block.

---

## 5. Mobile — verify on a phone

Not an afterthought: the agent verifies offer 3 of 7 on their phone between showings
(agent-workflow §2). Two panes don't fit a phone, so the relationship from §0 has to
survive a single column.

**Strategy:** the **Summary is primary**; the Document is one tap away. Tapping a
field's provenance handle opens the contract **to that field's source** — provenance
becomes a *drill-down* instead of a side-by-side, but the same bidirectional link.
*Needs your attention* leads, so a thumb-scrolling agent hits the consequential
fields first. State persists; verify is interruptible and resumable mid-set.

The desktop two-pane and the mobile drill-down are **the same workspace at two
widths**, not two designs — the provenance link is the invariant; the layout degrades
gracefully around it.

---

## 6. Design forks (locked)

All five confirmed. Recorded with rationale; the mockup is built on them.

1. **Pane ratio (desktop).** Recommend **document-light at rest (≈40/60 doc/summary)
   — the summary is where the agent acts — widening the document dynamically when a
   field is focused.** Alternative: fixed 50/50 with a draggable divider.
2. **App nav / sidebar treatment.** The known open question (icon-rail width,
   hover-expand vs. icons-only). Recommend **a thin icons-only rail in verify** — the
   agent is in a focused task; nav shouldn't compete with the two panes. Hover-expand
   is fine elsewhere; verify stays quiet.
3. **Mobile strategy.** Recommend the **summary-primary + provenance-drill-down** of
   §5, over a tabbed Document/Summary or a stacked scroll.
4. **Document pane behavior.** Recommend **full document, auto-focusing** the active
   field's source — over showing only the relevant snippet. The agent sometimes needs
   to see a clause in context, not just the extracted line.
5. **Grouping order.** Recommend **attention-first, then Money / Timing /
   Contingencies / Terms** — comprehension order over raw form order.

---

## 7. Next & deferred

- **The mockup.** Once §6 is settled, I build an interactive mockup of the verify
  workspace (frontend-design skill, real design tokens) — desktop two-pane and the
  mobile drill-down.
- **Other screens, deferred to their own specs:** the comparison view (the depth
  loop's screen — `04`/`05` and `handoff` already feed it), the listings home, the
  share surface (its own constraints, handoff §3), the reconciliation gate (IA §2.1,
  states §4.1), upload/ingestion states (states §2).
- **Component extraction.** The two-pane workspace, the field row, the state markers,
  and the provenance handle are reusable primitives — they belong to
  `09-component-library/` once this screen's mockup proves their shape.

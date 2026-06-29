# Screen — [Name]

> **Status:** v0.1 — screen spec
> **Derives from:** [list source docs and the specific sections each contributes]
> **Owns:** [what this screen is the canonical home for]

---

## 0. The one organizing idea

*One sentence.* What spatial or conceptual metaphor unifies this screen? Everything
in the sections below serves this idea. If two people disagree about a component,
bring it back here first.

The organizing idea should derive from the **workflow moment** this screen occupies:
what the user's trust arc demands at this point, not what's technically available.

---

## 1. Layout — regions and hierarchy

A labeled ASCII sketch (boxes, not wireframes) showing every region. Then prose:
one paragraph per region explaining its trust job, not its contents.

```
┌─────────────────────────────┐
│                             │
│   [REGION A]                │
│                             │
├─────────────────────────────┤
│  [REGION B]   │  [REGION C] │
│               │             │
│               │             │
├─────────────────────────────┤
│  [REGION D — action]        │
└─────────────────────────────┘
```

**Region A.** What it does for trust. Who the reader is in this moment.
**Region B.** …
**Region C.** …
**Region D.** …

**Hierarchy principle.** State it: what the screen tells the user to look at first,
and why that ordering serves the trust obligation. The verify workspace inverts
"everything equally" to *attention first, reading second*; every spec must articulate
its hierarchy explicitly.

---

## 2. The state grammar, on screen

Map every relevant field state from `states-and-edge-cases.md` §1 to a visually
distinct on-screen treatment. The cardinal rule holds at the pixel level:

> **No two of these may look alike.** A shared dash, blank, or grey "N/A" is a
> defect the mockup must not introduce.

| State | On-screen treatment |
|---|---|
| Present — confident | … |
| Present — agent-corrected | … |
| Empty-on-form | … |
| Not-captured | … |
| Not-applicable | … |
| Unreadable | … |

Add any screen-specific states beyond the field-level grammar here (e.g., upload
failures, share-gate acknowledgments, comparison states).

---

## 3. Information design of an element

Pick the screen's **core repeating unit** (a field row, a comparison card, an offer
entry) and decompose it. Left-to-right (or top-to-bottom for stacked mobile) specify:

- **Label** — which copy register, which vocabulary `label` verbatim.
- **Value or state** — how a confident value renders vs. each absence state.
- **Provenance handle** — how the source-tracing affordance appears on *this*
  surface. On the verify workspace it is live (document pane responds); on the share
  surface it is a static inline §-citation. Name the form; don't defer.
- **Action** (if any) — what the user can do from this element. On the seller surface:
  none. On verify: confirm / correct / mark unreadable.

Glosses (vocabulary §1.2) — always-on or on-demand? Name the default for this
surface and why it differs from (or matches) the verify workspace.

---

## 4. Interactions & gates

List every user action and gate in this screen. For each:

- **Trigger** — what the user does (or what condition fires it)
- **Behavior** — what happens
- **Gate** (if any) — what prevents it or requires acknowledgment first

The share gate (states §3) is the canonical example: tapping Share with an
unacknowledged high-stakes unknown raises the acknowledgment prompt; low-stakes
unknowns don't block.

The seller surface is read-only: document all zero-interaction states explicitly —
"the seller cannot correct, cannot log in, cannot acknowledge." Zero is a design
decision, not an oversight.

---

## 5. Mobile / degraded environment

This section is not optional. The verify workspace degrades gracefully from two-pane
to a summary-primary drill-down. The share surface assumes mobile-primary.

Answer for each degradation:

- **Viewport narrowing (mobile).** What changes layout; what is preserved. Which
  regions stack, which collapse, which are hidden vs. secondary.
- **No hover.** Where did the spec lean on hover? How is that affordance carried at
  touch? (On the share surface: provenance is a tap, never a hover.)
- **Static PDF export.** If this surface might be exported: how does each invariant
  survive? Name the static form for every affordance that requires interactivity.
  (Inline §-citation printed, glosses footnoted, etc.) Reference handoff §3
  degradation matrix.
- **Accessibility baseline.** Minimum semantic obligations for this screen
  (contrast, ARIA roles, tap-target size). A detailed pass is deferred to screen
  design, but the baseline must be named.

---

## 6. Design forks (to confirm, then lock)

A named fork for every decision this spec can't make alone — where two reasonable
options exist and the choice will determine the mockup. For each fork:

- State the question.
- Give the two (or three) options with their trade-offs.
- Give a recommendation with rationale, citing the doctrine, workflow, or IA section
  that anchors it.
- Mark as **LOCKED** (decided here) or **DEFER** (named reason + named home for
  resolution).

**Every locked fork must be recorded in `11-design-decisions/decisions.md`** with a
`DEC-n` handle before this spec is considered complete.

**Rule:** a fork may not remain open indefinitely. Either lock it with rationale or
defer it explicitly with a reason and a home. "We haven't decided" is not a fork
state; it is a missing decision.

---

## 7. Deferred

An explicit list. Every deferral names a reason and a home. Nothing falls off — it
is either in scope (§§0–6) or explicitly named here with where it goes.

Format:
- **[What]** — [why deferred] → [home: `folder/`, next milestone, etc.]

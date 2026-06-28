# docside-experience

> **Design the world's most trustworthy way to understand a real estate contract.**

This repository is the **experience definition** for Docside — the design system,
trust doctrine, information architecture, workflows, and screen specs that govern how
the product looks, reads, and earns trust. It is the *what trust requires* layer; the
implementation lives in the separate `manderso90/docside` repo (see `CLAUDE.md`).

Everything here flows from the mission above, and from one binding principle:

> **The mission governs the unit; the doctrine governs every multiple of it.**

---

## Where to start

1. **`NORTH-STAR.md`** — the aha and the `upload → verify → share` spine. The one-page
   anchor; read it first.
2. **`00-foundations/trust-doctrine.md`** — how trust is earned: provenance, honest
   uncertainty, the inverted-ranking guarantee. Everything downstream derives from it.
3. **`00-foundations/domain-vocabulary.md`** — the contract-term → plain-language →
   form-location map, with the five translation hazards. The IP that copy depends on.

---

## The map

| Path | What it holds | Status |
|---|---|---|
| `NORTH-STAR.md` | aha · spine · one-sentence test | written |
| `00-foundations/` | trust doctrine · domain vocabulary | written |
| `01-user-research/` | interviews, JTBD, usability, funnel | stub |
| `02-information-architecture/` | object model · the two zones · routes | written |
| `03-critical-path/` | stage-by-stage elaboration of the spine | stub (anchored in NORTH-STAR) |
| `04-agent-workflow/` | the agent's journey: modes, trust arc, loops | written |
| `05-seller-workflow/` | the seller's single-pass read-only journey | written |
| `06-handoff/` | the agent→seller seam; the degradation matrix | written |
| `07-screen-design/` | the verify workspace spec + interactive mockup | written (first screen) |
| `08-states-and-edge-cases/` | the grammar of absence; failure as proof | written |
| `09-component-library/` | reusable primitives (row, state markers, panes) | stub (awaits screens) |
| `10-copy-guidelines/` | the four speakers · hazard rendering · worked specimen | written |
| `11-design-decisions/` | ADRs / decision log | stub |
| `assets/` | fonts, exports, static assets | stub |

---

## How the docs relate

```
                    NORTH-STAR  (hub: aha + spine + test)
                         │
        ┌──── 00-foundations: trust-doctrine ──── domain-vocabulary ────┐
        │              │                                  │              │
  08-states     10-copy-guidelines                  02-information-architecture
 (the grammar)   (+ worked-specimen)                  (the two zones)
        │              │                                  │
        └──────────────┴───────► 06-handoff ◄─────────────┘
                                     │
                 04-agent-workflow ──┴── 05-seller-workflow
                                     │
                          07-screen-design (verify workspace)
```

The doctrine is the source of truth. **If a downstream doc contradicts the doctrine or
`NORTH-STAR.md`, those win** until deliberately, version-bumped, changed at the source.

---

## Conventions

- Every doc opens with a **status line and version**; decisions are version-bumped
  there (mirroring `STATEMENT.md` discipline in the main repo).
- **Defer-lines over open backlogs:** every deferral names a reason and a home.
- **Form references are pinned to C.A.R. Form RPA, Revised 6/25**, verified against
  the actual form — not reconstructed from memory. A form revision requires
  re-grounding (see `domain-vocabulary.md` §6).
- See `CLAUDE.md` for the full working conventions and the cross-repo seam.

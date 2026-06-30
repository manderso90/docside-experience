# STATUS

> **What this is:** the one orientation page to read before opening the repo. It
> reflects the committed state and names what's next. When a section's state changes,
> update the row here — this is the canonical status surface (the README's table can
> point here rather than duplicate it).
> **Last updated:** 2026-06-30
> **One-line state:** the design system is substantially complete through the screen
> layer — foundations, trust specs, IA, both workflows, the handoff, two of four
> screens, and a started decision log are all written and committed. Two screens, user
> research, and the component library remain; the brand identity and the
> static-provenance "hard column" are parked-but-live.

---

## Section status

| Section | Artifact(s) | Ver | State |
|---|---|---|---|
| `/NORTH-STAR.md` | the aha + spine + one-sentence test | v0.1 | ✅ written |
| `00-foundations/` | trust-doctrine · domain-vocabulary · high-stakes-fields-pointer | v0.5 / v0.2 / v0.1 | ✅ written |
| `01-user-research/` | — | — | ⛔ stub (reasoned from first principles, not yet grounded) |
| `02-information-architecture/` | information-architecture | v0.2 | ✅ written |
| `03-critical-path/` | critical-path (spine index) | v0.1 | ✅ written |
| `04-agent-workflow/` | agent-workflow | v0.2 | ✅ written |
| `05-seller-workflow/` | seller-workflow | v0.2 | ✅ written |
| `06-handoff/` | handoff (form/channel + email delivery) | v0.2 | ✅ written |
| `07-screen-design/` | verify-workspace **+ mockup** · share-surface | v0.2 / v0.1 | ◑ 2 of 4 screens |
| `08-states-and-edge-cases/` | states-and-edge-cases | v0.3 | ✅ written |
| `09-component-library/` | — | — | ⛔ stub (awaits more screens + brand adoption) |
| `10-copy-guidelines/` | copy-guidelines · worked-specimen | v0.2 / v0.1 | ✅ written |
| `11-design-decisions/` | decisions (DEC-1 … DEC-8) | v0.1 | ◑ growing (DEC-7/8 added; ≈9 more indexed to backfill) |
| `_templates/` | screen-spec-template | v0.1 | ✅ one template |
| `assets/` | pointer to external brand files | — | pointer only |

**Screens:** verify ✅ (spec + interactive mockup) · share ✅ (spec; no mockup) ·
**upload ⛔ (not started)** · **comparison ⛔ (not started)**.

---

## Decisions logged

`11-design-decisions/decisions.md` holds the running log. Written in full:

- **DEC-1** — Share delivery: live link over both SMS and email; PDF deferred.
- **DEC-2…DEC-6** — the five share-surface forks (headline leads · §-citation
  always-visible inline · high-stakes unknowns at elevated weight · glosses always-on ·
  the non-laundering prohibition list).
- **DEC-7** — Comparison-share access control: email-gated recipient access, expiring +
  agent-revocable (resolves the handoff §8 open question).
- **DEC-8** — Default seller-priority dimensions & order: net to seller ▸ contingencies ▸
  financing strength ▸ close speed; user-controllable; suppress-on-unreadable.

An index of ~9 earlier locked decisions sits below them, to promote to full entries as
each comes up for review (the central IA decision, the reconciliation gate, the
correction/audit clause, the verify-workspace forks, etc.).

---

## What's next

**Recommended: the comparison-view screen spec** (`07-screen-design/comparison-view.md`).
Its plan is written and current — `07-screen-design/comparison-view-plan.md` (**v2.1**),
which incorporated an external review and Morris's decisions (DEC-7 access control, DEC-8
default dimensions). Both former blockers are resolved, so the spec is ready to write.

Every screen built so far — verify and share — lives on the doctrine's
*understanding-trust* surface (a single offer, made clear). The comparison view is the
**only** screen that exercises *ranking-trust*: legibility of order, honest weighting
against seller priorities, and the **inverted-ranking guarantee** — the most
product-specific guarantee in the doctrine, which exists *only* on this screen and has
never been rendered. It is also the retention engine (NORTH-STAR's depth loop). Speccing
it completes the design layer's coverage of both trust surfaces.

**Runner-up: the upload-flow spec** (`07-screen-design/upload-flow.md`) — completes the
activation triad (upload → verify → share). Lower-risk, because its hard parts (ingestion
failure states) are already specified in states §2.

**The condition that flips them:** if the activation cycle isn't yet working
end-to-end in practice and the alpha is blocked on it, do **upload** first and let
comparison follow.

---

## Parked, but live

| Thread | Status | Unblocks |
|---|---|---|
| **Brand identity** | inspiration, not adopted (external; pointer in `assets/`) | every mockup, the component library, the verify-mockup reskin |
| **Static-provenance "hard column"** | open — the source appendix is undesigned (DEC-3) | the future PDF-form spec (handoff §9); email-the-PDF |
| **Link access-control model** | open decision (handoff §8) | safe share links once email/forwarding is in scope |

---

## Where this fits (context, not verified here)

This is the **specification** repo. The implementation lives in `manderso90/docside`
(auth, email pipeline, extraction, scoring, comparison UI). The whole project's arc is
the two converging toward the **closed alpha**, whose success metric is agents
completing the full `upload → verify → share` cycle. The experience repo is now mature
enough to *drive* that convergence rather than trail it — which makes a **cross-repo
alignment check** (does what's built match what these specs now require?) the real path
to the alpha, alongside the screens above.

---

## How to use this repo

Doctrine-first. Before any design task, read in order: `NORTH-STAR.md` →
`00-foundations/trust-doctrine.md` → the relevant `domain-vocabulary.md` entries → the
closest existing screen spec or workflow doc. Derive from specs; don't invent laterally.
Every change passes the doctrine §7 test (more trustworthy, or only more finished?) and
the NORTH-STAR test (on the path to a share-worthy summary?). See `CLAUDE.md` for the
full conventions and the cross-repo seam.

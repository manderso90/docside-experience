# STATUS

> **What this is:** the one orientation page to read before opening the repo. It
> reflects the committed state and names what's next. When a section's state changes,
> update the row here — this is the canonical status surface (the README's table can
> point here rather than duplicate it).
> **Last updated:** 2026-06-30
> **One-line state:** the design system is substantially complete through the screen
> layer — foundations, trust specs, IA, both workflows, the handoff, three of four
> screens, and a growing decision log are all written and committed. The comparison view
> is now specced (all three ranking-trust `TODO(design)` markers resolved). One screen
> (upload), user research, and the component library remain; the brand identity and the
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
| `07-screen-design/` | verify-workspace **+ mockup** · share-surface · comparison-view | v0.2 / v0.1 / v0.1 | ◑ 3 of 4 screens |
| `08-states-and-edge-cases/` | states-and-edge-cases | v0.3 | ✅ written |
| `09-component-library/` | — | — | ⛔ stub (awaits more screens + brand adoption) |
| `10-copy-guidelines/` | copy-guidelines · worked-specimen | v0.2 / v0.1 | ✅ written |
| `11-design-decisions/` | decisions (DEC-1 … DEC-17) | v0.1 | ◑ growing (DEC-9…DEC-17 added for comparison; Forks A/B + ≈13 more indexed to backfill) |
| `_templates/` | screen-spec-template | v0.1 | ✅ one template |
| `assets/` | pointer to external brand files | — | pointer only |

**Screens:** verify ✅ (spec + interactive mockup) · share ✅ (spec; no mockup) ·
comparison ✅ (spec; no mockup — mockup is the LOCK-pending-mockup trigger for Forks
C/D, E, I) · **upload ⛔ (not started)**.

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
- **DEC-9…DEC-17** — the comparison-view forks: hybrid ranked-spine + matrix, offers as
  rows (9) · basis line + Customize-expands-in-place (10) · three-tier suppression /
  withheld order (11, runtime-dependent) · net computed-only-from-traceable-components,
  else suppressed (12) · legibility = matrix + adjacent preview + pairwise delta (13) ·
  live re-ranking, mobile→apply-then (14) · per-offer atom in a side pane/drill-down linked
  to verify (15) · free-text "Other terms," never scored (16) · set-provisional marker (17).
  DEC-9/12/14 are LOCK-pending-mockup.

An index of earlier locked decisions sits below them (now including comparison Forks A/B —
two-doc split, gate-as-sibling), to promote to full entries as each comes up for review
(the central IA decision, the reconciliation gate, the correction/audit clause, the
verify-workspace forks, etc.).

---

## What's next

**Done since last update: the comparison-view screen spec**
(`07-screen-design/comparison-view.md`, v0.1) — written from the plan
(`comparison-view-plan.md` v3.0), resolving all three ranking-trust `TODO(design)` markers
(§4.1 legibility, §4.2 honest weighting, §5 inverted-ranking guarantee) and locking Forks
C–K as DEC-9…DEC-17. The comparison view was the **only** screen exercising *ranking-trust*
(the rest live on the *understanding-trust* surface), so this completes the design layer's
coverage of both trust surfaces. Two follow-ons are now briefed but unwritten:
`comparison-share-surface.md` (Appendix B of the spec) and `reconciliation-gate.md` (the
upstream dependency).

**Recommended next: the comparison mockup** — it is the LOCK-pending-mockup trigger for
Forks C/D (does the matrix read as a scoreboard?), E (live re-rank on mobile), and I (net
suppression on a real packet). Blocked only on brand adoption for visual tokens.

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
| **Re-share / forwarding UX** | comparison-share access model decided (DEC-7); the re-invite / who-has-access *screen flow* is downstream | the comparison-share surface spec |

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

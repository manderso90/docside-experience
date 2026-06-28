# North Star

> **Status:** v0.1 — anchor. Deliberately short. This is the file you re-read to
> reorient, so it stays glanceable. Detail lives in `03-critical-path/`; trust
> mechanics live in `00-foundations/trust-doctrine.md`. This file points at both.

---

## The aha

> **Upload one document → see a clean, accurate, professional summary the agent is
> proud to put their brand on.**

That is the moment the product earns. Everything in this repo either moves an agent
toward it or is off the path.

The deeper value — **multi-offer comparison against seller priorities** — is not a
second aha. It is the depth that earns *retention* once the first aha has landed.
The mission governs the unit; comparison is a multiple of it (doctrine, binding
principle).

---

## What activation means

Activation is **the full `upload → verify → share` cycle**, not the first upload.
An agent who uploads and stops has not been activated; an agent who uploads,
confirms the read, and sends a summary they're proud of has.

- **Alpha:** a closed cohort of **15–25 agents** (not 200–300). Depth of completed
  cycles over breadth of signups.
- **The metric is the cycle, not the click.**

---

## The spine

**Single offer — the activation path:**

```
upload  →  verify  →  share
```

**Many offers — the depth that retains (N > 1):**

```
upload 1…N  →  verify each  →  compare  →  share
```

Comparison is not a separate path. It is the same spine, fanning out where there is
more than one offer, then converging back to share.

### Each stage owes a trust obligation

The spine is not just a flow; every stage has a named thing it must get right, and
each maps to a foundation already written.

| Stage | What happens | Trust obligation | Anchored in |
|---|---|---|---|
| **Upload** | the contract enters | don't silently mangle the input; an unreadable file is *reported*, not faked | doctrine §3.2; the `ocr_no_text` guard; "the extension lies" (a `.pdf` was a zip) |
| **Verify** | the agent checks the read before their name goes on it | honest uncertainty (present / empty-on-form / unreadable) and provenance, surfaced so the agent can actually check | doctrine §3.1, §3.2; copy three-way grammar; hazard rules |
| **Compare** *(N>1)* | offers ranked against seller priorities | legible order, honest user-controllable weighting, no ranking from a guessed number | doctrine §4, §5; the inverted-ranking guarantee |
| **Share** | the branded summary goes out | term-based explanation, free text quoted verbatim, and provenance that **reaches the seller**, not just the agent | doctrine §3.1 (shared-summary decision), §3.3; the worked specimen |

The aha is *won* at **share** (the agent is proud to send it) but it is *earned* at
**verify** (the agent trusted the read enough to put their name on it). A share that
the agent didn't really verify is a hollow aha — and the first time the seller
catches an error, trust is gone. So verify is not a checkpoint to minimize; it is
where the brand-on-it confidence is built.

---

## The one-sentence test (experience-repo level)

Before any screen, flow, component, or copy change ships:

> **Does this move the agent closer to a summary they're proud to put their brand
> on — through upload, verify, or share — or does it sit outside that path?**

"Outside the path" is not automatically wrong, but it must justify itself against
this question, the way every change is checked against §17 in the main repo. This
is the experience-repo companion to the doctrine's §7 test: §7 asks *is it
trustworthy?*; this asks *is it on the path?* A change should pass both.

---

## How to use this file

- **Scope-check folders against it.** Every folder in this repo should trace to a
  stage of the spine or to the foundations the stages depend on. A folder that
  can't is a candidate for deletion, not expansion.
- **It is the hub, not the detail.** The aha and spine are settled here; the
  stage-by-stage walkthrough, screen flows, and edge cases live downstream and cite
  back to this anchor.
- **If a downstream doc contradicts this file, this file wins** until it is
  deliberately, version-bumped, changed here.

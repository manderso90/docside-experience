# HIGH_STAKES_FIELD_KEYS — Pointer

> **Status:** v0.1 — pointer
> **What this is:** a governance pointer, not a definition. The list itself lives in
> the main repo (`manderso90/docside`). This file names what depends on it here, why
> a fork would be worse than none, and how to find the authoritative source.

---

## 1. Where it lives

`HIGH_STAKES_FIELD_KEYS` is **defined in the main repo** (`manderso90/docside`).

Its precise location within that repo is **to be confirmed against the current
codebase** before citing it — likely the Zod schema for the extracted offer, the
shared constants layer, or the field-metadata file that feeds the extraction
pipeline. This repo does not assert or copy that location; the main repo's file
system and git history are authoritative.

**How to find it:** search the main repo for `HIGH_STAKES_FIELD_KEYS` (exact
string). It may also be named as an enum or a typed array; the search pattern is the
right tool, not this pointer.

---

## 2. What depends on it here

Two distinct gates reference this list by name; both treat it as a single-source
import, not a locally maintained copy:

1. **Stakes-weighted verify gate** (`08-states-and-edge-cases.md` §3) — an
   unreadable or low-confidence read in a `HIGH_STAKES_FIELD_KEY` field (purchase
   price, financing type, close date, contingencies, buyer-broker comp) requires an
   explicit agent acknowledgment before the share can proceed. Low-stakes unknowns
   do not gate share. The gate exists at the verify/share boundary, in the
   **agent's** workspace — not on the seller surface.

2. **Share-time acknowledgment in the agent handoff** (`06-handoff/handoff.md` §8 ·
   `08-states-and-edge-cases.md` §3) — when the agent shares a summary containing a
   high-stakes unknown, the acknowledgment prompt ("This summary couldn't read the
   purchase price — share anyway?") surfaces *exactly the fields* in
   `HIGH_STAKES_FIELD_KEYS`, and no others. The list's scope determines the gate's
   scope directly.

Both of these are the **agent's** concern at verify/share time. The seller surface
is read-only; the seller does not acknowledge anything. High-stakes unknowns are
**displayed honestly** to the seller — see `07-screen-design/share-surface.md` §2
and §6 — but the *gate* is upstream, already closed before the summary leaves the
agent's hands.

---

## 3. Governance rule: single-source, never a fork

> **A stale copy here is worse than no copy.**

If this pointer contained a local copy of the list, it would inevitably diverge from
the main repo as fields are added, renamed, or reclassified. A diverged copy means:

- The verify gate runs against the wrong set of fields.
- The share acknowledgment fires on the wrong unknowns.
- The seller sees a prominence treatment (share-surface.md §6) that doesn't match
  what the agent was asked to acknowledge.

All three silently undermine trust at the most consequential moments in the product.
The cost of looking up the authoritative list is lower than the cost of any one of
those failures.

**Rule:** when an experience-repo spec needs to reference a specific field key,
cite the identifier by name (e.g., `purchase_price`) and note it is in
`HIGH_STAKES_FIELD_KEYS` — do not reproduce the set. The main repo's source is the
only truth; this pointer is the seam.

---

## 4. Cross-repo sync obligation (for CLAUDE.md tracking)

This file records the dependency; `CLAUDE.md`'s cross-repo seam section governs how
to handle it. When the main repo reclassifies a field (adds, removes, or renames a
key in `HIGH_STAKES_FIELD_KEYS`), both the verify gate behavior and the
share-surface honest-display treatment must be reviewed for consistency. Neither doc
needs to change its *principle*; the field set it applies to may change.

---
output:
  pdf_document:
    keep_tex: true
    latex_engine: lualatex
    extra_dependencies: ["mathtools", "amsmath", "amssymb"]
monofont: "Menlo"
---

# Job Map — Schema Generalization Plan

*Written 2026-05-27. Goal: evolve Job Map from a single-purpose OMFS tool into a
flexible app where any couple (or individual) is guided through setup and the
"role-specific" fields are generated from their own field/position rather than
hardcoded to oral surgery.*

## Guiding principles (the safety system)

These are non-negotiable because this is a live, data-bearing personal tool:

1. **Never edit the live file directly.** All work happens on a copy
   (`index_refactor.html`); the live `index.html` is only overwritten after
   in-browser testing, and a dated backup is made first.
2. **The Google Sheet column names are the data contract.** Saving/loading
   loops over a fixed list of field *keys* (`EXTRA_FIELDS`). As long as those
   keys are never renamed, no refactor can lose or corrupt stored data — only
   how fields are *displayed* changes.
3. **Verify every step two ways:** a JavaScript syntax check, then an
   in-browser look. Promote to live only when both pass.
4. **One small, reversible piece at a time.** Each phase below is independently
   shippable and independently revertible (git, or the dated backup file).

## Phase 0 — The schema seam *(DONE, now live)*

A single `CAREER_SCHEMA` object is the one source of truth for the
role-specific field group (formerly the hardcoded "OMFS specifics"). The
add-job **form** and both **map popups** now generate those fields by looping
over the schema instead of repeating hardcoded HTML. This is the structural
change everything else builds on, and it has been in daily use through ~15
build iterations without affecting data. *Risk realized: none.*

## Phase 1 — Route the Details table through the schema *(SAFE — do first)*

**Goal.** The big "Details" view (`renderJobDetails`) still lists the
role-specific fields by hand. Make it read from `CAREER_SCHEMA` like the form
and popups already do, so *every* surface comes from one place.

**Touches.** One render function, display only. No data, no save/load.

**Risk.** Low. The worst case is a cosmetic re-ordering of the Details list,
which is visible immediately and trivially adjusted.

**Verify.** Open several jobs' Details; confirm every role field appears, with
the right labels, and the financial rows (production, total comp) stay put.

**Rollback.** Revert the single function; nothing else depends on it.

## Phase 2 — De-gender the people model *(LOW–MEDIUM)*

**Goal.** Replace hardcoded "His / Her" language with names drawn from a
`profile.people` list, so the app fits any pairing (or a single person). "His
Impressions" becomes "{name}'s Impressions," "Her situation" becomes
"{name}'s situation," etc.

**Touches.** Many label strings and the profile object. The underlying data
keys (`hisExcite`, `herFit`, …) can stay as internal keys at first; only the
*displayed* labels change. This keeps it low-risk.

**Risk.** Medium, only because it touches many strings. Mitigated by doing it
section by section (form headers, then modals, then the score panel), verifying
after each.

**Verify.** Set two names in Profile; confirm every visible "his/her" reflects
the names; confirm scores and saved data are unchanged.

## Phase 3 — Career field-set templates *(MEDIUM)*

**Goal.** Ship a small library of starter schemas — e.g. *Surgical specialty
(OMFS)*, *Physician (employed)*, *Academic / faculty*, *Attorney*,
*Software engineer*, *Generic professional* — and a picker (in Settings) that
swaps which template `CAREER_SCHEMA` uses. The user can then rename/add/remove
fields from the chosen starter.

**Touches.** Adds a template array and a settings control; persists the choice.
Because fields are keyed by name, switching templates never destroys data
entered under other keys — it just stops *showing* fields the new template
omits (they remain in the sheet, recoverable).

**Risk.** Medium. Main care point: a clean editing UI for fields, and making
sure a template switch never silently drops stored values.

**Verify.** Switch templates; confirm form/popups/Details all update together;
confirm a job saved under one template keeps its data when viewed under
another.

## Phase 4 — Guided first-run setup wizard *(BIGGER — most caution)*

**Goal.** On first run (no profile yet), walk the user through: who's searching
(one person or a couple) and names; each person's current field, role, and
city; which career drives the move vs. trails; home cities / family anchors;
a field template to start from; and a few plain-language weight questions. The
wizard writes `profile`, the schema choice, `weights`, `destinations`, and
`people` — all of which already have storage keys, so the data plumbing exists.

**Touches.** A new multi-step flow and first-run detection. This is the largest
piece and the one most worth building behind a flag and testing hardest.

**Risk.** Higher (new UI surface, conditional logic). Mitigated by building it
as an additive overlay that can be skipped, and never letting it overwrite an
existing profile.

**Verify.** Run it in a fresh state; confirm it populates everything correctly;
confirm it never triggers for an existing user with data.

## Phase 5 — Optional: AI-assisted field suggestion *(DEFER)*

"Describe your field and I'll suggest what to track." Genuinely useful, but it
requires calling a model at runtime, which means an API key and a small backend
— a different deployment story than today's static page + Sheet. Treat as a
nice-to-have layered on top of the curated template library, not a dependency.

## Prerequisite before this becomes an app for *other* people

The Apps Script `/exec` URL currently lives in the public repo. Generalizing
for other users makes a shared-secret-in-public-code problem worse, not better.
Securing the sheet (token + removing the hardcoded URL) should land before any
public, multi-user version — independent of the phases above, but a gate on
"real app for strangers."

## Suggested order

Phase 1 next (safe, satisfying, completes the "one source of truth" story).
Then 2. Then 3. Decide on 4 only once 1–3 feel solid. 5 and the security gate
whenever the multi-user ambition becomes concrete.

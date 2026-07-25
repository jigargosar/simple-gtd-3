# Concerns

Raised 2026-07-25, after reading `simplegtd_spec_v3_004.md` in full, spike 001
in full, and parts of spike 002. Nothing here has been acted on.

## What the spikes prove the spec does not need to say

Spike 002 never saw spike 001. Where the two landed in the same place
independently, convention is doing the work and the spec can stay quiet.

- The keymap. Both picked `c` capture, `/` search, `?` help, `1`/`2`/`3`
  filters, `j`/`k` navigation, `x` and `Space` for done, `Alt`+arrows to
  reorder, `Ctrl+Z` undo, `m` move, `s` new section, `Enter` to edit. The spec
  names zero keys.
- Delete protection. Both split it the same way: undo for a task, confirm
  dialog for a section. The spec says only "protected against accidental
  deletion".
- Shape. Sticky header, capture bar on top, segmented All/Active/Done, chevron
  section tabs, "Add a task" at the foot of each card, checkbox left of a
  one-line task, cursor row marked with a left bar.
- Both invented a named person in the seed data. That is a model artifact, not
  a spec finding.

## Where the spec genuinely leaves room

The two spikes diverged here, so these are real open decisions.

- **Control visibility.** 001 hides every section tool until hover. 002 shows
  pencil / up / down / trash at rest. Opposite answers.
- **Capture shape.** 001 puts the destination inline in the field, no submit
  button. 002 gives capture its own row with a destination dropdown, an
  explicit `FILE →` button, and a teaching hint line underneath.
- **Navigation model.** 001 uses `gg` / `G`. 002 uses `Home` / `End` plus
  `→` / `←` to step in and out of a row's buttons.
- **Help organisation.** 001 groups by verb, 002 by object.
- **Visual direction.** Light risograph versus dark green. Nothing in common.

## Drag and drop — both built it, neither documented it

Both spikes made task rows and section tabs `draggable`, and both left it
almost undiscoverable. The spec never mentions dragging. It should either
require it or rule it out, because right now every spike invents it and then
hides it.

## Spec defects

- Non-negotiables is a placeholder. Without it there is no pass/fail gate, so
  spikes can only be preferred, not judged.
- Capture is a placeholder, yet the spec calls the app "a capture surface".
  Better as an intent in Non-negotiables than as a section to fill.
- Pending item 3 is stale — it names `functional-indexing`, already corrected
  to `fractional-indexing` in commit 5e65b5e and in the Data model section.
- Sections are never stated to be reorderable, though Data model implies it.
- Undo is never mentioned. Both spikes built it anyway.
- No stack is named, and nothing says what a spike may substitute. This is why
  001 hand-ported `fractional-indexing` rather than importing it.
- `localStorage` is named without a schema version, without a rule for corrupt
  data, and without saying what happens when two tabs write at once.
- "A task is a line of text" pins presentation, and duplicates the next
  sentence, which already rules out due dates, tags, notes and subtasks.
- "so only its header remains" is mechanism, not requirement.

## Spike 001 defects

Verified by reading the file.

- `dropTask` never expands a collapsed target section, though `moveRow` and
  `askMoveTask` both do. Drop a task on a collapsed section and it disappears
  into it with no feedback.
- `dragover` sets `data-hover` on a section, and no CSS rule exists for it.
  Dropping on a section's empty area gives no feedback at all.
- The drag grip is `opacity: 0` at rest, 22px wide, `aria-hidden`, and a
  non-focusable `span`. Mouse-only, and invisible until hovered.
- The section tab is draggable with no affordance and no mention in help.
- Corrupt stored state falls back to the seed set, silently replacing real
  data.
- `render()` rebuilds the column's `innerHTML` wholesale then restores focus by
  hand. Works here, has no React equivalent, and is the fiddliest code in the
  file.
- Pink carries three meanings — done, cursor row, cursor section.

## Spike 002 defects

From partial reading and screenshots. Less thorough than 001 above.

- A collapsed section can be renamed, leaving an empty card strip below the
  rename field.
- `renameSection` saves without re-rendering; the redraw depends on the caller.

## Process risks

- The instruction's read restriction is the only thing keeping spikes
  independent. If a session ignores it, or shares context with another, the
  comparison is worthless.
- All spikes must run on the same model, or the comparison measures the model
  rather than the spec.
- Each spike's up-front questions are the under-specification data. Log them
  before answering.
- Decide in advance what to do if all four converge. Then there is no design
  choice left and the pick is aesthetic — a fine outcome, but worth knowing
  first.

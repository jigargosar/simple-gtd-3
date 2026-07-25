# Caveats

Limits on everything in `concerns.md`, and on anything I said in the session of
2026-07-25. Read this before trusting a finding.

## The biggest one: convergence may be the model, not the spec

Spikes 001 and 002 agreed on the keymap, on the delete-protection split, and on
the overall shape. I read that as evidence the spec is clear enough to leave
those unstated.

It might instead be evidence that the same model reaches for the same defaults.
Both spikes also independently invented a seed persona called Priya, which no
spec could have caused. That is the same phenomenon with the spec removed, and
it should lower confidence in the keymap finding too.

Two ways to tell them apart, neither done:

- Run a spike on a different model and see whether the keymap still converges.
- Run a spike against a deliberately vaguer spec and see whether convergence
  drops.

Until one of those happens, treat "the spec does not need to say this" as a
hypothesis.

## Sample size

Two spikes. Agreement between two runs is weak evidence either way. Disagreement
between two runs is stronger — it proves the spec permits both.

## What I actually read

- `simplegtd_spec_v3_004.md` — in full.
- `simplegtd_dashboard_v3_001.html` — in full, both passes.
- `simplegtd_dashboard_v3_002.html` — fragments only: the section and task
  render functions, the click dispatch, `addSection`, `renameSection`,
  `deleteSection`, and a grep for rename-related names. Every 002 finding is
  therefore shallower than the 001 findings, and 002 may hold defects as bad as
  001's that I have not looked for.
- No other file in the repo. Not `package.json`, not any config, not the git
  history beyond the four commit subjects shown at session start.

## Things I asserted and had to correct

- I said spike 002 has no drag-and-drop. It does — task rows and section tabs
  are both `draggable`, same as 001.
- I said renaming a section in 002 hides its tasks. Collapse hides them.
  Renaming a collapsed section is the actual, much smaller flaw.
- I said 002's console errors climbed from 1 to 3. The error count stayed at 1;
  the DevTools *Issues* count is what changed.
- I said the spec pins the interaction design. It pins the macro layout and the
  action list. Capture is a placeholder, so most of the interaction design is
  open.

Three corrections in one session on claims made from screenshots. Weight any
screenshot-derived statement accordingly.

## Unverified claims carried over from the spikes themselves

- 001 says its inlined order-key code is faithful to `fractional-indexing`
  v4.0.0. I did not diff it against the real library. Its own load-time
  self-check covers four cases only.
- 001 annotates contrast ratios in CSS comments. Those are the spike's numbers,
  not measured by me.
- I read accessibility problems out of the code. No screen reader, no keyboard
  walkthrough, no automated a11y pass was run against either spike.
- The 002 collapsed-rename flaw is inferred from `renderSection` plus a
  screenshot. Not reproduced.

## Stack claims

Any mention of React, TypeScript, Vite, Tailwind or pnpm as "the build stack"
comes from the global CLAUDE.md preference, not from this repo. I never looked
for a `package.json`, so I do not know whether app code exists at all, or what
it uses.

## What was proposed and never done

- The spec was not edited. There is no `v3_005`. Every spec fragment I drafted
  is a draft only.
- `inst.md` is a reconstruction. Spike 001's original prompt was never
  available to me; the instruction was rebuilt from the spec plus the
  constraints 001 visibly obeyed.
- Empty placeholder files for spikes 003 and 004 were discussed and never
  created.
- The five-task comparison protocol for judging spikes was proposed and not
  adopted.

## Method risks still open

- Nothing enforces the read restriction in `inst.md` beyond the instruction
  itself. A session that ignores it silently invalidates its own spike.
- All spikes must run on the same model for the comparison to be about the
  spec. See the first section — this cuts both ways.
- Each spike's up-front questions are the under-specification data. They are
  worth logging before they are answered, and none have been logged so far.

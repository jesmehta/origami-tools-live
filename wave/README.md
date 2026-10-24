# Wave Generator

Single-file HTML tool (`index.html`, open directly — no build, no server)
that covers the material with fold lines in both x and y, spaced
alternately by a **step** `s` and a **jump** `j`. Same sheet, margins, grid,
zoom/pan, project save/load and SVG/PNG/ZIP export as the other tools
(`common/`).

## Why it exists

Requested 2026-10-18 as "a new tool based on same framework of paper
sizing, interaction, export", with these inputs:

- step size `s` — 8–15 mm
- jump size `j` — 2s by default, ± s as an optional field
- edge bend — yes / no
- anchor — corner / centre

Follow-up the same day: "defaults to square papers, dont allow partial steps
along the edge, expand or shrink the black margin to give exact fit".

## The pattern

The material is fitted to **whole gaps** — no partial step or jump at any
edge. The margin fields are the *nominal* margin (dashed grey on screen);
the cut outline (black) moves in or out from it to the nearest gap
boundary, never leaving less than 5 mm of margin (`MIN_M`). The status bar
gives each axis's material length and resulting margins (L/R, B/T). Along
each axis the gaps run:

| Edge bend | Sequence |
|---|---|
| off | s, j, s, j … |
| on  | s, s, j, s, j … (an extra step first) |

x and y use the same sequence (x from the left, y from the bottom).

- **Corner** — the left and bottom edges stay at the nominal margin (◆ at
  the lower-left corner); the sequence runs right and up, and the right / top
  edges land on whichever gap boundary is nearest the nominal margin. That
  last panel can be a step or a jump.
- **Centre** — `s (j s)^(k−1)`, plus the extra edge-bend step at **both**
  ends when edge bend is on, with the step count `k` whose length is nearest
  the nominal material; centred, so it is symmetric in x and y, starts and
  ends on a step, and both margins are equal.

If not even one step fits, the status bar says so and nothing is drawn.
The outermost gap boundaries are the cut, so they are not also drawn as
folds.

## Using it

- **Steps** panel: *Step s* (slider + field, 8–15 mm). *Custom jump* off →
  `j = 2s` (the jump field shows it, greyed). On → set `j` anywhere in
  s–3s; changing `s` keeps a custom `j` clamped into the new range.
  *Edge bend*, *Anchor* (Corner / Centre).
- No dragging: wheel zooms, drag pans, *Fit view* resets.
- Export file names carry the parameters:
  `wave_s10_j20[_edge]_corner|center_<stamp>.svg|png|zip`.

## Decisions

- **Margins are nominal; the cut outline fits the pattern** (unlike the other
  tools, where the margin outline is fixed and the pattern is cropped). Nearest
  boundary in either direction, so a margin can grow or shrink; floor of 5 mm
  (the shared margin minimum) so the cut never runs off the sheet edge.
- **Default sheet: 270 square** (at s = 10, j = 20, it fits exactly at 10 mm
  margins).
- **Edge bend in centre mode is applied at both ends**, since centre mode is
  defined as symmetric.
- **One fold colour** for all lines; no step/jump or mountain/valley
  distinction. Confirmed by the user as not needed (2026-10-18).
- **Corner mode may end on a jump-wide panel** at the right / top edge —
  whichever whole-gap boundary is nearest the nominal margin, step or jump.
  Confirmed by the user as fine (2026-10-18); no step-only filter.
- `j` is stored even while *Custom jump* is off, so toggling it back on
  restores the last custom value.

## Changelog

- 2026-10-18 — first version.
- 2026-10-18 — square default sheet (270 × 270); no partial gaps: the cut
  outline snaps to the nearest whole-gap boundary, nominal margin shown
  dashed, effective margins in the status bar.
- 2026-10-18 — renamed from *Step Grid* to *Wave Generator*: folder
  `step-grid/` → `wave/`, export names `step-grid_…` → `wave_…`, project
  `tool` id `step-grid` → `wave` (no saved projects existed yet, so no
  migration).

## TODO / watch out for

- The edge-bend reading ("start with an extra s" = an extra step *before*
  the first s, both ends when centred) is an interpretation of the brief,
  not yet confirmed — check against a folded sample.
- No templates folder yet.
- *Fit to grid* and the margin fields still set the nominal margin only; the
  cut outline is then re-fitted, so *Fit to grid* has little visible effect.

# Helix Generator

Single-file HTML tool (`index.html`, open directly; no build, no server)
that draws the fold pattern for a strip that rolls up into an `n`-sided tube
whose diagonals run round it as helices, with a glue flap to close it. It uses
the same sheet, margins, grid, zoom/pan, project save/load and SVG/PNG/ZIP
export as the other tools (`common/`).

## Why it exists

Requested 2026-11-14 as a tool for the live section, with these inputs:

- `n`: sides of the polygon
- `w`: side width
- `d`: distance (the step height)
- `k`: number of steps
- `m`: glue flap width

The brief: draw a `w × d` rectangle, repeat it `n` times along x and `k`
times along y, and add a top-left → bottom-right diagonal to each. Then draw it
as long straight lines: the verticals, each of height `k·d`, `n + 1` of them
at spacing `w`, plus the diagonals that line up across cells as single lines.
Finally, add a strip `m` mm wide past the rightmost edge as a glue flap, with
fold lines that match those at the leftmost edge.

## The pattern

Strip coordinates: `u` runs along the strip from its left edge, `v` runs down
from its top edge. The body is `n·w × k·d` and the flap adds `m`, so the
strip is `L = n·w + m` long.

| Family | Lines |
|---|---|
| Verticals | `u = i·w` for every `i ≥ 1` with `u < L`. `u = 0` is the cut edge. `u = n·w` is the body/flap fold, and any verticals beyond it fall inside a flap wider than `w`. |
| Step lines | `v = j·d`, `j = 1 … k−1`, across the whole strip. Always drawn. |
| Diagonals | `u = w·(c + v/d)` for integer `c`, from `(c·w, 0)` to `((c+k)·w, k·d)`, cropped to the strip. Each is one line, not one segment per cell. |

**Glue flap.** The pattern repeats every `w` along `u`, so continuing every
family past `n·w` produces exactly the first `m` mm of the strip again. Glued
under the first column, the flap's folds land on the left edge's folds. With
`m = 0` there is no flap, and `u = n·w` is the cut edge.

**Placement.** The strip is centred on the sheet, running along x. If it
doesn't fit inside the
margins, the cut outline turns red and the status bar gives the size needed.

**Derived values** (shown under the inputs): the circumradius
`w / (2 sin(π/n))` and inradius `w / (2 tan(π/n))` of the `n`-gon, the tube
height `k·d`, the diagonal angle `atan(d/w)` and its length per cell, and the
climb per full turn, `n·d`.

## Using it

- **Helix** panel: `n` (3–60), `w`, `d` (≥ 1 mm), `k` (1–300). Defaults: `n = 3`, `w = 80`, `d = 10`, `k = 20`,
  `m = 10`, so the strip is 250 × 200 mm, on an A3 sheet.
- **Glue flap** panel: `m` (≥ 0; capped at the body length).
- The flap is shaded on screen only, and is not exported.
- There is no shape dragging: the wheel zooms, a drag pans, and *Fit view*
  resets the view.
- In the export, the folds are grouped as `<g id="fold">`, containing
  `verticals`, `steps` and `diagonals`, so a laser workflow can split them. The
  cut is `<g id="cut">`. File names carry the parameters:
  `helix_n3_w80_d10_k20_m10_<stamp>.svg|png|zip`.

## Decisions

- **Step lines are always drawn.** At first they were a checkbox (on by
  default), because the brief's list of straight lines named only the verticals
  and the diagonals. The user confirmed on 2026-11-14 that they are part of the
  pattern, with no toggle.
- **Defaults `n = 3`, `w = 80`, `d = 10`, `k = 20`** (set by the user,
  2026-11-14). With a 10 mm flap the strip is 250 × 200 mm. That doesn't fit
  inside an A4 sheet's 10 mm margins in either orientation, so the default
  sheet is A3 landscape.
- **Page coordinates and a fixed cut**, as in Wave: the cut is the strip
  outline, not the margin rectangle. The margin is only the area the strip must
  fit inside (dashed on screen).
- **Centred, not anchored to a corner:** this gives equal leftover on both
  sides for printing and cutting.
- **One fold colour**, with no mountain/valley distinction (as in Wave). The
  families are kept apart as SVG groups instead.

## Changelog

- 2026-11-14: first version.

## TODO / watch out for

- Not yet checked against a folded sample: whether the flap should taper (it
  is a plain rectangle).
- Only one handedness (top-left → bottom-right diagonals). A mirror option
  would give the opposite twist.
- No templates folder yet.

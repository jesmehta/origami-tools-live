# Changelog

## 1.0.0: public repository (2026-10-24)

Migrated the open-source tools from the development repository to
`origami-tools-live`, starting a fresh public Git history. Earlier development
milestones are recorded below.

## Earlier development milestones

The dates are from the development history. They predate this repository.

### 2026-10-18: Wave Generator

New tool (first built as "Step Grid", renamed the same day). Fold lines in x and
y at step `s`, jump `j`, step, jump …, with an optional edge bend, anchored at a
corner or centred. The cut outline fits whole gaps.

### 2026-10-13: shared zoom for pages with several views

`OT.wireZoom` / `OT.zoomFieldset` accept a label and ids, so one page can have
more than one zoomable canvas.

### 2026-10-03: zoom and pan

A *View* panel (**−** / **+** / *Fit view*) plus scroll-wheel zoom about the
pointer, in Mirror Pleats (linear and radial), X Span and Hypar. Screen only,
never exported. *Fit view* returns to the tool's own framing. A closer zoom
narrows hit-testing and snapping, so points can be placed more finely. Mirror
Pleats and X Span gained middle/right-drag pan, as Hypar already had.

### 2026-09-28: Mirror Pleats line order and vertical ghosts

- Generated lines keep one order on every vertical and never cross.
- Lines can be drawn to the ghosts of verticals: on the radial page, and above
  and below the sheet on the linear page.

### 2026-09-25 / 26: shared features

All the tools moved onto a shared `common/` module and gained:

- A backlink to the landing page at the top of every tool (an outlined
  arrow-shaped button).
- **Palette:** sage-green canvas (faint dash texture), cream panels and rust
  accents (titles, links, handles, ◆). Green fold and black cut lines are kept.
  Screen only; exports unchanged.
- On-screen strokes halved. The export stroke width is unchanged; it is a
  fabrication setting with its own field.
- **Foldable sidebar sections:** click a heading (▾ / ▸) to collapse it, plus
  *Expand all* / *Collapse all*. Remembered per page in the browser.
- **Tooltips:** sidebar explanations moved into hover tooltips (`data-tip`);
  sections with one show ⓘ. The one-line hint in the status bar stays.
- **Export:** SVG, PNG, and ZIP (both together). Every file name carries a
  local-time stamp, `<tool>_YYYY_MMDD_HHMMSS.svg|png|zip`. JSZip is loaded from
  cdnjs only when a ZIP is first requested.
- **Sheet size presets:** a *Size* dropdown plus ⇄ (swap portrait/landscape),
  read from `common/page-sizes.txt`. Opened from disk, the built-in copy is
  used. Hypar gained a sheet.
- **Margins, 5–15 mm (default 10):**
  - **↔** left & right and **↕** top & bottom, each symmetric, with 🔗 to keep
    them equal;
  - *Fit to grid* and a *Margin* edit mode put the margin lines on the grid
    (the radial page's polar grid has no fitting);
  - the pattern is cropped at the margin line, and the export is the whole
    page at true size with the margin outline as the cut line;
  - in Mirror Pleats and X Span the model's rectangle *is* the area inside the
    margin.
- **Grid** (screen only, never exported, clipped to the page):
  - square, every *Spacing* mm through the sheet centre, in Mirror Pleats
    linear, X Span and Hypar;
  - polar on the radial page: rings and spokes around the ◆ centre.
- **Snapping** (*Snap* checkbox; hold **Alt** to place freely):
  - **candidates:** existing points, rays at every multiple of 15° and 22.5°
    from the relevant anchor, and grid crossings, with a single grid line as
    the fallback;
  - moving a whole line, vertical or polygon snaps whenever any of its end
    handles can;
  - this replaced the old "Snap lines to 45°" checkbox.
- **Projects:**
  - **Save…** (`<tool>_<stamp>.json`) and **Load…** (a .json, or an .svg these
    tools exported, since the project is embedded in every exported SVG);
  - a *Templates…* dropdown and drag-and-drop;
  - starter templates for each tool.
- **Mirror Pleats radial:** the centre may be inside the sheet. Verticals
  become rays, trails stop after one lap, and the Kawasaki check keeps them
  flat-foldable.
- Off-canvas line handles are shown at the nearest visible point, so they stay
  grabbable.

### 2026-09-23: landing page

A root landing page with a thumbnail and a link for each tool. Default page size
A4 landscape (297 × 210 mm).

### 2026-09-20: X Span Generator

New tool: one continuous rhombus lattice on vertical lines, with Regular and
Irregular modes, chains in 0.5 steps, drag-to-set angle, and variable chain
heights.

### 2026-09-20: Hypar Generator

New tool: concentric offset contours and corner diagonals of a convex polygon.

### 2026-09-20: Mirror Pleats

New tool: linear and radial pages on a shared engine. Verticals are drawn edge
to edge, and lines reflect outward past the first and last vertical. The radial
page has an enforce-from-centre option, verticals through any edge, and grey
ghost lines for geometry outside the rectangle.

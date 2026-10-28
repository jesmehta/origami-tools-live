# Origami Tools

Small browser tools for origami/folding-based design and fabrication. Each one
draws a fold or crease pattern on a sheet at true size and exports it as SVG or
PNG, ready for a laser cutter, plotter or printer.

Open **[index.html](index.html)** for a landing page with a thumbnail and a link
for each tool. No build step, no install: every page is plain HTML and opens
straight from disk (`file://`) or from any static web server. A few features
(project templates, the editable sheet-size list) need a server; from disk the
tools use built-in defaults instead.

## Tools

- **[Mirror Pleats](mirror-pleats/index.html)**: draw verticals across a
  rectangle, draw lines between them, and each vertical mirrors those lines
  onward to build a trail of V-pleats. Separate
  [linear](mirror-pleats/linear.html) and [radial](mirror-pleats/radial.html)
  pages, ordered and random layouts, dimensions/measuring, SVG/PNG export.
  See [mirror-pleats/README.md](mirror-pleats/README.md).

- **[Hypar Generator](hypar/index.html)**: drag out a regular (or
  free-cornered convex) polygon, get concentric offset contours and corner
  diagonals to the centre, with an optional centre cut. SVG/PNG export. See
  [hypar/README.md](hypar/README.md).

- **[X Span Generator](x-span/index.html)**: a lattice of rhombi inside a
  rectangle whose vertices all lie on vertical lines (the vertical diagonals).
  Regular mode: evenly spread verticals, straight lines, defined by angle or
  number of chains. Irregular mode: free verticals, the lines bend at each one
  while the tiling stays continuous. Measure, dimensions, SVG/PNG export. See
  [x-span/README.md](x-span/README.md).

- **[Wave Generator](wave/index.html)**: fold lines across the material in
  both x and y, spaced step `s`, jump `j`, step, jump … (`j` = 2s, or set
  anywhere in s–3s). Optional edge bend (an extra step first); anchored at the
  lower-left corner running outward, or centred and symmetric, starting and
  ending on a step. The cut outline fits whole gaps (no partial steps at the
  edges). Fully parametric. SVG/PNG export. See [wave/README.md](wave/README.md).

## Shared features

Every tool loads `common/common.js` + `common/common.css` (a plain script
defining one global, `OT`; no modules, so the pages still open from disk):

- **Sheet:** size presets ([common/page-sizes.txt](common/page-sizes.txt)) with
  a portrait/landscape swap, and 5–15 mm margins. The pattern is cropped at the
  margin, and the margin outline is exported as the cut line. Wave is the
  exception: its margin is nominal, and the cut outline is fitted to whole
  gaps of the pattern instead.
- **Grid & snap:** a screen-only grid (square, or polar on the radial page),
  plus snapping to points, 15°/22.5° angle rays and the grid. Hold **Alt** to
  place freely.
- **Projects:** save/load as JSON, with the project also embedded in every
  exported SVG, plus starter templates and drag-and-drop.
- **Export:** SVG, PNG or ZIP (both), with time-stamped file names.
- **View:** zoom and pan (screen only), foldable sidebar sections, and hover
  tooltips in place of long explanations.

The full history is in [CHANGELOG.md](CHANGELOG.md).

## Documentation

How the code is laid out, the UI conventions, the geometry, and the design
decisions behind it all: [docs/](docs/README.md).

## Licences

| What | Licence |
|---|---|
| Code (all `.html`, `.js`, `.css`) | GPL-3.0-or-later: [LICENSE](LICENSE) |
| Documentation (`.md`) and the author's own images (`assets/`) | CC BY 4.0: [LICENSE-docs](LICENSE-docs) |
| Project templates (`*/templates/`) | CC BY 4.0, as documentation |
| [JSZip](https://stuk.github.io/jszip/) | Not bundled. Loaded at runtime from cdnjs for ZIP export, under its own licence (MIT or GPLv3) |
| [opentype.js](https://opentype.js.org/) | Not bundled, and not used by these tools. `common.js` has an optional helper (`OT.opentypejs`) that would load it from cdnjs if a page called it (MIT) |
| Patterns you make with the tools | Yours. Neither licence claims the files you export |

## Citing

If you use these tools in teaching, research or a publication, please cite
them. [CITATION.cff](CITATION.cff) has the details (GitHub's "Cite this
repository" button reads it).

Created and maintained by Jesal Mehta.

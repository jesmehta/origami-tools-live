# Origami tools: documentation

Documentation for the tools in this repo, from overview down to the reasoning
behind them. Each file stands on its own and links to the next level down.

| File | What it covers |
|---|---|
| [ARCHITECTURE.md](ARCHITECTURE.md) | How the code is laid out: the shared `common/` module and its API, each tool's state model, the render/interaction loop, how export works |
| [INTERFACE.md](INTERFACE.md) | UI conventions shared by all tools: sidebar layout, tooltips, sheet/margin, grid & snap, handles, export naming |
| [MATH.md](MATH.md) | The geometry: mirror reflection, rays + Kawasaki, x-span and hypar summaries, clipping, margins on the grid, snapping candidates |
| [DECISIONS.md](DECISIONS.md) | Design decisions, alternatives that were rejected, and why |

Per-tool reference (usage, per-tool decisions, changelog) is in each tool's own
README:
[mirror-pleats](../mirror-pleats/README.md) ·
[x-span](../x-span/README.md) ·
[hypar](../hypar/README.md) ·
[wave](../wave/README.md).

The top-level [README](../README.md) is the index of tools, and
[CHANGELOG.md](../CHANGELOG.md) has the history.

All documentation is CC BY 4.0; see [LICENSE-docs](../LICENSE-docs).

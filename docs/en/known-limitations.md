# Known limitations

## Coverage

| Area | Current coverage and limits |
|---|---|
| DWG | LibreDWG 0.13.4 full JSON adapted to an owned model; no DXF intermediate |
| Geometry | Lines, circles/arcs, ellipses, 2D polylines, widths/bulges, splines, solids and points |
| Blocks/attributes | Nested transforms, basic INSERT and ATTDEF/ATTRIB; no additional XREF file loading |
| Hatch/leader | Basic boundaries, solid/continuous-line patterns and primary leader styles; special features diagnosed |
| Dimensions | Stored graphics block; no dimension regeneration |
| Layout/viewports | Rectangular top views and basic freeze; nonrectangular/perspective/detail overrides limited |
| Text | TEXT, basic MTEXT formatting/alignment/stacks, horizontal SHX and fallback TrueType |
| Layers/navigation | Independent display/print checks, selected-layer highlight, viewport selection, pan/zoom |
| Snaps | Basic endpoint/midpoint/center/quadrant and rectangular viewport frame; not universal CAD snap compatibility |
| Plot/PDF | Paper, orientation, margins, scale, display/window extents, CTB pens, SHX search and font subsets |
| Persistence | Explicit settings v3 export, old settings import and model JSON; no DWG editing/saving |

Complex linetypes, transparency, per-viewport overrides, detailed typography, nonrectangular viewports, dimension regeneration, special hatches, nonzero thickness and proxies are not fully compatible. Accepted DWG generations do not guarantee correct handling of every drawing. Unsupported features and substitutions are diagnosed.

Annotations use read-only/locked flags, subject to PDF-reader behavior. Search/visible-text clipping boundaries can differ. Export stops when scene limits are reached rather than producing a partial PDF.

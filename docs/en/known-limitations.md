# Known limitations

## Coverage

| Area | Current coverage and limits |
|---|---|
| DWG | LibreDWG 0.13.4 full JSON adapted to an owned model; no DXF intermediate |
| Geometry | Lines, circles/arcs, ellipses, 2D polylines, widths/bulges, splines, solids and points |
| Linetypes | Embedded text/SHX shapes on lines, circles, arcs, ellipses, splines and zero-width polylines with arc segments; scale, offsets and relative/absolute rotation. Wide paths, changing elevation, ambiguous cusp tangents and some rotation modes remain limited |
| Blocks/attributes | Nested transforms, basic INSERT and ATTDEF/ATTRIB; no additional XREF file loading |
| Hatch/leader | Basic boundaries, solid/line patterns and primary leader styles; special features diagnosed |
| Dimensions | Stored graphics block; no dimension regeneration |
| Layout/viewports | Rectangular, closed polyline (including arcs), circle, ellipse and closed spline boundaries, top views and basic freeze; region boundaries/perspective/detail overrides limited |
| Text | TEXT, basic MTEXT formatting/alignment/stacks, horizontal SHX and fallback TrueType |
| Layers/navigation | Independent display/print checks, selected-layer highlight, viewport selection, pan/zoom |
| Snaps | Basic endpoint/midpoint/center/quadrant and viewport frames; curve tests use bounded accuracy/subdivision and spline frames have no dedicated snaps; not universal CAD snap compatibility |
| Plot/PDF | Paper, orientation, margins, scale, display/window extents, CTB pens, SHX search and font subsets |
| Persistence | Explicit settings v3 export, old settings import and model JSON; no DWG editing/saving |

Complex linetypes, transparency, per-viewport overrides, detailed typography, region viewport boundaries, dimension regeneration, special hatches, nonzero thickness and proxies are not fully compatible. Accepted DWG generations do not guarantee correct handling of every drawing. Unsupported features and substitutions are diagnosed.

Annotations use read-only/locked flags, subject to PDF-reader behavior. Search/visible-text clipping boundaries can differ. Export stops when scene limits are reached rather than producing a partial PDF.

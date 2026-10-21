# Known limitations

Version 0.1.4 includes rendering changes through 0.1.3-dev26. Development-number sections below are implementation history. Windows/original CAD appearance, frame, alpha and CTB comparisons remain pending.

## Coverage

| Area | Current coverage and limits |
|---|---|
| DWG | LibreDWG 0.13.4 full JSON adapted to an owned model; no DXF intermediate |
| Geometry | Lines, circles/arcs, ellipses, 2D polylines, widths/bulges, splines, solids and points |
| Linetypes | Embedded text/SHX shapes on lines, circles, arcs, ellipses, splines and zero-width and supported constant/tapered-width straight/arc polylines; scale, offsets and relative/absolute/upright rotation. Upright supports nonreflected projections; reflected/degenerate frames retain diagnosed solid preview. Per-layout PSLTSCALE is applied; MSLTSCALE remains unsupported. Leading-dot patterns and pen dots in supported wide patterns are implemented. unstable width joins, changing elevation, ambiguous cusp tangents and some rotation modes remain limited |
| Blocks/attributes | Nested transforms, basic INSERT and ATTDEF/ATTRIB; no additional XREF file loading |
| Hatch/leader | Basic boundaries, solid/line patterns and primary leader styles; special features diagnosed |
| Dimensions | Stored graphics block; no dimension regeneration |
| Layout/viewports | Rectangular, closed polyline (including arcs), circle, ellipse and closed spline boundaries, top views and basic freeze; region boundaries/perspective/detail overrides limited |
| Text | TEXT, basic MTEXT formatting/alignment/stacks, horizontal SHX, inline fonts, loaded static TTF/OTF outlines and fallback TrueType |
| Layers/navigation | Independent display/print checks, selected-layer highlight, viewport selection, pan/zoom |
| Snaps | Basic endpoint/midpoint/center/quadrant and viewport frames; curve tests use bounded accuracy/subdivision and spline frames have no dedicated snaps; not universal CAD snap compatibility |
| Plot/PDF | Paper, orientation, margins, scale, display/window extents, CTB pens, SHX search and font subsets |
| Persistence | Explicit settings v3 export, old settings import and model JSON; no DWG editing/saving |

Complex linetypes, transparency, per-viewport overrides, detailed typography, region viewport boundaries, dimension regeneration, special hatches, nonzero thickness and proxies are not fully compatible. Accepted DWG generations do not guarantee correct handling of every drawing. Unsupported features and substitutions are diagnosed.

Annotations use read-only/locked flags, subject to PDF-reader behavior. Search/visible-text clipping boundaries can differ. Export stops when scene limits are reached rather than producing a partial PDF.

Static font faces only: variable fonts/collections and vertical faces are unsupported. Missing requested variants use diagnosed fallback. PDF glyph outlines remain vectors. General search uses the bundled subset; outlined Bidi has the limited ActualText-anchor path described below. Basic paragraphs and implicit Bidi are implemented; contextual font boundaries and complex override shaping remain pending.

Basic MTEXT paragraph controls are supported: left/right margins, first-line/hanging indents, left/center/right alignment, left tabs and at-least/exact spacing. Justified/distributed alignment and right/center tabs are supported in dev10. Justification with tabs, contextual/Bidi scripts and overflowing tab fields retains diagnosed preview. Detailed line breaking, decimal tabs and columns remain pending. Legacy model JSON without a spacing style keeps its old spacing. Exact spacing does not expand for oversized spans.

Cluster integrity/canonical glyphs are implemented in dev11. Segmentation uses browser Intl.Segmenter data; full Unicode line breaking/kinsoku and full UAX #9 Bidi are not implemented. Contextual-word font changes and stack boundaries retain diagnosed preview. General search glyphs remain limited by bundled-font coverage/canonical equivalents. Dev12 outlined Bidi uses logical ActualText anchors only for suitable loaded TrueType glyphs. Missing visible glyphs, excluded spans and unsafe search clipping refuse export.

TEXT/MTEXT support basic implicit Bidi for Arabic/Hebrew mixed with Latin text and numbers. Paragraph levels are resolved before wrapping; each retained line is reordered afterwards. ASCII brackets, numbers/fractions and combining marks retain their original backing strings.

Complex override shaping, non-ASCII mirrored characters, tabs/stacks/tracking and contextual-word font changes retain diagnosed preview. This bounded Unicode 15.0 class implementation does not claim full UAX #9 conformance. Suitable loaded faces and ActualText-aware PDF readers are required. Extractors may return visual-order text with inserted direction controls; the original logical string is stored in ActualText.

Arabic-letter/mark words with the same font and metrics retain joining across color, underline, overline and strike boundaries. Whole words are measured/shaped before paint is assigned through verified glyph provenance; source strings remain unchanged.

A ligature crossing a paint boundary stays whole and uses its first logical component paint with a diagnostic. Marks inherit their base/ligature paint. Unverifiable glyph ownership falls back to a diagnosed whole-word first-paint preview.

Scope is same-font Arabic-letter/mark-only words. Font changes, other contextual scripts, punctuation/mixed words, joining controls and stacks remain limited. Complex Bidi override shaping and broader mirroring remain pending.


LRM (U+200E), RLM (U+200F) and ALM (U+061C) participate as zero-width strong directional marks in paragraph, number and bracket resolution. They are excluded from glyph geometry/coverage without changing source strings; PDF ActualText/comments retain the original marks. Mark-only spans produce no glyphs or missing-font warnings.

Bundled-font RTL punctuation/brackets are encoded in the same visual order as Canvas. Text-mode PDF refuses unsafe marked logical groups with cropped, excluded or clipped spans. Complex override shaping, joining controls, broader mirroring, tabs/stacks/tracking and contextual-word font boundaries remain limited. Full UAX #9 conformance is not claimed.


LRE (U+202A) and RLE (U+202B) establish nested directional embeddings; PDF (U+202C) terminates the latest embedding/override. Paragraph resolution precedes line reordering, preserving embeddings across wrapped lines. Here PDF names the Pop Directional Formatting control.

Formatting controls produce no glyphs, advance or missing-font substitutions; original strings remain in ActualText/comments. Unmatched PDF is ignored and unclosed embeddings terminate at paragraph end. Explicit levels are bounded to 125, with overflow counts consumed before valid stack entries are popped.

Complex override shaping, joining controls, broader mirroring and combinations with tabs/stacks/tracking remain limited. Embedding boundaries within joining words or combining clusters retain diagnosed preview. Contextual-word font boundaries remain pending. Full UAX #9 conformance is not claimed.


LRO (U+202D) and RLO (U+202E) override the direction of simple Latin, numeric, Japanese and basic Hebrew text. PDF (U+202C) ends the latest embedding/override. Nested opposite overrides, temporary neutral embeddings and continuation across wrapped lines are supported.

Override shaping runs are kept separate from ordinary RTL runs and shape visual-order text. This prevents retaining an original-order ffi ligature or logical-order kerning after reversal. Fallback Canvas drawing/measurement forces each resolved run rather than only setting its paragraph base. Controls add no glyph/advance; original source remains in ActualText/comments.

Contextual letters/combining marks under overrides, inline formatting within overridden words, direction boundaries within joining words/clusters and combinations with tabs/stacks/tracking retain diagnosed preview. Contextual font boundaries, joining controls and broader mirroring remain limited. Full UAX #9 conformance is not claimed.


## 0.1.3-dev17: Directional isolates

LRI (U+2066), RLI (U+2067), FSI (U+2068) and PDI (U+2069) now support directional isolation. Isolating run sequences prevent inner Latin, numbers and Hebrew from changing surrounding order. FSI uses the first strong character outside nested isolates, defaulting to LTR if none exists.

PDI closes outstanding embeddings/overrides inside its isolate and restores the outer state. PDF controls cannot end isolates. Paragraph resolution precedes wrapping; line-final whitespace/isolate controls reset to the paragraph level. Paragraph first-strong detection skips isolate contents. Separate overflow counts bound isolate/embedding depth; unclosed scopes end with the paragraph.

Isolate controls add no glyph, advance or missing-font warning; original source remains in PDF ActualText/comments. Empty isolates also preserve shaping boundaries rather than creating cross-boundary ligatures. Contextual letters/marks under overrides, overridden-word inline formatting, directional boundaries within joining words/clusters and tabs/stacks/tracking retain diagnosed preview. Contextual font boundaries, joining controls and non-ASCII mirroring remain limited. Full UAX #9 conformance is not claimed.


## 0.1.3-dev18: Contextual width/oblique boundaries

Arabic-letter/mark-only words now support inline width (W) and oblique (Q) changes when font settings match. The whole word is shaped first; verified source/glyph ownership determines the glyph transforms. This avoids changing initial/medial/final forms by independently shaping substrings.

Adjusted advances drive wrapping, subsequent text positions and search anchors; measurement includes sheared ink bounds. Marks transform from their original positioned geometry. Colors and underline/overline/strike use the adjusted owned intervals, with matching shear on decoration paths.

Ligatures crossing metric boundaries retain the first logical component width/shear with diagnostics. Unverified glyph ownership uses whole-word first paint/metrics preview. Font changes, other contextual scripts, punctuation/mixed words, joining controls, complex overrides and tabs/stacks/tracking remain limited. Original source stays in PDF ActualText/comments.


## 0.1.3-dev19: Contextual height/alignment boundaries

Arabic-letter/mark-only words now support height (H) and vertical alignment (A0/A1/A2) changes within the same font. Whole-word shaping precedes verified glyph transforms. Mixed absolute/relative heights use the entity base height rather than mistaking the first absolute inline height for that base.

Baseline/center/cap-top alignment uses the tallest cap on the same line. Baseline shifts compensate outer shear to prevent horizontal drift; marks transform with their owning glyph height/alignment. Adjusted metrics drive wrapping, line spacing and search anchors. Underline/overline/strike follow the owned height and baseline.

Ligatures crossing height/alignment or other metric boundaries retain first-logical-component metrics with diagnostics. Unverified ownership uses whole-word first-format preview. Font boundaries, other contextual scripts, punctuation/digits/directional controls in mixed words, joining controls, complex overrides and tabs/stacks/tracking remain limited. Original text stays in PDF ActualText/comments.


For a blank saved layout, inspect the diagnosed viewport. Dev20 distinguishes a view outside renderable model geometry from empty output caused by layers/clipping. Saved view centers and scales are not changed automatically; use Model to inspect geometry. Fit-only splines retain interpolation warnings because original control points are absent and CAD curvature comparison remains necessary.


Dev21 supports opaque drawing-background masks on planar horizontal single-column multileader text, with margin factors 1–5. Canvas uses its current background; PDF uses white. The rectangle follows measured text; missing requested fonts also affect mask size. Explicit-color/transparency backgrounds, columns, vertical/tilted text and frames remain diagnosed limitations. Original CAD appearance comparison is pending.


Dev22 adds rectangular multileader text frame preview for planar horizontal single-column text. A measured text rectangle is padded by the stored Landing Gap. Frames use base text entity color/lineweight with a preview warning because original CAD frame attributes are unverified. Missing/invalid gaps or unsupported text planes omit frames and retain text. Explicit-color/transparency backgrounds and remaining leader extensions stay pending.


## 0.1.3-dev23: Opaque explicit-color backgrounds

Planar horizontal single-column multileader text now previews stored ACI/RGB backgrounds. Canvas and color/source PDFs use the stored color; grayscale PDF converts to gray and black PDF uses white. Backgrounds bypass pen color/screening overrides. Background, frame and foreground colors remain independent; backgrounds are fully opaque.

MULTILEADER_BACKGROUND_COLOR_PREVIEW remains because original CAD CTB behavior is unverified. Missing/invalid or ByLayer/ByBlock colors omit only the background with diagnostics. Transparency, columns, vertical/tilted text, CAD frame attributes, hooks and remaining overrides stay pending. Text and background dimensions depend on the loaded font metrics.


## 0.1.3-dev24: Explicit-alpha backgrounds

Planar horizontal single-column multileaders support explicit alpha for drawing-background and ACI/RGB fills. The low byte of stored 0x020000AA is opacity 0–255 (0 clear, 255 opaque). Legacy zero/unset background fields remain opaque. This does not implement general entity or layer transparency.

Canvas composites the current background or saved color over underlying geometry. PDF retains vector fills and alpha; black output applies saved alpha to white backgrounds. Source/color and grayscale policies and bypassing background pen color/screening overrides follow dev23. Text and frames remain opaque. Clear backgrounds create no paint, bounds or selection surface.

Inherited, unknown or malformed encodings omit only the background with diagnostics. Original CAD display/plot transparency switches and CTB matching remain unverified, retaining MULTILEADER_BACKGROUND_ALPHA_PREVIEW. Columns, vertical/tilted text, ByLayer/ByBlock background colors, CAD frame attributes, hooks and remaining overrides stay pending.


## 0.1.3-dev25: Connections and stored line spacing

Do not duplicate stored doglegs as additional hooks. Hidden-only or empty branches create no detached dogleg, and vertical attachment adds no horizontal dogleg. Use per-branch visibility overrides and node/entity/style attachment precedence. Multiple branches share one dogleg. Unknown attachment directions/override bits stop atomic expansion with diagnostics.

EnableLanding relates to the text gap and is not treated as the same switch as EnableDogleg. Do not extend or move stored WCS endpoints/text positions by guessing. Retain stored entity values rather than replacing them from the global override bitmask alone. Attachment underlines/overlines, automatic extensions, curve connections/breaks, legacy arrow arrays and block attribute overrides remain pending.

Saved at-least/exact line spacing now enters shared text layout, affecting factors, tall inline text, background/frame extents and searchable PDF positions. Exact spacing does not expand for large letters, so source settings can intentionally overlap text. Unknown styles retain legacy layout with diagnostics. Windows/original CAD appearance comparison is pending.


## 0.1.3-dev26: Attachment underline/overline preview

Preview R06 attachment underlines/overlines for horizontal types 5/6 and vertical type 10. Retain stored connection anchors and derive vector rules from shared measured text width. Horizontal rules include the saved Landing Gap; vertical rules center on the saved anchor. Do not rescale stored coordinates or gaps.

Support planar horizontal single-column text with straight unbroken connections. Determine the actual side from node direction and anchor, then resolve attachment type from context, entity and style. Hidden/empty branches create no rule; shared identical connections are deduplicated.

Paint background, frame, attachment rules, then text. Rules use base leader color, lineweight and simple linetype independently of inline text color/background alpha. Share layers, transforms, clips, selection and normal PDF pens. Complex linetypes or unsafe conditions omit only the rule with diagnostics.

All-line type 8, curves/breaks, missing/invalid anchors or gaps, ambiguous side, columns, vertical text and tilted planes omit only the attachment rule with MULTILEADER_ATTACHMENT_LINE_PENDING. Ordinary attachment types add no rule. Complex linetypes use MULTILEADER_ATTACHMENT_LINETYPE_PENDING; unsafe neutral-model metadata uses MTEXT_ATTACHMENT_LINE_PREVIEW. MULTILEADER_ATTACHMENT_LINE_PREVIEW records that original CAD appearance remains unverified. Fallback font measurement also changes rule length.

Neither original drawing contains targeted multileaders; authored fixtures cover the feature. Windows, original CAD and CTB comparisons remain pending. Next investigate per-line saved positions for all-line type 8. Legacy arrows/block attribute overrides and CAD frame/alpha comparison remain pending.

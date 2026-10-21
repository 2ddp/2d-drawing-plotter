# User guide

2D Drawing Plotter 0.1.4 is a local Windows 11 x64 application for viewing 2D DWG drawings and exporting PDF. It does not edit drawings. Japanese is the default UI language. Select English in the Language menu at the top right to switch without reopening the drawing or resetting plot settings. Only the language preference is saved in profile/preferences.json inside the application folder and restored at the next launch. If the folder is read-only, the language applies to the current session only. Drawing text and layer names are not translated.

## Start

Extract the complete Windows ZIP into a writable folder and double-click START.cmd. Python 3.13.16 x64 and application bytecode are bundled; no separate Python setup is needed. Keep the console open while using the app and close the tab and console to exit. Do not replace runtime with an older release. Administrator permission, Git, Node.js and pip are unnecessary.

## Open and navigate

Use **Open DWG** or drop one DWG file onto the drawing area to open a drawing (128MB input limit, 120-second parser timeout). Select Model or Layout under **Model / layout**.

The toolbar at the right center switches selection/pan modes, zoom and fit. Middle-button drag pans; the wheel zooms, including while choosing a print window. In selection mode, click or right-button drag selects entities. A rectangle dragged right uses full containment; a rectangle dragged left uses crossing selection. Shift adds and Esc clears. Visible entities inside viewports are included. Text selection uses bounds.

The layer list independently controls visibility and printing and highlights selected entity layers. A hidden layer still prints if its print checkbox is enabled. The original DWG is never modified.

## PDF export

- Choose A0–A4 or a custom paper size and orientation. Preset width/height are calculated and disabled.
- **Extents** plots all objects enabled for printing in the selected model or layout; **Display** uses the area currently shown on screen; **Window** uses a rectangle specified by two opposite corners. Each option has an explanation below it. Toggle snapping with its checkbox or Alt.
- Margin is under page details and defaults to 0mm. Output is centered.
- Choose fit-to-paper or 1:n. Fit shows a calculated, disabled denominator. A clipping warning appears near scale only when content exceeds the page.
- Drawing/layout units are used automatically. Unspecified units assume mm with a diagnostic. Use manual unit correction only if needed.

Use **Save PDF** to save directly. There is no PDF preview feature.

## Pens, colors and CTB

**Base lineweight** keeps the same field name in both lineweight modes. Drawing / color uses it when no lineweight is set in the drawing, CTB or color settings. Uniform applies it to all geometry. The explanatory text updates when the mode changes.

Output color is black (default), drawing colors, or per-color settings. The collapsed CTB/per-color section inside color/lineweight imports CTB and edits the used ACI colors, widths and screening. Row numbers are display order, not new ACI values. TrueColor does not use ACI pens.

The color editor supports RGB (default), HSL, HEX, palette, screen picking and reset to drawing color. The native Windows picker magnifies nearby pixels. A browser screen-capture fallback requires share permission; picking can be cancelled.

Screening mixes with white; it is not opacity. CTB color, lineweight, screening and grayscale are supported. Drawing-color mode ignores pen color/grayscale overrides but preserves lineweight and screening. There is no global grayscale selector. CTB linetype, cap, join and pattern overrides have limitations reported in diagnostics. STB is unsupported.

## Fonts and search

Load authorized SHX or static TTF/OTF through **Fonts** for stroke or filled-outline text. Fonts are never downloaded automatically. Noto Sans JP is the bundled fallback; missing/unsupported glyph substitutions are diagnosed.

Horizontal SHAPES 1.0/1.1, UNIFONT 1.0 and BIGFONT 1.0 are supported. BIGFONT assumes Shift-JIS. Vertical text, special variants and universal font compatibility are not implemented. Limits are 16MB per file, 64MB total and 64 fonts. Fonts remain in the tab's memory and are not included in settings JSON.

SHX lineweight can use a separate value (default 0.10mm) or the geometry pen. Filled TrueType weight is not changed. SHX search additions can be invisible text, annotations, or none. TrueType remains searchable even with none. Only used glyphs are embedded in PDF. Search, copying and annotation search vary by PDF reader. Missing visible/invisible fallback glyphs stop export rather than silently dropping text.

## Settings and JSON

Settings are saved only by explicit export. There is no per-drawing autosave. Pens, paper, snapping and same-name layer settings can be imported. Window bounds, selected view and drawing ID are not saved. Legacy v1 and independent format v1–v3 settings are accepted; new exports use v3.

Open parsed JSON accepts LibreDWG 0.13.4 full JSON. Save parsed JSON exports the independent DrawingDocument with diagnostics. These formats differ; saved independent models cannot currently be reopened directly. JSON contains drawing data and must not be published without authorization.

## Troubleshooting

Diagnostics group identical causes into one row. Warning and information counts refer to distinct causes; the total diagnosis count is shown separately. Expand an entity count to inspect every affected ID. Exported DrawingDocument JSON keeps the individual diagnoses.

For a missing Python runtime, follow README.html. For missing or altered files, extract a fresh distribution into a new folder rather than mixing versions. For parse failures, check DWG generation, input size and timeout. For display/export differences, inspect **Diagnostics**. Export is stopped if the scene limit is exceeded.

Extrusion thickness that does not affect the 2D outline is reported as information. Thickness that changes the outline after a tilted block transform remains a warning. This classification uses thickness and direction retained when reading the DWG.

Constant-width and segment-linear tapered polylines containing straight segments and circular arcs render and export as filled vector dash outlines. Tapers continue across gaps, and supported closed contours retain joins and holes. Approximate curve joins and unsupported width steps are identified in diagnostics. MTEXT underline, overline and strikethrough are shared vector rules for screen and PDF.

Legacy curve-fit/spline-fit polylines use their stored drawing vertices. Spline control frames are excluded from linework and snapping. Reopen the original DWG to refresh older exported model JSON that lacks vertex-role metadata.

WIPEOUT masks cover underlying geometry using the screen background color and white in PDF. Stored draw order and frame display/plot settings are respected. Display-only frames are excluded from PDF. Mask layers follow the visibility and printing controls.

MTEXT tracking (0.75–4 times the normal spacing) adjusts glyph positions, wrapping, stacked rows and decorations. Tracking changes spacing independently of glyph width. Unsupported formatting is identified in diagnostics.

MTEXT inline ACI and RGB colors are shared by screen and PDF. ACI colors participate in per-color pen settings.

Nonrectangular viewports support closed polylines with arc segments, circles, ellipses and closed splines. Viewing and PDF export use the same vector boundary. Selection and snapping share curve interaction data with bounded accuracy and subdivision. Circle and ellipse frames provide center and quadrant snaps; bulged polylines provide actual endpoints, arc midpoints and other semantic snaps, not artificial subdivision points. Region boundaries, open or self-intersecting boundaries, discontinuities and subdivision limits are reported in diagnostics.

Complex linetypes with embedded text and SHX shapes are supported on lines, circles, circular arcs, ellipses, splines and zero-width polylines with straight or arc segments. Viewing and PDF use the same vector curves, and embedded text remains searchable and copyable. Ellipse distances are measured along the physical axes, keeping symbol size independent of the axis ratio. Discontinuous spline spans restart the pattern without connecting strokes. Load required SHX files using the SHX controls. Missing shapes leave the dash pattern intact; missing text fonts use the bundled fallback, with the reason shown in diagnostics. Constant-width and segment-linear tapered polylines with straight/circular segments are also supported. Closed contours support straight or forward-tangent arc segments. Wide dot patterns, unstable joins, changing-elevation curves, reversals without a unique tangent and unsupported rotation modes have diagnosed fallback rendering.

## Inline and TrueType fonts

Use Fonts to load permitted SHX, TTF or OTF files. SHX matches filenames; TrueType matches family/style, including inline MTEXT requests. Use static instances for variable fonts. Check Diagnostics for missing faces/variants. Loaded fonts are used only in this tab.

## MTEXT paragraph display

Left/right margins, first-line/hanging indents, left/center/right alignment, justified/distributed alignment and left/right/center tab stops affect both the viewer and PDF. Values use the initial text height; an inline height change does not rescale paragraph margins.

DWG at-least spacing expands for tall spans; exact spacing retains its baseline distance. Justification expands wrapped lines; distribution also expands the final line. Right/center tabs align the following field by its styled width. Combining justification with tabs, contextual scripts or overflowing tab fields uses diagnosed preview. Detailed line breaking, decimal tabs and columns remain pending.

## Combining marks and graphemes

Wrapping and font fallback keep combining sequences intact. Color/face/height changes inside a cluster use its first character style and report a diagnostic. Available composed glyphs may be used for display without changing drawing strings. PDF search/comments retain the original sequences.

Contextual-word font boundaries and cluster/stack boundaries remain incomplete. This does not guarantee all-language glyph or color-emoji rendering. PDF checks bundled-font coverage or suitable outlined Bidi glyphs with safe logical ActualText before export.

## Basic Arabic/Hebrew placement

TEXT/MTEXT support basic implicit Bidi for Arabic/Hebrew mixed with Latin text and numbers. Paragraph levels are resolved before wrapping; each retained line is reordered afterwards. ASCII brackets, numbers/fractions and combining marks retain their original backing strings. Load a suitable static TTF/OTF through Fonts. Loaded outlines are shared with PDF.

Search/copy stores original logical ActualText. Missing visible glyphs stop export. If clipping/exclusions prevent retention of a complete search line, include the full line or choose Comments/None. Extracted order/directional controls depend on the PDF reader.

Complex override shaping, non-ASCII mirrored characters, tabs/stacks/tracking and contextual-word style changes retain diagnosed preview. This bounded Unicode 15.0 class implementation does not claim full UAX #9 conformance. Suitable loaded faces and ActualText-aware PDF readers are required.

Basic outlined Bidi uses searchable anchors only in Text mode. Comments/None modes omit those anchors while retaining visible vector outlines.

## Contextual word colors and rules

Arabic-letter/mark words with the same font and metrics retain joining across color, underline, overline and strike boundaries. Whole words are measured/shaped before paint is assigned through verified glyph provenance; source strings remain unchanged. Load a suitable static TrueType face.

A ligature crossing a paint boundary stays whole and uses its first logical component paint with a diagnostic. Marks inherit their base/ligature paint. Unverifiable glyph ownership falls back to a diagnosed whole-word first-paint preview.

Scope is same-font Arabic-letter/mark-only words. Font changes, other contextual scripts, punctuation/mixed words, joining controls and stacks remain limited. Complex Bidi override shaping and broader mirroring remain pending. Check diagnostics and appearance outside this scope.


LRM (U+200E), RLM (U+200F) and ALM (U+061C) participate as zero-width strong directional marks in paragraph, number and bracket resolution. They are excluded from glyph geometry/coverage without changing source strings; PDF ActualText/comments retain the original marks. Mark-only spans produce no glyphs or missing-font warnings.

Bundled-font RTL punctuation/brackets are encoded in the same visual order as Canvas. Text-mode PDF refuses unsafe marked logical groups with cropped, excluded or clipped spans. Complex override shaping, joining controls, broader mirroring, tabs/stacks/tracking and contextual-word font boundaries remain limited. Full UAX #9 conformance is not claimed.


LRE (U+202A) and RLE (U+202B) establish nested directional embeddings; PDF (U+202C) terminates the latest embedding/override. Paragraph resolution precedes line reordering, preserving embeddings across wrapped lines. Here PDF names the Pop Directional Formatting control.

Formatting controls produce no glyphs, advance or missing-font substitutions; original strings remain in ActualText/comments. Unmatched PDF is ignored and unclosed embeddings terminate at paragraph end. Explicit levels are bounded to 125, with overflow counts consumed before valid stack entries are popped.

Complex override shaping, joining controls, broader mirroring and combinations with tabs/stacks/tracking remain limited. Embedding boundaries within joining words or combining clusters retain diagnosed preview. Contextual-word font boundaries remain pending. Full UAX #9 conformance is not claimed.


LRO (U+202D) and RLO (U+202E) override the direction of simple Latin, numeric, Japanese and basic Hebrew text. PDF (U+202C) ends the latest embedding/override. Nested opposite overrides, temporary neutral embeddings and continuation across wrapped lines are supported.

Override shaping runs are kept separate from ordinary RTL runs and shape visual-order text. This prevents retaining an original-order ffi ligature or logical-order kerning after reversal. Fallback Canvas drawing/measurement forces each resolved run rather than only setting its paragraph base. Controls add no glyph/advance; original source remains in ActualText/comments.

Contextual letters/combining marks under overrides, inline formatting within overridden words, direction boundaries within joining words/clusters and combinations with tabs/stacks/tracking retain diagnosed preview. Contextual font boundaries, joining controls and broader mirroring remain limited. Full UAX #9 conformance is not claimed.


## 0.1.4: Directional isolates

LRI (U+2066), RLI (U+2067), FSI (U+2068) and PDI (U+2069) now support directional isolation. Isolating run sequences prevent inner Latin, numbers and Hebrew from changing surrounding order. FSI uses the first strong character outside nested isolates, defaulting to LTR if none exists.

PDI closes outstanding embeddings/overrides inside its isolate and restores the outer state. PDF controls cannot end isolates. Paragraph resolution precedes wrapping; line-final whitespace/isolate controls reset to the paragraph level. Paragraph first-strong detection skips isolate contents. Separate overflow counts bound isolate/embedding depth; unclosed scopes end with the paragraph.

Isolate controls add no glyph, advance or missing-font warning; original source remains in PDF ActualText/comments. Empty isolates also preserve shaping boundaries rather than creating cross-boundary ligatures. Contextual letters/marks under overrides, overridden-word inline formatting, directional boundaries within joining words/clusters and tabs/stacks/tracking retain diagnosed preview. Contextual font boundaries, joining controls and non-ASCII mirroring remain limited. Full UAX #9 conformance is not claimed.


## 0.1.4: Contextual width/oblique boundaries

Arabic-letter/mark-only words now support inline width (W) and oblique (Q) changes when font settings match. The whole word is shaped first; verified source/glyph ownership determines the glyph transforms. This avoids changing initial/medial/final forms by independently shaping substrings.

Adjusted advances drive wrapping, subsequent text positions and search anchors; measurement includes sheared ink bounds. Marks transform from their original positioned geometry. Colors and underline/overline/strike use the adjusted owned intervals, with matching shear on decoration paths.

Ligatures crossing metric boundaries retain the first logical component width/shear with diagnostics. Unverified glyph ownership uses whole-word first paint/metrics preview. Font changes, other contextual scripts, punctuation/mixed words, joining controls, complex overrides and tabs/stacks/tracking remain limited. Original source stays in PDF ActualText/comments.


## 0.1.4: Contextual height/alignment boundaries

Arabic-letter/mark-only words now support height (H) and vertical alignment (A0/A1/A2) changes within the same font. Whole-word shaping precedes verified glyph transforms. Mixed absolute/relative heights use the entity base height rather than mistaking the first absolute inline height for that base.

Baseline/center/cap-top alignment uses the tallest cap on the same line. Baseline shifts compensate outer shear to prevent horizontal drift; marks transform with their owning glyph height/alignment. Adjusted metrics drive wrapping, line spacing and search anchors. Underline/overline/strike follow the owned height and baseline.

Ligatures crossing height/alignment or other metric boundaries retain first-logical-component metrics with diagnostics. Unverified ownership uses whole-word first-format preview. Font boundaries, other contextual scripts, punctuation/digits/directional controls in mixed words, joining controls, complex overrides and tabs/stacks/tracking remain limited. Original text stays in PDF ActualText/comments.

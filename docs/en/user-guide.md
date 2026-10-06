# User guide

2D Drawing Plotter 0.1.2 is a local Windows 11 x64 application for viewing 2D DWG drawings and exporting PDF. It does not edit drawings. Japanese is the default UI language. Select English in the Language menu at the top right to switch without reopening the drawing or resetting plot settings. Only the language preference is saved in profile/preferences.json inside the application folder and restored at the next launch. If the folder is read-only, the language applies to the current session only. Drawing text and layer names are not translated.

## Start

Extract the complete Windows ZIP into a writable folder and double-click START.cmd. Python 3.13.16 x64 and application bytecode are bundled; no separate Python setup is needed. Keep the console open while using the app and close the tab and console to exit. Do not replace runtime with an older release. Administrator permission, Git, Node.js and pip are unnecessary.

## Open and navigate

Use **Open DWG** or drop one DWG file onto the drawing area to open a drawing (128MB input limit, 120-second parser timeout). Select Model or Layout under **View**.

The toolbar at the right center switches selection/pan modes, zoom and fit. Middle-button drag pans; the wheel zooms, including while choosing a print window. In selection mode, click or right-button drag selects entities. A rectangle dragged right uses full containment; a rectangle dragged left uses crossing selection. Shift adds and Esc clears. Visible entities inside viewports are included. Text selection uses bounds.

The layer list independently controls visibility and printing and highlights selected entity layers. A hidden layer still prints if its print checkbox is enabled. The original DWG is never modified.

## PDF export

- Choose A0–A4 or a custom paper size and orientation. Preset width/height are calculated and disabled.
- Choose printable extents, current display, or a two-point window. Toggle snapping with its checkbox or Alt.
- Margin is under page details and defaults to 0mm. Output is centered.
- Choose fit-to-paper or 1:n. Fit shows a calculated, disabled denominator. A clipping warning appears near scale only when content exceeds the page.
- Drawing/layout units are used automatically. Unspecified units assume mm with a diagnostic. Use manual unit correction only if needed.

Use **Save PDF** to save directly. There is no PDF preview feature.

## Pens, colors and CTB

Output color is black (default), drawing colors, or per-color settings. The collapsed CTB/per-color section inside color/lineweight imports CTB and edits the used ACI colors, widths and screening. Row numbers are display order, not new ACI values. TrueColor does not use ACI pens.

The color editor supports RGB (default), HSL, HEX, palette, screen picking and reset to drawing color. The native Windows picker magnifies nearby pixels. A browser screen-capture fallback requires share permission; picking can be cancelled.

Screening mixes with white; it is not opacity. CTB color, lineweight, screening and grayscale are supported. Drawing-color mode ignores pen color/grayscale overrides but preserves lineweight and screening. There is no global grayscale selector. CTB linetype, cap, join and pattern overrides have limitations reported in diagnostics. STB is unsupported.

## Fonts and search

Load authorized SHX through **SHX fonts** for vector stroke text. Fonts are never downloaded automatically. Noto Sans JP is the bundled fallback; missing/unsupported glyph substitutions are diagnosed.

Horizontal SHAPES 1.0/1.1, UNIFONT 1.0 and BIGFONT 1.0 are supported. BIGFONT assumes Shift-JIS. Vertical text, special variants and universal font compatibility are not implemented. Limits are 16MB per file, 64MB total and 64 fonts. Fonts remain in the tab's memory and are not included in settings JSON.

SHX lineweight can use a separate value (default 0.10mm) or the geometry pen. Filled TrueType weight is not changed. SHX search additions can be invisible text, annotations, or none. TrueType remains searchable even with none. Only used glyphs are embedded in PDF. Search, copying and annotation search vary by PDF reader. Missing visible/invisible fallback glyphs stop export rather than silently dropping text.

## Settings and JSON

Settings are saved only by explicit export. There is no per-drawing autosave. Pens, paper, snapping and same-name layer settings can be imported. Window bounds, selected view and drawing ID are not saved. Legacy v1 and independent format v1–v3 settings are accepted; new exports use v3.

Open parsed JSON accepts LibreDWG 0.13.4 full JSON. Save parsed JSON exports the independent DrawingDocument with diagnostics. These formats differ; saved independent models cannot currently be reopened directly. JSON contains drawing data and must not be published without authorization.

## Troubleshooting

Diagnostics group identical causes into one row. Warning and information counts refer to distinct causes; the total diagnosis count is shown separately. Expand an entity count to inspect every affected ID. Exported DrawingDocument JSON keeps the individual diagnoses.

For a missing Python runtime, follow README.html. For missing or altered files, extract a fresh distribution into a new folder rather than mixing versions. For parse failures, check DWG generation, input size and timeout. For display/export differences, inspect **Diagnostics**. Export is stopped if the scene limit is exceeded.

Extrusion thickness that does not affect the 2D outline is reported as information. Thickness that changes the outline after a tilted block transform remains a warning. This classification uses thickness and direction retained when reading the DWG.

Open constant-width polylines containing straight segments and circular arcs render and export as filled vector dash outlines. Approximate curve joins are identified in diagnostics. MTEXT underline, overline and strikethrough are shared vector rules for screen and PDF.

Legacy curve-fit/spline-fit polylines use their stored drawing vertices. Spline control frames are excluded from linework and snapping. Reopen the original DWG to refresh older exported model JSON that lacks vertex-role metadata.

WIPEOUT masks cover underlying geometry using the screen background color and white in PDF. Stored draw order and frame display/plot settings are respected. Display-only frames are excluded from PDF. Mask layers follow the visibility and printing controls.

MTEXT tracking (0.75–4 times the normal spacing) adjusts glyph positions, wrapping, stacked rows and decorations. Tracking changes spacing independently of glyph width. Unsupported formatting is identified in diagnostics.

MTEXT inline ACI and RGB colors are shared by screen and PDF. ACI colors participate in per-color pen settings.

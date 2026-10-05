# User guide

2D Drawing Plotter 0.1.0 is a local Windows 11 x64 application for viewing 2D DWG drawings and exporting PDF. It does not edit drawings. Japanese is the primary language; English documentation is available, but the UI currently remains Japanese.

## Start

Extract the complete Windows ZIP into a writable folder and double-click START.cmd. Python 3.13.16 x64 and application bytecode are bundled; no separate Python setup is needed. Keep the console open while using the app and close the tab and console to exit. Do not replace runtime with an older release. Administrator permission, Git, Node.js and pip are unnecessary.

## Open and navigate

Use 「DWGを開く」 to open a drawing (128MB input limit, 120-second parser timeout). Select Model or Layout under 「表示するビュー」.

The toolbar at the right center switches selection/pan modes, zoom and fit. Middle-button drag pans; the wheel zooms, including while choosing a print window. In selection mode, click or right-button drag selects entities. A rectangle dragged right uses full containment; a rectangle dragged left uses crossing selection. Shift adds and Esc clears. Visible entities inside viewports are included. Text selection uses bounds.

The layer list independently controls visibility and printing and highlights selected entity layers. A hidden layer still prints if its print checkbox is enabled. The original DWG is never modified.

## PDF export

- Choose A0–A4 or a custom paper size and orientation. Preset width/height are calculated and disabled.
- Choose printable extents, current display, or a two-point window. Toggle snapping with its checkbox or Alt.
- Margin is under page details and defaults to 0mm. Output is centered.
- Choose fit-to-paper or 1:n. Fit shows a calculated, disabled denominator. A clipping warning appears near scale only when content exceeds the page.
- Drawing/layout units are used automatically. Unspecified units assume mm with a diagnostic. Use manual unit correction only if needed.

Use 「PDFを保存」 to save directly. There is no PDF preview feature.

## Pens, colors and CTB

Output color is black (default), drawing colors, or per-color settings. The collapsed CTB/per-color section inside color/lineweight imports CTB and edits the used ACI colors, widths and screening. Row numbers are display order, not new ACI values. TrueColor does not use ACI pens.

The color editor supports RGB (default), HSL, HEX, palette, screen picking and reset to drawing color. The native Windows picker magnifies nearby pixels. A browser screen-capture fallback requires share permission; picking can be cancelled.

Screening mixes with white; it is not opacity. CTB color, lineweight, screening and grayscale are supported. Drawing-color mode ignores pen color/grayscale overrides but preserves lineweight and screening. There is no global grayscale selector. CTB linetype, cap, join and pattern overrides have limitations reported in diagnostics. STB is unsupported.

## Fonts and search

Load authorized SHX through 「SHXフォント」 for vector stroke text. Fonts are never downloaded automatically. Noto Sans JP is the bundled fallback; missing/unsupported glyph substitutions are diagnosed.

Horizontal SHAPES 1.0/1.1, UNIFONT 1.0 and BIGFONT 1.0 are supported. BIGFONT assumes Shift-JIS. Vertical text, special variants and universal font compatibility are not implemented. Limits are 16MB per file, 64MB total and 64 fonts. Fonts remain in the tab's memory and are not included in settings JSON.

SHX lineweight can use a separate value (default 0.10mm) or the geometry pen. Filled TrueType weight is not changed. SHX search additions can be invisible text, annotations, or none. TrueType remains searchable even with none. Only used glyphs are embedded in PDF. Search, copying and annotation search vary by PDF reader. Missing visible/invisible fallback glyphs stop export rather than silently dropping text.

## Settings and JSON

Settings are saved only by explicit export. There is no per-drawing autosave. Pens, paper, snapping and same-name layer settings can be imported. Window bounds, selected view and drawing ID are not saved. Legacy v1 and independent format v1–v3 settings are accepted; new exports use v3.

Open parsed JSON accepts LibreDWG 0.13.4 full JSON. Save parsed JSON exports the independent DrawingDocument with diagnostics. These formats differ; saved independent models cannot currently be reopened directly. JSON contains drawing data and must not be published without authorization.

## Troubleshooting

For a missing Python runtime, follow README.html. For missing or altered files, extract a fresh distribution into a new folder rather than mixing versions. For parse failures, check DWG generation, input size and timeout. For display/export differences, inspect 「診断」. Export is stopped if the scene limit is exceeded.

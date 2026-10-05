# Supported DWG inputs

Accepted headers are AC1012, AC1014, AC1015, AC1018, AC1021, AC1024, AC1027 and AC1032 (R13, R14, 2000, 2004, 2007, 2010, 2013 and 2018 format families). Limits are 128 MB input and 120 seconds parsing. Accepted headers do not guarantee accurate parsing/rendering of every file or entity. Support depends on LibreDWG 0.13.4 and the adapter/scene. No 3D editing, DWG writes or intermediate DXF conversion occurs. Unsupported/substituted content is diagnosed.

MULTILEADER branches, arrows, landings, text and block annotations use the shared screen/PDF model. Per-line settings, straight-line gaps, layers and snapping are supported. Specialized formatting and approximations appear in drawing diagnostics.

WIPEOUT masks cover underlying geometry using the screen background color and white in PDF. Stored draw order and frame display/plot settings are respected. Display-only frames are excluded from PDF. Mask layers follow the visibility and printing controls.

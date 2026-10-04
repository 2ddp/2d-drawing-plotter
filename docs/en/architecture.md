# Architecture and parser boundary

GNU LibreDWG runs as a standalone CLI and writes its usual full JSON to a local file. It is not linked into the application and contains no DrawingDocument, viewer, layer UI or PDF logic. The only parser change is Unicode JSON encoding.

`bin/win64/dwgread.exe --version`

`bin/win64/dwgread.exe -O JSON -o parsed.json input.dwg`

The CLI works without the application or browser. Version 0.13.4 is pinned. Its published, version-specific JSON is not an internationally standardized neutral CAD format. The adapter alone translates that structure into DrawingDocument. Viewer and PDF share the resulting Scene. No DXF conversion occurs. Process separation is a technical boundary, not a final GPL legal opinion.

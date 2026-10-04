# Validation record — dev.39

## dev.39: naming and release artifacts

295 JavaScript tests and 30 Python tests passed. The same 295 JavaScript tests passed against both maintained sources and minified release modules. A bytecode-only server compiled with pinned CPython 3.13.16 started in isolation without application maintenance source. Existing regressions cover legacy settings import, settings export, vector PDF/font subsets/search, and network restrictions.

The 121-file runtime allowlist, pinned input hashes and ZIP integrity were verified. Static checks found no development payloads, developer absolute paths, or external page/CSS/fetch resource references. This is not Windows physical acceptance, whole-system packet monitoring, or final legal clearance. Pending items remain in RELEASE-CHECKLIST.json.

## dev.38 validation (previous version)

Development environment: Linux. 295 JavaScript regressions passed both against maintained and minified executable modules; 30 Python tests passed. Bytecode-only isolated server startup was verified.

Chrome Headless 151.0.7922.34 exercised executable JS/bytecode with drawing input UI, zoom/pan, model/layout, layers, CTB and PDF download. All 38 page requests were local; unexpected external requests, page exceptions and baseline CSP violations were zero. An intentional external fetch was rejected by CSP. The generated PDF had one page and 4,632 bytes.

The browser test used a controlled parser fixture, not the Windows dwgread executable. Windows parser/pixel-picker execution, real-drawing acceptance and OS/browser-wide packet monitoring remain pending. Fixed hashes, source/map/test/history exclusion, HTTP protections, connect rejection and package regeneration are checked separately. Automated checks are not release approval. Pending gates are recorded in RELEASE-CHECKLIST.json.

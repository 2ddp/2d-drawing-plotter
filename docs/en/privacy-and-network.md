# Network and local storage scope

The HTTP server listens only on a random 127.0.0.1 port, checks Host and requires same-origin plus a session token for POST. Requests are logged to the local console. Browser fetches use only /api/status, /api/parse, /api/ctb, /api/picker, /api/pick, /api/pick-cancel and the bundled TTF. JS, CSS, PDF libraries and fonts are local. No CDN, update check, WebSocket or telemetry is implemented.

CSP limits scripts, connects and fonts to the same origin. A Python audit hook rejects external connects, binds and DNS in this process. Neither mechanism is an OS-wide firewall or a guarantee about browser/parser subprocess behavior.

Parser input copies and JSON use OS temporary storage and are normally removed; forced termination can leave files. Fonts remain in tab memory. Screen capture is user-initiated. PDF/JSON/settings are explicitly saved by the user; input DWG is not written.

Static checks, external-connect rejection, local HTTP/API and executable-JS operations/PDF tests run in the development environment. Windows offline acceptance and complete packet/process monitoring are pending. Browser/OS independent connections must be distinguished during physical testing.

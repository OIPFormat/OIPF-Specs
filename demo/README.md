# OIPF — interactive demo

`index.html` is a self-contained interactive architecture demo (no build, no dependencies).

- **Technical view (default)** — *As-is vs With-OIPF*: field devices → control → edge/data → OIPF runtime → consumers, with protocol-labelled links (4–20 mA, OPC UA, MQTT/Sparkplug, SQL, REST) and animated data flow. Toggle between the bespoke point-to-point reality and the OIPF-routed architecture.
- **Executive view** — the OIPF decision loop (observe → infer → check → recommend → approve → act → record → learn) with the feedback path animating back.

Open `index.html` in any browser. To host it: Settings → Pages (serve from `/docs` or a `gh-pages` branch).

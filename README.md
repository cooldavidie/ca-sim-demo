# CA-SIM — live demo

**Compute Availability Simulator**: an event-level digital twin for AI data center power and cooling
infrastructure (SST / BESS / 800 VDC bus / ATS / UPS / CDU / GPU racks). The north-star metric is
**Compute Availability** — for any electrical or cooling event: how much compute is lost, for how long,
and what margin remains.

**Try it:** https://cooldavidie.github.io/ca-sim-demo/

## What you can do in the demo

- **Scenario cards** — one click loads an architecture + an event + a batch plane and runs it end to end.
- **Build** — a single-line diagram editor: drag components from the palette, wire a terminal to a terminal or onto a
  busbar, undo / redo, auto-arrange top-down; the inspector shows each parameter with its valid range, its unit and
  where the engine reads it. The normative content is hashed (SLD-DSL); placement on the canvas is not.
- **Simulate** — event-level run at dt = 0.5 ms: bus voltage, PSU holdup, pump coast-down, GPU thermal throttling,
  and the compute trace that results — played back on the same diagram. The run covers the event: its last change
  plus 10 s (at least 60 s, at most 300 s). An event that leaves the system in a new state — an N-1 trip, a load that
  stays at a new level — always runs the full 300 s and is judged on that window, which the result states; an event
  that does not fit in 300 s is reported as not determined rather than passed.
- **Coverage certificate** — sweep two parameters into a pass / derate / outage heatmap, export the
  certificate JSON (sha256 fingerprint) or a print-ready PDF report.
- **Control-loop resonance screening** — DC-link voltage-control loop against grid impedance
  (quartic characteristic polynomial, Durand-Kerner roots) with a stable / marginal / unstable plane.
- **Protection-window EMT** — a separate µs-level module for fault clearing and selectivity; the fault-class
  verdict folds in what the remaining loads suffer (thermal throttle, power cap, a healthy rack lost), and cells
  past the module's search limit with the bus still held are labelled as an assumption boundary, not a collapse.
- **N-1 component events** — `internal.*` entries (a pump failing, a solid-state breaker opening) with the
  loads behind the opened device as the expected loss and the verdict on everything beyond them.
- **Cooling plant and facility management** — chillers, DX compressors, pump stations and air handlers on the same
  motor model as the CDU pumps (trip, coast-down, restart delay, anti-short-cycle), a BMS that restarts them in
  priority bands, and three heat nodes (coolant loop, facility water, room air) with a thermal tail after the run.
  Results with a cooling plant are marked preview.
- **Ride-through compliance as data** — 25 public rules (ERCOT, PJM, ENTSO-E, OCP, ITIC, SEMI F47 …), each
  with its source clause; the selected rule's verdict enters the certificate. Where a rule excludes cooling, only the
  cooling actually inside the measured draw is subtracted, and ERCOT / PJM's tripped-cooling carve-out is read
  device by device.
- **OpenUSD export** — the SLD, the event, and a run's time-sampled results as `.usda` for digital-twin stages.

## Provenance

Built from public sources only: parameter defaults are industry white-paper order of magnitude
(800 VDC concept papers, ERCOT-class grid-code conventions); load-side events are calibrated against
the public MIT Supercloud dataset (arXiv 2108.02037) and NLR GenAI H100 power profiles (arXiv 2604.07345);
the resonance model follows arXiv 2605.17190. Every model's calibration level is declared in the
certificate footer (`doc` = datasheet-declared, not yet test-calibrated), every default carries a provenance
record, and a validation ladder computes what may be signed — today nothing is, and the certificate says so.

## Links

- Open event dictionary (EDL, CC-BY 4.0): https://github.com/cooldavidie/edl-dict
- Article: *link forthcoming*

## Notes

- Runs fully in the browser — no backend, nothing uploaded.
- The optional AI event-drafting feature asks for your own Anthropic API key and calls the API directly
  from your browser; the key is kept in `localStorage` only.
- This repository hosts the built demo only. Source is not published at this time — contact below.

Contact: davidchen.cch@gmail.com · David Chen

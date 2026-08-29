# CA-SIM — live demo

**Compute Availability Simulator**: an event-level digital twin for AI data center power and cooling
infrastructure (SST / BESS / 800 VDC bus / ATS / UPS / CDU / GPU racks). The north-star metric is
**Compute Availability** — for any electrical or cooling event: how much compute is lost, for how long,
and what margin remains.

**Try it:** https://cooldavidie.github.io/ca-sim-demo/

## What you can do in the demo

- **Scenario cards** — one click loads an architecture + an event + a batch plane and runs it end to end.
- **Build** — drag a single-line diagram; the normative content is hashed (SLD-DSL), display coordinates are not.
- **Simulate** — event-level run at dt = 0.5 ms over 60 s: bus voltage, PSU holdup, pump coast-down,
  GPU thermal throttling, and the compute trace that results.
- **Coverage certificate** — sweep two parameters into a pass / derate / outage heatmap, export the
  certificate JSON (sha256 fingerprint) or a print-ready PDF report.
- **Control-loop resonance screening** — DC-link voltage-control loop against grid impedance
  (quartic characteristic polynomial, Durand-Kerner roots) with a stable / marginal / unstable plane.
- **Protection-window EMT** — a separate µs-level module for fault clearing and selectivity.
- **OpenUSD export** — the SLD (and a run's time-sampled results) as `.usda` for digital-twin stages.

## Provenance

Built from public sources only: parameter defaults are industry white-paper order of magnitude
(800 VDC concept papers, ERCOT-class grid-code conventions); load-side events are calibrated against
the public MIT Supercloud dataset (arXiv 2108.02037) and NLR GenAI H100 power profiles (arXiv 2604.07345);
the resonance model follows arXiv 2605.17190. Every model's calibration level is declared in the
certificate footer (`doc` = datasheet-declared, not yet test-calibrated).

## Links

- Open event dictionary (EDL, CC-BY 4.0): https://github.com/cooldavidie/edl-dict
- Article: *link forthcoming*

## Notes

- Runs fully in the browser — no backend, nothing uploaded.
- The optional AI event-drafting feature asks for your own Anthropic API key and calls the API directly
  from your browser; the key is kept in `localStorage` only.
- This repository hosts the built demo only. Source is not published at this time — contact below.

Contact: davidchen.cch@gmail.com · David Chen

# CA-SIM — live demo

**Compute Availability Simulator**: an event-level digital twin for AI data center power and cooling
infrastructure (SST / BESS / 800 VDC bus / ATS / UPS / CDU / GPU racks). The north-star metric is
**Compute Availability** — for any electrical or cooling event: how much compute is lost, for how long,
and what margin remains.

**Try it:** https://cooldavidie.github.io/ca-sim-demo/

Built from public sources only: parameter defaults are industry white-paper order of magnitude
(800 VDC concept papers, ERCOT-class grid-code conventions); load-side events are calibrated against
the public MIT Supercloud dataset (arXiv 2108.02037) and NLR GenAI H100 power profiles (arXiv 2604.07345).
Calibration level of every model is declared in the certificate footer (`doc` = datasheet-declared).

- Article: (link forthcoming)
- Open event dictionary (EDL, CC-BY): https://github.com/cooldavidie/edl-dict
- Notes: runs fully in the browser (no backend, nothing uploaded); the optional AI event-drafting
  feature asks for your own Anthropic API key and calls the API directly from your browser.
- This repo hosts the built demo only. Source is not published at this time; contact below.

Contact: davidchen.cch@gmail.com · David Chen

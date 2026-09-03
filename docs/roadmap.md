# Roadmap

The roadmap deliberately separates a safe first release from broader research.
Dates will be assigned after funding and maintainer capacity are confirmed.

## Phase 0 — Public project foundation

- publish scope, architecture, threat model, and contribution policy;
- select the repository license and governance baseline;
- isolate deployment-specific prototype code;
- define reproducible development and test environments.

## Phase 1 — Reproducible prototype

- publish the minimal XDP datapath and Go loader/controller;
- support observe and shadow modes;
- document kernel, driver, and generic-mode requirements;
- publish a local traffic-generation test procedure;
- expose stable counters and reason codes.

## Phase 2 — Datapath hardening

- complete bounds-checked IPv4 and IPv6 parsing;
- define fragmentation and extension-header behaviour;
- introduce explicit map capacities and safe defaults;
- add whitelist and temporary address/prefix maps;
- add verifier, unit, fuzz, and negative-path tests.

## Phase 3 — Adaptive mitigation controller

- implement deterministic rate windows;
- add per-address and prefix aggregation;
- implement strike history and escalating temporary TTLs;
- add expiry and restart reconciliation;
- document threshold selection and false-positive controls.

## Phase 4 — Evaluation and initial release

- run reproducible throughput and CPU benchmarks;
- evaluate shadow decisions on production-derived aggregate scenarios;
- publish false-positive and recovery analysis;
- document deployments in front of common DNS stacks;
- complete security review and publish the first supported release.

## Later research — not promised for the initial release

- dynamic baselines and anomaly scoring;
- multi-node policy coordination;
- privacy-preserving shared reputation;
- stable application feedback interfaces;
- optional TCP transport-level signals for DNS over TLS and HTTPS frontends.


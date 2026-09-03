# Threat model

This document defines the initial security boundary. It will evolve with the
implementation and must be reviewed before a supported release.

## Assets

- availability of the recursive DNS service;
- CPU, memory, socket, and connection capacity on the DNS host;
- integrity of XDP policy and BPF maps;
- availability of legitimate clients behind shared prefixes or NAT;
- privacy of DNS users and operational telemetry.

## In-scope threats

- high-rate UDP/53 traffic from individual source addresses;
- coordinated traffic visible at IPv4 or IPv6 prefix granularity;
- repeated abusive behaviour after a temporary mitigation expires;
- malformed or suspiciously structured traffic detectable with bounded parsing;
- selected amplification-oriented QTYPE policy violations;
- state-exhaustion attempts against counters and mitigation maps;
- controller restart or temporary userspace failure;
- accidental operator misconfiguration that could cause broad drops.

## Out-of-scope threats

- attacks that saturate capacity before packets reach the host;
- spoofing that cannot be distinguished at the observation point;
- compromise of the Linux kernel, privileged controller, or deployment host;
- semantic inspection of encrypted DoH/DoT requests at XDP;
- guaranteed attribution of an attack to a person or organisation;
- replacement for resolver correctness, DNSSEC validation, or upstream filtering.

## Primary safety risks

### False-positive prefix mitigation

A shared NAT, mobile carrier, enterprise, or public resolver can concentrate
legitimate traffic. Prefix-level enforcement therefore requires longer
observation, stricter evidence, configurable prefix sizes, bounded TTLs, and a
shadow-mode validation path.

### Parser disagreement

The XDP parser must never attempt to replicate a full DNS implementation. Every
read must be bounds-checked, fragmented traffic must have an explicit policy,
and ambiguous packets should pass unless an operator knowingly selects a more
restrictive mode.

### Persistent stale policy

Temporary mitigation entries require monotonic expiry and controller
reconciliation. Restarting or upgrading the controller must not accidentally
convert a temporary action into a permanent ban.

### State exhaustion

All maps and userspace collections require fixed limits. Behaviour at capacity
must be deterministic, observable, and tested under adversarial cardinality.

## Privacy

The design does not require storing DNS query names or building user profiles.
Metrics should use aggregate counters and reason labels. If diagnostic sampling
is later added, it must be opt-in, bounded, documented, and disabled by default.

## Security invariants

- no enforcement without explicit operator enablement;
- every automatic ban has an expiry;
- every drop path has a stable reason counter;
- whitelist evaluation precedes automatic mitigation;
- map capacity and prefix width are configuration-visible;
- malformed input cannot cause out-of-bounds access;
- controller loss does not silently broaden policy;
- default configuration does not retain query names or client histories.


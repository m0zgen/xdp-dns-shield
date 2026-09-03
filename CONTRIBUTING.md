# Contributing

XDP DNS Shield is currently in pre-release preparation. Until the first code
publication, useful contributions include architecture review, threat-model
feedback, reproducible abuse scenarios, and deployment constraints from DNS
operators.

## Principles

- Keep the XDP datapath minimal and verifier-friendly.
- Prefer deterministic, explainable policy over opaque classification.
- Bound all state and document capacity behaviour.
- Treat false positives as a first-class availability risk.
- Do not submit production query logs, client addresses, secrets, or customer
  information.
- Include tests and operational documentation with behavioural changes.

## Before opening an issue

For suspected vulnerabilities, follow [SECURITY.md](SECURITY.md) instead of
opening a public issue. For design proposals, describe the threat, intended
operator outcome, failure modes, and how the behaviour can be tested.

## Developer workflow

Build, formatting, test, and sign-off requirements will be added with the first
source publication. Contributions will be accepted under the repository's
Apache-2.0 license.


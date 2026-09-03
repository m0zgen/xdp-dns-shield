# Benchmarking plan

Benchmarks must be reproducible and must distinguish packet-processing capacity
from the capacity of the surrounding network and DNS stack.

## Questions

- What packet rate can the datapath pass and drop in native and generic modes?
- What is the incremental CPU cost with observation enabled?
- How does map cardinality affect lookup and update behaviour?
- How quickly does the controller detect, install, expire, and reconcile policy?
- What legitimate traffic is affected by address or prefix decisions?
- Does the system recover predictably after controller restart and map pressure?

## Test modes

- baseline with no XDP program;
- XDP loaded in pass-only mode;
- observe mode with accounting;
- shadow mode with controller evaluation;
- enforce mode with address and prefix matches.

## Reported metrics

- packets per second and loss at the generator and target;
- host CPU by core and controller CPU/memory;
- pass/drop counts by stable reason;
- map occupancy, insertion failures, and eviction/expiry counts;
- decision latency from completed observation window to installed policy;
- expiry and recovery latency;
- false-positive and false-negative counts for labelled scenarios;
- kernel, NIC, driver, queue, CPU, and generator configuration.

## Reproducibility requirements

Benchmark scripts, traffic profiles, configurations, raw aggregate results, and
the commit identifier under test must be published. Production traffic must not
be redistributed. Any production-derived scenario must be anonymised and
reconstructed as a synthetic profile without query names or client identifiers.


---
name: load-testing
group: Quality
description: >-
  Design and run load tests with realistic traffic patterns against a stated baseline. Use when
  stress-testing systems with k6, Locust, or concurrency benchmarks.
---

# Load Testing

A load test that doesn't map to a real usage pattern tells you nothing useful — the goal isn't to generate traffic, it's to answer a specific question (can this handle launch day, where's the bottleneck, did the last deploy regress performance).

## Workflow

1. **Get the specific question being answered first.** "Load test my API" is too vague — is this capacity planning (how many concurrent users before failure), regression testing (did this change slow things down), or spike testing (can it survive a sudden traffic surge)? Each needs a different test shape.
2. **Model realistic traffic, not uniform hammering.** Real users don't all hit the same endpoint at the same rate — mix read-heavy and write-heavy paths in proportions that match actual usage if known, and say so explicitly as an assumption if not.
3. **Ramp gradually, don't spike from zero.** Start at a baseline load, step up incrementally (e.g. every 30-60 seconds), and watch for the point where latency or error rate inflects — that inflection point, not the test's max load, is usually the actual answer to "how much can this handle."
4. **Define pass/fail thresholds up front** — e.g. p95 latency under 500ms, error rate under 1%. Without a threshold, "the test ran" isn't the same as "the system passed."
5. **Watch server-side metrics alongside client-side results** — CPU, memory, DB connection pool exhaustion, queue depth. The load-test tool's own output (requests/sec, latency) only tells half the story; correlate with the system's own metrics to find the actual bottleneck.

## Choosing a tool

- **k6** — scriptable in JavaScript, good default for API load testing, integrates well into CI.
- **Locust** — Python-based, good when the test logic itself needs to be complex (e.g. simulating multi-step user flows with state).
- **Apache JMeter** — GUI-first, heavier, still common in enterprise contexts with existing JMeter test suites.

Default to k6 unless the user already has infra around one of the others.

## Anti-Patterns & Constraints

- Don't run a load test against production without explicit confirmation the user understands the risk — a poorly-scoped load test can take down a live system serving real users. Always ask whether this targets staging or production before writing a script.
- Don't report a single "requests per second" number as the whole answer — always pair throughput with latency percentiles and error rate, since a system can hit high RPS while still failing badly for individual users.

## Output format

Provide the runnable test script for the chosen tool, with a comment explaining the ramp stages and thresholds. Follow with a short summary of what question this test answers and what metrics to watch on the server side during the run.

See `references/k6-script-template.md` for a ready k6 example to adapt.

## Verification & Quality Checklist

- [ ] Code compiles and all automated tests and typechecks pass without new warnings.
- [ ] Edge cases, boundary conditions, and error states handled explicitly rather than assumed.
- [ ] No hardcoded secrets, credentials, or insecure defaults introduced.
- [ ] Changes are covered by a test that fails without them.

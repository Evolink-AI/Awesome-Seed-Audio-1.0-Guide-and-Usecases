# Recurring Update Contract

This repository is maintained by a quality-first use-case discovery loop.

## Schedule And Search Boundary

- Cadence: every two days at 10:00 Asia/Shanghai
- Search source: X/Twitter
- Exact query: `"seed audio"`
- Time window: the preceding 48 hours
- Publication cap: no more than 10 new use cases per run

The cap is not a quota. A run may publish fewer cases, or a verified no-op, when the evidence does not meet the selection rules in [Maintenance Guide](maintenance.md).

## Review Boundary

Every candidate is classified as selected, unsure, or dropped. Selected cases must preserve the public source, creator, date, evidence-grounded notes, and media attribution. The workflow does not reconstruct unpublished prompts or infer results from incomplete posts.

Unsure candidates remain in local review evidence rather than being published. Raw exports and private curation artifacts are not committed to this repository.

## Publication Gate

Before a push, the run must verify:

1. candidate handoff integrity and duplicate-source checks
2. README/data equality and localization parity
3. template structure and repository community files
4. R2 object origins and public links
5. EvoLink conversion surfaces and UTM attribution
6. zero unresolved P0/P1 audit findings

The run is complete only after the commit is pushed, GitHub Actions reaches a terminal passing state, and the remote README and media are read back successfully. A clean no-op must satisfy the same evidence boundary without creating an empty commit.

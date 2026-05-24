<!-- SPDX-License-Identifier: CC-BY-SA-4.0 -->

# Validation-log entry: Stage 1 release default model → Claude Haiku 4.5

**Decision date:** 2026-05-23
**Decided by:** Aaron Caswell
**Affected artifact:** `steelman-core` `engine.backends.anthropic.DEFAULT_MODEL_ID`
**Governance level:** Level 1 (per the `DEFAULT_MODEL_ID` docstring: "model change is a detector-affecting decision")

## What changed

`engine.backends.anthropic.DEFAULT_MODEL_ID` was changed from `claude-opus-4-7` to `claude-haiku-4-5`. The price-table comment in `engine/telemetry/prices.py` was updated to reflect the new default. Two test stubs (`tests/test_cli.py`, `tests/test_golden_e2e.py`) that previously hardcoded the literal `"claude-opus-4-7"` now reference `DEFAULT_MODEL_ID` so a future default change does not silently break the offline-cache-hit assertion they exercise.

The change is shipped with the `v0.1.0+rubric-0.2` Stage 1 release.

## Why

Cost. Per the price table:

| Model | Input $/M | Output $/M | Relative cost vs Opus |
|---|---|---|---|
| `claude-opus-4-7` | 15.00 | 75.00 | 1× |
| `claude-sonnet-4-6` | 3.00 | 15.00 | 5× cheaper |
| `claude-haiku-4-5` | 0.80 | 4.00 | ≈19× cheaper |

The Phase 5b live evaluation against `matched_v0.1` cost $5.20 on Opus (42 examples, 291 calls). Extrapolated to the matched_v0.2 dataset that Stage 2 demands (≥40 examples per direction, two-labeler — call it ~100 examples ≈ 700 calls), an Opus evaluation pass would run ~$13. A Haiku pass on the same scale would run ~$0.70. Over the Stage 2 cadence (weekly evals plus ad-hoc `analyze` invocations), the spread becomes load-bearing for whether the maintainer can run evaluation freely or has to budget it.

## What was NOT done

A Haiku-vs-Opus comparison pass on `matched_v0.1` to quantify the detector-quality delta. The Phase 6.1 hand-off (`validation-log/2026-05-23-matched_v0.1-detector-tuning.md`) recommended this as a $1 follow-up before the default-model decision. The maintainer has accepted the quality risk without that comparison on the grounds that:

1. Stage 1 ships with documented detector-quality carry-overs already (`self_contradiction` 33.33% asymmetry breach, `claim_burst` 20.83% asymmetry breach, both attributed to the small N=6-per-direction synthetic-single-labeler dataset rather than the model). Adding a documented model-tier carry-over to the same pile is consistent with the Stage 1 → Stage 2 hand-off posture.
2. Stage 2 will re-evaluate against `matched_v0.2` (the real-world ≥20-per-direction two-labeler dataset that is the load-bearing remediation for both breaches). At that point the comparison naturally happens against a dataset that actually distinguishes labeling variance from model bias. Running the comparison now on the small synthetic dataset would not produce a reliable signal.
3. The change is reversible. `DEFAULT_MODEL_ID` is one constant; bumping back to Opus or Sonnet for any specific workflow is `AnthropicBackend(model_id="claude-opus-4-7")` away.

## What is expected to happen

- Per-token engine cost drops by ≈19× for all default invocations.
- Detector quality drops by an unknown amount. The three production-quality detectors on `matched_v0.1` (`explicit_refusal`, `yes_no_non_answer`, `green_flags`) likely degrade least; the three with already-documented quality gaps (`self_contradiction`, `no_support_provided`, `claim_burst`) likely degrade more. None of this is measured on this dataset — it is expected behavior consistent with Anthropic's published Opus → Sonnet → Haiku capability ordering.
- Sibling product repos (`steelman-read`, `steelman-brief`, ...) consuming the engine in Stage 2 should expect to either accept Haiku quality, override the model_id explicitly per workflow, or trigger the matched_v0.2 re-evaluation that informs a model-tier policy decision.

## What evaluation was done before this change

- `bash scripts/phasekit-verify.sh`: 309 passed, 1 skipped (live smoke; opt-in).
- No live evaluation pass. The change is conservative on the safety axis (cheaper, lower-quality default; pipeline machinery is model-agnostic) and aggressive on the cost axis. Quality risk is documented above.

## Cross-references

- Engine constant: `engine/backends/anthropic.py` `DEFAULT_MODEL_ID`
- Price table: `engine/telemetry/prices.py`
- Phase 6.1 entry that flagged the comparison-pass follow-up: `validation-log/2026-05-23-matched_v0.1-detector-tuning.md` "Open items"
- Phase 5b baseline (Opus): `evaluation/reports/2026-05-18-matched_v0.1.md`
- Phase 6.1 post-tuning (Opus): `evaluation/reports/2026-05-23-matched_v0.1.md`

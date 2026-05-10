# Stage 0 → Stage 1 transition — steelman-core scaffolded

**Date:** 2026-05-09
**Type:** Roadmap stage transition (cross-cutting; ROADMAP.md is the affected artifact)
**Affected artifacts:** Sibling repository `steelman-core` created at `../steelman-core/`; `validation-log/` directory canonicalized at meta-repo root.

## What changed

Stage 1 of `ROADMAP.md` (Steelman Core — the engine) has been initiated. The sibling repository `steelman-core` was scaffolded using [phasekit](https://github.com/porkchop/phasekit) with the `default` profile. The new repo contains the phasekit-installed agents, hooks, settings, and 7-phase build templates, plus filled-in project-owned specs:

- `steelman-core/docs/SPEC.md` — concrete Stage 1 specification derived from `ARCHITECTURE.md`, `RUBRIC.md` v0.2, and `MISSION.md`
- `steelman-core/docs/ARCHITECTURE.md` — engine-side reification of the constitutional architecture, including layer boundaries, data model, runtime dependencies, testing strategy, and the AGPL-3.0 / CC BY-SA 4.0 license boundary at the package level
- `steelman-core/docs/PROD_REQUIREMENTS.md` — what "ready for downstream consumers" means for a library-only Stage 1
- `steelman-core/CLAUDE.md` — orientation for AI assistants working in the engine repo, including the cross-repo invariants
- `steelman-core/README.md` — public entry point

Tech stack for the engine has been committed to: Python 3.12+, pydantic v2, the `anthropic` SDK behind a swappable backend abstraction, `uv` for dependency management, `ruff` + `mypy --strict` for lint and typecheck, `pytest` + `hypothesis` for tests, filesystem cache by default. None of these were pre-decided in the foundational documents; they are Stage 1 design decisions and are recorded here so that any future amendment can name what was changed.

Separately, the `validation-log/` directory was canonicalized at the meta-repo root. The earlier scratch location at `mnt/user-data/outputs/steelman-meta/validation-log/` was an artifact of the export tooling used during Stage 0 drafting; the existing README and the v0.1→v0.2 adversarial-review entry were moved to `./validation-log/` via `git mv` and the `mnt/` tree was removed. `README.md` and `ARCHITECTURE.md` (in this repo) already reference the root location, so no doc edits were required.

## What evidence prompted the change

- All foundational documents are at v0.1 or later (RUBRIC at v0.2 following the adversarial-review entry of the same date). Stage 0 gating criterion (a) is met.
- Licensing decisions in `LICENSING.md` are explicit and will be enforced by license headers and the `engine/` ↔ `rubric-impl/` package boundary in the new repo. Stage 0 gating criterion (c) is met.
- The Stage 0 → Stage 1 transition is conditioned on (b) "adversarial review of the rubric completed" and (d) "public location for the meta-repo established." Both are **partially met**; see the next section. The maintainer's judgment, recorded here for review, is to proceed with engine scaffolding while explicitly tracking these as cross-cutting Stage 1 work rather than treating them as fully closed.

## Open Stage 0 gates carried into Stage 1

Two Stage 0 gating criteria remain open and are tracked here so that the project does not silently treat them as resolved:

**(b) Cross-faction adversarial review of the rubric.** The v0.1 → v0.2 review was LLM-based (a single source) per `validation-log/2026-05-09-adversarial-review-chatgpt.md`. `GOVERNANCE.md` Level 4 amendments require cross-faction validation, and the prior entry itself notes: "the next round of rubric review should be more deliberately diverse — at minimum, a mix of human reviewers with different ideological starting points." Treating v0.2 as the rubric the engine implements is acceptable for Stage 1 *implementation work* (detectors, evaluation harness, refusal gates), because that work is internal and reversible. It is **not** acceptable as the rubric of record for any product-stage launch. Before Stage 2 (Steelman Read), a deliberately diverse human review of v0.2 must be solicited and its results recorded as a validation-log entry.

**(d) Public location for the meta-repo.** The meta-repo currently has a single remote (`origin`) but no published URL is named in any document. This is required because the sibling product repos and any external reviewers must be able to reach the constitutional documents read-only. Naming a public host (e.g., GitHub) and confirming the repo is reachable there is a Stage 1 cross-cutting task, owed before any work is solicited from external reviewers.

These two open items are not blockers for engine implementation; they are blockers for product-stage launch and for external-review activities. They will be resolved in their own validation-log entries.

## What evaluation was done before this change

- `ROADMAP.md` Stage 0 gating criteria were enumerated and evaluated against the current state of the repo and the `validation-log/` entry of the same date. Two of four are fully met; two are partially met as described above.
- The phasekit tool was inspected at `~/dev/projects/aaron/phasekit/` before bootstrap to verify it is non-destructive (idempotent enrichment), language-agnostic, and produces project-owned specs that are customizable without modifying phasekit itself.
- The license boundary was verified to map cleanly onto the directory structure phasekit installs: `engine/` and `cli/` (AGPL-3.0) sit alongside `rubric-impl/` and `evaluation/` (CC BY-SA 4.0) without sharing imports, satisfying the boundary intent in `LICENSING.md`.

## What was projected

- Engine implementation work can begin in `steelman-core` immediately, working through phasekit's audit-first phase loop starting from Phase 0 (project bootstrap) which is now nearly complete.
- The version-sync invariant between `RUBRIC.md` and `steelman-core/rubric-impl/` will be enforced at engine startup and in CI from Phase 1 onward. A mismatch will be a deployment-blocking error, not a warning.
- Cost telemetry will exist from Phase 1, allowing the project to validate the `ROADMAP.md` Stage 1 budget assumption ($200–$500/month) against actual evaluation-pass costs before committing to Stage 2.
- The two open Stage 0 gates (cross-faction review, public hosting) will be resolved in their own log entries before Stage 2 begins.

## What the actual impact has been

To be filled in as `steelman-core` work progresses. First concrete data points expected:

- Phase 1 (domain model and core engine) approval: confirms the data models in `ARCHITECTURE.md` survive contact with implementation.
- First evaluation pass on a politically-matched mini-dataset: the first real test of whether symmetric-application reporting works as described.
- Cost telemetry from the first non-trivial evaluation pass: validates or refutes the Stage 1 budget projection.
- Cross-faction rubric review entry: closes Stage 0 gate (b).
- Public-hosting entry: closes Stage 0 gate (d).

This entry will be updated as those data points land.

## Notes on process

This is the first cross-repo transition log entry. Future entries that affect both `steelman-meta` and a sibling repo should follow the same pattern: name the affected artifacts in both repos, record what was decided here so that the engine repo can reference it, and note any open governance items the transition does not close.

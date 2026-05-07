# Steelman — Roadmap

> **Status:** Draft v0.1. This document describes the bootstrap plan for the ecosystem. It changes more often than the foundational documents — as stages complete, as evidence accumulates, and as priorities adjust based on validation. Updates are recorded in the validation log.

## How this roadmap works

The ecosystem is built in stages. Each stage produces specific artifacts and validates specific assumptions before the next stage begins. Stages do not advance on calendar pressure; they advance when their gating criteria are met.

This is the inverse of typical product roadmaps that fix dates and adjust scope. Here, scope is fixed by what must work for the next stage to be possible, and time adjusts to whatever the work actually requires.

The roadmap is not a contract. It reflects current best understanding of the path; it will be revised as evidence accumulates. Significant revisions are recorded in the validation log with reasoning.

## Stage 0 — Foundations

**What it produces.** The meta-repository with foundational documents in working draft form: `MISSION.md`, `ECOSYSTEM.md`, `RUBRIC.md`, `ARCHITECTURE.md`, `GOVERNANCE.md`, `LICENSING.md`, this roadmap, and the validation log structure.

**Gating criteria for Stage 1.**
- All foundational documents drafted at v0.1 or later.
- Adversarial review of the rubric completed: a reviewer attempts to find symmetric application failures and the rubric is revised in response.
- Licensing decisions confirmed and applied to the meta-repo.
- Public location for the meta-repo established.

**Notes.** Stage 0 is mostly writing, not coding. It is the cheapest stage in budget terms but the most consequential in setting the project's direction. Time spent here is not optional.

## Stage 1 — Steelman Core (the engine)

**What it produces.** A working analytical engine implementing Tier 1 categories of the rubric. Source code, evaluation datasets for each Tier 1 category, test suites, documentation. Not yet exposed to end users.

**Components.**
- Repository scaffolded with phasekit.
- Rubric implementation in code, version-synced with `RUBRIC.md`.
- Tier 1 detectors: self-contradiction, unsupported claim, question-dodging, gish-gallop pattern.
- Argument extraction pipeline producing argument cards.
- Output assembly with full provenance.
- Caching layer.
- Evaluation harness with symmetric application checks across the political spectrum.

**Gating criteria for Stage 2.**
- All Tier 1 detectors operational with documented accuracy on evaluation datasets.
- Symmetric application validated: detection rates for similar offenses are comparable across politically diverse examples.
- Provenance complete: every output traces back to specific rubric clauses and supporting evidence in the input.
- Engine is installable and runnable by a third party following the documentation.

**Notes.** Stage 1 is the longest and most expensive stage. The quality of the engine determines whether anything downstream is worth building. Resist the temptation to move to Stage 2 before Stage 1 is solid; a thread analyzer running on a flaky engine produces flaky analyses, which damages trust in everything that follows.

This stage is also where most of the budget goes. API costs for evaluation runs, model experimentation, and possibly fine-tuning add up. Aggressive caching and tiered model usage matter from day one.

## Stage 2 — Steelman Read (thread analyzer)

**What it produces.** A simple user-facing product. Web interface (and CLI) where a user pastes a URL or text and receives engine analysis. Stateless beyond caching. No user accounts in v1.

**Components.**
- Repository scaffolded with phasekit, dependent on engine-repo.
- Web interface for URL/text input.
- Output rendering: argument cards, fallacy detections with explanations, claim graph (where relevant).
- Public deployment at minimal cost.

**Gating criteria for Stage 3.**
- Thread analyzer used by the project's contributors and a small set of external testers (target: 20-50 testers across diverse political backgrounds) for at least three months.
- User feedback collected and major issues addressed.
- No major credibility-damaging errors observed in the test period.
- Cost per analysis understood and within sustainable budget.

**Notes.** The thread analyzer's value is largely internal: it validates the engine before more public products. External users provide feedback, but the primary purpose is to find engine quality issues at low stakes.

If the thread analyzer reveals significant engine problems, return to Stage 1 work rather than pushing forward. The substrate matters more than the schedule.

## Stage 3 — Steelman Brief (brief generator)

**What it produces.** A topic-level product. User specifies a topic (with a thesis statement); the system produces a structured brief with strongest arguments per side, key disputes, and provenance.

**Components.**
- Repository scaffolded with phasekit, dependent on engine-repo.
- Topic specification interface.
- Aggregation pipeline (initially with user-supplied source links; possibly later with limited search-based discovery).
- Brief rendering and persistence.
- Versioning for briefs (state of debate at time of generation).

**Gating criteria for Stage 4.**
- Brief generator produces useful briefs for at least 10 contested topics across the political spectrum.
- Briefs evaluated by reviewers from different ideological backgrounds; no consistent bias observed.
- Topic data model proven sufficient for the engine's needs.
- Cost per brief understood and within budget.

**Notes.** This stage is where the topic-level data model gets stress-tested. If the model proves inadequate for representing real debates, this is the moment to fix it before the atlas depends on it.

## Stage 4 — Steelman Reply (reply assistant)

**What it produces.** A generative product. The user is composing a reply; the system analyzes the thread and the draft, surfaces analytical context, and offers feedback on the draft. The most complex product.

**Components.**
- Repository scaffolded with phasekit, dependent on engine-repo.
- Browser extension or web interface (decision made at start of stage).
- Real-time analysis of user drafts.
- Symmetric self-application: the user's drafts are analyzed by the same standards as the thread.
- Refusal logic for out-of-scope assistance.
- AI-assisted markers on any generated content.

**Gating criteria for Stage 5.**
- Reply assistant used by a closed beta cohort for at least three months.
- Symmetric self-application validated: users report that the assistant flags their own fallacies as readily as opposing views' fallacies.
- Refusal behavior tested: the assistant correctly declines to help with personal attacks, gish gallops, etc.
- No major credibility-damaging incidents.
- Authenticity and disclosure questions addressed in product UX.

**Notes.** This is where the project's neutrality commitment is most directly tested by users. If the reply assistant feels biased to users on any side, the project has failed at this stage and must address the issue before further stages.

The reply assistant is also where the "Goodhart" risk is highest — users may try to optimize their drafts for the analyzer's approval rather than for genuine quality. The product's design must resist this, including by sometimes recommending disengagement rather than helping the user reply at all.

## Stage 5 — Steelman Notes (labeler)

**What it produces.** The first publicly-exposed product. A Bluesky labeler running the engine against a configurable scope of public posts. Users subscribe; subscribers see labels on the content they view.

**Components.**
- Repository scaffolded with phasekit, dependent on engine-repo.
- Bluesky labeler API integration.
- Scope and threshold configuration (which posts are labeled).
- Conservative labeling: only Tier 1 categories with high confidence; pattern surfacings where appropriate.
- Public dispute interface integrated with the labeler.
- Cross-faction validation infrastructure for high-stakes label classes.

**Gating criteria for Stage 6.**
- Labeler operational on Bluesky with non-trivial subscriber count.
- Dispute volume manageable; resolutions are timely and consistent.
- No systematic bias detected in label distribution across political directions.
- The project has demonstrated it can correct errors visibly and quickly.

**Notes.** This is the stage that exposes the project to its first significant reputational risk. Errors here are public and persistent. The labeler must not launch until the engine is robust enough to survive public scrutiny and the dispute machinery is operational.

This is also the stage where the project starts developing a public reputation across political lines. That reputation is fragile. The first months of operation matter disproportionately for long-term credibility.

## Stage 6 — Steelman Atlas and Steelman Record

**What it produces.** The most ambitious products. Steelman Atlas is a public, persistent map of contested topics. Steelman Record monitors specific politicians, pundits, and public intellectuals on policy questions.

**Components.** Specified in detail at the start of Stage 6, based on what has been learned from earlier stages.

**Gating criteria.** The project's continued existence and credibility. Stage 6 is not gated by a fixed checklist; it is gated by the project being mature enough for these products to launch responsibly.

**Notes.** Stage 6 may be split into two stages with Atlas before Record, or vice versa, or they may run in parallel. The decision is made when Stage 5 has stabilized.

Steelman Record in particular has highest reputational stakes. If the project cannot operate Steelman Notes with broad credibility, it should not attempt Steelman Record.

## Cross-stage work

Some work runs across all stages and is not assigned to any specific one.

**Validation log maintenance.** Throughout. Every stage adds entries; the log is one of the artifacts that demonstrates the project's self-improvement.

**Rubric evolution.** Refinements (Level 3) and amendments (Level 4) happen as evidence accumulates. The starter rubric is small; categories are added when the engine can support them and the governance procedure can validate them.

**Governance maturation.** Stage 1 has only maintainers. Stage 2-3 introduces basic dispute interfaces. Stage 4-5 introduces formal Level 1 and Level 2 dispute handling. Stage 5-6 brings the dispute panel and cross-faction validation online.

**External engagement.** Throughout. Reviewers from across the political spectrum are recruited continuously. Public communication about the project's purpose and limits is consistent.

## Budget by stage

Approximate operating costs (excluding the maintainers' time):

- **Stage 0:** Negligible. Documentation work; possibly $50/month for development tools.
- **Stage 1:** $200-500/month. Heavy API usage for evaluation and experimentation; modest infrastructure for the engine repo.
- **Stage 2:** $300-600/month. Engine costs continue; thread analyzer hosting; small but real ongoing API costs for analyses.
- **Stage 3:** $500-900/month. Brief generation is more expensive per query; aggregation across multiple sources amplifies costs.
- **Stage 4:** $700-1500/month. Reply assistant in beta; per-user costs scale with engagement.
- **Stage 5:** $1500-4000/month. Public labeler running against meaningful Bluesky volume. This is where costs scale most.
- **Stage 6:** $3000+/month. Atlas storage and serving; public-figure tracker curation.

These are rough estimates. Actual costs depend heavily on caching effectiveness, model choice (cheaper models for some stages dramatically reduces costs), usage volumes, and infrastructure decisions. The project should build cost telemetry from Stage 1 forward and re-estimate at each stage.

If the available budget cannot sustain the next stage's projected costs, the project does not advance. Either the cost model improves (cheaper models, better caching, scope reduction) or the stage is deferred.

## Indicators of trouble

The roadmap should be revisited if any of the following occur:

- **Symmetric application failures.** Evaluation datasets show consistent bias the engine cannot fix. This is a fundamental problem; address it before advancing.
- **Persistent low engine accuracy.** Stage 1 work produces an engine that doesn't reach acceptable accuracy on Tier 1 categories. The rubric may be wrong, the implementation may be wrong, or the categories may not be tractable; investigate before continuing.
- **External hostility from across the spectrum.** If the project is criticized from one direction only, that's expected; if it's criticized from all directions, that may indicate it's serving none.
- **Budget collapse.** Sustained inability to fund the current stage's operating costs. Either find sustainable funding, narrow scope, or close the project.
- **Maintainer drift.** The maintainers find themselves making decisions that favor one political direction. Pause the project and address this seriously; project drift is the most dangerous failure mode.

If any of these occur, return to Stage 0 thinking — re-examine the foundations, not just the current stage's implementation.

## Indicators of success

The roadmap is working if:

- Each stage's gating criteria are met before advancing.
- The validation log shows substantive entries about what was tried, what was learned, and what changed.
- External reviewers from different political directions report finding the project's outputs useful and fair.
- Disputes are filed and resolved with reasoning users find understandable.
- The rubric evolves through the procedures rather than through ad-hoc edits.
- The project's costs remain within a sustainable range.

These are process indicators, not outcome metrics. Outcome metrics (effect on discourse quality at scale) take years to assess and are difficult to attribute. Process indicators are what the project can manage in the near term.

## Revisions to this roadmap

Substantive revisions to the roadmap are recorded in the validation log with reasoning. Minor adjustments (date estimates, component breakdowns) can be made without ceremony. The numbered stages and their gating criteria are stable; the work within each stage adapts to what's learned.

The roadmap is a working hypothesis about the path forward. Like any working hypothesis, it earns or loses credibility based on what evidence accumulates. The validation log is the record of how the hypothesis fares.

# Steelman — Governance

> **Status:** Draft v0.1. This document describes how disputes are handled and how foundational documents change. The procedures here are themselves amendable, but only through the same procedures they describe.

## What this document is

The project's commitment to contestability is meaningful only if there are real procedures by which the rubric, the engine, and the foundational documents can be challenged and improved. This document specifies those procedures.

The procedures are designed to be:

- **Public.** The rules are visible; their application is visible; the outcomes are visible.
- **Effortful.** Disputes require engagement with the rubric, not just complaint volume.
- **Self-applying.** Disputes are evaluated using the same standards the rubric applies elsewhere.
- **Resistant to capture.** High-stakes changes require cross-faction validation; no single faction can drive the rubric.

The procedures are not designed to maximize the throughput of disputes. They are designed to produce decisions that hold up over time.

## Levels of dispute

Different kinds of disputes have different stakes and are handled differently.

**Level 1 — Specific label dispute.** A user disputes a single label applied to a specific post or argument. The criterion may have been misapplied, the supporting span may have been misread, or the call may be on the borderline.

**Level 2 — Pattern dispute.** A user demonstrates that the engine consistently misapplies a category, with multiple specific examples. This is product feedback rather than per-label correction; it implies a possible engine or rubric refinement.

**Level 3 — Rubric refinement.** A change to how a category is defined, what evidence triggers it, or where its scope lies. Smaller than adding or removing a category, but still affects how the engine applies the category going forward.

**Level 4 — Rubric amendment.** Adding a new category, removing an existing category, changing fundamental definitions, or revising the principles in `MISSION.md`. The most consequential changes.

Each level has its own procedure.

## Level 1 — Specific label disputes

**How to file.** A user with access to the disputed label submits a dispute through the standard interface. The submission requires:

1. A reference to the specific label being disputed.
2. Selection of a dispute type:
   - "Criterion misapplied" (the label's criteria don't match the content)
   - "Span misread" (the supporting span doesn't show what the engine claims)
   - "Borderline call" (the call is defensible but the user believes the other side is more defensible)
   - "Out of scope" (the engine should not have analyzed this content at all)
3. A reasoning chain supporting the dispute. The reasoning must reference specific rubric clauses or features of the content. Generic dismissals ("this is wrong because the engine is biased") are not sufficient and will be rejected at intake.

**Initial evaluation.** The dispute is evaluated by the engine itself against the rubric. Three possible outcomes:

- **Dispute appears strong.** The engine flags the dispute for human review with a recommendation to consider modifying or withdrawing the label.
- **Dispute appears weak.** The engine flags the dispute as containing fallacies (in which case, which ones) or as not engaging with the actual rubric criteria.
- **Borderline.** The engine cannot confidently classify the dispute.

The engine's preliminary evaluation is not the final word; it is information for the human reviewer.

**Human review.** Disputes flagged for human review are handled by the dispute resolution group (initially the project maintainers; eventually the elected dispute panel described below). The reviewer:

1. Examines the disputed label and the dispute reasoning.
2. Applies the rubric to determine whether the criterion was met.
3. Documents the determination and the reasoning.

**Outcomes.** Possible outcomes:

- **Label upheld.** The criterion was met; the label stands. The dispute is recorded and visible alongside the label.
- **Label disputed.** The criterion may or may not have been met; reasonable interpretation differs. The label is marked as disputed; both the label and the dispute reasoning are visible to viewers.
- **Label withdrawn.** The criterion was not met; the label was an error. The label is removed; the withdrawal is recorded.
- **Label refined.** The original label is replaced with a more accurate one (e.g., a definitive label is downgraded to a pattern surfacing).

**Visibility.** All Level 1 disputes and their resolutions are public. The disputant's identity may be pseudonymous (similar to Bluesky labeler conventions) but the dispute reasoning and resolution are not redactable.

**No retroactive cascade.** A Level 1 resolution applies to the specific label disputed. It does not automatically reapply to other labels using the same criterion. If the dispute reveals a pattern problem, the reviewer escalates to Level 2.

## Level 2 — Pattern disputes

**How to file.** A user submits a Level 2 dispute by demonstrating that the engine consistently misapplies a category. The submission requires:

1. The category in question.
2. Multiple specific examples (typically at least five) where the user believes the category was misapplied.
3. An analysis of the pattern — what the engine appears to be doing wrong, and why.
4. Where applicable, examples of cases where the category was applied correctly, to demonstrate that the user understands the criterion and is not just disputing all applications.

**Initial evaluation.** Pattern disputes go directly to human review; the engine does not preliminarily evaluate them, because the dispute is precisely about the engine's pattern of behavior.

**Human review.** Reviewers examine the cited examples and assess:

1. Whether the pattern the disputant identifies is real.
2. If real, whether the pattern indicates an engine implementation issue (the engine is failing to apply the rubric correctly) or a rubric issue (the rubric itself is producing the wrong calls).
3. What change, if any, would address the pattern without introducing new problems.

**Outcomes.** Possible outcomes:

- **No pattern.** The cited examples don't actually demonstrate a consistent issue. The dispute is closed with reasoning.
- **Engine issue.** The rubric is correct but the engine is misapplying it. An engine update is scheduled, with appropriate evaluation before deployment.
- **Rubric issue.** The rubric itself produces the cited problems. A Level 3 rubric refinement is initiated.
- **Acceptable pattern.** The pattern exists but is consistent with the rubric's intended behavior. The dispute is closed with reasoning explaining why.

**Visibility.** Level 2 dispute filings, evaluations, and outcomes are public.

## Level 3 — Rubric refinement

**Initiation.** A Level 3 refinement may be initiated by:

- Resolution of a Level 2 dispute that identified a rubric issue.
- A proposal from any user or contributor.
- A proposal from the maintainers based on internal observations.

**Proposal contents.** A refinement proposal specifies:

1. The category being refined.
2. The current criterion (quoted exactly).
3. The proposed criterion (quoted exactly).
4. The reasoning for the change.
5. Examples illustrating the change's effect.
6. An assessment of any side effects (other categories affected, edge cases newly created or resolved).

**Evaluation.** Refinement proposals undergo:

1. **Adversarial review.** A reviewer attempts to find cases where the proposed criterion produces wrong calls or where it favors arguments from one political direction over others. The proposal stands or falls based on whether it survives this review.

2. **Symmetric application check.** The proposed criterion is evaluated against matched examples from across the political spectrum. If it produces meaningfully different rates of detection for similar offenses depending on political direction, the criterion is rejected and reformulated.

3. **Public comment period.** The proposal is published for at least two weeks with a clear "comment by" date. Comments are public and considered in the final evaluation.

4. **Maintainer decision.** The maintainers, with input from the dispute panel where one exists, accept, reject, or modify the proposal. The decision and its reasoning are public.

**Implementation.** Accepted refinements are implemented in code, evaluated against the test sets (with a hard requirement that they don't regress symmetric application), and deployed with version bumps to the rubric.

**No retroactive relabeling.** Refinements apply to new analysis going forward. Old analyses are not retroactively updated. Users viewing old analyses see them with their original rubric version.

**Visibility.** Level 3 proposals, comments, evaluations, and decisions are public and persisted.

## Level 4 — Rubric amendment

The most consequential changes. Adding or removing categories. Changing fundamental definitions. Revising the principles in `MISSION.md`.

**Initiation.** A Level 4 amendment may be initiated by:

- The maintainers, based on internal review.
- A proposal from any user or contributor that meets a sponsorship threshold (described below).

**Sponsorship threshold.** Because Level 4 amendments are consequential, casual proposals are filtered out. A user-initiated Level 4 proposal requires sponsorship: at least N established contributors (where established is defined by quality of past Level 1-3 participation; specific thresholds in the implementation document) endorse the proposal as worth considering. Sponsorship is not endorsement of the substance; it is endorsement that the proposal is serious enough to evaluate.

**Cross-faction validation.** Level 4 amendments require validation across ideological lines. The mechanism is adapted from Community Notes' bridging algorithm: a proposal is adopted only if endorsed by contributors whose past dispute and refinement participation indicates ideological diversity. The specific algorithm is implemented in code, public, and itself subject to refinement.

This requirement is the strongest defense against rubric capture. A faction cannot drive a Level 4 amendment by mobilizing its own contributors; agreement from contributors with different rating histories is required.

**Public comment period.** Level 4 proposals have a longer public comment period than Level 3 (at least four weeks). The comment period is announced widely, including to known critics of the project from any direction.

**Adversarial review.** The same adversarial review applied to Level 3 refinements applies to Level 4 amendments, but more thoroughly. A specific reviewer is assigned to find the strongest argument against the proposal, regardless of whether they personally support or oppose it. The strongest counterargument is published alongside the proposal.

**Decision.** The maintainers make the final decision after comments and validation. The decision is public, with full reasoning addressing the most substantive comments and counterarguments. If the maintainers' decision goes against the cross-faction validation result, the reasoning must explicitly address why.

**Implementation.** Accepted amendments require corresponding updates to `RUBRIC.md`, the engine code, evaluation datasets, and any other affected documents. Implementation is staged: the amendment is announced with an effective date, and analyses produced before that date remain under the old version.

## Maintainers and the dispute panel

**Maintainers.** Initially, the project maintainers are the people building the project. As the project grows, this role formalizes. Maintainers have decision authority over:

- Engine implementation.
- Architecture decisions.
- Final word on Level 3 and Level 4 outcomes (subject to cross-faction validation requirements at Level 4).

Maintainers' identities are public. Their reasoning on contested decisions is published.

**Dispute panel.** When the project's dispute volume warrants it, a dispute panel is established. The panel handles Level 1 and Level 2 disputes that require human review, freeing maintainers to focus on architectural and Level 3+ matters.

Panel members are selected to be ideologically diverse. The selection process is public. Panel members serve fixed terms with rotation. A panel member who appears to be applying the rubric inconsistently across political directions is subject to removal through a transparent procedure.

The panel exists to scale dispute handling, not to replace maintainer judgment on architectural decisions.

## Rubric-level artifacts beyond the rubric document

Some artifacts have rubric-level influence on the engine's analysis even though they are not the rubric document itself. These are governed under the same procedures as the rubric.

**The canonical formulation library.** Referenced in the strawman pattern (see `RUBRIC.md`), this is a maintained set of defensible formulations of common positions on contested topics. Because the library influences what the engine considers a strawman, it has substantial bias-risk surface area. Additions and modifications to the library follow the Level 4 amendment process, including cross-faction validation. The library is open source under CC BY-SA 4.0.

**Evaluation datasets.** The datasets used to verify the engine's behavior define what "working correctly" means in practice. Curation decisions for these datasets are governed at the rubric level: the inclusion criteria are public, contested cases are reviewed adversarially, and changes to inclusion criteria follow the Level 3 or Level 4 amendment procedure depending on scope.

**Fine-tuned model weights.** Model weights produced by the project embody analytical decisions. The training data, training configurations, and evaluation results are public. Significant changes (replacing a base model, retraining on substantially different data) follow Level 4 amendment procedures.

The principle behind these treatments: any artifact whose curation could shift the engine's analysis in politically asymmetric directions is governed at the rubric level. A project that opens its rubric while keeping the canonical formulation library private has not actually opened its rubric.

## What governance does not do

**It does not censor.** The project does not remove content from platforms, advise platforms to remove content, or otherwise act on content beyond producing analytical labels. The governance of the project is governance of its own analytical claims, not governance of speech.

**It does not adjudicate disputes about content the project has not analyzed.** Users cannot file disputes about labels the engine did not produce. Users cannot ask the project to label content that the engine has not been requested to analyze.

**It does not replace platform moderation, journalism, or fact-checking.** The project's analytical scope is structural fallacies and argument patterns, not factual accuracy in general or content acceptability. Other organizations do those jobs; the project complements rather than replaces them.

**It does not provide advisory opinions.** The governance procedures handle specific disputes about specific labels and specific rubric clauses. They do not produce general statements about "what the rubric thinks of X." The rubric's content is in `RUBRIC.md`; questions about how it would apply to hypothetical cases are answered by applying it.

## What happens when governance fails

The procedures here are imperfect. They will sometimes produce wrong outcomes. Worse, they may sometimes be captured by patient bad-faith actors who learn the procedures and game them.

When this happens, the responses available include:

**Procedural amendment.** The procedures themselves are amendable through Level 4 amendments. If a procedure is consistently producing bad outcomes, the procedure is the problem.

**Maintainer override.** In extreme cases, maintainers can override governance outcomes. This power is constrained: overrides are public, justified in detail, and themselves subject to Level 4 review at the next opportunity. Overrides that appear to favor one political direction systematically are project-ending events; the project's credibility cannot survive them.

**Project closure.** If the governance procedures cannot be made to work, the project closes rather than continuing in compromised form. The artifacts (rubric, engine, documentation) remain available. Closure is preferable to operating a captured project under the original name.

These responses are listed in escalation order. The default is to use the procedures and improve them. Closure is a last resort.

## Initial bootstrap

The procedures described here cannot all be operational on day one. Bootstrap proceeds as follows:

**Phase 1 (pre-launch).** Maintainers handle all decisions. The rubric and architecture are drafted with adversarial review by the maintainers themselves and any reviewers they recruit. There is no public dispute machinery yet because there are no public outputs to dispute.

**Phase 2 (early users).** Level 1 disputes are accepted and handled by maintainers directly. The dispute interface is built. The validation log is started.

**Phase 3 (growth).** Dispute volume grows; a dispute panel is established. Level 2 disputes are formalized. Cross-faction validation infrastructure is built.

**Phase 4 (full governance).** All four levels of dispute are operational. Cross-faction validation is in production for Level 4 amendments. The procedures are documented in detail and have been tested.

The project's growth pace is constrained by governance maturity. New products are not launched until the governance to support them is in place. This is a feature, not a bug — the labeler in particular cannot launch responsibly without operational dispute machinery.
# Rubric v0.2 — Revisions following adversarial review

**Date:** 2026-05-09
**Type:** Rubric refinement (Level 3 in `GOVERNANCE.md` terms)
**Affected artifacts:** `RUBRIC.md` (replaced), `GOVERNANCE.md` (small addition)

## What changed

The rubric moved from v0.1 to v0.2. The structural changes are documented in the rubric's own changelog; this entry records the reasoning, the evidence, and the project's response.

Major changes:

- Tier 0 (proposition extraction, attribution, claim typing) was added as a universal pre-layer.
- Tier 1 was made explicitly precision-first.
- "Unsupported claim" was split into "No-support-provided" (Tier 1, descriptive) and "Support-quality-unknown" (Tier 2).
- "Question-dodging" was demoted to Tier 2 with two narrow Tier 1 cases retained ("Explicit refusal," "Yes-or-no non-answer").
- "Gish gallop" was demoted to Tier 2 dynamic pattern with Tier 1 "Claim-burst" added as descriptive precursor.
- Self-contradiction guardrails (modality, scope, attribution, temporal) were promoted from edge-case prose to explicit criteria.
- Three Tier 1 green-flag labels were added (calibrated uncertainty, explicit concession, charitable restatement).
- Three Tier 2 patterns were added (equivocation, missing premise, citation laundering).
- A governance note for the canonical formulation library was added to the strawman section.
- The disputes section was revised to clarify that substantive self-application remains the default, with a pre-submission checklist added as a help layer.

## What evidence prompted the change

An external adversarial review of v0.1 was solicited and received. The review identified specific concerns about the v0.1 rubric:

1. Several Tier 1 categories were vulnerable to false positives because they lacked a stable proposition-extraction substrate. Sarcasm, quotation, hypotheticals, and reported speech could trigger labels intended for endorsed assertions.

2. The v0.1 policy of "the engine errs toward flagging when in doubt" for Tier 1 unsupported-claim labels was argued to be backwards. False positives in publicly-visible labels damage credibility disproportionately to the cost of missed cases.

3. The "Unsupported claim" category combined two distinct things: claims with literally no support, and claims whose support was unclear. The reviewer argued for splitting these so that the descriptive case could be a clean Tier 1 label and the harder case could be a Tier 2 pattern.

4. "Question-dodging" and "Gish gallop" were argued to be too semantics-heavy and too dependent on conversational dynamics for Tier 1. The reviewer proposed demoting them to Tier 2 with narrow Tier 1 cases retained.

5. The v0.1 rubric was argued to be one-sided in its incentive structure: it labeled what went wrong but did not label what went right, leaving no positive incentive gradient for users.

6. Several real and structurally-detectable patterns were missing: equivocation, missing premise, citation laundering.

7. The reviewer argued that the disputes section's commitment to applying the rubric to disputes themselves was a "powder keg" and proposed defaulting to procedural responses, with logical analysis of disputes only available as an opt-in.

The review also raised a concern about the strawman pattern's reliance on a "canonical formulation library" of defensible position statements. The reviewer noted this library would itself be a site of bias risk but did not propose specific governance for it.

## What evaluation was done

Each of the reviewer's substantive recommendations was evaluated against the project's principles documented in `MISSION.md`. The criterion was: does this change make the rubric more aligned with the principles, or less?

For most recommendations, the answer was clearly "more aligned":

- Tier 0 is a structural improvement that reduces false positives without changing what the rubric tries to do.
- Precision-first for Tier 1 follows directly from the principle that false positives are worse than false negatives for credibility.
- Splitting categories where they conflate distinct things produces cleaner, more defensible labels.
- The green-flag labels are structural and symmetric (detection depends only on explicit markers), so they don't introduce new bias risk.
- The new Tier 2 patterns are real, structural, and were just gaps in v0.1.

For one recommendation, the answer was "less aligned":

The reviewer's suggestion to soften the disputes section — defaulting to procedural responses rather than substantive engagement — would have weakened the project's self-application commitment. The neutrality commitment in `MISSION.md` specifies that the engine applies symmetrically across viewpoints; the contestability commitment specifies that analytical claims are inspectable and disputable. Together these imply that disputes about the rubric must themselves be subject to the rubric. A dispute system that exempts disputes from the rubric's own analysis quietly carves out a domain where the project's commitments do not apply.

The reviewer's underlying concern — that substantive engagement with disputes will feel adversarial in practice — is real and valid. But the appropriate mitigation is presentation, not principle. The v0.2 dispute section retains substantive self-application as the default while adding a pre-submission checklist that helps users formulate effective disputes before submitting. The checklist is positioned as help, not as a gate.

For the canonical formulation library concern, the reviewer correctly identified the bias risk but did not propose specific governance. The v0.2 rubric adds an explicit governance note: the library is treated as a rubric-level artifact governed under the same Level 4 amendment procedures as the rubric itself, including cross-faction validation. This treatment was added not because of the reviewer's specific recommendation but because the principle was implicit in the reviewer's concern and the project's own commitments.

## What was projected

The projected impact of v0.2 is:

- Reduced false-positive rate on Tier 1 labels, especially for self-contradiction (due to attribution guardrails) and the unsupported-claim category (due to splitting and the load-bearing requirement).
- Better calibration: more cases will surface as Tier 2 patterns or uncertainty acknowledgments rather than as Tier 1 definitive labels.
- More balanced incentive structure: green flags give users something to optimize toward, not just fallacies to avoid.
- Greater coverage of common structural patterns through the new Tier 2 additions.
- The canonical formulation library, when it exists, will be governed at the rubric level rather than as an engine internal — reducing the risk that bias is introduced through curation choices that are not visible to reviewers.

The disputes section is projected to remain a source of friction with users whose disputes contain detectable patterns. This is accepted; the alternative (procedural deflection) is judged worse for the project's credibility over time.

## What the actual impact has been

To be filled in over time as the engine is implemented and the rubric is exercised against real content. The first concrete data point will come from Stage 1 (Steelman Core) implementation: each Tier 1 detector should achieve high precision on the evaluation datasets, and the symmetric application checks across the political spectrum should pass.

This entry will be updated as evidence accumulates.

## Notes on process

This is the first substantive validation log entry. The fact that v0.1 changed in response to external review is itself the project's first demonstration of the contestability commitment. The review was not solicited from a politically diverse panel; it came from a single source (an LLM-based critique tool). The next round of rubric review should be more deliberately diverse — at minimum, a mix of human reviewers with different ideological starting points.

A subsequent entry should record the results of that broader review and any revisions it prompts.
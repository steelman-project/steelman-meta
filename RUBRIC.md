# The Steelman Rubric

> **Status:** Draft v0.1. This is a starter rubric — deliberately small, with categories chosen for tractability and structural neutrality. It will grow through the amendment procedure, not through ad-hoc additions.

## What this document is

The rubric is the engine's constitution. It defines what the engine analyzes, how it makes calls, where it refuses to operate, and how confident it is in different categories. Every component of the ecosystem applies this rubric faithfully. Every output the engine produces can be traced back to specific rubric clauses.

The rubric is open source under CC BY-SA 4.0. It is a living document, but it is not edited casually. Changes go through the procedure described in `GOVERNANCE.md`.

## Principles governing the rubric

**Structural over substantive.** The rubric prefers categories that can be evaluated by examining the structure of an argument without needing to know what's true about the world. "This argument contains a contradiction with itself" is structural. "This argument is wrong about climate science" is substantive. The starter rubric is almost entirely structural; substantive categories require much more elaborate machinery and are deferred.

**Symmetric across viewpoints.** Every category in the rubric must apply equally to arguments from any political, ideological, or cultural position. If a category can be applied to one side's arguments but not the other's because of how the criterion is defined, the criterion is wrong. This is checked by adversarial review: for each category, can examples be constructed where the category applies to arguments from across the political spectrum, with similar frequency for similar offenses?

**Confidence-graded.** Categories are graded for how confidently the engine can apply them. High-confidence categories are applied definitively. Lower-confidence categories are surfaced as patterns the user can evaluate, with explicit acknowledgment of uncertainty. The engine does not apply categories outside its confidence range.

**Refusable.** The rubric explicitly names cases the engine should not analyze. These refusals are not modesty disclaimers; they are operational rules. The engine that respects its scope is more trustworthy than the engine that overreaches.

**Self-applying.** The rubric applies to disputes about the rubric itself. Criticism of the rubric using fallacious reasoning is recognizable to the engine. Proposed changes are evaluated by the same standards as labels.

## Categories — Tier 1 (high confidence, structural)

These categories can be applied with high confidence because they depend on observable features of the argument itself. The engine produces definitive labels in these categories, with the supporting evidence shown.

### Self-contradiction

**Definition.** An argument contains a self-contradiction when the same speaker, within the same argumentative context, asserts both a proposition and its negation, or asserts propositions that cannot all be true together, without acknowledging or resolving the inconsistency.

**Criterion.** The engine identifies a self-contradiction when (1) two or more propositions are asserted by the same speaker, (2) those propositions cannot all be true under standard logical interpretation, and (3) the speaker does not acknowledge the tension or attempt to reconcile it.

**Examples.**
- A speaker argues both "We must respect the will of voters" and "This referendum result should be ignored" without explaining what distinguishes the cases.
- A speaker claims "Free markets always produce optimal outcomes" and "This industry needs government intervention to function" without addressing the tension.

**Edge cases.**
- Apparent contradictions across different contexts or domains are not contradictions; the engine should look for whether the speaker is making the claims in the same argumentative scope.
- Acknowledged tensions ("I know this seems inconsistent, but here's why...") are not contradictions; the engine respects acknowledgment.
- Evolution of views over time is not contradiction; the engine considers temporal context where available.

**Refusals.**
- The engine does not flag contradictions across different speakers as contradictions. That is disagreement, not inconsistency.
- The engine does not flag contradictions where reconciliation would require resolving a contested empirical question. "Crime is up" vs "Crime is down" is a factual dispute, not a logical contradiction unless the same speaker asserts both.

### Unsupported claim

**Definition.** A factual claim is unsupported when it is asserted as true without accompanying evidence, citation, or reasoning, in a context where evidence would be expected.

**Criterion.** The engine flags a claim as unsupported when (1) the claim is empirical (about how the world is, not about values or preferences), (2) the claim is non-trivial (not common knowledge), (3) no source, evidence, or reasoning chain is provided, and (4) the argumentative context makes evidence reasonable to expect.

**Examples.**
- "Studies show that policy X causes outcome Y" with no study cited.
- "Most people agree that..." with no polling or other support.
- Specific numerical claims without sources.

**Edge cases.**
- Claims that are genuinely common knowledge in the relevant context do not require citation. The engine errs toward flagging when in doubt; users can dispute false flags.
- Casual conversational claims may not warrant evidence-flagging; the engine considers whether the surrounding discourse treats the claim as load-bearing for the argument.

**Refusals.**
- The engine does not assess whether a cited source actually supports the claim. That is fact-checking and is outside scope.
- The engine does not flag value claims (claims about what should be the case) as unsupported by evidence; those require different analysis.

### Question-dodging

**Definition.** A response dodges a question when the question is clearly posed, the responder addresses the question directly enough to demonstrate understanding, but the response substitutes a different topic, claim, or question for the one asked.

**Criterion.** The engine identifies dodging when (1) a question or specific claim is posed in a previous message, (2) the response acknowledges the previous message (by quoting, referencing, or directly replying), and (3) the response's substantive content addresses a different question or claim than the one posed.

**Examples.**
- "Did you make this claim in 2019?" → "What matters is the policy now, which is..."
- "How does your theory account for X?" → "X is just a distraction from the real issue, which is..."

**Edge cases.**
- Refusing to answer with explicit acknowledgment ("I won't answer that question because...") is not dodging. The engine flags pattern of dodging, not pattern of refusal.
- Responses that address the question implicitly while focusing on a different framing may or may not be dodging; the engine surfaces the pattern with lower confidence in these cases.

**Refusals.**
- The engine does not assess whether a response is the *best* answer to a question. It only assesses whether the response addresses the question at all.

### Volume-vs-engagement asymmetry (gish gallop pattern)

**Definition.** A gish gallop pattern occurs when a participant in a discussion makes many distinct claims in rapid succession, such that engaging with each claim would take much longer than making them, and the conversational dynamic discourages the responder from focusing on any single claim.

**Criterion.** The engine identifies a gish gallop pattern when (1) a single message contains multiple distinct factual or argumentative claims (typically 4 or more), (2) the claims are not all in support of a single coherent argument but are independent or weakly connected, (3) responding to each claim adequately would require substantially more effort than making the claim, and (4) the speaker has not focused the discussion on any one claim.

**Examples.**
- A reply that lists 7 alleged problems with the opponent's position, each requiring its own factual investigation.
- A response that pivots through multiple unrelated topics in quick succession.

**Edge cases.**
- Genuine multi-pronged arguments with coherent connections between points are not gish gallops; the engine looks for whether the points are mutually supporting or independent.
- Long substantive responses that develop a single argument with multiple facets are not gish gallops, even if the response is long.

**Refusals.**
- The engine does not flag every multi-point response as a gish gallop. The pattern requires both volume and lack of focus.
- The engine cannot reliably distinguish gish gallops from comprehensive responses without context; this category is borderline Tier 1, and the engine surfaces uncertainty when the call is close.

## Categories — Tier 2 (medium confidence, surface as patterns)

These categories are real and worth surfacing, but the engine cannot apply them with the same confidence as Tier 1. They are presented to users as "this might be X, here's why we think so" rather than as definitive labels.

### Motte-and-bailey (scope shift)

**Definition.** A motte-and-bailey occurs when a speaker advances a strong, controversial claim (the bailey), and when challenged, retreats to a weaker, more defensible claim (the motte), then later advances the strong claim again as if the weaker claim supported it.

**Criterion (pattern).** The engine flags a possible motte-and-bailey when (1) a speaker has advanced two related claims of significantly different strength in the same discussion, (2) the speaker shifted from the stronger to the weaker claim in response to challenge, and (3) the speaker subsequently treats the strong claim as established despite only the weak claim being defended.

**Why Tier 2.** Detecting this pattern reliably requires understanding the relationship between the two claims well enough to know one is stronger than the other, which is closer to substantive analysis than structural analysis.

### Goalpost-shifting

**Definition.** Goalpost-shifting occurs when a speaker, having implicitly or explicitly accepted a standard for what would change their mind, raises that standard or changes the criterion when the standard appears to have been met.

**Criterion (pattern).** The engine flags a possible goalpost-shift when (1) a speaker has stated or implied criteria for what would constitute adequate evidence or argument on a question, (2) those criteria have apparently been met, and (3) the speaker introduces additional criteria that were not previously stated.

**Why Tier 2.** Requires tracking criteria across a conversation and recognizing when they have been met, which is harder than spotting a single-message structural feature.

### Strawmanning

**Definition.** Strawmanning occurs when a speaker characterizes an opposing position in a way that is significantly weaker, more extreme, or otherwise distorted from the version a reasonable proponent would defend.

**Criterion (pattern).** The engine flags a possible strawman when (1) a speaker characterizes an opposing position, and (2) the characterization differs significantly from defensible formulations of that position. The engine surfaces the strongest defensible formulation alongside the speaker's characterization for the user to compare.

**Why Tier 2.** This is partly substantive — the engine needs to know what defensible formulations of positions look like. The engine is more reliable for well-known positions and less reliable for novel or niche claims.

## Categories — Tier 3 (deferred, requires more machinery)

These categories are recognized as important but are not in the v1 rubric. They require capabilities the engine does not yet have or raise concerns about neutrality that have not yet been addressed.

- **False equivalence.** Requires assessing whether two compared things are actually similar in the relevant respects. Substantive.
- **Cherry-picking evidence.** Requires knowing the broader landscape of evidence. Substantive and prone to bias.
- **Loaded language and framing.** Categorizable but politically charged; requires careful work to apply symmetrically.
- **Bad-faith concession demands.** Recognizable but requires understanding intent.
- **Sea-lioning.** Requires assessing tone and intent across multiple messages.

These will be added to the rubric over time, with adversarial review for each, and only when the engine can apply them with reliability comparable to Tier 1 or 2 categories.

## What the engine does not analyze

These are operational refusals. The engine does not produce output in these areas, regardless of user request.

**Truth of contested empirical claims.** The engine does not say whether the claim "policy X reduced outcome Y" is true. It says whether the claim is supported by cited evidence in the post being analyzed.

**Verdict on debates.** The engine does not declare which side of a contested debate is correct. It surfaces the strongest formulations on each side, the evidence cited for each, and the points of dispute.

**Single-score judgments of people.** The engine does not produce composite scores ranking individuals on argumentative quality. It analyzes specific arguments and posts.

**Content involving minors.** The engine does not analyze posts authored by or substantially about identifiable minors, even if the posts are public.

**Content involving private individuals.** The engine does not analyze posts about identifiable private individuals (people who are not public figures and have not voluntarily entered public discourse on the topic) beyond what those individuals have themselves made public.

**Mental state attribution.** The engine does not assess whether someone is "being honest" or "arguing in good faith" in some intent-based sense. It assesses observable patterns. A user who has deployed gish gallops repeatedly is described as having a pattern of deploying gish gallops, not as a "bad-faith arguer."

**Aesthetic, stylistic, or rhetorical quality not bearing on logical structure.** The engine does not evaluate whether prose is well-written, whether tone is appropriate, or whether rhetoric is elegant. These are outside scope.

## Confidence and uncertainty

The engine produces outputs with explicit confidence markers:

- **Definitive labels.** Used for Tier 1 categories where the structural criteria are clearly met. Example: "This message contains a self-contradiction between the claim X and the claim Y."

- **Pattern surfacings.** Used for Tier 2 categories and for Tier 1 categories where the criteria are partially but not fully met. Example: "This may be a gish gallop pattern. The message contains 6 distinct claims with weak connections between them. You can review the analysis here."

- **Uncertainty acknowledgments.** Used when the engine cannot make a confident call. Example: "This message is borderline for the dodging criterion. The response references the question but addresses a related but distinct topic. You may want to evaluate this manually."

- **Refusals.** Used when the engine determines the case is outside its scope. Example: "I cannot evaluate whether this empirical claim is true; that is outside the engine's scope. I can note that no source is cited."

The engine prefers acknowledging uncertainty to producing confident wrong calls. False positives in fallacy detection are particularly costly because they damage the engine's credibility and can be used to dismiss legitimate arguments.

## Symmetry and self-application

For every label the engine applies to a thread or message, the same engine should apply the same label to equivalent moves in any other thread or message, regardless of the political position of the speaker. This symmetry is checked through evaluation datasets that include matched examples across the political spectrum.

The engine also applies to itself. Disputes about labels are evaluated using the rubric. Criticism of the rubric using fallacious reasoning is recognizable. The engine's own output, including this document, can be analyzed by the engine and found wanting.

## Versioning

The rubric is versioned. The current version applies to all new analyses. Previous versions remain accessible so that historical analyses can be understood in their original context. Analyses are tagged with the rubric version that produced them.

When the rubric changes, the validation log records what changed and why. Old analyses are not retroactively re-labeled; the original labels stand with the version that produced them, and disputes that prompted the change are linked.

## Disputes about rubric application

A user who believes a label was misapplied can dispute it through the procedure described in `GOVERNANCE.md`. Disputes that demonstrate the criterion was not actually met result in the label being marked as disputed (not removed). Disputes that demonstrate a pattern of similar misapplications can prompt rubric refinement.

Disputes are evaluated using the rubric. A dispute that consists of a fallacy ("this label is wrong because the engine is biased") is treated by the engine as a dispute that contains a fallacy. A dispute that points to specific structural features the criterion missed is treated as substantive feedback.

This recursive structure is intentional. A rubric that cannot survive its own application is not a rubric.

# The Steelman Rubric

<!-- RUBRIC_VERSION: 0.2 -->

> **Status:** Draft v0.2. A starter rubric — deliberately small, with categories chosen for tractability and structural neutrality. Grows through the amendment procedure described in `GOVERNANCE.md`, not through ad-hoc additions.

## Changelog

### v0.2 (this version)

Revisions following external adversarial review of v0.1. See `validation-log/` for the review and the project's response.

- Added **Tier 0** (proposition extraction, attribution, claim typing) as a universal pre-layer that all higher tiers depend on.
- Made Tier 1 explicitly **precision-first**: definitive labels fire only when criteria are clearly met; otherwise the engine produces a Tier 2 pattern surfacing or an uncertainty acknowledgment.
- Replaced **Unsupported claim** with **No-support-provided** (Tier 1, descriptive, load-bearing requirement) and added **Support-quality-unknown** (Tier 2).
- Demoted **Question-dodging** (now Tier 2 pattern) and added narrow Tier 1 cases: **Explicit refusal to answer** and the specific yes/no non-answer pattern.
- Demoted **Gish gallop** (now Tier 2 dynamic pattern) and added **Claim-burst** (Tier 1, descriptive count).
- Added explicit guardrails to **Self-contradiction** (modality, scope, attribution, temporal) as part of the criterion rather than as edge-case prose.
- Added **Tier 1 green flags** (calibrated uncertainty, explicit concession/update, charitable restatement) — applied only when explicit markers are present.
- Added Tier 2 patterns: **Equivocation/term shift**, **Missing premise/non sequitur**, **Citation laundering / unclear support mapping**.
- Added explicit governance note for the **canonical formulation library** referenced by the strawman pattern.
- Revised **Disputes** section: substantive self-application remains the default; pre-submission guidance is added as a help layer, not a deflection layer.

## What this document is

The rubric is the engine's constitution. It defines what the engine analyzes, how it makes calls, where it refuses to operate, and how confident it is in different categories. Every component of the ecosystem applies this rubric faithfully. Every output the engine produces can be traced back to specific rubric clauses.

The rubric is open source under CC BY-SA 4.0. It is a living document, but it is not edited casually. Changes go through the procedure described in `GOVERNANCE.md`.

## Principles governing the rubric

**Structural over substantive.** The rubric prefers categories that can be evaluated by examining the structure of an argument without needing to know what's true about the world. "This argument contains a contradiction with itself" is structural. "This argument is wrong about climate science" is substantive. The starter rubric is almost entirely structural; substantive categories require much more elaborate machinery and are deferred.

**Symmetric across viewpoints.** Every category in the rubric must apply equally to arguments from any political, ideological, or cultural position. If a category can be applied to one side's arguments but not the other's because of how the criterion is defined, the criterion is wrong. This is checked by adversarial review: for each category, can examples be constructed where the category applies to arguments from across the political spectrum, with similar frequency for similar offenses?

**Precision-first for definitive labels.** Tier 1 labels are designed to be high precision (rarely wrong when they fire), even at the cost of missing some cases. When in doubt, the engine prefers a lower-confidence pattern surfacing or an uncertainty acknowledgment over a confident wrong call. False positives in fallacy detection are particularly costly because they damage credibility and can be used to dismiss legitimate arguments.

**Confidence-graded.** Categories are graded for how confidently the engine can apply them. High-confidence categories are applied definitively. Lower-confidence categories are surfaced as patterns the user can evaluate, with explicit acknowledgment of uncertainty. The engine does not apply categories outside its confidence range.

**Receipts-first.** Every label includes the extracted proposition(s) it applied to, the minimum quotes or snippets needed to verify the call, and the specific rubric clause(s) used. The user can inspect the basis of any analytical claim.

**Refusable.** The rubric explicitly names cases the engine should not analyze. These refusals are not modesty disclaimers; they are operational rules. The engine that respects its scope is more trustworthy than the engine that overreaches.

**Self-applying.** The rubric applies to disputes about the rubric itself. Criticism of the rubric using fallacious reasoning is recognizable to the engine. Proposed changes are evaluated by the same standards as labels. The dispute UX is designed to make this engagement constructive rather than combative, but the principle is preserved.

## Tier 0 — Preconditions (extraction, attribution, claim typing)

Tier 0 is a universal pre-layer. No Tier 1 or Tier 2 label may be applied unless Tier 0 has produced a stable set of propositions and attributed them correctly. Tier 0 itself is not a category that produces user-facing labels; it is the substrate that makes the other tiers reliable.

### 0.1 Proposition extraction

The engine extracts a list of propositions from each message, broken into minimal declarative units. Each proposition is identifiable by an index within the source text and traceable to a specific span.

### 0.2 Attribution and speech-act classification

Each extracted proposition is classified as one of:

- **Assertion (endorsed):** the speaker is presenting the proposition as their own view.
- **Question:** the speaker is asking, not asserting.
- **Hypothetical or conditional:** "If X, then Y..." — used in argument but not endorsed as fact.
- **Quotation or paraphrase:** the speaker is restating what someone else said.
- **Reported speech:** "They claim that..." — attributing a position to others.
- **Sarcasm or irony marker present:** the engine reduces confidence in endorsement.

**Rule.** Tier 1 definitive labels may only be applied to propositions classified as **Assertion (endorsed)**. Quoted, hypothetical, sarcastic, or reported propositions are out of scope for definitive labeling.

### 0.3 Claim typing

Each proposition is typed as:

- **Empirical:** claims about how the world is, including numeric and statistical claims.
- **Normative:** "should," "ought," value judgments, preferences.
- **Definitional:** claims about meaning ("X means...").
- **Meta-discourse:** claims about the conversation itself ("you're dodging," "you changed the topic").

Different categories of analysis apply to different claim types. The "no-support-provided" label, for example, applies only to empirical claims.

### 0.4 Context windowing

For conversation-dependent labels (contradiction, dodging, gish gallop, motte-and-bailey, goalpost shifting), the engine defines the **argumentative context** as: same thread or explicitly linked thread, same topic cluster (engine-defined with confidence markers), within a bounded window of time and message distance.

**Rule.** The engine does not claim cross-context inconsistency without strong scope match. Apparent contradictions across very different topics, very different time periods, or different conversational contexts are not labeled as contradictions without explicit user expansion of scope.

## Categories — Tier 1 (high precision, definitive when criteria are clearly met)

### Self-contradiction

**Definition.** A self-contradiction occurs when the same speaker, within the same argumentative context, asserts both a proposition and its negation, or asserts propositions that cannot all be true together, without acknowledging or resolving the inconsistency.

**Criterion.** The engine identifies a self-contradiction when all of the following are true:

1. Two or more endorsed assertions (per Tier 0.2) are made by the same speaker.
2. The propositions cannot all be true under standard logical interpretation.
3. The propositions share the same argumentative scope (per Tier 0.4).
4. The speaker does not acknowledge the tension or attempt reconciliation.

**Required guardrails.** Before applying this label, the engine checks:

- **Modality shift:** "always" vs "often," "must" vs "should," confidence-level changes are not contradictions.
- **Scope or quantifier:** "in general" vs "in this case," "some" vs "all," general statements vs particular cases.
- **Attribution:** quoted, paraphrased, hypothetical, or reported propositions cannot create contradictions per Tier 0.2.
- **Temporal:** evolution over time is not contradiction if the speaker signals the change ("I used to think..., now...").

**Examples.**
- "We must respect the will of voters" + "This referendum result should be ignored" without an explained distinction between the cases.
- "Free markets always produce optimal outcomes" + "This industry needs government intervention to function" without reconciliation.

**Refusals.**
- Disagreements between different speakers are not self-contradictions; they are disagreements.
- Apparent contradictions that hinge on resolving contested empirical facts are not labeled as logical contradictions unless the same speaker asserts both sides in the same context.

### No-support-provided (empirical, load-bearing)

**Definition.** An empirical claim has no support provided when it is used as a load-bearing premise in an argument but is presented without any citation, evidence, or reasoning chain.

**Criterion.** The engine labels **No-support-provided** when all of the following are true:

1. The proposition is empirical (per Tier 0.3).
2. The proposition is non-trivial in context (not common knowledge or obvious definitional ground).
3. The proposition is load-bearing — the argument depends on it, not merely casual color or rhetorical flourish.
4. The message provides no citation or link to a source, no concrete evidence, and no explicit reasoning chain connecting the claim to other premises.

**Notes.**

- This label is descriptive, not accusatory. The user-facing phrasing is "no support provided," not "unsupported." The distinction matters.
- "Common knowledge" is context-dependent. The engine errs toward uncertainty when the line is unclear, preferring not to fire rather than firing on a borderline case.

**Examples.**
- "Studies show policy X causes outcome Y" with no study, dataset, or reasoning cited.
- "Most people agree that..." with no poll, survey, or sourcing.
- Specific numerical claims presented without any source.

**Refusals.**
- The engine does not assess whether a cited source actually supports the claim. That is fact-checking, which is out of scope.
- The engine does not apply this label to normative ("should," "ought") claims, which require different analysis.
- The engine does not flag casual rhetorical claims that are not load-bearing for the argument.

### Explicit refusal to answer

**Definition.** A responder explicitly states they will not answer a question or provide requested information.

**Criterion.** The engine labels **Explicit refusal** when:

1. A clear question or specific request is present in the prior context.
2. The responder explicitly indicates refusal — phrases like "I won't answer that," "I'm not going to discuss that," "I refuse to engage with that."

**Notes.**

- Refusal is not automatically a negative move. Some questions are inappropriate; some refusals are principled.
- This label exists primarily to prevent mislabeling of explicit refusals as "dodging." Refusing openly is structurally different from dodging.

### Yes-or-no non-answer

**Definition.** A response answers a yes/no question without containing yes, no, or an explicit refusal, and substantively pivots to a different topic.

**Criterion.** The engine labels **Yes-or-no non-answer** when:

1. The question can be classified (via Tier 0) as a yes/no question.
2. The response neither contains a clear yes/no answer nor an explicit refusal (per the Explicit refusal label).
3. The response's extracted propositions address materially different content than the question's extracted ask.

**Notes.**

- This is a narrow Tier 1 case. Broader dodging patterns are handled in Tier 2.
- The engine produces side-by-side: the question's extracted ask, the response's extracted answer content, and the gap between them.

### Claim-burst (descriptive volume signal)

**Definition.** A single message contains many distinct endorsed propositions.

**Criterion.** The engine labels **Claim-burst** when:

1. A message contains at least N distinct endorsed propositions per Tier 0 (default N = 6; configurable).
2. The engine can produce the extracted proposition list.

**Notes.**

- Claim-burst is a descriptive signal, not a fallacy label. It is not pejorative.
- It is often a precursor signal for the Tier 2 gish-gallop pattern but does not imply that pattern by itself.
- The label exists to make volume visible without making accusations the engine cannot support from a single message.

### Green flags (Tier 1, explicit markers only)

These labels are applied only when the marker is explicit and attributable. They exist to create an incentive gradient toward better discourse without requiring substantive truth judgments. Each is structural and symmetric: detection depends on observable language, not inferred quality.

#### Calibrated uncertainty

**Definition.** The speaker explicitly communicates uncertainty or confidence level about a claim.

**Criterion.** Applies when the speaker uses clear calibration markers attached to a proposition: "I'm not sure," "my confidence is 60%," "I could be wrong about this," "as far as I know."

#### Explicit concession or update

**Definition.** The speaker explicitly concedes a point, updates their stated belief, or retracts a prior claim.

**Criterion.** Applies when the speaker uses explicit update markers: "you're right about X," "I retract Y," "I changed my mind because...," "good point, I hadn't considered that."

#### Charitable restatement

**Definition.** The speaker explicitly attempts to restate the other side's position fairly before responding.

**Criterion.** Applies when the speaker uses explicit restatement markers — "if I understand you correctly...," "your view is...," "let me restate your position..." — and the restated proposition can be compared to the opponent's prior statements in scope.

## Categories — Tier 2 (medium confidence, surfaced as patterns)

Tier 2 categories are real and worth surfacing, but the engine does not produce definitive labels for them. They are presented to users as "this may be X, here's why we think so, and here are the alternative interpretations."

### Possible question pivot or dodging (pattern)

**Definition.** A response may be dodging when it acknowledges a question but substantively answers a different question or shifts framing to avoid the requested content.

**Pattern criteria.**

1. A question or specific request is present in prior context.
2. The response references the prior message (by reply, quote, or direct address).
3. The response's extracted propositions do not address the question's extracted ask, or address a materially different ask.

**Required output.** The question's extracted ask, the response's extracted answer propositions, a short explanation of the mismatch, and explicit acknowledgment that "different framing" and "dodge" can be hard to distinguish.

**Why Tier 2.** Determining whether a response addresses the same question or a substantively different one is semantics-heavy and context-dependent. The Tier 1 yes-or-no non-answer is the narrow definitive case; broader patterns live here.

### Gish gallop pattern (dynamic)

**Definition.** A gish gallop pattern may be present when a participant repeatedly introduces many distinct claims such that engagement cost is asymmetrically high, and the speaker resists narrowing the discussion.

**Pattern criteria.**

1. A sequence of claim-bursts (per Tier 1) across multiple messages.
2. Weak coherence across the introduced claims — they are independent or weakly connected, not all supporting one coherent argument.
3. The speaker does not narrow the focus when prompted to do so.

**Required output.** Per-message claim lists, a timeline of when claims were introduced, and an indication of whether narrowing was prompted and how the speaker responded.

**Why Tier 2.** The pattern requires conversation dynamics across multiple turns, not a single message. A single message with many points could be a genuinely multi-faceted argument; only the conversational dynamic distinguishes a gish gallop.

### Support-quality-unknown

**Definition.** A claim has support-quality-unknown when citations or links are present but the engine cannot determine relevance or claim-to-source mapping.

**Pattern criteria.**

1. One or more links or citations are provided in the message, and one or more of:
   - No explicit mapping of which citation supports which claim.
   - Citations are inaccessible, broken, or paywalled.
   - Citations are too generic to evaluate in context (e.g., a link to a publication's homepage rather than a specific article).

**Notes.**

- This is not "debunking." It is a structural support-mapping signal.
- The label exists to prevent gaming where any link counts as "support" regardless of whether it actually relates to the claim.

### Citation laundering (unclear support mapping pattern)

**Definition.** A pattern where citations are used as rhetorical cover without clear claim-to-source linkage, creating the appearance of support without the substance.

**Pattern signals.**

- "Studies show..." followed by a list of links with no mapping of which study supports which claim.
- Citations to secondary commentary when primary evidence is implied.
- High citation volume combined with low explicit claim-to-source mapping.

**Required output.** The exact claims that appear to be supported, the list of citations provided, and the missing mapping highlighted.

### Motte-and-bailey (scope shift)

**Definition.** A motte-and-bailey occurs when a speaker advances a strong, controversial claim (the bailey), and when challenged, retreats to a weaker, more defensible claim (the motte), then later treats the strong claim as established despite only the weak claim being defended.

**Pattern criteria.**

1. A speaker has advanced two related claims of significantly different strength in the same discussion.
2. The speaker shifted from the stronger to the weaker claim in response to challenge.
3. The speaker subsequently treats the strong claim as established despite only the weak claim being defended.

**Why Tier 2.** Detecting this pattern reliably requires understanding the relationship between two claims well enough to know one is stronger than the other, which is closer to substantive analysis than pure structural analysis.

### Goalpost shifting (criteria drift)

**Definition.** A speaker, having implicitly or explicitly accepted a standard for what would change their mind, raises the standard or changes the criterion when the standard appears to have been met.

**Pattern criteria.**

1. The speaker stated or implied criteria for what would constitute adequate evidence or argument.
2. Those criteria appear to have been met (structurally — without requiring the engine to adjudicate the substantive merit).
3. The speaker introduces additional criteria that were not previously stated.

**Why Tier 2.** Requires tracking criteria across a conversation and recognizing when they have been met, which is harder than spotting a single-message structural feature.

### Strawmanning (pattern, receipts required)

**Definition.** A strawman may be present when a speaker characterizes an opposing position in a way that is significantly weaker, more extreme, or otherwise distorted from the version a reasonable proponent would defend.

**Pattern criteria.**

1. A characterization of an opposing position is offered.
2. The characterization materially diverges from one of:
   - The opponent's own prior statements in-thread (when available).
   - The canonical formulation library (when applicable — see governance note below).
   - Multiple candidate defensible formulations, presented to the user with confidence labels.

**Required output.** Side-by-side comparison: the characterization, the opponent's closest prior statements (if available), and the canonical formulation (if applicable). Confidence markers and alternative interpretations are included.

**Why Tier 2.** This is partly substantive — the engine needs to know what defensible formulations of positions look like. The engine is more reliable for well-known positions and less reliable for novel or niche claims.

**Governance note: the canonical formulation library.** The strawman pattern can refer to a "canonical formulation library" — a maintained set of defensible formulations of common positions on contested topics, used as a reference for what counts as a strawman. This library has substantial influence over what the engine considers a strawman, and it is therefore governed under the same procedures as the rubric itself: changes go through the cross-faction validation procedure described in `GOVERNANCE.md`. The library is treated as a rubric-level artifact, not a routine engine internal. It is open source under CC BY-SA 4.0 like the rubric, and additions or modifications follow the Level 4 amendment process.

Until the canonical formulation library exists in mature form, the strawman pattern relies primarily on the opponent's own prior statements in-thread. The library is a v2+ artifact, not a v0.2 deliverable.

### Equivocation or term shift (pattern)

**Definition.** A key term may be shifting in meaning across an argument, enabling a misleading inference. The shift is unacknowledged.

**Pattern signals.**

- The same term repeats across turns with different inferred definitions or qualifiers nearby.
- The argument's inference depends on treating the different uses as the same meaning.

**Required output.** The term, two inferred meanings (or uses) with evidence snippets, and the location where the inference bridges them.

### Missing premise or non sequitur (pattern)

**Definition.** A conclusion is asserted from premises without an explicit connecting step, leaving a logical gap.

**Pattern signals.**

- Premise propositions extracted from the argument.
- Conclusion proposition extracted.
- A connecting proposition that would bridge them is absent and must be supplied as a hypothesis.

**Note.** The engine labels any proposed missing premise as hypothetical and invites user review. The engine should not assert that the user "actually meant" a specific connecting premise; it should surface the gap and a possible bridge.

## Categories — Tier 3 (deferred)

These categories are recognized as important but are not in the v1 rubric. They require capabilities the engine does not yet have or raise neutrality concerns that have not yet been addressed.

- **Truth of contested empirical claims.** Fact-checking. Substantive and resource-intensive.
- **Cherry-picking evidence.** Requires knowing the broader landscape of evidence on a topic.
- **False equivalence.** Requires assessing whether two compared things are actually similar in the relevant respects.
- **Loaded language and framing.** Recognizable but politically charged; requires careful work to apply symmetrically.
- **Sea-lioning and bad-faith questioning.** Requires intent inference.
- **Mind-reading and intent attribution** beyond observable patterns.

These will be added to the rubric over time, with adversarial review for each, and only when the engine can apply them with reliability comparable to Tier 1 or 2 categories.

## What the engine does not analyze (operational refusals)

These are operational refusals. The engine does not produce output in these areas, regardless of user request.

**Truth adjudication of contested empirical claims.** The engine does not say whether the claim "policy X reduced outcome Y" is true. It may say whether support is provided or whether claim-to-source mapping is structurally clear.

**Verdict on debates.** The engine does not declare which side of a contested debate is correct. It surfaces the strongest formulations on each side, the evidence cited for each, and the points of dispute.

**Single-score judgments of people.** The engine does not produce composite scores ranking individuals on argumentative quality. It analyzes specific arguments and posts.

**Content involving minors.** The engine does not analyze posts authored by or substantially about identifiable minors, even if the posts are public.

**Content involving private individuals.** The engine does not analyze posts about identifiable private individuals (people who are not public figures and have not voluntarily entered public discourse on the topic) beyond what those individuals have themselves made public, and applies extra caution even then.

**Mental state attribution.** The engine does not assess whether someone is "being honest" or "arguing in good faith" in some intent-based sense. It assesses observable patterns. A user who has deployed gish gallops repeatedly is described as having a pattern of deploying gish gallops, not as a "bad-faith arguer."

**Aesthetic or stylistic evaluation.** The engine does not evaluate whether prose is well-written, whether tone is appropriate, or whether rhetoric is elegant unless directly relevant to structural clarity (e.g., definitional ambiguity surfaced as such).

## Confidence and uncertainty

The engine produces outputs with explicit confidence markers:

- **Definitive labels.** Used for Tier 1 categories where structural criteria are clearly met. Example: "This message contains a self-contradiction between the claim X and the claim Y."

- **Pattern surfacings.** Used for Tier 2 categories and for Tier 1 categories where criteria are partially but not fully met. Example: "This may be a gish gallop pattern. The conversation contains a sequence of claim-bursts; coherence across claims appears weak; the speaker did not narrow when prompted."

- **Uncertainty acknowledgments.** Used when the engine cannot make a confident call. Example: "This message is borderline for the dodging criterion. The response references the question but addresses a related but distinct topic. You may want to evaluate this manually."

- **Refusals.** Used when the engine determines the case is outside its scope. Example: "I cannot evaluate whether this empirical claim is true; that is outside the engine's scope. I can note that no source is cited."

The engine prefers acknowledging uncertainty to producing confident wrong calls.

## Symmetry and self-application

For every label the engine applies in one case, it should apply the same label to equivalent moves in any other case, regardless of the political position of the speaker. This symmetry is checked through evaluation datasets that include matched examples across the political spectrum and across rhetorical styles.

The engine also applies to itself. Disputes about labels are evaluated using the rubric. Criticism of the rubric using fallacious reasoning is recognizable. The engine's own output, including this document, can be analyzed by the engine and found wanting. The dispute UX (described below) is designed to make this self-application constructive rather than combative, but the principle is preserved.

## Versioning

The rubric is versioned. The current version applies to all new analyses. Previous versions remain accessible so historical analyses can be understood in their original context. Analyses are tagged with the rubric version that produced them.

When the rubric changes, the validation log records what changed and why. Old analyses are not retroactively re-labeled; the original labels stand with the version that produced them, and disputes that prompted the change are linked.

## Disputes about rubric application

A user who believes a label was misapplied can dispute it through the procedure described in `GOVERNANCE.md`.

### Pre-submission guidance (a help layer, not a gate)

Before a dispute is submitted, the system offers a checklist to help users formulate effective disputes:

- Does your dispute reference a specific criterion clause from the rubric?
- Does your dispute address the extracted proposition(s) and their attribution?
- Does your dispute contest the scope or context windowing the engine used?
- Does your dispute provide counter-snippets that change how the criterion applies?

This is guidance, not a gate. Users may submit disputes that don't satisfy the checklist; the checklist exists because clear disputes are more likely to succeed and less likely to be misunderstood. The checklist is shown before submission as a help, not after submission as a rejection reason.

### Default dispute handling: substantive engagement

Once submitted, disputes receive substantive engagement. The engine applies the rubric to the dispute's reasoning, surfacing structural concerns where they exist. This is the project's commitment to self-application: the rubric must operate on disputes about the rubric itself, including disputes that contain the patterns the rubric is designed to detect.

The presentation of substantive analysis matters. The engine's response to a dispute is not adversarial labeling. It is a structured analysis that shows:

- Which criterion clauses the dispute cited (or did not cite).
- The extracted propositions in the dispute and their attribution per Tier 0.
- Any structural concerns the engine identified, with the supporting clauses.
- An invitation to revise the dispute or proceed to human review.

A dispute that contains a structural concern is not "rejected." The user is shown the analysis and given the option to revise. If the user proceeds despite the analysis, the dispute moves forward to human review with the engine's analysis attached.

### Resolution outcomes

Disputes that demonstrate the criterion was not met result in the label being marked as **disputed** (not silently removed). The original analysis remains accessible, with the dispute and resolution linked. Disputes that demonstrate a pattern of misapplication can prompt rubric refinement through the procedure in `GOVERNANCE.md`.

Disputes do not retroactively change historical labels. The original label stands with the dispute attached; new labels apply the refined criterion. This prevents gaming through dispute volume.

### Why substantive engagement is the default

The project's contestability commitment depends on the rubric applying to itself. A dispute system that defaults to procedural deflection — "your dispute doesn't reference the right clause, please try again" — quietly carves out a domain where the rubric does not operate. That is the kind of inconsistency the neutrality commitment is designed to prevent.

The cost of substantive engagement is real: it can feel uncomfortable to users whose disputes contain patterns the rubric detects. The project accepts this cost because the alternative — letting the rubric operate everywhere except on its own contestation — is a credibility problem that compounds over time.

The mitigation is presentation, not principle. The system shows the analysis with the supporting clauses, frames it as structured feedback rather than judgment, and gives the user the option to revise. The pre-submission checklist exists to reduce the frequency of disputes that invite uncomfortable analysis in the first place.

This recursive structure is intentional. A rubric that cannot survive its own application is not a rubric.
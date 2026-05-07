# Steelman — Mission and Principles

> **Status:** Draft v0.1. This document is foundational and changes only through deliberate review, not incidental edits. Proposed changes go through the amendment procedure described in `GOVERNANCE.md`.

## What this project is

**Steelman** builds an ecosystem of tools for analyzing, navigating, and contributing to public discourse — particularly online argumentation. The shared goal across all components is to make online discourse healthier by making the structure of arguments more legible, by making manipulative rhetorical moves visible to bystanders, and by giving individuals better tools to think, write, and read.

The project takes its name from the practice of *steelmanning*: restating an opposing argument in its strongest, most defensible form before engaging with it. The name commits the project to a specific stance — that good discourse requires meeting opposing positions at their strongest, not their weakest, and that any tool meant to improve discourse must apply the same standard to itself.

The project is composed of two cooperating subsystems:

The **Argument Facilitator** operates at individual scale. It helps a single user understand a thread, draft a reply, or recognize a fallacy. The unit of analysis is one post, thread, or draft. The user is the customer.

The **Topic Aggregator** operates at collective scale. It maps the landscape of arguments on contested topics, weighs evidence, surfaces the strongest formulations on each side, and tracks how debates evolve. The unit of analysis is a topic, claim, or argument across many sources.

Both subsystems are built on a shared analytical engine and a shared rubric. The engine reads posts and produces structured analysis: argument cards, evidence objects, fallacy detections, claim graphs. The rubric defines what the engine is trying to do and how it makes calls. Every product in the ecosystem is, at its core, a different way of exposing the engine to different users for different purposes.

## What this project is not

It is not a truth oracle. It does not adjudicate contested empirical claims. It does not score people. It does not declare winners of debates. It does not advocate for political positions. It does not censor or suppress content. It does not replace human judgment.

These are explicit limits, not modesty disclaimers. The project's analytical capabilities will be deliberately scoped to what can be done reliably and fairly, and the project will refuse to operate outside that scope even when users request it.

## The priority order

When the project's goals come into tension — and they will — they are prioritized in this order:

**Impact first.** The project exists to improve discourse. Decisions that increase real impact on discourse quality take priority over decisions that maximize adoption or further the project's other goals.

**Adoption second.** A tool that no one uses cannot have impact. Adoption matters, and the project will pursue growth and reach where doing so is consistent with the impact goal. But adoption is instrumental, not terminal. Features that grow usage at the cost of the impact goal will not be built.

**Decentralization third.** Where possible, the project favors open infrastructure, pluralistic governance, and decentralized deployment. Decentralization makes the project more resilient and harder to capture. But it is the lowest-priority of the three, and centralization will be accepted where it serves impact better than the alternative.

This ordering is not negotiable on any individual decision. It is the standard against which decisions are checked.

## Core commitments

### Neutrality

The project does its best to find correct answers and apply consistent standards regardless of which political, ideological, or cultural position those standards favor in any given case. The engine will flag fallacies and weak arguments wherever they appear, including on positions the project's contributors privately favor.

This commitment is structural, not aspirational. The project's contributors have political views, and good intentions do not survive the pressures of usage and growth. Neutrality is preserved through:

- A public, contestable rubric that can be inspected and disputed.
- Categories of analysis that prioritize structural features over substantive judgments.
- Symmetric application — the engine applies the same standards to drafts the user is writing as to posts the user is replying to.
- Public refusal to adjudicate questions where the engine cannot operate fairly.
- Cross-ideological validation for high-stakes changes to the rubric or engine.

When the project fails this commitment, it should be visible and correctable. When it cannot meet this commitment for a specific category of analysis, it refuses to operate in that category rather than operating poorly.

### Contestability

Every analytical claim the engine produces should be inspectable and disputable. Users can see why a label was applied, point at specific criteria, and argue that the criteria were misapplied or that the criteria themselves are wrong.

Contestability is layered. At the lowest level, individual labels are explained and disputable. At the next level, patterns of labels can be challenged with empirical evidence ("the engine consistently mishandles this kind of case"). At the highest level, the rubric itself is amendable through a public procedure.

The project rejects black-box analysis as a matter of principle. Analysis that cannot be inspected cannot be trusted, and a discourse-quality tool that cannot be trusted is worse than no tool at all.

### Transparency

The engine, the rubric, evaluation datasets, fine-tuned model weights, and the governance machinery are open source. This is a structural defense against bias and capture, not just an ideological preference.

Transparency does not extend to user data, security-relevant operational details, or in-progress dispute resolutions. The procedures are public; the personal applications of them sometimes are not.

### Restraint

The engine operates within scoped, well-defined categories. It does not freelance into harder problems just because users request it. Specifically:

- It identifies argument structure and rhetorical patterns. It does not declare claims true or false.
- It detects structural fallacies (gish gallop, motte-and-bailey, contradictions, dodging). It is more cautious about substantive fallacies (strawman, false equivalence) that require knowing what positions actually look like.
- It surfaces the strongest formulations of arguments on contested topics. It does not declare which side is "winning" except in narrow, clearly-labeled senses (traction, evidence density, responsiveness to rebuttals — never a single composite verdict).
- It does not analyze content involving private individuals beyond what they have voluntarily made public, and it does not analyze content involving minors.

When the engine encounters cases it cannot handle reliably, it says so. "I'm not sure" is a valid output, and a frequent one.

### Self-application

The engine's standards apply to the project itself. Disputes about labels are evaluated by the same rubric that produces them. Criticism of the rubric is examined for the same fallacies the rubric identifies. The project's own communications, including documents like this one, can be analyzed by the engine and found wanting.

This is not symbolic. A discourse-quality tool that cannot survive its own analysis is not credible.

## The relationship to platforms

The project does not seek to harm or undermine specific platforms. It seeks to improve the quality of discourse wherever discourse happens. If the project's existence puts pressure on platforms to improve their own moderation, surfacing of context, or treatment of bad-faith content, that is a welcome side effect — but it is not a goal, and the project's design will not be shaped to maximize damage to any specific platform.

The project will deploy on platforms that allow it (Bluesky's labeler infrastructure, browser extensions, standalone tools) and will not deploy on platforms that don't. It will not violate platform terms of service to gain reach. It will not scrape at scale where doing so is prohibited.

This is not a strategic choice. It is a consistency check. A project committed to honest discourse cannot operate by dishonest means.

## The relationship to users

Users are not customers in the sense that the project optimizes for what they want. They are participants in a system that has its own goals and standards. The project will sometimes refuse to do what users ask — refuse to help draft a personal attack, refuse to label something a fallacy when the structural criteria don't fit, refuse to declare a winner where the rubric says no winner can be declared.

This will cost adoption. It is intentional. The project's value depends on its standards being non-negotiable, and a project whose analysis bends to user preference is just a sophisticated mirror.

Users who want a tool that helps them win arguments at all costs are not the audience. The audience is users who want to think and write better, and who understand that requires a tool willing to push back on them.

## The relationship to truth

The project is not in the business of declaring what is true. It is in the business of making the structure of arguments about what is true more legible.

For empirical questions where strong expert consensus exists, the engine may surface that consensus and the evidence supporting it. For empirical questions that are genuinely contested, the engine maps the dispute rather than resolving it. For value questions, the engine identifies them as value questions and does not treat them as empirical disputes in disguise.

The engine is not neutral about reasoning quality. It is neutral about the conclusions that good reasoning should reach.

## Sustainability

The project will be sustained at whatever budget level is available without compromising its principles. If the available budget cannot support the full ecosystem, the project will narrow scope to what can be done well rather than dilute quality across more components.

Revenue, if any, comes from sources that do not compromise the neutrality commitment. Acceptable: subscriptions for advanced features, licensing the engine for non-conflicting commercial use, grants from sources without ideological conditions, donations. Not acceptable: advertising, sponsorship by political organizations, any arrangement that creates a financial incentive to favor specific positions or platforms.

If the project cannot be sustained on these terms, it will be archived rather than compromised.

## Amendment

This document changes only through the procedure described in `GOVERNANCE.md`. Proposed changes are public, evaluated on their merits, and accepted only when they strengthen the project's mission rather than weaken it.

The default action when in doubt is to leave this document unchanged. Foundational documents that drift in response to short-term pressures stop being foundational.

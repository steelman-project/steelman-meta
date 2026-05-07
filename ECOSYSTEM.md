# Steelman — Ecosystem Vision

> **Status:** Draft v0.1. This document describes the intended shape of the project and the reasoning behind it. It is more revisable than `MISSION.md` but should still change deliberately, with the validation log capturing why.

## The problem this ecosystem addresses

Public online discourse has structural problems that no single product can fix. Bad-faith rhetorical moves are invisible to most readers. Strong arguments and weak arguments look similar at the surface. Contested topics produce more heat than understanding because the actual landscape of arguments is hard to see. Reply assistants are coming whether anyone wants them or not, and the ones built to maximize engagement will drag discourse further into manipulation.

A single tool cannot address all of this. A thread analyzer helps individual readers but doesn't change the landscape. An atlas of arguments helps people understand topics but doesn't reach people in the moment of arguing. A reply assistant changes how people argue but doesn't help readers evaluate what they're seeing.

The ecosystem is the answer. Multiple products, each addressing a different failure mode of online discourse, sharing a common analytical engine and a common rubric. Each product strengthens the others: usage of one populates data the others depend on; analysis from one validates calls made by another; trust earned by one transfers credibility to the next.

## The two subsystems

### The Argument Facilitator (individual scale)

Helps individuals participate in discourse better. Components:

- **Steelman Read** (the thread analyzer). A user supplies a link to a thread or pastes text. The system produces an argument map (claims, reasons, evidence), flags structural fallacies with explanations, identifies the strongest version of each side's position, and assesses the evidence supporting each claim. No persistent profiles; no public scores.

- **Steelman Reply** (the reply assistant). A user is composing a reply to a thread. The system analyzes both the thread and the user's draft. It surfaces the strongest version of the position the user is disagreeing with, identifies fallacies in the user's draft as well as in the thread, suggests concessions and clarifying questions where appropriate, and offers concise responses that name rhetorical fouls when the thread contains them. It also assesses whether the thread is worth engaging with at all and recommends disengagement when the productive move is silence.

- **Steelman Coach** (the personal coach). Optional component for users who want sustained feedback on their own argumentative habits. Analyzes patterns over time across a user's drafts (with explicit consent, never on posts without it). Private to the user.

### The Topic Aggregator (collective scale)

Maps the landscape of arguments on contested topics. Components:

- **Steelman Brief** (the brief generator). A user supplies a topic. The system produces a structured brief: the strongest arguments on each side with evidence, the key empirical disputes, the key value disputes, the points of common ground, and what new evidence would change the picture. Time-bounded — briefs reflect the state of the debate at the time of generation.

- **Steelman Atlas** (the debate atlas). Persistent topic pages that maintain the current state of arguments, evidence, and rebuttals. Updates as new arguments emerge. Multi-dimensional scoreboards (evidence density, dialectical performance, traction) shown separately rather than as a single composite. Provenance tracking for argument formulations rather than identity scoring for people.

- **Steelman Record** (the public-figure tracker). Narrowly-scoped accountability tooling for politicians, pundits, and public intellectuals who have voluntarily entered public discourse on policy questions. Tracks claims, predictions, retractions, and consistency over time. Right-of-reply built in. Treated as journalism with editorial standards, not as social scoring.

### The connecting layer

**Steelman Notes** (the labeler) sits between the subsystems. Deployed initially on Bluesky's labeling infrastructure, it exposes the engine's analysis as labels on public posts. Users subscribe; subscribers see labels on the content they view. The labeler is the public face of the engine — the first product where engine outputs reach people who didn't request them — and is the most carefully governed of the components.

The name deliberately echoes Community Notes; the lineage is real and acknowledged. Steelman Notes differs in that it analyzes argument structure rather than fact-checking specific claims, and in that the analysis comes from a public engine applying a public rubric rather than from individual contributor judgments.

## The shared substrate

All components are built on a common foundation:

The **analytical engine** turns posts into structured analysis. Argument cards (claim + reasoning + evidence + assumptions). Evidence objects (sources + quoted content + assessment). Fallacy detections (category + criterion + supporting span). Claim graphs (relationships between arguments and rebuttals). All components consume engine output; only the engine produces it.

The **rubric** defines what the engine is trying to do and how it makes calls. Categories of analysis, definitions, examples, edge cases, confidence grades, explicit refusals. Public, versioned, contestable. Every component applies the rubric faithfully or fails its own consistency check.

The **contestability machinery** handles disputes. Users dispute specific labels, point at criteria, propose rubric refinements. High-stakes changes require cross-faction validation in the bridging-algorithm style. Low-stakes refinements pass through faster procedures. All of it is public and versioned.

The **governance procedures** describe how the rubric and the engine evolve. Who can propose changes. How proposals are evaluated. What kinds of changes require what kinds of validation. This is the slowest-changing layer and the most carefully designed.

## How the components compose

The complementarity is more specific than "they all improve discourse." Concrete connections:

The thread analyzer's output is the data structure the brief generator consumes. Argument cards extracted from threads can populate topic pages in the atlas. Fallacy patterns identified at the thread level become inputs to the public-figure tracker's longitudinal analysis.

The brief generator gives the reply assistant context. When a user is replying about a contested topic, the assistant draws on the brief to ground the exchange in the broader debate state. The user sees not just the immediate thread but the strongest arguments and key disputes around the topic.

The atlas validates the engine. If the atlas's "top arguments" don't survive scrutiny when individual users analyze them through the thread analyzer, that's a flag for the engine. If the engine labels something a fallacy at thread level that the atlas treats as a serious position at topic level, that's a flag too. The two scales check each other.

The labeler's public exposure forces engine quality up. When the engine's outputs are visible to people who didn't request them, errors become reputation costs. This pressure is healthy: the labeler should not launch until the engine is good enough to survive it, and continued labeler operation depends on continued accuracy.

The personal coach trains users in the same vocabulary the labeler uses publicly. A user who has been coached on their own gish gallops is better equipped to recognize them in others. The vocabulary of structural fallacies spreads through use.

## The trajectory

The ecosystem is not built all at once. The order of construction matters because each stage validates the substrate for the next.

**Stage 0: Foundations.** The mission, the rubric, the architecture, the governance procedures. Documents only. This stage produces the meta-repo and the artifacts in it.

**Stage 1: The engine.** A working analytical engine implementing the rubric. Code, tests, evaluation datasets. Used internally; no public-facing product yet.

**Stage 2: Thread analyzer.** Simplest user-facing product. Validates engine quality with low stakes. The user requests analysis; nobody else sees the output.

**Stage 3: Brief generator.** First topic-level product. Modest scope, useful immediately. Surfaces topic-level structure problems before committing to a full atlas.

**Stage 4: Reply assistant.** Generative product. Higher complexity than diagnostic tools because it produces content, but uses the same engine. Symmetric self-application is the design lock that keeps it honest.

**Stage 5: Labeler.** First publicly-exposed product. Requires the contestability machinery to be fully operational and the engine to be hardened. Deploys on open infrastructure (Bluesky) where the legal and technical posture is friendliest.

**Stage 6: Atlas and public-figure tracker.** Highest-scale, highest-stakes products. Depend on substantial usage of earlier products to populate them. Built last because they require everything else to be working.

Each stage's transition gate is the same: the substrate (engine, rubric, contestability) is strong enough to support the next stage. Stages do not advance on schedule pressure; they advance when ready.

## What this is not

The ecosystem is not a content moderation system. It does not remove content, suspend accounts, or push platforms to do either. Its outputs are analytical, not punitive.

It is not a search engine. Users do not query it for information about the world; they query it for analysis of arguments about the world.

It is not a social network. There is no feed, no follower graph, no engagement optimization. Users come for specific analysis and leave with specific outputs.

It is not a replacement for journalism, fact-checking organizations, or human editors. It complements these by providing structural analysis at scale that humans cannot economically provide. Where high-stakes substantive judgment is needed, humans remain in the loop.

It is not finished even when all six stages ship. The engine improves continuously through the contestability machinery. The rubric evolves through validated disputes. The validation log records what was tried and what was learned. The project is more like an organism than a product — it grows, it adapts, and it can die if it stops being useful.

## Risks the ecosystem creates and how it answers them

**The "another partisan tool" risk.** Mitigated by the structural neutrality commitments: open rubric, open engine, symmetric application, cross-faction validation, public refusals to operate where neutrality cannot be maintained.

**The "scaled bad-faith" risk** (the reply assistant making manipulation more sophisticated rather than less). Mitigated by the assistant's design: it analyzes the user's own drafts as well as the thread, refuses to help with certain rhetorical moves, recommends disengagement when warranted, and surfaces concessions before rebuttals.

**The "captured rubric" risk** (the rubric drifting to favor one side over time). Mitigated by the amendment procedure: high-stakes changes require cross-faction agreement, all changes are versioned and public, and the validation log catches patterns of drift.

**The "Goodhart" risk** (users optimizing for the engine's measures rather than the underlying quality). Mitigated by the engine refusing to score people, by the public visibility of the rubric making gaming harder to hide, and by continuous evolution of the rubric in response to gaming patterns.

**The "tribal scoreboard" risk** (the topic aggregator becoming sports for political tribes). Mitigated by the multi-dimensional scoreboards, the explicit separation of traction from evidence quality, and the design choice to emphasize "best arguments on each side" over "who's winning."

**The "abandonment" risk** (the project losing momentum and leaving the engine in a state where it can be misused). Mitigated by open-sourcing the engine and rubric: if the project is abandoned, the artifacts remain available for others to fork or learn from, and the documents capture enough of the reasoning that the project does not need to be reconstructed from scratch.

## What success looks like

In the small: a thread analyzer that careful readers find genuinely useful, a brief generator that produces shareable summaries of contested topics, a reply assistant that demonstrably improves the quality of replies that pass through it, a labeler that bystanders trust across ideological lines.

In the large: a working demonstration that contestable, transparent, structurally-fair analytical tools can be built and sustained. Other projects build on the rubric and the engine. The vocabulary of structural fallacies spreads through online discourse. People who use the tools become better at thinking and writing, and that effect propagates beyond the user base.

The project does not need to dominate any market to succeed. It needs to demonstrate that a particular kind of tool is possible, and to make that demonstration public and forkable.

If after several years the project has produced a small, trusted set of tools used by careful thinkers across the political spectrum, and if the rubric and engine have been adopted or adapted by other projects pursuing similar goals, that is success.

If the project has grown large but compromised on neutrality to do so, that is failure regardless of size.

# Steelman — Architecture

> **Status:** Draft v0.1. This document describes the technical structure of the ecosystem. It changes more often than `MISSION.md` or `RUBRIC.md`, but changes are deliberate and recorded.

## What this document is

The ecosystem consists of multiple products built on a shared substrate. This document describes the substrate — the engine, the data model, the contestability machinery — and how individual products consume it. Each product has its own architecture document with its specific concerns; this document covers what they share.

## Architectural principles

**Substrate first.** The engine and data model are the source of truth. Products are interfaces over the substrate. Substrate decisions constrain product decisions, never the reverse.

**Rubric-faithful.** Every analytical output is traceable to specific rubric clauses. The engine cannot produce labels that the rubric does not authorize. When the rubric does not cover a case, the engine refuses or surfaces uncertainty rather than improvising.

**Composable, not monolithic.** Components communicate through stable interfaces. Replacing one component (a different fallacy detector, a different LLM backend) does not require changing others. This matters because the engine will evolve, and the architecture should let it evolve component by component.

**Contestable end to end.** Every analytical claim carries provenance: which rubric version, which model, which input, which criteria triggered. If a user disputes a label, the system can reproduce the call and explain it.

**Privacy-preserving by default.** User data is minimized, segregated, and not used for analysis without explicit consent. Public data is analyzed; private data is not.

**Open where openness matters.** The engine, the rubric implementation, the contestability machinery, and the evaluation datasets are open source. Operational specifics, security infrastructure, and user data are not.

## The shared substrate

### The data model

All products produce and consume the same structured objects. The shape of these objects is part of the project's stable public interface.

**Argument card.** A normalized representation of a single argumentative move. Contains:
- A claim (the proposition being asserted)
- A reasoning chain (how the claim is supported, if at all)
- Evidence references (links, citations, quoted facts)
- Assumptions (what must be true for the argument to hold)
- Stance (pro/con/conditional relative to a thesis, where applicable)
- Provenance (where this formulation appeared, with timestamps)

**Evidence object.** A reference to a source supporting (or contesting) a claim. Contains:
- A canonical identifier (URL, DOI, citation)
- The specific quoted content the citation supports
- An assessment of whether the source actually supports the claim (deferred to substantive analysis; v1 only records the citation, not whether it's accurate)
- The type of source (primary, secondary, opinion, etc.)

**Fallacy detection.** A specific application of a rubric category to a span of text. Contains:
- The rubric category and version
- The criteria that triggered (which clauses of the rubric)
- The supporting span (the specific text that triggered the detection)
- The confidence level (definitive, pattern, uncertain)
- The reasoning chain (how the engine concluded the criteria were met)

**Claim graph.** A graph of argumentative relationships within a thread or topic. Nodes are argument cards; edges are relationships (supports, rebuts, qualifies, asks-about). Used for thread-level and topic-level analysis.

**Topic.** A bounded subject of debate, with a thesis statement framing the question. Contains references to argument cards, key empirical disputes, key value disputes, and provenance information.

**Dispute.** A formal challenge to an analytical claim. Contains:
- The disputed object (label, argument card, topic representation)
- The dispute type (criterion misapplied, substantive error, scope issue)
- The disputant's reasoning
- The resolution (if any) and rationale

These objects are versioned. Schema changes are explicit and rubric updates may produce new fields, but old objects remain valid under their original schemas.

### The analytical engine (Steelman Core)

**Steelman Core** is the analytical engine. It reads input (a post, thread, or document) and produces structured output (argument cards, fallacy detections, claim graphs). Every product in the ecosystem consumes Core's output; only Core produces it.

**Pipeline structure:**

1. **Ingestion and normalization.** Input is parsed into a canonical form: text content, author identifier (where applicable), timestamp, threading relationships, embedded media references. Different sources (raw text, social platform posts, web pages) feed into the same downstream stages.

2. **Argument extraction.** The text is analyzed to identify claims, reasoning, and evidence references. This produces a draft set of argument cards. This stage uses LLMs heavily and is the most expensive.

3. **Fallacy detection.** Each rubric category is checked against the input. Detections are produced with confidence levels and supporting evidence. Tier 1 categories produce definitive labels when criteria are met; Tier 2 categories produce pattern surfacings; cases below confidence thresholds produce uncertainty acknowledgments.

4. **Graph construction.** For thread or topic input, argument cards are connected by their argumentative relationships. The graph captures who is responding to whom and how.

5. **Output assembly.** Results are packaged with full provenance: rubric version, model versions used, input identifier, confidence levels, and supporting spans for every claim.

**Backend abstraction.** The engine uses LLMs as one component but is not bound to a specific model. The abstraction layer allows swapping between Anthropic models, other commercial models, or local models depending on cost, latency, and accuracy needs. Different stages of the pipeline can use different models — cheap models for initial classification, expensive models for hard cases.

**Caching.** Analytical outputs are cached aggressively. Most thread analyses requested by users will be analyses someone else has already requested. Cache invalidation respects rubric version: when the rubric changes, cached analyses are flagged as produced under an older version, and users can request fresh analysis.

**Evaluation.** Every change to the engine is evaluated against the evaluation datasets before deployment. Regressions in symmetric application are blocking — a change that improves overall accuracy but makes the engine less even-handed across the political spectrum is not deployed without rubric-level review.

### The rubric integration

The rubric is implemented in code as a structured definition that the engine consumes. Each category has:

- A canonical name and version
- A definition (matching the rubric document)
- Detection logic (the algorithmic specification)
- Examples and counter-examples (used for evaluation)
- Confidence thresholds
- Refusal cases

When the rubric document changes, the code implementation must be updated and re-evaluated against the test sets. Documents and code stay in sync through a versioning protocol — the rubric document and the engine code share version numbers, and a mismatch is a deployment-blocking error.

### The contestability machinery

Disputes are first-class objects with their own lifecycle.

**Dispute creation.** A user who disputes a label provides:
- A reference to the specific label being disputed
- A categorization of the dispute (criterion misapplied, scope issue, substantive error, rubric problem)
- Reasoning supporting the dispute, with specific reference to rubric criteria where applicable
- Optional: proposed alternative label or rubric refinement

The dispute creation flow requires effort proportional to the claim. There is no one-click "this is wrong" button. Users must engage with the rubric to dispute outputs of the rubric.

**Dispute evaluation.** Disputes are evaluated by the engine against the rubric. A dispute that contains fallacies (using the rubric's own categories) is recognizable and can be flagged. A dispute that points at specific structural features the criterion missed is substantive and is routed to human review.

**Dispute resolution.** Resolutions are public and versioned. A resolved dispute produces:
- A determination (label stands, label disputed, label withdrawn, rubric refinement proposed)
- Reasoning supporting the determination
- Links to any rubric changes the dispute prompted

Disputes do not retroactively change historical labels. The original label stands with the dispute attached; new labels apply the refined criterion. This prevents gaming through dispute volume.

**Cross-faction validation.** For high-stakes changes (rubric amendments, withdrawal of common-pattern labels, expansions of refusal scope), the bridging-algorithm-style validation requires endorsement from contributors with diverse rating histories. The mechanism is described in detail in `GOVERNANCE.md`.

### The validation log

Every meaningful change to the engine, the rubric, or the components is recorded in the validation log. Entries include:

- What was changed
- What evidence prompted the change
- What evaluation was done before deployment
- What the projected impact was
- What the actual impact has been (filled in over time)

The validation log is the artifact that makes the project visibly self-improving. It is also the document that catches drift: re-reading it periodically should let an outside reviewer assess whether the project is moving toward its goals or has wandered.

## Product architecture

Each product is a different way of exposing the substrate. They all consume the same engine, apply the same rubric, and contribute to the same data model.

### Steelman Read (thread analyzer)

The simplest product. A user supplies input (a URL or pasted text); the engine produces analysis; the result is rendered to the user. No persistent state beyond cache. No public output. Steelman Read is where engine quality is validated before more visible products launch.

Architecturally: a web interface (and possibly CLI) that accepts input, calls Core, renders output. Stateless beyond caching.

### Steelman Brief (brief generator)

A user supplies a topic; the engine produces a structured brief. More complex than thread analysis because it requires aggregating multiple sources, identifying common arguments, and synthesizing a topic-level view. Uses the topic data model.

Architecturally: an interface that accepts a topic specification, runs an aggregation pipeline (which may include user-provided source links and possibly some search-based discovery), produces a brief, and persists it. Briefs are versioned because the state of debates changes; the user sees when a brief was generated and what it represents.

### Steelman Reply (reply assistant)

The most complex product. The user is composing a reply; the system analyzes both the thread and the user's draft, surfaces information about the thread (steelmanned opposing view, fallacies, recommended engagement strategy), and analyzes the user's draft for the same patterns it detects in others' content.

Architecturally: a tighter integration loop. The system analyzes the thread once (or pulls from cache), then runs incremental analysis on the user's draft as it changes, surfacing feedback continuously. This requires careful UX work — fast feedback, non-intrusive delivery, useful suggestions rather than noise.

Steelman Reply is the only product that produces content (suggested phrasings, named-fallacy responses). All such content carries clear AI-assisted markers. The product refuses to help with rhetorical moves that violate the rubric: no help drafting personal attacks, no help with gish gallops, no help with bad-faith concession demands.

### Steelman Notes (labeler)

The first publicly-exposed product. Deployed as a Bluesky labeler, it applies analytical labels to public posts on that platform. Users subscribe; subscribers see labels on the content they view. Non-subscribers see nothing.

Architecturally: a service that monitors a configurable scope of Bluesky content (chosen by the labeler operator), runs Core analysis on items meeting threshold criteria (controversial, high-engagement, requested), produces labels, and publishes them through the Bluesky labeler API.

Steelman Notes is governed more strictly than the diagnostic products. Every label is publicly attributable to the labeler. Disputes are visible. The threshold for applying labels is conservative — better to under-label than to apply weak labels publicly.

### Steelman Atlas (debate atlas)

A public, persistent map of contested topics. Topic pages show the current state of arguments, evidence, and rebuttals, with multi-dimensional scoreboards (evidence density, dialectical performance, traction) shown separately rather than as a composite.

Architecturally: Steelman Atlas is fundamentally a database with a public reading interface. Topics are seeded by curators initially and grow through user contributions and engine analysis. The data model is the topic and argument card system already described.

Cold-start is a real problem here: a topic with three arguments isn't a useful atlas. Atlas launches with a small set of topics that have been curated thoroughly, expanding only as the substrate has enough density to support more.

### Steelman Record (public-figure tracker)

Narrowly scoped to politicians, pundits, and public intellectuals on policy questions. Tracks claims, predictions, retractions, and consistency over time. Right-of-reply built in.

Architecturally: Steelman Record is a curated database. Subjects are deliberately added; analysis is curated and reviewed before publication. This product is closer to journalism than to automated analysis. Core assists, but humans make publication decisions.

This product launches last because it has the highest reputational stakes and requires the most mature substrate.

## Repository structure

The codebase is organized to reflect the architectural separation:

```
steelman-meta/                      (this repo — foundational documents)
  MISSION.md
  ECOSYSTEM.md
  RUBRIC.md
  ARCHITECTURE.md
  GOVERNANCE.md
  LICENSING.md
  ROADMAP.md
  validation-log/

steelman-core/                      (the analytical engine)
  rubric-impl/  (rubric as code, in sync with steelman-meta/RUBRIC.md)
  evaluation/   (evaluation datasets, public)

steelman-read/                      (thread analyzer, phasekit-scaffolded)
steelman-brief/                     (brief generator, phasekit-scaffolded)
steelman-reply/                     (reply assistant, phasekit-scaffolded)
steelman-notes/                     (labeler, phasekit-scaffolded)
steelman-atlas/                     (debate atlas, phasekit-scaffolded)
steelman-record/                    (public-figure tracker, phasekit-scaffolded)
```

The meta-repo is the source of truth for foundational documents. Each other repo depends on the meta-repo's documents; they are read-only dependencies.

Steelman Core is the source of truth for the implementation of the engine and rubric-as-code. Product repos depend on Core as a library or service.

Cross-repo updates require explicit coordination: a rubric change in the meta-repo triggers a corresponding update in Core, which triggers re-evaluation of any product repos that consume the affected categories.

## Deployment

The deployment posture is "as little infrastructure as can support the current usage." Early stages run on minimal infrastructure (a small VPS or serverless deployment); later stages scale up as needed.

The engine can run as a library (consumed in-process by products) or as a service (consumed over the network). The early-stage default is library — simpler deployment, no service-to-service authentication. Later, when products run independently or third parties build on the engine, the service deployment becomes useful.

The labeler and atlas have specific deployment requirements (platform integration for the labeler, persistent storage for the atlas) that are addressed in their respective architecture documents.

## Versioning and evolution

The rubric, the engine, and the data model all version independently. Compatibility is explicit:

- Engine version N supports rubric versions M through M' (with M' = N's "current" rubric).
- Data model schemas are forward-compatible; old objects remain valid.
- Products specify which engine versions they support.

Breaking changes are rare and announced. Most evolution is additive: new rubric categories, new model backends, new fields in data objects. The architecture is designed to make additive change easy and breaking change visible.

## Cost-conscious choices

Several architectural decisions reflect the project's low-budget posture:

- Aggressive caching, especially for engine outputs that are expensive to generate.
- Tiered model usage (cheap models for easy classification, expensive models reserved for hard cases).
- Library-first deployment to avoid service infrastructure costs.
- Bluesky-first deployment for the labeler to avoid expensive social platform integrations.
- Curated-launch strategy for the atlas to avoid data-acquisition costs at scale.

The architecture supports scaling up if usage and budget grow, but does not require expensive infrastructure to deliver useful products at small scale.

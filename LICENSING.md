# Steelman — Licensing

> **Status:** Draft v0.1. This document specifies the licensing strategy for project artifacts. Changes go through the standard amendment procedure.

## Principles

The project's licensing reflects its commitments. The components that must be inspectable to be trusted are open. The components that can be operationally sensitive without harming trust may be closed. Where licensing is unclear, the default is openness in directions consistent with the project's mission.

The choice of specific licenses reflects a balance: strong enough to keep the artifacts from being privatized into closed competitors, permissive enough that legitimate use and adaptation is possible.

## What must be open source

The following artifacts are open source as a matter of project commitment, not strategic choice. Without them being open, the project's neutrality and contestability commitments cannot be honored.

### The rubric (`RUBRIC.md` and supporting documents)

License: **Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0).**

Rationale: The rubric is the analytical constitution. Its content must be public and its derivatives must remain public. CC BY-SA enforces that adaptations remain openly licensed, preventing forks into closed proprietary rubrics that could trade on the project's authority while concealing their actual criteria.

Attribution requirement: Adaptations must credit the original project clearly enough that users of the derivative can find the source.

### The analytical engine

License: **GNU Affero General Public License v3 (AGPL-3.0).**

Rationale: The engine is where bias would live if it existed. Open-sourcing it makes the analytical claims inspectable. AGPL is chosen specifically because the engine is likely to be deployed as a service, and AGPL's network-use clause requires that modifications to the engine remain open even when used in service-only contexts. A permissive license would allow someone to fork the engine, modify it (potentially in biased directions), and run it as a service without sharing the modifications.

The cost: some organizations refuse to use AGPL software. This is acceptable. The project does not need every organization to use the engine; it needs organizations that do use the engine to operate transparently. Organizations that find AGPL incompatible with their needs are encouraged to use alternative tools.

Dual-licensing option: Reserved. If commercial entities later want to embed the engine in proprietary contexts, dual-licensing (AGPL for community use, commercial license for closed use) is consistent with the project's principles and may provide a sustainability path. This is not committed to at v1; it remains an option.

### Fine-tuned model weights

License: **Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)** for weights and training configurations.

Rationale: Model weights produced by the project — fine-tuned models for fallacy detection, argument extraction, or other engine components — embody analytical decisions and must be inspectable. If the project quietly trains models with biased data, no amount of open engine code reveals the bias. Open weights and open training data together are required for trust.

Practical considerations: hosting weights at scale may require external infrastructure (Hugging Face, GitHub LFS, or similar). The project commits to making weights available through at least one publicly-accessible host with redundant backup.

### Evaluation datasets

License: **Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)** for datasets curated by the project.

Rationale: Evaluation datasets define what "working correctly" means for the engine. They are where bias hides most invisibly: a perfectly fair engine evaluated against biased examples produces biased optimization. The datasets must be inspectable, with their inclusion criteria and labeling decisions public.

Practical considerations: evaluation datasets may include third-party content (posts, articles, etc.) that has its own copyright. The project's curation, labels, and metadata are CC BY-SA; the underlying content remains under its original licenses. The datasets are structured so that the project's contributions (the labels and analyses) are clearly distinguishable from the third-party content.

For posts on social platforms, the datasets reference the posts (by URL or platform-specific identifier) rather than reproducing them where copyright would prevent reproduction. This may make the datasets less self-contained but respects underlying rights.

### The contestability machinery and governance code

License: **GNU Affero General Public License v3 (AGPL-3.0).**

Rationale: The procedures by which disputes are handled and the rubric is amended must be inspectable. Closed governance code would let the project (or a fork) quietly subvert its own commitments. AGPL ensures these mechanisms remain transparent even in service deployments.

### The data model and interface specifications

License: **Creative Commons Attribution 4.0 International (CC BY 4.0)** or public domain (CC0), maintainers' choice per specification.

Rationale: Interface specifications are most useful when widely adopted. Permissive licensing here encourages other projects to use the same data structures, increasing interoperability. The shared substrate becomes more valuable as more projects use it.

## What may be open source (case-by-case)

The following components have open-source as a default but the licensing decision is made per-component based on circumstances at the time of release.

### Product user interfaces

The user-facing components of each product (thread analyzer UI, brief generator interface, reply assistant UX, atlas frontend) are evaluated individually.

**Default direction: open source under AGPL-3.0** for products whose outputs reach public discourse. The labeler and reply assistant in particular benefit from open UI code because the UI shapes how engine outputs are presented to others; a closed UI could distort presentation in ways the open engine cannot prevent.

**Acceptable to keep source-available or proprietary**: the thread analyzer UI, the brief generator UI, the personal coach. These produce private outputs to individual users; UI distortions don't affect public discourse. Keeping these closed if it serves project sustainability is consistent with the project's principles.

The case-by-case decision is made when the product is built and recorded in the validation log.

### Product-specific adapters

Adapters that connect the engine to specific platforms (Bluesky labeler API client, browser extension content scripts, social platform integration) are typically open-sourced under AGPL-3.0 because they affect how the engine reaches public discourse, but the decision is made per-adapter.

### Documentation beyond the rubric

The architecture document, ecosystem vision, governance procedures, and other foundational documents are licensed under **CC BY-SA 4.0** by default.

The roadmap, validation log, and other operational documents are likewise CC BY-SA 4.0 unless they contain operationally-sensitive material (security incidents, individual contributor matters), in which case they may be redacted before publication.

## What is not open source

The following are not open-sourced because openness in these areas would harm the project or its users.

### User data

User-submitted disputes, reply-assistant drafts, personal-coach analyses, and any other user content are not open-sourced. The data structures are open; the user data within them is not.

User data is minimized: the project collects what is necessary for the function and no more. Where user data is retained (e.g., to support continued use of the personal coach), it is retained under the project's privacy policy and not used for training without explicit consent.

### Operational security infrastructure

Specific authentication tokens, rate-limiting parameters, abuse-detection patterns, and infrastructure configurations that would assist adversaries gaming the system are not published. The principles are public; the operational specifics are not.

### In-progress disputes and unpublished analyses

Disputes that are still being evaluated, analyses that have not yet been published, and rubric proposals that are still being refined are not necessarily public during the in-progress phase. They become public when complete (with the procedure described in `GOVERNANCE.md`).

### Personal information of contributors

Contributor identities are public unless contributors choose to participate pseudonymously. The choice is the contributor's. Contact information, personal addresses, and similar identifying information are never published without consent.

## License compatibility and interactions

**AGPL and CC BY-SA together.** The engine (AGPL) and rubric (CC BY-SA) are compatible because they are different kinds of artifacts: code and a specification document. The engine implements the rubric; the rubric does not require that implementations use the same license, only that adaptations of the rubric document remain openly licensed.

**Third-party dependencies.** The engine and other code components use third-party libraries. License compatibility is checked: AGPL-licensed code can use libraries under most permissive licenses (MIT, BSD, Apache 2.0) and other copyleft licenses (GPL family). Libraries with incompatible licenses are not used.

**External integrations.** Where the project integrates with platforms (Bluesky's labeler API, social platforms' APIs where permitted), the integration code is AGPL but the platforms themselves are governed by their own terms. The project respects platform terms; the project's open licensing applies to the project's code, not to the platforms.

## Trademark and project naming

The project's name and any associated logos or branding are reserved. Forks of the engine or rubric must not use the project's name in ways that imply endorsement or affiliation. The trademark is held by the project's maintainers (or eventual nonprofit, if one is established).

This is consistent with practice in open-source projects with reputational stakes. The code is open; the brand is not. A fork may legitimately use the engine and rubric to build a different project; it should not call that project by the original project's name.

Specific trademark policy will be developed as the project grows. v1 commitment: the project name is reserved for use by the canonical project; forks are welcome but use distinct names.

## Sustainability and licensing

The licensing choices here do not preclude sustainability. Possible revenue sources consistent with the licensing:

- **Hosted services.** AGPL allows the project to operate hosted services and charge for them; the engine remains open and self-hostable. Hosted services may include analysis at scale, customized labelers, or integration support.
- **Commercial licensing.** Where the AGPL incompatibility is the only barrier to a legitimate commercial use, a commercial license can be granted. This is a future option, not a v1 commitment.
- **Grants and donations.** The project structure (open source, neutral, non-commercial in primary intent) is compatible with grants from foundations, individual donations, and similar funding sources.
- **Support and consulting.** Helping organizations integrate the engine, customize the rubric for specific contexts (e.g., for educational settings), or operate labelers can be a commercial service.

What is not acceptable:
- Advertising in any project-operated product.
- Sponsorship by political organizations.
- Any arrangement that creates a financial incentive to favor specific positions, platforms, or outcomes.

## Changes to licensing

License changes are Level 4 amendments. They require the full procedure in `GOVERNANCE.md`: cross-faction validation, public comment period, adversarial review, and explicit reasoning.

Licenses can become more open without going through the full procedure (a tightening). Licenses cannot become more closed without it (a loosening of openness commitments). This asymmetry reflects the project's bias toward transparency.

If the project closes (per `GOVERNANCE.md`), the open-source artifacts remain under their existing licenses. The closure cannot retroactively privatize what was open.

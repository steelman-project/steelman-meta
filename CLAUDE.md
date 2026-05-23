# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

`steelman-meta` is the **foundational-documents repo** for the Steelman ecosystem. It contains no code, no build system, no tests — only seven Markdown documents and (eventually) a `validation-log/` directory. There are no commands to run, lint, or build. Treat this repo as a constitution: the documents constrain everything that gets built in the sibling repos.

The ecosystem (mostly not yet built) is laid out in `ARCHITECTURE.md` and consists of `steelman-core` (the analytical engine and rubric-as-code) plus product repos `steelman-read`, `steelman-brief`, `steelman-reply`, `steelman-notes`, `steelman-atlas`, `steelman-record`. Each of those repos depends on this one as a read-only source of truth.

## Document hierarchy and how it constrains edits

The documents are deliberately ordered by stability. Edit accordingly:

| Document | Stability | Meaning for edits |
|---|---|---|
| `MISSION.md` | Foundational; changes only via Level 4 amendment | Default action when in doubt is to leave it unchanged. |
| `RUBRIC.md` | Foundational; analytical constitution | Must stay version-synced with `steelman-core/rubric_impl/` once that exists. A mismatch is treated as a deployment-blocking error. |
| `ARCHITECTURE.md` | Deliberate but more revisable than mission/rubric | Changes are recorded in the validation log. |
| `GOVERNANCE.md` | Procedures are themselves amendable, only via the procedures they describe | |
| `LICENSING.md` | Tightening (more open) is unconstrained; loosening requires Level 4 | |
| `ROADMAP.md` | Changes most often as stages complete | Substantive revisions get a validation-log entry. |
| `README.md` | Stays in sync with the above | |
| `validation-log/` | Append-only ledger of changes | Entries are `YYYY-MM-DD-short-description.md` with the schema in the directory's README. |

The four-level dispute/amendment procedure in `GOVERNANCE.md` (Level 1 specific label → Level 2 pattern → Level 3 rubric refinement → Level 4 rubric amendment) governs *how* changes happen. Even when working solo, edits to foundational documents should look like what those procedures would produce: explicit reasoning, named criteria, examples, adversarial-review consideration, and a validation-log entry for substantive changes.

## Cross-document invariants to preserve

These are the consistency points that silently rot if one document changes without the others:

- **Subsystem and product names** — the two-subsystem split (Argument Facilitator / Topic Aggregator) and the six product names (Steelman Read / Brief / Reply / Notes / Atlas / Record) appear in `README.md`, `MISSION.md`, `ECOSYSTEM.md`, `ARCHITECTURE.md`, and `ROADMAP.md`. Renaming or restructuring requires updating all of them in one change.
- **Stage numbering** — Stages 0–6 in `ROADMAP.md` are referenced from `ECOSYSTEM.md` ("The trajectory") and the gating-criteria language in `ARCHITECTURE.md`. Keep them aligned.
- **Tier 1 categories** — `RUBRIC.md` defines categories (self-contradiction, unsupported claim, question-dodging, gish-gallop pattern); `ARCHITECTURE.md` and `ROADMAP.md` reference "Tier 1" as the engine's initial scope. Adding/removing a category is a Level 4 amendment that touches all three.
- **License assignments** — `LICENSING.md` is authoritative; `README.md` summarizes it. `ARCHITECTURE.md` and `ECOSYSTEM.md` mention "open source" in passing — those mentions must not contradict `LICENSING.md`'s actual assignments (rubric/datasets/weights are CC BY-SA 4.0; engine/contestability/governance code is AGPL-3.0).
- **Refusal scope** — the engine's explicit refusals (no truth adjudication, no person-scoring, no minors, no private individuals beyond what they made public) appear across `MISSION.md`, `ECOSYSTEM.md`, `RUBRIC.md`. These are load-bearing commitments; don't soften them in one document while leaving the others.

## Known state discrepancies

- `README.md` and `ARCHITECTURE.md` reference a `validation-log/` directory at the repo root, but the only existing validation-log artifact is at `mnt/user-data/outputs/steelman-meta/validation-log/README.md`. The `mnt/user-data/outputs/` path looks like a scratch/export location, not the intended canonical home. Before writing the first real entry, confirm with the user where the directory should live (most likely: create `validation-log/` at the repo root and move the existing README there).
- Sibling repos (`steelman-core`, `steelman-read`, etc.) are described in `ARCHITECTURE.md` but do not yet exist. The project is at Stage 0; references to "the engine" or "Steelman Core" in the documents are forward-looking.

## Editorial style of these documents

The existing documents share a deliberate voice worth preserving when editing:

- Each document opens with a `> **Status:** Draft v0.1.` blockquote noting how the document changes.
- Section ordering goes principles → mechanics → edge cases → what this is not.
- "Not" sections are explicit and load-bearing, not modesty disclaimers — preserve them when editing.
- Categorical claims ("the project will refuse...", "the engine does not...") are commitments, not aspirations. Don't downgrade them to "tries to" or "aims to" without a governance reason.
- No marketing language, no emoji, no first-person plural cheerleading.

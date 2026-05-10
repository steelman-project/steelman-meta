# Steelman — Validation Log

This directory records what has been tried, what has been learned, and what has changed in the project. It is the artifact that demonstrates the project is visibly self-improving rather than just nominally so.

## Format

Entries are markdown files named `YYYY-MM-DD-short-description.md`. Each entry includes:

- **What changed.** A clear statement of what was modified (rubric clause, engine component, architecture decision, etc.).
- **What evidence prompted the change.** What was observed, what disputes were filed, what evaluations were run.
- **What evaluation was done before deployment.** Test results, adversarial review notes, symmetric application checks.
- **What the projected impact was.** What was expected to happen.
- **What the actual impact has been.** Filled in over time as evidence accumulates. May span multiple updates.

## Why this exists

The project commits to contestability and self-improvement. Those commitments are meaningful only if there is a record showing how they have actually played out. The validation log is that record.

Re-reading the log periodically should let any reviewer assess whether the project is moving toward its goals or has wandered. If the log shows a pattern of changes that consistently favor one political direction, that pattern is visible and addressable. If the log shows a pattern of accepting changes too quickly without adversarial review, that pattern is visible and addressable. The log is the project's mirror.

## Initial entries

The first substantive entries will accumulate as Stage 0 work completes and Stage 1 begins. Until then, this directory holds only this README.

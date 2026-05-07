# Steelman — Meta Repository

This repository contains the foundational documents for **Steelman**, an ecosystem of tools designed to make online discourse healthier through structural analysis of arguments, transparent rubrics, and contestable governance.

The project takes its name from the practice of *steelmanning* — restating an opposing argument in its strongest, most defensible form before engaging with it. The name describes the project's core commitment: every component is built to surface the strongest version of arguments across the political spectrum, and to apply analytical standards symmetrically regardless of which side any given call favors.

The ecosystem is composed of two cooperating subsystems:

- The **Argument Facilitator** operates at individual scale: thread analyzer, reply assistant, personal coach.
- The **Topic Aggregator** operates at collective scale: brief generator, debate atlas, public-figure tracker.

Both subsystems share an analytical engine and a public rubric. The rubric defines what the engine analyzes and how it makes calls. The engine implements the rubric. Every analytical claim is contestable through public procedures.

## Documents

Read in this order if you are new to the project:

1. **[MISSION.md](MISSION.md)** — What the project is, what it is not, and the principles that govern it.
2. **[ECOSYSTEM.md](ECOSYSTEM.md)** — The vision for how the components compose into a system and the trajectory by which they are built.
3. **[RUBRIC.md](RUBRIC.md)** — The analytical constitution. What the engine analyzes, how it makes calls, where it refuses to operate.
4. **[ARCHITECTURE.md](ARCHITECTURE.md)** — The technical structure: the shared substrate, the data model, the contestability machinery, how products consume the engine.
5. **[GOVERNANCE.md](GOVERNANCE.md)** — How disputes work and how the rubric evolves.
6. **[LICENSING.md](LICENSING.md)** — What is open source, what is not, and why.
7. **[ROADMAP.md](ROADMAP.md)** — The bootstrap plan with stages and gating criteria.

The `validation-log/` directory records what has been tried, what has been learned, and what has changed.

## Status

This is an early-stage project. The documents are working drafts. The project's methods include adversarial review of its own foundations; expect changes as the rubric in particular is stress-tested.

## Contributing

The project welcomes contribution but operates with deliberately strong filters on what gets accepted. Read the foundational documents before opening issues or proposals. Disputes about analytical claims go through the procedures in `GOVERNANCE.md`, not through general issue tracking.

The project is committed to neutrality across political and ideological lines. Contributions that would compromise this commitment are not accepted, regardless of the contributor's intentions.

## Licensing

The licensing strategy is detailed in `LICENSING.md`. Briefly:

- The rubric, evaluation datasets, and fine-tuned model weights are CC BY-SA 4.0.
- The analytical engine, contestability machinery, and governance code are AGPL-3.0.
- Other components are licensed individually as they are built; the default direction is openness.

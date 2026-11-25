# Context Workbench

## Purpose
Context Workbench is an early-stage project for engineering, evaluating, and improving the business context that feeds Databricks Genie Ontology. Its goal is a versioned source of truth for the definitions teams own, with evidence of how faithfully Genie applies those definitions.

The primary workflow is reviewing a change in business meaning. A reviewer should be able to see what changed, who approved it, which assets and Genie targets depend on it, and which answers are expected to change. The first pilot will test how much of that review existing tools can support and where a dedicated workbench would help.

## Tech Stack
- Markdown, Git, Reffy, and ReffySpec for project context and planning.
- Proposed pilot surfaces are Unity Catalog metric views and Pages, one curated Genie Agent, and native Agent benchmarks. The Genie Agent CI/CD example is a starting point for versioning and publishing with Databricks Declarative Automation Bundles.
- The workbench application stack, storage for definition history, and deployment model are open.

## Project Conventions

### Code Style
The repository is documentation-only. Use Markdown for project notes and follow the repository's Reffy and ReffySpec conventions for artifact filenames, change IDs, and spec structure. Application code conventions are open.

### Architecture Patterns
- Give each business definition a stable identity, a business owner, and a scope. Use bindings to identify the governed assets that implement or explain it. For the pilot, keep the calculation in the governed metric view and record the version reviewed together with the associated Page and Genie Agent configuration.
- Explore an append-only approval history inspired by the Lasm meaning ledger. Record when a version takes effect, who approved it, why, and which policy authorized the approval. Preserve earlier versions when a definition is superseded so a reviewer can reconstruct the meaning used for a past report or answer.
- Allow business units to own distinct definitions of a shared term. Record an approved equivalence or conversion where one exists. A question spanning units may require clarification when there is no approved combined definition.
- Review changes to approved meaning and changes to delivered context together. A new attribution rule can justify new expected answers. A change to instructions, mappings, or examples can be evaluated against the same expectations.

### Testing Strategy
Start with one dealership sales-pace definition and one curated Agent. Use a contract signed April 30, a delivery on May 1, and a dealership closure in the first week of May to expose differences in attribution and elapsed selling days. Establish independently reviewed expectations before running the benchmark. Include held-out rephrasings and a case where the expected behavior is to ask for clarification. Keep evaluation questions and reference answers out of Genie tuning examples.

Compare the current and candidate context using the same data snapshot, evaluation date, and identity. Inspect generated SQL for date, scope, and grain as well as checking the result. Record the definition version, Agent configuration, and evaluation identity with each run. The pilot succeeds if a reviewer can trace a wrong answer to the definition, asset mapping, or delivered context and verify a correction on held-out questions.

### Git Workflow
Version project context and planning documents in Git. Keep exploratory artifacts under `.reffy/artifacts/`, proposed changes under `.reffy/reffyspec/changes/`, and current specs under `.reffy/reffyspec/specs/`. Follow the repository's [ReffySpec instructions](AGENTS.md) when opening a proposal. Branching and release conventions are open.

## Domain Context
Dealership sales pace depends on which event qualifies as a sale, which local date assigns it to a reporting month, how elapsed selling days account for store closures, and how sales are aggregated across dealerships with different calendars. These are business decisions owned by the relevant domain. The context layer can also describe business terms, entities, synonyms, data grain, and when Genie should ask for clarification.

## Important Constraints
- Workbench authority covers the team's approved definitions, asset bindings, and release evidence. Genie may also draw on context learned from assets and usage.
- Evaluation records observed behavior. Definition owners approve changes to business meaning. A curated Agent benchmark provides evidence for that Agent. Broader Ontology discovery through Genie One needs its own check if brought into scope.
- Use the pilot to learn which existing governed assets can be referenced directly and whether release review requires additional tooling. Generating assets from definition history remains open.

## External Dependencies
- Databricks Unity Catalog and Genie for governed assets, context delivery, and evaluation.
- Existing accelerator candidates cover ontology readiness, KPI-to-asset authoring, deployment, and Agent benchmarking. [Databricks accelerator notes](../artifacts/databricks-genie-context-accelerators.md)
- Lasm (LogicalAssembly) is the project formerly called Nuveris. The meaning-ledger reference uses Reffy project ID `nuveris` in the shared Paseo workspace `nuveris-v1`. The reference and its implications for the pilot are documented in the [workbench ideation note](../artifacts/genie-ontology-context-workbench.md).

## Project references

- [Seed discussion](../../seed.md)
- [Context Workbench README](../../README.md)

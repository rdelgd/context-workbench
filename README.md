# Context Workbench

Context Workbench is an early-stage project for engineering, evaluating, and improving the business context that feeds Databricks Genie Ontology. Its goal is to give teams a versioned source of truth for the definitions they own and a way to test whether Genie applies those definitions correctly.

## What the workbench would do

A business definition can span a metric calculation, a data model, and guidance about how to interpret a question. The workbench would connect those pieces so a reviewer can see what changed, where the definition is used, and which answers should change as a result.

- Record business terms, metric definitions, and interpretation rules with an owner and scope.
- Map definitions to the Databricks assets that implement or explain them, such as Unity Catalog metric views and curated Genie Agent instructions.
- Review and publish updated context, with a record of the definitions and assets in each release.
- Compare Genie’s answers with approved expectations using representative questions, held-out rephrasings, and edge cases.

Evaluation results would guide improvements to mappings, examples, and instructions. Changes to business meaning would go through review by the definition’s owner.

## Example: dealership sales pace

What counts toward May sales pace when a contract is signed on April 30 and the vehicle is delivered on May 1? The definition needs to specify which event counts as a sale, which date assigns it to a month, and how dealership closures affect the number of elapsed selling days.

The workbench would link those decisions to the assets Genie uses and to tests that expose differences between interpretations. If the business changes the qualifying event from signing to delivery, a reviewer could see which assets need updating and which expected answers should move.

## Project status

The project is in exploration. The [seed discussion](seed.md) explains the initial direction. The [Reffy artifact](.reffy/artifacts/genie-ontology-context-workbench.md) develops the idea and sketches a first experiment with one sales-pace definition and one Genie Agent.

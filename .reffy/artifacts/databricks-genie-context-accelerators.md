# Public Databricks accelerators for Genie context engineering

This note follows the [Context Workbench exploration](genie-ontology-context-workbench.md). The public Databricks tools reviewed here cover assessment, authoring, deployment, and evaluation. Together they offer a way to test the workbench idea with a real business definition before committing to an app. This comparison is based on public repositories and documentation.

## What to reuse

| Tool | Where it fits |
| --- | --- |
| **Genie Ontology Readiness** | Deploy the Databricks App as-is to assess workspace readiness. Its read-only assessment scores areas such as Unity Catalog metadata, relationships, metrics, domains, and Genie adoption. It provides a prioritized enablement plan and points to other accelerators. [Repository and deployment guide](https://github.com/databricks-solutions/genie-ontology-readiness) |
| **AI/BI Design-First Accelerator** | Use a KPI spec and an existing Unity Catalog schema to generate metric views and Genie configuration. It also includes dashboard generation and a greenfield workflow. The KPI-to-asset workflow is the part most relevant to Context Workbench. [Accelerator repository](https://github.com/databricks-solutions/databricks-aibi-design-first-accelerator) |
| **Genie Workbench** | Use the app as-is for curated Agent evaluation and optimization. It can propose governed metric views, attach approved candidates, and use benchmarks to check their effect on Agent accuracy. Its semantic blueprint is based on the selected Agent’s configuration. [Semantic blueprint](https://databricks-solutions.github.io/databricks-genie-workbench/docs/features/semantic-model/), [Auto-Optimize](https://github.com/databricks-solutions/databricks-genie-workbench/blob/main/docs/docs/features/auto-optimize.md) |
| **Genie Agent CI/CD example** | Start here for versioning and publishing. The retail example uses Git and a Declarative Automation Bundle to manage metric-view YAML and Genie Agent configuration, including instructions, examples, and benchmark questions. [Reference implementation](https://github.com/databricks-solutions/databricks-blogposts/tree/main/2026-08-genie-agent-cicd) |

## Try one sales-pace definition first

Use the CI/CD example and native Genie Agent benchmarks for the first pass. Keep the approved calculation in a governed metric view and use a Unity Catalog Page to record the business meaning, including what counts as a sale and how the selling calendar works. Link the Page to the implementing asset. [Unity Catalog Pages](https://docs.databricks.com/aws/en/uc-semantics/pages)

Create a boundary case with an April 30 contract, a May 1 delivery, and a dealership closure during the first week of May. Compare results against an independently reviewed expectation that reflects the approved attribution date and selling-day denominator. Include held-out rephrasings and record the definition version and Agent configuration alongside the results. [Genie Agent benchmarks](https://docs.databricks.com/aws/en/genie-agents/monitor)

If broader Ontology behavior matters for the pilot, ask Genie One the same question and inspect its citations for the definition and assets it selected. This gives a direct check on what Genie One surfaces alongside the curated Agent benchmark. [Genie One citations](https://docs.databricks.com/aws/en/genie-one/chat)

## What would justify building

Use a proposed shift from contract signing to delivery to test whether Git and the existing tools give the definition owner enough information to approve the release. Can the reviewer identify the affected Pages, metric views, Agent settings, and benchmark expectations in one review? Can they tell which answer changes were intended and which are regressions?

If that review still requires substantial manual tracing, the first custom capability worth exploring is a definition-centered review that connects affected assets and evaluation evidence to the approved decision. The pilot should establish which links and evidence are missing in practice.

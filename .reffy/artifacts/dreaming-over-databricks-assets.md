# Dreaming over Databricks assets

Context Workbench could have a “dreaming” state that reviews the day’s changes across Databricks and asks what they make possible for the context Genie uses. A run could surface a better source for an existing metric, recognize that two domains have started using the same term differently, or turn a recurring misinterpretation into a benchmark case. The output would be a set of candidate changes ready for the same review, testing, and possible deployment as a proposal from a person. [Context Workbench exploration](genie-ontology-context-workbench.md)

## What a run would look at

Start with changes since the last successful scan in a domain the workbench already understands. Compare catalog metadata and versioned asset definitions against the previous scan. Follow known bindings from approved terms to metric views, Pages, and Genie configurations, then use available lineage to look upstream and downstream at relevant tables, jobs, notebooks, and dashboards. A newly published asset outside the current bindings can still be a candidate if the run can explain its relevance. Unity Catalog metadata is permission-filtered, and lineage only records events it can capture. Each run should record what it observed and which sources it could inspect, so a gap in coverage carries through to review. [Information schema](https://docs.databricks.com/aws/en/sql/language-manual/sql-ref-information-schema), [Lineage system tables](https://docs.databricks.com/aws/en/admin/system-tables/lineage)

The workbench could combine signals that look unimportant on their own. A new dealership calendar, a dashboard switching to elapsed selling days, and a Genie answer that divides by calendar days together suggest a concrete improvement. The same scan might find a different dashboard using contract date. That would warrant a question about scope and ownership before any shared definition is proposed.

## What a reviewer would get

Each candidate would show the asset changes that prompted it, the current definition and configuration versions, a proposed diff, and the expected effect on answers. It would identify the owners and consumers affected and offer a test that could disprove the proposal. A run could surface competing interpretations or send an unresolved question to the owner when the evidence supports several explanations. Repeated observations could update the evidence on an existing candidate.

For example, suppose a new governed selling-day calendar can implement the already approved sales-pace denominator. The workbench could propose binding the metric to that calendar and updating the Page and Genie guidance to explain the closure rule. The review would use the existing April 30 contract, May 1 delivery, and May closure case. The candidate should fix the denominator while preserving the approved attribution date. A proposal to move attribution from contract signing to delivery would carry different expected answers and require a business decision. [Sales-pace pilot](genie-ontology-context-workbench.md#sales-pace-is-a-useful-first-experiment)

Run a selected candidate against the current configuration in an evaluation target, using independently reviewed expectations and held-out questions. Attach the results to the candidate and check that the referenced baseline is still current before publishing an approved revision through the normal release workflow. The Lasm-inspired history would preserve the approved definition, exact assets, and evaluation evidence that explain the release.

## First experiment

Replay a few known asset changes for the sales-pace domain, including a relevant calendar update, an unrelated metadata edit, and a change that raises a genuine definition question. Compare the workbench’s candidates with what a domain owner would have flagged. See whether a reviewer can understand the evidence and start a benchmark from the proposed diff, and whether the run can finish without a proposal when the changes have no bearing on approved context. Use that replay to decide which signals warrant a daily scan and how broadly to look.

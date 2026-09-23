IMPORTANT SCOPE CORRECTION — LENDING ONLY

This task is part of the Lending Relationship Intelligence application.

Do NOT use, inspect, migrate, reference, join, or design around:

- Customer_latest.parquet
- the ~3.67 million customer population
- CCR customer-master logic
- CCR exposure populations
- CCR databases, schemas, routes, or entity models

Customer_latest.parquet belongs exclusively to the CCR workstream.

For Lending, preserve the currently established Lending portfolio/exposure
population and Lending entity/relationship sources.

The Lending relationship intelligence architecture must be based on the
Lending sources already identified in the architecture/lineage audit:

- Lending portfolio/exposure population
- CAM / V3 evidence
- governed normalized Lending relationship data
- external SEC/web research
- Stylus where explicitly invoked
- external-overlay findings
- governed AI-defined relationships
- review/governance state

Do not introduce a new customer-master dependency into Lending.

All previous findings involving Customer_latest.parquet must be treated as
CCR-only findings and ignored for this Lending task.

Continue with Prompt 3 using the results of Prompt 1 and Prompt 2 as the
authoritative Lending baseline.

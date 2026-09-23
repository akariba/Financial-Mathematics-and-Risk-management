Apply the engineering operating contract.

TASK: WRITE THE TARGET CANONICAL ARCHITECTURE

No production implementation yet.

Read:
- LENDING_FOUNDATION_AUDIT.md
- LENDING_CUSTOMER_MASTER_RECONCILIATION.md
- existing benchmark/loss-attribution reports
- current schemas

PURPOSE

Define ONE canonical intelligence architecture while retaining distinct source authorities.

The target conceptual flow must be:

PORTFOLIO / EXPOSURE SUBJECT
        ↓
CANONICAL ENTITY
        ↔
CANONICAL RELATIONSHIP
        ↔
CANONICAL / EXTERNAL ENTITY

and:

SOURCE
↓
DOCUMENT / RECORD
↓
OBSERVATION
↓
ENTITY RESOLUTION
↓
RELATIONSHIP CANDIDATE
↓
TAXONOMY RECONCILIATION
↓
EVIDENCE / QUALITY ASSESSMENT
↓
DECISION
↓
CANONICAL / REVIEW / REJECTED
↓
PUBLICATION PROJECTION

Design exact contracts for:

1. entity
2. entity identifier
3. entity alias
4. customer-master linkage
5. portfolio membership
6. exposure facts
7. source
8. document
9. observation
10. entity mention
11. evidence
12. relationship candidate
13. canonical relationship
14. relationship observation support
15. relationship taxonomy
16. taxonomy mapping/substitution
17. relationship decision
18. transition/lineage ledger
19. review state
20. external finding
21. AI relationship definition/version/instance
22. event
23. signal
24. entity-event link
25. relationship-event link
26. impact assessment

For every object specify:
- key
- stable identity
- required fields
- optional fields
- foreign keys
- lifecycle
- source authority
- immutable fields
- mutable fields
- audit fields

Define relationship identity carefully.

The same entity pair may legitimately have:
- multiple relationship types
- multiple source observations
- multiple states over time

Therefore do not deduplicate solely by endpoint pair.

Define how bidirectional relationships work.

Define how temporal states work.

Define source precedence but NEVER by destructive overwrite.

Define unified read projection semantics.

Define review semantics separately from source truth.

Create:

backend/data/LENDING_TARGET_CANONICAL_ARCHITECTURE.md

Include a migration map from all existing stores into the target concepts.

STOP.

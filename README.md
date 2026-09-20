The Lending relationship research backend is now validated end-to-end.

All acceptance tests passed.

FREEZE the working backend behavior:
- CAM baseline
- R2D2 Web/SEC integration
- caching
- reconciliation
- review workflow
- external overlay
- six-input preset contract

Do not refactor or redesign those components.

NEXT GOAL:
Build the main Lending Relationship Intelligence page for senior credit / portfolio analysis.

LENDING ONLY.

The page must make the network useful immediately, not look like a technical database screen.

FIRST VIEW

1. TOP SUMMARY
Show concise portfolio intelligence:
- Lending clients
- validated CAM relationships
- current relationships
- hidden / indirect relationships
- historical relationships
- pending external proposals
- material/high-confidence relationships
- highly connected entities

Use real existing data only.

2. PRIMARY NETWORK MAP
Make the relationship network the dominant visual.

Requirements:
- portfolio Lending clients as primary nodes
- related/non-client entities also visible
- node size based on a meaningful available metric such as connectivity, or exposure only if actual exposure data exists
- clearly distinguish Lending clients from external entities
- CAM relationships = primary/trusted edges
- approved external relationships = distinct overlay
- pending external proposals = visually distinct/dashed
- direct/indirect relationships distinguishable
- clicking any node pivots the network around that entity
- clicking an edge opens evidence and relationship details
- support end-to-end traversal through non-client entities
- never truncate the network arbitrarily

3. CREDIT INSIGHT PANEL
When a node is selected show:
- entity name / CAGID if available
- relationship count
- direct vs indirect
- relationship families
- current / emerging / historical
- material relationships
- concentration/dependency indicators
- source coverage
- CAM vs external evidence

4. RELATIONSHIP INTELLIGENCE
Surface the relationships most useful to a senior credit analyst:
- critical supplier
- customer dependency
- revenue concentration
- technology dependency
- infrastructure dependency
- guarantor
- sponsor / ownership
- lender / backleverage financing
- strategic partner
- major contracted customer
- legal/regulatory relationship

Do not create synthetic risk scores.

5. AI ECOSYSTEM / BUBBLE VIEW
Add a useful “AI Ecosystem” view using existing relationship data.

Allow analysts to isolate:
- AI / model companies
- hyperscalers
- semiconductors / hardware
- infrastructure / data centers
- investors / lenders
- enterprise customers

Use actual entity classifications available in the database.
Do not invent categories where data cannot support them.

6. WORLD MAP
Add a secondary geographic relationship view if reliable entity geography exists.

Show:
- Lending clients
- connected entities
- geographic concentrations
- selected relationship paths across locations

Do not fabricate locations.
If geographic data is missing, clearly show coverage limitations.

7. EXTERNAL INTELLIGENCE
Integrate the existing R2D2 workflow into the page:

- Research Web
- Deep Validation: Web + SEC
- cached/live indicator
- source badges
- exact excerpts
- confidence
- credit materiality
- CAM corroboration / external proposal / conflict / mention-only

Do not run research automatically.

8. MENTIONS / NEWS
Add a compact external-intelligence area for relevant relationship mentions.

Separate:
- evidence supporting an actual relationship
- mention-only/context
- emerging/new relationship evidence

Mention-only information must never appear as a confirmed network edge.

9. CITI / INTERNAL RISK DATA
Inspect the existing internal data already in the repository.

If genuine Lending exposure, OSUC, distribution-risk, facility, drawn/unfunded, or similar fields exist, add them as optional overlays/filters.

Do NOT infer or invent these fields.

Examples:
- node sizing by exposure
- OSUC filter
- distribution-risk filter
- facility/exposure detail

Only implement what the actual source data supports.

10. UX
Most important information must be visible on the first page.

Avoid a long configuration form as the main experience.

Target layout:

[ Portfolio summary KPIs ]

[             LARGE RELATIONSHIP NETWORK              ]
[ Filters / views                      Selected entity ]

[ Credit concentrations / dependencies / key links   ]

[ AI Ecosystem ] [ Geographic Map ] [ External Intel ]

[ Detailed relationship/evidence table ]

Keep drill-down available, but make the first screen immediately informative.

Do not add decorative charts with no credit purpose.

TEST
Use real existing Lending entities and relationships.

Verify:
- network uses validated database
- non-client entity pivot works
- CAM/external distinction works
- evidence drill-down works
- AI ecosystem filtering works where data exists
- geographic view uses only genuine locations
- internal risk overlays use only genuine source fields
- CAM baseline remains unchanged

Do one implementation/validation cycle only.
No loops.
No repeated redesign.

Return only:
- main Lending page PASS/FAIL
- end-to-end network PASS/FAIL
- credit insight panel PASS/FAIL
- AI ecosystem view PASS/FAIL
- geographic view PASS/FAIL
- external intelligence integration PASS/FAIL
- internal risk overlay PASS/FAIL
- CAM baseline unchanged PASS/FAIL

Then STOP.

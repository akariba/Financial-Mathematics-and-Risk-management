Continue from the restored Lending route.

SCOPE: /lending ONLY.

Do not modify:
- CCR page
- CCR routes
- CCR components
- CCR data
- Customer_latest.parquet
- frozen CAM baseline
- working R2D2 Web/SEC integration
- caching/reconciliation/review workflow

GOAL

Improve ONLY the existing Lending page into the senior-credit relationship intelligence page.

Use the existing Lending data and existing working backend.

Implement on /lending:

1. Portfolio summary KPIs
- Lending clients
- validated CAM relationships
- current relationships
- hidden/indirect relationships
- historical relationships
- pending external proposals
- high-confidence/material relationships

2. Large Lending relationship network as the main visual
- Lending clients as primary nodes
- external/non-client related entities visible
- CAM edges clearly trusted
- approved external relationships as separate overlay
- pending proposals dashed/distinct
- direct vs indirect distinguishable
- click node = pivot around that entity
- click edge = open relationship evidence

3. Selected entity panel
Show:
- name
- CAGID if available
- relationship count
- direct/indirect counts
- relationship families
- current/emerging/historical
- material dependencies/concentrations
- CAM vs external evidence

4. Credit-focused filters
Use only real available data:
- critical supplier
- customer dependency
- technology dependency
- infrastructure dependency
- revenue concentration
- guarantor
- sponsor/ownership
- lender/backleverage
- strategic partner
- contracted customer

5. External intelligence panel
Keep the working:
- Research Web
- Deep Validation Web + SEC
- cached/live status
- confidence
- materiality
- exact excerpts
- source links
- proposal/review status

6. Do not run R2D2 automatically.

7. Do not add World Map or AI Ecosystem yet.
First make the core Lending page and end-to-end network excellent and stable.

8. No redesign loops.
One implementation cycle only.

Acceptance test:
- /lending uses Lending data only
- network loads from validated CAM database
- node pivot works
- edge evidence works
- external overlay works
- R2D2 panel still works
- CAM baseline unchanged
- CCR unchanged

Return only:
- Lending page PASS/FAIL
- network PASS/FAIL
- node pivot PASS/FAIL
- evidence drilldown PASS/FAIL
- external overlay PASS/FAIL
- R2D2 preserved PASS/FAIL
- CAM unchanged PASS/FAIL
- CCR unchanged PASS/FAIL

Then STOP.

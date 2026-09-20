The Lending route is now correctly restored.

Do NOT add AI Ecosystem, world map, news bubbles, or any new visualization yet.

LENDING ONLY.

Perform one focused usability/data-consistency correction pass on the existing /lending page.

DO NOT modify:
- frozen CAM baseline
- R2D2 Web/SEC integration
- preset
- caching
- reconciliation
- review workflow
- CCR application or CCR data

FIX THESE SPECIFIC ISSUES:

1. STRICT LENDING SOURCE ISOLATION

The Lending source inventory must not display or ingest files from backend/data/ccr or any CCR-specific source.

I can currently see SQL-1 (4).csv identified as CCR data in the Lending source inventory.

Exclude CCR-folder files completely from:
- Lending source inventory
- Lending document counts
- Lending evidence search
- Lending relationship extraction

Do not delete the CCR files themselves.

2. SELECTED-ENTITY METRIC CONSISTENCY

For the selected Lending entity, reconcile all displayed metrics from the same validated CAM relationship set.

If the selected entity has 27 trusted relationships, then:
- connected-entity count
- direct/indirect counts
- relationship-family counts
- current/historical counts
- CAM evidence/source-document counts

must be internally consistent with those relationships.

Do not show 27 trusted links while displaying misleading zero relationship metrics unless zero is genuinely correct and explicitly explained.

3. FILTER BEHAVIOR

Entity selection must not accidentally leave incompatible filters active and produce an apparently empty client.

When a new entity is selected:
- preserve analyst filters only where they remain applicable;
- otherwise clearly indicate that active filters hide relationships;
- provide one-click “Show all relationships for this entity”.

Never silently make a connected entity look like it has no relationships.

4. NETWORK READABILITY

Keep the complete validated network available, but make the default selected-entity view usable.

Default:
- selected entity in center
- first-degree relationships visible
- second-degree relationships available on expansion
- no arbitrary deletion/truncation
- analyst can expand/pivot through the full network

Do not render the entire 767-edge network as an unreadable hairball by default.

5. FIRST-PAGE PRIORITY

Keep:
- summary KPIs
- search/filter
- R2D2 Assist
- network
- entity profile
- relationship/evidence table

Move the full Source Inventory into a collapsed:
“Data provenance / source inventory”
section or drawer.

The senior credit analyst should not need to scroll through dozens of source filenames during normal analysis.

6. RELATIONSHIP TABLE

For the selected entity, default the table to its validated relationships.

Clicking a network edge must:
- select the atomic relationship;
- show exact CAM provenance;
- show source document;
- show exact excerpt/location where available.

7. DO NOT REDESIGN THE WHOLE PAGE.

Make only these corrections.

TEST ONCE using CAVALRY PARENT LP and one other well-connected Lending client.

Return only:

- CCR source isolation PASS/FAIL
- selected-entity metric consistency PASS/FAIL
- filter behavior PASS/FAIL
- network readability PASS/FAIL
- relationship table PASS/FAIL
- provenance drilldown PASS/FAIL
- CAM baseline unchanged PASS/FAIL
- R2D2 preserved PASS/FAIL
- CCR application unchanged PASS/FAIL

Then STOP.

No loops.
No additional features.

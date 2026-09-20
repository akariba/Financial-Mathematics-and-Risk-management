The previous validation result is incorrect.

Visual evidence shows that:

http://127.0.0.1:5173/lending

is still rendering the CCR Correlations page.

This is a FAIL.

Fix route/component separation only.

Requirements:

1. /lending must render the Lending relationship application.
2. /lending must NOT render:
   - CCR CORRELATIONS
   - CCR CLIENTS ONLY
   - CCR client lookup
   - GFCID search
   - Customer_latest.parquet
   - CCR snapshot statistics
   - any CCR-specific component or data source

3. Inspect:
   - App.tsx
   - routing logic
   - Layout.tsx
   - Lending page/component imports
   - CCR page/component imports

4. Restore the existing Lending RelationshipDatabase / Lending relationship page to /lending.

5. Preserve all existing Lending backend functionality:
   - CAM database
   - 767 validated relationships
   - R2D2 Web + SEC
   - caching
   - reconciliation
   - review workflow
   - external overlay

6. Do not modify the CCR page.
7. Do not modify CCR data.
8. Do not modify the frozen CAM baseline.
9. Do not redesign anything.
10. Do not report PASS based only on code inspection.

VALIDATION MUST INCLUDE ACTUAL HTTP/UI CHECK:

Open:
http://127.0.0.1:5173/lending

Confirm visible page contains Lending terminology and does NOT contain:
"CCR CORRELATIONS"
"CCR CLIENTS ONLY"
"Customer_latest.parquet"

Then open the CCR route separately and confirm CCR still works.

Return only:

- /lending renders Lending UI PASS/FAIL
- no CCR content on /lending PASS/FAIL
- Lending data source PASS/FAIL
- Lending backend preserved PASS/FAIL
- CCR route unchanged PASS/FAIL
- CAM baseline unchanged PASS/FAIL

If any check fails, report FAIL.

Then STOP.

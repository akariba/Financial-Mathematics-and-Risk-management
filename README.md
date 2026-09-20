STOP the current implementation direction.

You mixed the Lending product work with the CCR page.

Correct this now.

SCOPE
LENDING ONLY.

Do not redesign, modify, delete, or reuse the CCR page.

The CCR page, CCR routes, CCR data, and CCR UI must remain completely separate and unchanged.

TASK

1. Inspect only the files changed in the immediately previous run.

2. Identify any change that caused:
   - Lending routes to render CCR UI;
   - CCR components to be reused in Lending;
   - CCR labels/data/routes to appear in the Lending workflow;
   - Lending navigation to redirect to CCR.

3. Revert only those incorrect changes.

4. Restore the existing Lending page as the working base.

5. The Lending route must remain:
   /lending

6. The Lending page must use only:
   - Lending/CAM relationship database
   - Lending external research layer
   - Lending R2D2 Web/SEC workflow
   - Lending review workflow

7. Do NOT use:
   - CCR data
   - Customer_latest.parquet for Lending
   - CCR client search
   - CCR GFCID population
   - CCR components
   - CCR relationship logic
   - CCR page design

8. Preserve the already-working Lending backend:
   - CAM baseline
   - 767 validated relationships
   - external research integration
   - Web + SEC
   - caching
   - reconciliation
   - review workflow
   - graph overlay
   - six-input preset contract

9. Do not rebuild the Lending solution from scratch.

10. Do not start the new visualization work yet.

FIRST restore clean separation only.

Acceptance test:

- /lending opens the Lending relationship page
- Lending page contains no CCR labels or CCR data
- CCR page remains available separately and unchanged
- Lending CAM database remains unchanged
- Lending R2D2 integration remains functional
- no cross-lane imports or data dependencies were introduced

Return only:

- Lending route restored PASS/FAIL
- CCR unchanged PASS/FAIL
- Lending data isolation PASS/FAIL
- Lending backend preserved PASS/FAIL
- CAM baseline unchanged PASS/FAIL

Then STOP.

No loops.
No redesign.
No additional implementation after the separation is fixed.

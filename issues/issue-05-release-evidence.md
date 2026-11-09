# Issue #5 — Release evidence and test result discrepancy

**Upstream:** https://github.com/Gayatri-Education/Gayatri-Demo/issues/5  
**Evidence type:** Test-result discrepancy described in upstream issue

## Reported mismatch

The issue says `RELEASE_EVIDENCE_v4.0.0.md` reports 34 tests passed and a passing decoupled-import check, while running the referenced import test reportedly failed because `central_platform.models` could not be imported.

## Why this matters

Release evidence must describe the exact source revision and environment that were tested. A stale or non-reproducible passing count can mislead reviewers.

## Recommended correction

1. Run tests from a clean checkout at a recorded commit SHA.
2. Capture the exact command, Python version, dependency versions, output, and exit code.
3. Separate test collection failures from test assertion failures.
4. Generate the release evidence from CI results rather than manually retaining old counts.
5. Keep the release blocked if mandatory import/startup checks fail.

## Verification required

Re-run the full test suite and the focused import test against the same commit referenced by the release evidence. No passing test count is claimed by this report.

## Upstream status

Returned as **closed** when checked on 2026-11-09. Closure alone does not validate the reported test discrepancy.

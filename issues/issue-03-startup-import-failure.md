# Issue #3 — Startup import failure: missing internal schema package

**Upstream:** https://github.com/Gayatri-Education/Gayatri-Demo/issues/3  
**Evidence type:** Startup failure described in upstream issue

## Reported environment

- Windows
- Python 3.13.14
- v4.0.0 source ZIP
- Dependencies installed from `requirements.txt`

## Reported reproduction

The startup command `python -m app.main` reportedly failed with a `ModuleNotFoundError` for `central_platform.models`. The issue also notes imports from `central_platform.models.schema` while the downloaded source did not contain the expected `central_platform/models` package.

## Recommended correction

1. Inspect repository history and all imports that reference `central_platform.models.schema`.
2. Restore the intended internal schema package or migrate all imports to one deliberate canonical location.
3. Preserve the actual data contract used by courses, learning state, retrieval, and tutor orchestration.
4. Add import/serialization smoke tests and a clean-checkout startup test.
5. Verify packaging includes the restored modules.

Do not try to solve a missing internal application module by installing an unrelated third-party package.

## Verification required

Run the startup command and full test collection from a clean checkout and fresh virtual environment. Record Python version, dependency installation output, and exact exit codes. No source-code fix is included here.

## Upstream status

Returned as **closed** when checked on 2026-11-09. Re-check the current default branch before treating this as resolved.

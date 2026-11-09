# Issue #4 — v4.0.0 release artifacts missing

**Upstream:** https://github.com/Gayatri-Education/Gayatri-Demo/issues/4  
**Evidence type:** Release/documentation mismatch described in upstream issue

## Reported mismatch

The issue reports that project documentation lists v4.0.0 Portable ZIP and Setup EXE assets, while the GitHub Releases page available during the review showed v3.0.1 assets rather than the documented v4.0.0 packages.

## Impact

Testers may be unable to obtain the exact packaged build referenced by the documentation, making release validation and reproducibility difficult.

## Recommended correction

1. Confirm which version is approved for release.
2. Publish the exact v4.0.0 assets to the official GitHub Release if that release is authorized.
3. Ensure filenames, release notes, package manifest, and download links all refer to the same version.
4. Verify the downloaded assets on a clean Windows environment.
5. If v4.0.0 is not ready, update documentation so it does not imply that unavailable packages can be downloaded.

## Verification required

Check the official Releases page and download the published artifacts. Record filenames, file sizes, version metadata, and test results. No release asset is included or claimed here.

## Upstream status

Returned as **closed** when checked on 2026-11-09. Confirm current Releases state independently.

# Issue #10 — Conflicting SHA-256 checksums

**Upstream:** https://github.com/Gayatri-Education/Gayatri-Demo/issues/10  
**Evidence type:** Conflicting values in tracked documentation

## Reported values

The upstream issue records two different SHA-256 values for the documented v4.0.0 portable ZIP:

- `SHA256SUMS.txt`: `2563E931B5D165F4F892A93475EEC1D53B83A85521C67E1526EDA474EE59F710`
- `RELEASE_EVIDENCE_v4.0.0.md`: `4904166843DEA97754C5E67A96A2D1D220DB0B82F0F8D2DA6957BC86AFDB1C42`

The original report states that the actual portable ZIP was unavailable, so neither value was independently validated against the artifact during that review.

## Recommended correction

1. Obtain the exact final release ZIP from the official release source.
2. Calculate SHA-256 directly from those bytes using a trusted local tool.
3. Update the checksum manifest and release evidence from the same verified build artifact.
4. Verify the downloaded file against the published manifest.
5. Keep the release checksum claim unresolved until the actual asset is available.

## Verification required

Record the artifact filename, file size, calculated digest, and source URL. Do not choose one of the conflicting values by assumption.

## Upstream status

Returned as **closed** when checked on 2026-11-09. This report does not claim an independently verified checksum.

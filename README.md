# Gayatri AI — QA Findings & Verification Notes

This repository records QA observations made while reviewing the public **Gayatri Demo v4.0.0** project.

- Upstream project: https://github.com/Gayatri-Education/Gayatri-Demo
- Review target: v4.0.0 source repository and its tracked release documentation
- Prepared by: Nishant Makwane
- Purpose: keep issue observations, reproduction context, and verification limits in one place.

## Important scope

This is an independent QA-notes repository, not the upstream product source code. It does **not** claim that upstream defects have been fixed. The upstream issues linked below were observed as **closed** when checked on 2026-11-09; closing an issue alone does not prove that a fix is present or verified.

## Findings

| Upstream issue | Topic | Evidence classification | Note |
|---|---|---|---|
| [#2](https://github.com/Gayatri-Education/Gayatri-Demo/issues/2) | Mastery score can increase for ungraded/irrelevant input | Reproduction described in issue | Requires end-to-end event/evaluation verification |
| [#3](https://github.com/Gayatri-Education/Gayatri-Demo/issues/3) | App startup fails on missing internal schema package | Reported startup reproduction | Verify current default branch and clean install |
| [#4](https://github.com/Gayatri-Education/Gayatri-Demo/issues/4) | v4.0.0 release assets missing from Releases | Release/documentation mismatch | Confirm current release assets |
| [#5](https://github.com/Gayatri-Education/Gayatri-Demo/issues/5) | Release evidence reports tests passing while import test fails | Reproduction described in issue | Regenerate evidence from clean CI |
| [#9](https://github.com/Gayatri-Education/Gayatri-Demo/issues/9) | Potential unsafe HTML rendering | Static code-review concern | Runtime exploit was not confirmed |
| [#10](https://github.com/Gayatri-Education/Gayatri-Demo/issues/10) | Conflicting SHA-256 values for portable ZIP | Values differ in tracked docs | ZIP was unavailable for independent hashing |

Detailed reports are in [issues/](issues/).

## Verification status

No upstream source-code patch is included in this repository at this stage. Proposed corrective actions and the evidence needed to verify them are documented per finding. Do not represent recommendations as completed fixes.

## Suggested verification workflow

1. Fetch the latest upstream default branch and issue states.
2. Reproduce each finding in a clean, supported environment.
3. Record exact commands, environment versions, output, and exit codes.
4. Implement fixes in an authorized upstream branch or pull request.
5. Add regression tests and rerun the relevant suite.
6. Verify release assets and hashes against the exact published binaries.

## Attribution

All product names, issue numbers, and linked source material refer to the upstream Gayatri Demo project. This repository contains QA summaries and recommendations, not copied upstream implementation code.

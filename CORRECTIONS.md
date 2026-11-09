# Proposed Corrections for Gayatri Demo QA Issues

**Target project:** https://github.com/Gayatri-Education/Gayatri-Demo  
**Prepared for:** https://github.com/nishantmak04/Gayatri-AI-Bug-Fixes

> **Status:** These are proposed technical corrections and acceptance checks. This commit does not claim that upstream source code has been modified, fixes have been merged, or tests have passed. Release-only issues require the actual release artifacts and maintainer access.

## Issue #2 — Mastery increases for arbitrary input

### Correction
1. Trace the complete event path from the UI/bridge through the tutor orchestrator and evaluator into the learning-state manager and database.
2. Distinguish graded from ungraded events explicitly.
3. Set correctness to null for greetings, irrelevant text, ordinary questions, and turns without reliable answer evaluation.
4. Update mastery only for evaluator-confirmed outcomes. Never infer correctness merely because a known misconception was not detected.
5. Attach real course, module, and topic identifiers to evaluated events. Preserve unknown identifiers as null.
6. Make event processing idempotent: replaying the same event ID must not apply mastery twice. Persist the event and aggregate update transactionally.
7. Derive topic mastery and weak-topic lists from persisted evaluated events. Show an honest “not enough evaluated answers yet” state when data is insufficient.

### Regression checks
- Junk input and ungraded questions leave mastery unchanged.
- An evaluated wrong answer does not increase mastery.
- An evaluated correct answer updates only the intended topic and course.
- Replaying an event ID twice changes mastery only once.
- Mastery remains bounded and survives restart.

**Done only when:** the end-to-end event path and persistence are tested, not merely an isolated state-manager method.

## Issue #3 — Startup fails because central_platform.models.schema is missing

### Correction
1. Search all imports, constructors, attribute accesses, serialized data, tests, and packaging configuration for expected schema types.
2. Restore the canonical internal package central_platform/models/ with __init__.py and schema.py, unless repository history establishes another intended location.
3. Define compatible schemas for types actually used by the application, including Course, Module, RAGChunk, MasteryState, TutorResponse, LearningEvent, and PedagogicalAction where referenced.
4. Match real constructor fields, optional values, enum values, serialization formats, and persisted SQLite/JSON records. Do not guess fields from names alone.
5. Use safe per-instance defaults for mutable fields; validate documented ranges and identifiers.
6. Add migration/default handling for older persisted records if schemas change.
7. Update packaging hidden imports/data only if required by the restored package layout.

### Regression checks
- Import every public schema and affected services/orchestrator.
- Construct, serialize, and deserialize representative valid objects.
- Reject malformed records with useful validation errors.
- Run full test collection from a clean environment; require zero collection errors.
- Run the documented startup preflight.

**Done only when:** a clean checkout imports and starts successfully and all relevant tests collect.

## Issue #4 — v4.0.0 release artifacts are missing

### Correction
1. Decide which deliverables are supported: portable ZIP, installer, or both.
2. Build from a clean, identified commit after code and test blockers are resolved.
3. Verify each deliverable exists, is non-empty, can be listed/extracted or installed, and launches in a clean supported Windows environment.
4. Publish the exact tested files to the GitHub Release with accurate filenames.
5. Verify the release page after upload and ensure README, setup guide, release notes, and package manifest link to the same release and filenames.
6. If an installer cannot be built, either fix the build pipeline or explicitly publish a ZIP-only release and correct all documentation.

### Acceptance checks
- The v4.0.0 release page contains every advertised artifact.
- Downloaded artifacts pass extraction/install and launch smoke tests.
- The tested commit and artifact names are recorded in release evidence.

**Maintainer action required:** publishing official binaries requires access to the upstream repository and its release process.

## Issue #5 — Release evidence reports passing tests despite import failures

### Correction
1. Fix the underlying import/startup blocker first; do not edit test expectations to make the report green.
2. Run the complete test suite from a fresh environment on the exact candidate commit.
3. Capture the real command, environment, commit SHA, test count, failures, and exit code in CI.
4. Generate release evidence from that CI run. Link the workflow run and retain test logs as artifacts.
5. Regenerate evidence whenever the tested source commit changes. Never carry forward an old passing count.

### Regression checks
- CI fails on collection errors and non-zero test exits.
- The evidence commit SHA equals the release candidate SHA.
- Reported pass/fail counts match raw CI output.

**Done only when:** a reviewer can open the linked run and reproduce the stated result.

## Issue #9 — Potential HTML injection in tutor responses and rendered content

### Correction
1. Inventory all dynamic HTML sinks, including innerHTML, outerHTML, insertAdjacentHTML, document.write, and HTML template interpolation.
2. For plain text, build DOM nodes and assign untrusted values with textContent.
3. If Markdown is required, parse it with a maintained, pinned parser and sanitize generated HTML with a maintained sanitizer immediately before insertion. For offline operation, bundle vetted dependencies locally.
4. Build evidence cards field-by-field; do not concatenate untrusted titles, document snippets, filenames, or model responses into HTML or attributes.
5. Treat model output, imported documents, user messages, RAG content, and filenames as untrusted even if they passed through a text cleaner.
6. Review URL protocols and navigation policy. Add a compatible Content Security Policy as defense in depth, not as a replacement for safe rendering.

### Regression checks
- Test script tags, event-handler attributes, SVG payloads, quote/attribute breakouts, javascript: URLs, malformed Markdown links, and ordinary safe Markdown.
- Verify hostile content is inert text or removed according to the documented rendering policy.
- Run tests in the actual Qt WebEngine/browser rendering environment, not only parser unit tests.

**Evidence qualification:** the reported finding is a static rendering risk; a runtime exploit was not confirmed in the original QA report.

## Issue #10 — Conflicting SHA-256 checksums

### Correction
1. Do not choose either published hash by guesswork.
2. Obtain the exact final release ZIP (and installer, if applicable) produced by the release build.
3. Compute SHA-256 directly from those final bytes using a reproducible release step.
4. Generate SHA256SUMS.txt, release evidence, and package metadata from one build manifest rather than maintaining hashes manually.
5. After upload, download the published asset again and independently hash it. Compare that value with the manifest.
6. If v4.0.0 has already been distributed with incorrect metadata, publish a clearly versioned corrected release rather than silently replacing bytes under an existing release identity.

### Acceptance checks
- The actual published file is available and independently hashable.
- The downloaded file's SHA-256 equals the manifest value.
- Every document refers to the same filename, version, and verified digest.

**Maintainer action required:** no authoritative checksum can be selected until the actual release ZIP is available. Documentation alone cannot verify binary integrity.

## Recommended implementation order

1. Reproduce baseline failures on the current upstream commit.
2. Restore schemas and unblock imports/startup (#3).
3. Correct event evaluation and mastery persistence (#2).
4. Secure dynamic rendering and add browser-engine regression tests (#9).
5. Re-run the full suite and regenerate evidence (#5).
6. Build and publish release assets, then verify hashes (#4 and #10).

## Verification record

| Item | Status |
|---|---|
| Issue findings | Documented in individual issue files |
| Proposed corrections | Documented above |
| Upstream source modifications | Not performed by this repository commit |
| Upstream tests | Not run / not claimed |
| Release binaries and checksums | Not independently verified |
| Upstream merge or release | Not claimed |

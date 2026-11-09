# Issue #9 — Potential unsafe HTML rendering

**Upstream:** https://github.com/Gayatri-Education/Gayatri-Demo/issues/9  
**Evidence type:** Static code-review concern  
**Runtime exploit:** Not confirmed in the reported review

## Reported observation

The upstream issue identifies UI rendering paths in `app/ui/index.html` that interpolate chat, tutor-card, or document-derived content into `innerHTML`. It also notes that HTML-like input may survive document cleaning.

This is a potential HTML injection / XSS risk. It must not be described as a confirmed exploitable vulnerability without controlled runtime verification.

## Recommended correction

1. Treat user messages, uploaded document text, filenames, retrieved content, and model output as untrusted.
2. Render plain text using safe DOM text APIs by default.
3. If rich HTML is genuinely required, use a maintained sanitizer with a strict allowlist and sanitize at the final rendering boundary.
4. Avoid building HTML strings with untrusted interpolation.
5. Add regression tests for harmless markup-like strings and verify they display as text rather than creating elements.

## Verification required

In an authorized test environment, trace each untrusted source to its final rendering sink. Verify the safe rendering behavior with harmless test strings and automated tests. Do not use real payloads against production users.

## Upstream status

Returned as **closed** when checked on 2026-11-09. Runtime exploitation was not confirmed in the original report.

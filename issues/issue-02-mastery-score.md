# Issue #2 — Mastery score increases for arbitrary input

**Upstream:** https://github.com/Gayatri-Education/Gayatri-Demo/issues/2  
**Priority reported upstream:** High  
**Evidence type:** Reproduction described in upstream issue

## Expected behavior

Mastery should reflect demonstrated understanding. Ungraded conversation, irrelevant text, and incorrect answers should not increase mastery.

## Reported observation

The upstream issue describes the following behavior:

- Five unrelated/junk prompts increased mastery from 0.45 to 0.70.
- A reported wrong answer triggered an evaluate action and increased mastery by 0.05 without a correctness decision.
- Repeating a question reportedly increased mastery to 1.00.
- Topic mastery remained unchanged and weak-topic tracking did not update as expected.

These are observations from the upstream issue report; they are not independently re-run in this repository.

## Recommended correction

1. Treat clarification, greetings, free-form conversation, and ungraded turns as `correctness = null`.
2. Update mastery only after an explicit evaluation outcome.
3. Carry canonical course/module/topic identifiers through the full tutor-to-learning-state event path.
4. Derive weak topics from evaluated evidence and documented thresholds.
5. Add end-to-end regression tests for irrelevant input, correct answers, incorrect answers, repeated questions, and topic-level analytics.

## Verification required

Trace the complete event path from tutor response generation through event persistence and analytics. Confirm ungraded events do not alter mastery and that evaluated outcomes update the correct module/topic. No fix is claimed here.

## Upstream status

The issue was returned as **closed** when checked on 2026-11-09. Closure is not proof that the current code passes the regression tests.

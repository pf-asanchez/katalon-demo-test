# Katalon Demo Test - Guided Learning Lab

This project is intentionally designed to fail in multiple ways so learners can practice debugging, object repository hygiene, and reliable test design in Katalon.

## Purpose

Use this repo to learn how to:
- Diagnose failing UI tests systematically
- Improve locator quality
- Apply consistent object naming standards
- Add synchronization (`waitForElement...`) before actions/assertions
- Keep tests readable and maintainable

## What Is Intentionally Broken

The `Demo` test case includes multiple intentional issues.

Known issue categories:
1. Assertion text mismatch
2. Assertion targets an element that is not present in the current page state
3. Missing/incorrect object for the expected UI state
4. Object path/name mismatch (`Home_lbl_Header` does not exist as referenced)

Important:
- These are challenge prompts, not direct fixes.
- Avoid copy/paste fixes; investigate each failure in logs and UI first.

## Learning Objectives

By the end, the learner should be able to:
- Trace a failure from execution log -> screenshot -> DOM -> Test Object
- Distinguish between:
  - wrong expected value
  - wrong page state
  - wrong object mapping
  - wrong object path/reference
- Create resilient selectors (not brittle positional selectors)
- Standardize object naming (`btn_`, `lbl_`, `txt_`, `inp_`, etc.)
- Add explicit waits where timing can cause flakiness

## Suggested Debug Workflow

Use this order for every failure:

1. Re-run only the failing test case.
2. Open the failure step in Katalon logs and note:
   - Keyword used
   - Object path
   - Expected vs actual output
3. Validate current browser state at failure time.
4. Open the related Test Object and inspect selector quality.
5. Confirm the test data drives the expected page state.
6. Add waits before interacting/verifying dynamic elements.
7. Re-run and verify only one variable changed at a time.

## Hints (Without Revealing Answers)

Use these hints only when blocked.

### Hint Set A: Assertion
- Confirm that the credentials used in the test should lead to the same UI state your assertion expects.
- If state and assertion conflict, fix the logic first, not the selector.

### Hint Set B: Object Existence
- Compare object references in script with folder/object structure in Object Repository.
- Katalon object paths are folder-based; small path format differences break lookups.

### Hint Set C: Locator Quality
- Current selectors rely on positional structure/class combinations that may match multiple elements.
- Prefer unique attributes (stable `id`, `name`, meaningful text anchors, or constrained parent context).

### Hint Set D: Synchronization
- Add `waitForElementVisible` (or suitable wait) before `click`, `setText`, and `verify...` on dynamic content.
- Keep timeout values intentional and consistent across the project.

## Locator Guidelines

Good locator traits:
- Unique on page
- Readable
- Stable across minor layout changes
- Tied to semantic attributes instead of visual position

Avoid:
- `nth-of-type` and index-based XPath unless no better option exists
- Overly broad CSS such as shared button classes without context
- Deep absolute DOM paths

## Naming Standards (Recommended)

Use clear prefix + feature + intent:
- `btn_Login`
- `input_Email`
- `input_Password`
- `lbl_LoggedInUser`
- `lnk_Logout`

General rules:
- Prefix by control type (`btn`, `input`, `lbl`, `lnk`, `dd`, etc.)
- Use PascalCase after prefix
- Keep names behavior-focused, not style-focused
- Keep folder structure aligned with page/module (`Login/`, `Home/`, etc.)

## Synchronization Standards

Recommended practices:
- Wait before action:
  - `waitForElementVisible`
  - `waitForElementClickable` (for click targets)
- Wait before verification when UI updates asynchronously
- Use fail-fast timeout defaults; increase only where justified

## Extra Improvements Learners Can Implement

- Replace hardcoded credentials with test data profiles/data files
- Split flow into reusable custom keywords (`login`, `assertLoggedInState`, etc.)
- Add negative and positive login scenarios
- Add teardown/cleanup patterns as needed
- Add comments only where intent is not obvious

## Challenge Checklist

Mark complete when each item is solved:
- [ ] Test runs without object path lookup errors
- [ ] Assertion checks the correct UI state for the chosen test data
- [ ] Missing/incorrect page object(s) are corrected
- [ ] Locators are upgraded to stable selectors
- [ ] Naming convention is consistent across objects
- [ ] Waits are added where needed to reduce flakiness
- [ ] Test remains readable after improvements

## Definition of Done (For This Lab)

You are done when:
- The scenario behavior is logically correct
- Objects are discoverable and consistently named
- Assertions validate the right thing at the right time
- The test is stable across repeated runs
- A new learner can understand the flow quickly

## Notes for Instructors/Reviewers

To keep this repo as a learning tool:
- Prefer code review comments that ask guiding questions
- Avoid posting direct selector or assertion answers in shared notes
- Focus feedback on debugging process and reasoning, not only final pass/fail

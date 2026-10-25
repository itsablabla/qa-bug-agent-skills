---
name: fix-reproduce
description: Reproduce each bug on the exact base build before changing code by running the tester's regression test and confirming it fails for the reported reason; reject tests that pass on the buggy build. Use before every fix.
---
# Reproduce First

## Procedure
1. Check out the base commit matching the bug record's fingerprint.
2. Start the app the way the target runs it, including production config values.
3. Run the tester's regression test (loaded from the tester's branch, never your own copy). It must FAIL, and the failure detail must match the reported actual result.
4. If it PASSES on the base, stop and file TEST-DEFECT ("test passes on buggy build"). A test that can't fail can't prove a fix.
5. If it fails for another reason (setup, timeout), fix the environment, not the test.
6. Still can't reproduce after 3 attempts with logs: mark CANNOT REPRODUCE with evidence, and ask the tester for the exact environment.
7. Reproduce a second way (plain curl, a real browser) before trusting a failure. In our lab, a test-tool stall produced a fake failure once.

## Exit criteria
Saved failing output for the reported reason, or a TEST-DEFECT / CANNOT REPRODUCE record.

Counterpart of tester skill: `qa-regression-tests`.

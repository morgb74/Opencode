You are in OpenCode Plan mode. Perform a review-only investigation of one Python file in my CVEAlerts test directory.

Project root:
- Current working directory should be ~/devops/CVEAlerts

Review directory:
- test/

Target filename:
- eva_cve_gui_0_5_9.py

Resolve the target as:
- test/eva_cve_gui_0_5_9.py

Important path rules:
- Do not use /devops/CVEAlerts.
- Use paths relative to the current project root.
- First confirm the file exists with a safe path check.
- If the file is not found, stop and report:
  - current working directory
  - whether test/ exists
  - nearest matching files under test/

OpenCode protocol requirements:
- Follow all active OpenCode project/global instructions, including AGENTS.md, opencode.json instructions, and applicable rules.
- Stay in Plan mode.
- Use read, grep, glob, and safe navigation tools before making conclusions.
- Respect permissions.
- Ask before running expensive, destructive, network-dependent, or outside-project commands.
- Do not use --dangerously-skip-permissions.
- Do not read secrets, credentials, private tokens, .env files, or unrelated system files.
- Do not edit, write, patch, delete, rename, move, or format files.
- If project rules conflict with this request, call out the conflict clearly and proceed with the safest review-only interpretation.

Scope:
- Focus first and deepest on the target file in test/.
- Review other files under test/ only when needed to understand imports, shared logic, older-version regressions, config/data dependencies, or runtime behavior.
- Do not review unrelated project areas unless the target file directly depends on them.

Review goal:
Produce a detailed code review focused on:
1. Logic bugs
2. Stability and reliability issues
3. Error handling gaps
4. Data validation problems
5. Edge cases and boundary conditions
6. Performance bottlenecks
7. Resource usage issues
8. Concurrency, timing, retry, timeout, and rate-limit risks
9. File I/O, path handling, encoding, and permissions problems
10. API/network failure handling
11. GUI/event-loop/threading issues
12. Security-relevant issues visible from the code
13. Maintainability, duplication, dead code, confusing structure, and testability
14. Python-specific problems such as mutable defaults, broad exceptions, implicit globals, import side effects, datetime/timezone mistakes, subprocess misuse, unsafe shell usage, and fragile parsing

Investigation process:
1. Confirm the target file exists under test/.
2. Map nearby files in test/.
3. Identify imports, entry points, GUI startup paths, scheduled/background tasks, config usage, network/API calls, file I/O, cache/state files, and output/alerting flows.
4. Build a concise mental model of what the target file does.
5. Review the target file in execution-flow order.
6. Trace important flows end to end:
   - CVE ingestion/fetching
   - parsing and normalization
   - filtering and deduplication
   - severity/scoring logic
   - alert generation
   - GUI display/update behavior
   - persistence/cache/state handling
   - error/retry behavior
7. Look for bugs that could cause missed alerts, duplicate alerts, false positives, false negatives, stale data, bad timestamps, incorrect severity handling, crashes, GUI freezes, silent failures, or corrupted state.
8. Check whether tests exist and whether they cover risky paths.
9. Do not implement anything yet. Create an implementation plan only.

Output format:

## Executive summary
- Overall risk level: Low / Medium / High
- The most important findings in priority order
- Whether the code appears safe to deploy/run as-is, and why

## Repository map
- Main target file
- Related files consulted
- Main entry points
- Important dependencies or external services
- Any files intentionally skipped and why

## System behavior summary
- What the application appears to do
- Main data flows
- Main state/cache/config flows
- Main GUI/runtime flows

## Findings
For each finding, include:
- ID, such as F-001
- Severity: Critical / High / Medium / Low
- Category: logic, stability, performance, security, maintainability, testing, GUI, or operations
- File and function/class/module
- What is wrong
- Why it matters
- Evidence from the code
- Likely impact
- Recommended fix
- Suggested test coverage

## Logic bug review
Summarize possible incorrect behavior in alert matching, deduplication, scoring, date handling, filtering, state management, GUI state, and output generation.

## Stability review
Summarize crash risks, unhandled exceptions, retry/timeout gaps, fragile assumptions, bad defaults, GUI freezes, thread/event-loop risks, and operational failure modes.

## Performance review
Summarize inefficient loops, repeated network/file operations, excessive parsing, unnecessary memory growth, slow startup, GUI responsiveness problems, and scalability risks.

## Security and safety review
Summarize unsafe subprocess/shell usage, path traversal risks, secret handling, unsafe deserialization/parsing, dependency risks visible from files, and network/API safety issues.

## Test review
- Existing tests found
- Missing tests
- High-value tests to add first
- Regression tests needed for the highest-risk findings

## Further implementation plan
Create a staged plan:
- Phase 1: Critical correctness/stability fixes
- Phase 2: Test coverage and regression tests
- Phase 3: Performance and responsiveness improvements
- Phase 4: Maintainability/refactoring
- Phase 5: Operational hardening

For each phase, include:
- Tasks
- Files likely affected
- Risk level
- Verification steps
- Rollback considerations

## Open questions
List anything that needs human confirmation before implementation.

## First 10 actions checklist
End with a concise checklist of the first 10 implementation actions I should take next.

Important:
- Be specific and evidence-based.
- Prefer concrete examples from the code.
- Include file/function references wherever possible.
- Do not make changes.
- Do not produce a patch yet.
- Do not claim tests were run unless they were actually run and the command/output summary is shown.

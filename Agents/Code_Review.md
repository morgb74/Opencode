You are in OpenCode Build mode, but this is a review-only task for source code.

Goal:
Review the target Python file and write the final Markdown report directly to:

test/Opencode_Review.md

Project root:
- Current working directory should be ~/devops/CVEAlerts

Review directory:
- test/

Target filename:
- eva_cve_gui_0_5_9.py

Target file:
- test/eva_cve_gui_0_5_9.py

Strict write permissions for this task:
- You may create or overwrite only this file:
  - test/Opencode_Review.md
- Do not modify, patch, format, rename, delete, or move any other file.
- Do not modify test/eva_cve_gui_0_5_9.py.
- Do not use touch.
- Do not create an empty report placeholder.
- Do not say the report is saved unless test/Opencode_Review.md has non-zero byte count and all required sections are present.

Review requirements:
Perform a detailed code review focused on:
- logic bugs
- stability and reliability issues
- error handling gaps
- edge cases
- performance problems
- GUI/event-loop/threading risks
- file I/O and path issues
- API/network failure handling
- security-relevant issues visible from the code
- maintainability and testability problems
- Python-specific problems

Required report sections:
# OpenCode Review

## Executive summary
## Repository map
## System behavior summary
## Findings
## Logic bug review
## Stability review
## Performance review
## Security and safety review
## Test review
## Further implementation plan
## Open questions
## First 10 actions checklist

Finding format:
For each finding include:
- ID
- Severity
- Category
- File/function/class
- What is wrong
- Why it matters
- Evidence from the code
- Likely impact
- Recommended fix
- Suggested test coverage

Save procedure:
1. Confirm:
   - pwd
   - ls -ld test
   - ls -l test/eva_cve_gui_0_5_9.py

2. Review the code.

3. Write the complete Markdown report directly to:
   - test/Opencode_Review.md

4. Use the OpenCode write tool if possible.
   If the report is too large for one write, use bash here-doc chunks:
   - first chunk uses cat > test/Opencode_Review.md
   - later chunks use cat >> test/Opencode_Review.md
   - every chunk must contain real report content
   - no placeholder text

5. Verify:
   - wc -c test/Opencode_Review.md
   - wc -l test/Opencode_Review.md
   - grep -n '^## ' test/Opencode_Review.md
   - head -20 test/Opencode_Review.md
   - tail -20 test/Opencode_Review.md

Failure rule:
If writing fails, stop. Do not regenerate a different report. Do not retry in a loop.

Final response:
Only report:
- final path
- byte count
- line count
- whether required sections are present
- any write problem encountered

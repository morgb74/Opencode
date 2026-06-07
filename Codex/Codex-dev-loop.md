# CVEAlerts Development and Testing Loop

## Repository and Branch Rules
**Main repository:** `https://github.com/morgb74/CVEAlerts`
**Repository name:** morgb74/CVEAlerts
- Always verify GitHub repository access before starting any work.
- Confirm the working tree and current branch are clean before changing files.
**Original GUI branch:** `feature/browser-gui`
**Current notifications branch:** `feature/email-notifications`
**Planned next branch:** `feature/csv-import-enrichment`
- Always work from the branch requested by the user.
- Push every completed test version to its active GitHub branch so it appears under `test\.`
## Important Paths
**Production GUI:**

- `src\cvealerts\eva_cve_gui.py`
**Production notification module:**

- `src\cvealerts\eva_cve_notifications.py`
**Supporting tracking module:**

- `src\cvealerts\eva_cve_tracking.py`
**PDF engine:**

- `src\cvealerts\eva_cve_pdf.py`
**Test directory:**

- test\
**GUI test naming:**

- `test\eva_cve_gui_`<version>.py
**Example:**

- `test\eva_cve_gui_0_5_9.py`
**Notification test naming:**

- `test\eva_cve_notifications_`<version>.py
## Safety Rules
- Never modify production src\ files unless the user explicitly requests promotion.
- Never modify `src\cvealerts\eva_cve_pdf.py` unless explicitly requested.
- Never overwrite or remove unrelated user changes.
- Do not refactor, restyle, rename, or alter unrelated behavior.
- Each version must contain only the requested planner items.
**Follow the instruction:**
- Following the usual controls of not changing, modifying, or removing any other logic apart from this change.

## Planner Process
- New ideas, bugs, cosmetic changes, and fixes are added to the planner for the next version.
- Maintain a precise list of all planned items.
- Do not implement planner items until the user says `PROCEED`.
**Before making changes:**
- Read back the exact scope.
- Confirm what will and will not change.
- State the planned version number.
- Wait for the explicit `PROCEED`.
- Once the user says `PROCEED`, implement every agreed planner item and nothing else.
- If additional issues are discovered during testing, add them to the next planner unless they block the current version.
- Do not silently include “helpful” unrelated improvements.
## Versioning Loop
**The first GUI test version starts from:**
- `src\cvealerts\eva_cve_gui.py`
- Every later version starts from the latest successful test version in `test\.`
- Copy the entire previous working file into a new versioned filename.
**Never deliver:**
- Patch-only files
- Small wrappers
- Placeholder files
- Partial implementations
- Always deliver complete, directly runnable Python code.
**Update:**
- File version header
- `GUI_VERSION`
- Commented change log
- Any module version constants
- Preserve all previous version comments and append the newest change at the top.
- Do not modify the previous versioned file.
- The user runs and soaks the new test version locally.
- The next version starts from the latest version that the user confirms is working.
## Required Git Workflow
**Before editing:**

- Verify GitHub access
- Confirm active branch
- Check git status
- Confirm source test version
**After implementation:**

- Review the version-to-version diff
- Confirm only intended changes exist
- Run tests
- Check git status
- Stage only the new versioned file
- Commit with a focused message
- Push to the active branch
- Confirm the worktree is clean
**The final response must include:**

- New test filename
- Branch
- Commit hash
- Summary of changes
- Tests performed
- Any test limitations
- Confirmation that no production files were changed
## Testing Requirements
- Every version receives testing proportional to its risk.

### Baseline Tests
- Python syntax compilation using py_compile
- Import checks
- Version-header verification
- Version constant verification
- Version-to-version diff review
- Git status check
- Non-ASCII and encoding-artifact scan
- Notification module self-test where relevant
- Confirm no unintended production changes
### Focused Logic Tests
**Use mocked data and temporary state/output directories to test:**

- NVD request handling
- API key validation
- Vendor classification
- Supported versus unsupported records
- Historical record retention
- Misc lookup behavior
- PDF generation
- PDF download/view behavior
- Adhoc email behavior
- Automatic notification behavior
- Attachment generation/reuse
- Duplicate notification suppression
- Retry and failure handling
- Settings and state persistence
- Backup creation and retention
- Refresh timer synchronization
- Per-browser acknowledgement state
- Server-only behavior
- Tests must not require real SMTP or NVD traffic when a deterministic mocked test is possible.

### Multi-Client Stress Testing
**For significant GUI, state, notification, API, or concurrency changes:**

- Start a temporary local HTTP server.
- Simulate at least 10 concurrent clients.
- Test page loading and state polling.
- Test simultaneous user actions.
- Verify shared state remains consistent.
- Verify per-browser state remains isolated where required.
- Confirm scans do not overlap.
- Confirm API requests are protected against spam.
- Confirm duplicate PDF work is avoided.
- Confirm duplicate emails are avoided.
- Confirm no crashes, deadlocks, or corrupt state files.
- Confirm removed functionality cannot still be triggered through hidden API routes.
### Real-World User Testing
**After sandbox testing:**

- User launches the versioned test file locally.
- User tests using local and remote browsers.
- User tests different browsers and multiple clients.
- User verifies GUI appearance and workflow.
- User checks logs, state files, PDFs, emails, downloads, backups, and timers.
- The version runs for an extended soak period, normally `24 hours` or longer.
- Bugs found during the soak are added to the next planner.
## Stability Audit Process
- Before promotion to src, perform a full code-review stability audit.

### Review priorities:

**`P1`:** Critical release blocker, data loss, security failure, crashes, or incorrect core behavior.
**`P2`:** Significant logic flaw, uncontrolled API/SMTP load, broken state handling, or major workflow failure.
**`P3`:** Lower-impact defect, hidden callable behavior, inconsistent error handling, or maintainability risk.
**`P4`:** Minor issue, cosmetic defect, stale wording, or low-risk cleanup item.
### Audit requirements:

- Review the full current GUI code.
- Review connected tracking, notifications, and PDF integration paths.
- Check newly introduced behavior and existing surrounding logic.
- Run compilation, focused tests, self-tests, concurrency tests, and stress tests.
- Report findings first, ordered by severity, with file and line references.
- Make no changes during a review-only request.
**The promotion threshold is:**
- No open `P1`, `P2`, `P3`, or `P4` findings.
**If findings exist:**

- Add them to the next version planner.
- User confirms the scope.
- User says `PROCEED`.
- Create another full versioned test file.
- Test and soak again.
- Repeat the stability audit.
## Production Promotion
**Promotion happens only when:**

- The latest test version has passed local testing.
- It has completed the requested soak period.
- The final stability audit has no `P1`–`P4` findings.
- The user explicitly requests promotion.
**Promotion process:**

- Use the latest proven test version as the source.
- Update the appropriate production files under `src\.`
- Preserve complete version comments and change history.
- Ensure imports reference the correct production module names.
- Do not copy test-only filenames into production imports.
- Run production-path compilation and integration tests.
- Review the complete promotion diff.
- Commit and push only after explicit user approval.
- Do not alter the PDF engine unless explicitly requested.
## Current Project State
**Latest GUI candidate:**

- `test\eva_cve_gui_0_5_9.py`
**Current branch:**

- `feature/email-notifications`
**Current status:**

- Version `0.5.9` has been pushed.
- It is undergoing a `24-hour` soak.
**It fixed:**
- Server-side Misc lookup cooldown protection
- Hidden legacy batch PDF API execution
- After the soak, run another strict `0.5.9` stability audit.
- If there are no `P1`–`P4` findings, promote the proven test code into src.
## Planned Next Phase
**Next branch:**

- `feature/csv-import-enrichment`
**Phase 1 goal:**

- Import a real CSV inventory containing hundreds of network devices.
- Normalize vendor, product, model, and installed software-version fields.
- Identify which current High and Critical CVEs affect those installed versions.
**Use:**
- `NVD API`
- `NVD JSON feeds`
- `CPE/configuration data`
- Vendor references
- Local caching/export files where appropriate
- Enrich the inventory or produce a separate enriched export.
**Expected enrichment fields include:**

- CVE ID
- Vendor
- Product/model
- Installed version
- Severity
- CVSS score/version
- Published date
- Affected status
- Match confidence
- Match reason
- Affected version range
- NVD link
- Vendor links
- Recommended next step
- Software update required
- Workaround available
- Manual review required
**Because NVD data is not always exact, classification should support:**

- Confirmed affected
- Likely affected
- Possibly affected
- Not affected
- Insufficient data
- Manual review required
- The real CSV will be placed in test\ when this phase begins. Inspect its actual columns before designing or implementing the importer.

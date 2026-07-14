---
name: analyze-azure-devops-bug
description: Use when the user opens an Azure DevOps Bug or work item and asks to inspect its description, comments, images, history, links, attachments, environment, deployment evidence, code impact, database state, or root cause.
---

# Analyze Azure DevOps Bug

## Overview

Build an evidence-first analysis from the user's already-open, logged-in Azure DevOps work item. Treat the Bug page as an index of claims, not proof of the root cause. Connect work-item evidence to source code, database metadata, deployment state, and environment identity before concluding.

## Capabilities and project policy

- Use a browser capability that can reuse the user's existing logged-in session.
- Use a systematic debugging workflow before proposing a root cause or fix.
- Use only project-approved, read-only database access when database verification is relevant.
- Use an appropriate document, spreadsheet, PDF, image, or archive capability to inspect attachments.
- Read the repository's `AGENTS.md` and local project instructions before source or environment investigation.

## Safety boundaries

- Keep Azure DevOps read-only unless the user explicitly asks for a change. Do not save fields, add comments, change state, reassign, upload files, or create links.
- Never open or directly access an environment that project policy marks as restricted. Record the displayed URL, label, and context, then mark that evidence as unverified.
- Do not identify an environment from a Bug label, URL label, or screenshot alone. A screenshot without host, database, schema, build, and capture time does not establish where it came from.
- Do not perform application or database writes without separate explicit authorization.
- Preserve the user's browser state. Close only research tabs created during the task, restore the original Bug Details tab, and finalize the controlled browser session.

## Workflow

### 1. Identify the current Bug

Use the current logged-in DevOps tab instead of opening a new unauthenticated session.

Record:

- work-item ID, title, type, state, reason, and assignee
- area path, iteration, severity or priority, module, and functional identifier
- environment labels and URLs exactly as displayed
- created and updated dates, reporter, tester, and developer when available
- fields that are empty or absent, because missing evidence limits the conclusion

### 2. Read every details section

Inspect Description, Repro Steps, System Info, Test Data, Discussion, acceptance criteria, and custom Details sections. Capture:

- expected and actual results
- reproducible steps and prerequisites
- exact table, column, route, API, script, job, report, user, case, or other identifiers
- error text, timestamps, environment claims, and relevant URLs
- acceptance criteria that actually belong to the current Bug

Expand collapsed content and note sections that are empty.

### 3. Inspect all comments and inline images

Read comments oldest to newest. For each relevant comment record author, date and time, text, state implication, and image or attachment references.

For each image, state separately:

- what it visibly proves
- what it suggests
- what it cannot prove

A database tree showing a column type proves only that the displayed client saw that metadata. Without connection identity, it does not prove which environment or database was shown.

### 4. Reconstruct History

Inspect the full History tab and create an exact timeline of:

- creation and assignment
- scope, build, or environment field changes
- workflow state changes such as Active, Resolved, Ready for Retest, Retest Failed, and Reopened
- developer and tester comments around each transition
- dates that can be compared with commits, migrations, builds, or deployments

Treat workflow state as a claim. `Ready for Retest` does not prove that code or DDL reached the tested environment.

### 5. Inspect Links and separate scope

Enumerate Parent, Child, Related, Duplicate, predecessor or successor, commit, pull request, build, and external links, even when the count is zero.

Open relevant linked work items read-only. Build a scope matrix:

| Item | Role | In current Bug scope? | Evidence used |
|---|---|---:|---|
| Current Bug | Reported failure | Yes | Actual and expected result |
| Parent Story | Business context | Only overlapping acceptance criteria | Requirement and intended design |
| Related item | Supporting context | Only if explicitly connected | Timeline, deployment, or dependency |

Do not import every parent requirement into the current Bug automatically.

### 6. Inspect Attachments

Open the Attachments section and record the count, including zero. For relevant files record filename, uploader, date, type, and relationship to the claim. Inspect the actual file with the appropriate capability; do not rely only on a preview thumbnail.

### 7. Validate external source and script links

Check the exact repository, branch or commit, and path shown in the Bug. If a link returns 404 or redirects:

- record it as stale, moved, permission-limited, or incorrect
- search the expected repository for the filename or distinctive identifier
- prefer one authoritative current path or commit
- do not conclude that implementation is absent merely because an old link is broken

If the destination might be restricted or its environment cannot be established without opening it, do not click, preview, follow redirects, or request it. Record only the URL and visible context, then mark it unverified.

### 8. Inspect source locally

Resolve frontend, backend, database, and infrastructure repository roots from `AGENTS.md`, the workspace, or user-provided paths. Search exact identifiers before broad concepts: table or column, migration filename, error code, endpoint, field name, module, route, and work-item ID.

Check source behavior, migrations or DDL scripts, configuration, tests, and version history where useful. Keep unrelated user changes untouched.

### 9. Verify database metadata when relevant

Use project-approved, read-only metadata queries. Record the connection identity used for the evidence:

- host and port
- database and schema
- table and column
- observed type or value
- observation time

Compare three independent states:

| Layer | Question |
|---|---|
| Expected | What does the Bug or requirement say should exist? |
| Executed intent | What does checked-in code or migration change? |
| Observed target | What does identified, read-only target metadata show now? |

Never use one environment's evidence to claim another environment's state. Never treat the presence of a migration as proof that it ran successfully.

### 10. Classify the root cause

Select one primary hypothesis, list supporting and conflicting evidence, and assign High, Medium, or Low confidence. Use categories such as:

- source or test-data issue
- frontend, API, or backend code defect
- database DDL, migration, or deployment gap
- wrong, stale, or ambiguously labelled environment
- stale link, permission issue, or client metadata or cache
- unverified because required evidence is missing

Prefer the narrowest conclusion justified by evidence. Distinguish historical root cause from current retest status because the environment may have changed since the screenshot or failed retest.

### 11. Restore browser state

Return to the original Bug Details tab, leave the user at the work item, close only tabs created for research, and finalize the browser session.

### 12. Report

Load and follow [references/report-template.md](references/report-template.md). Lead with the outcome, label facts versus inference, and include a paste-ready English DevOps comment without posting it.

## Evidence gates

| Evidence | What it proves | What it does not prove |
|---|---|---|
| Screenshot without connection identity | Visible client state | Environment identity or current state |
| Migration exists in source | Intended change is versioned | Migration was deployed or succeeded |
| `Ready for Retest` history state | Workflow transition occurred | Fix reached the tested environment |
| Current target metadata | Current state of the identified target | Another environment or historical state |
| Parent requirement | Business context | Automatic scope of the current Bug |
| Old link returns 404 | Link is currently unusable | Change never existed |

## Common mistakes

- Reading only Description and missing the decisive comment, History transition, linked item, or attachment.
- Treating a screenshot filename, UI label, or mixed environment text as environment identity.
- Saying code is fixed because a migration exists, without deployment evidence.
- Saying cannot reproduce because current metadata differs from an older screenshot, without explaining the timeline.
- Mixing the entire Parent Story into the Bug's acceptance scope.
- Opening a restricted environment or changing DevOps while performing analysis.
- Giving a confident root cause when host, database, schema, build, time, or deployment evidence is missing.


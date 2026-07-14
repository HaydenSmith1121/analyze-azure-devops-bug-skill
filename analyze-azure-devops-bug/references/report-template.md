# Azure DevOps Bug analysis report template

Use this structure by default. Omit a section only when it is genuinely irrelevant. State `None found` or `Not available` when an expected DevOps section is empty.

## Outcome

State the most likely issue, whether it is historical or current, confidence, and the main evidence limitation.

## Bug snapshot

- ID and title:
- State, reason, and assignee:
- Area, iteration, and priority:
- Reported environment:
- Created and updated:
- Expected result:
- Actual result:

## Evidence

| Source | Observed fact | What it supports | Limitation |
|---|---|---|---|
| Description |  |  |  |
| Comment or image |  |  |  |
| History |  |  |  |
| Linked item |  |  |  |
| Attachment |  |  |  |
| Local code or migration |  |  |  |
| Target metadata |  |  |  |

## Timeline

| Date and time | Actor | Event | Significance |
|---|---|---|---|
|  |  |  |  |

## Expected vs implemented vs observed

| Layer | Value or state | Evidence identity |
|---|---|---|
| Expected requirement |  | Bug, Story field, or comment |
| Checked-in code or migration |  | Repository, branch or commit, and path |
| Observed target |  | Host, database, schema, build, and observation time |
| Restricted target | Unverified unless user-provided evidence is sufficient | Do not access directly |

## Root-cause assessment

- Primary hypothesis:
- Category:
- Confidence: High, Medium, or Low
- Supporting evidence:
- Conflicting or missing evidence:
- Historical cause versus current status:

## Scope separation

| Work item | Relevant requirement | In this Bug's scope? | Reason |
|---|---|---:|---|
| Current Bug |  | Yes |  |
| Parent or related item |  |  |  |

## Environment and link risks

- Environment identity gaps:
- Restricted evidence that remains unverified:
- Broken, moved, permission-limited, or stale links:

## Retest checklist

- Confirm the tested target's host, database, schema, application build, and deployment time.
- Re-run the exact original reproduction steps and boundary values.
- Verify both database metadata and application or API behavior when both are in scope.
- Capture new evidence with target identity and timestamp.
- Check for regressions in dependent fields or flows named by the current Bug.

## Paste-ready English DevOps comment

```text
Analysis result:

Expected:

Observed evidence:

Most likely root cause:

Current status and limitation:

Recommended retest:
```


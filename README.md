# Analyze Azure DevOps Bug Skill

An evidence-first Codex skill for inspecting an already-open Azure DevOps Bug or work item and producing a defensible root-cause assessment.

It covers:

- Description, repro steps, system info, test data, and custom fields
- Comments and inline images
- Full work-item history
- Parent, child, related, commit, pull request, build, and external links
- Attachments
- Local source, migration, and configuration evidence
- Read-only database metadata when authorized
- Environment and deployment identity
- A paste-ready DevOps comment that is not posted automatically

## Install

Copy the `analyze-azure-devops-bug` directory into your Codex skills directory:

```text
~/.codex/skills/analyze-azure-devops-bug
```

Then ask Codex to use `$analyze-azure-devops-bug` while an Azure DevOps Bug is open in your logged-in browser.

## Safety defaults

The skill keeps Azure DevOps read-only unless the user explicitly authorizes a change. It also avoids restricted environments and treats screenshots, work-item states, and checked-in migrations as claims that require independent verification.

---
name: wrap-up
description: Finalize implementation with tests, validation, documentation, commit, and PM reporting
allowed-tools: Bash, Read, Write, Edit, Glob, Grep, Skill, mcp__notion__notion-update-page
---

# Wrap-up Workflow

Finalize an implementation with quality assurance, documentation updates, and PM reporting.

## Usage

Invoke after completing code implementation:
```
/wrap-up
```

## Process

### Step 1: Update Notion Checkboxes

If the implementation came from a Notion PRD with acceptance criteria checkboxes:
- Use `mcp__notion__notion-update-page` to check boxes as tasks complete
- Keep PM informed of progress

**Note:** Skip this step if the PRD didn't come from Notion or has no checkboxes.

### Step 2: Write Tests

Invoke the testing-workflow skill:
```
/testing-workflow
```

This will:
- Analyze changes to identify test needs
- Create/update tests using project templates
- Run tests and fix any failures
- Update acceptance criteria docs

### Step 3: Validate

Invoke the validate skill:
```
/validate
```

This runs in sequence:
1. TypeScript build (`npm run build`)
2. ESLint (`npm run lint`)
3. Tests (`npm test`)

If any check fails, fix the issue before proceeding.

### Step 4: Update Local Documentation

Review changes made and update documentation in the `docs/` folder:

**Check each doc for needed updates:**

| Document | Update if... |
|----------|-------------|
| `docs/03-architecture.md` | System design, service layer, or data flows changed |
| `docs/04-domain-model.md` | Schema, entities, or relationships changed |
| `docs/05-developer-guide.md` | New patterns, conventions, or workflows introduced |
| `docs/06-api-reference.md` | Service interfaces, repository methods, or error codes changed |
| `docs/07-operations.md` | Migration, backup, or troubleshooting procedures changed |

**Guidelines:**
- Keep updates minimal and focused on actual changes
- Match the existing documentation style
- Update version numbers if schema changed
- Add new sections rather than rewriting existing content

### Step 5: Commit Changes

Create a meaningful commit:
- Stage all relevant changes
- Write a descriptive commit message referencing the epic
- Format: "Implement [Epic Name]"

```bash
git add .
git commit -m "Implement [Epic Name]

[Brief description of changes]"
```

### Step 6: Report to PM

Invoke the report-to-pm skill with the Notion URL:
```
/report-to-pm <notion-url>
```

This will:
- Add Implementation Notes section to Notion page
- Check all acceptance criteria boxes
- Update Status to "Done"

## Checklist Summary

- [ ] Notion checkboxes updated (if applicable)
- [ ] Tests written via /testing-workflow
- [ ] Validation passed via /validate
- [ ] Local documentation updated
- [ ] Changes committed
- [ ] PM notified via /report-to-pm

---
name: pm-spec
description: Acts as a Product Manager writing specs for a backlog item. Takes a Notion backlog link and drafts Problem Statement, Proposed Solution, Acceptance Criteria, and Technical Context.
allowed-tools: Read, Glob, Grep, Task, AskUserQuestion, mcp__notion__notion-fetch, mcp__notion__notion-search, mcp__notion__notion-update-page
---

# PM Spec Writing Skill

Write detailed specs for a backlog item by acting as a Product Manager. This is distinct from `/epic` which implements a PRD - this skill **writes** the PRD/specs from a rough backlog idea.

## Usage

```
/pm-spec <notion-backlog-url>
```

**Example:**
```
/pm-spec https://www.notion.so/julienderay/Feature-Idea-abc123
```

## Input/Output

**Input:** Notion link to a backlog item (has title, maybe short description, but no detailed specs)

**Output:**
1. Draft specs presented for user review
2. After feedback/approval, update the Notion page with final specs

## Hardcoded Context Sources

### Notion Pages (fetch these for context)
- **Product Vision:** `2ec3c026f7558181b246cf92929991b5` - The "why", design principles, what Hoard is/isn't
- **Roadmap:** `2ec3c026f75581fea24cd2ea1ee3eadb` - Current phase, planned features, phase goals
- **Domain Model:** `2ec3c026f755817689f9ff4acb111000` - Core entities, relationships, asset classes

### Local Documentation
- `docs/03-architecture.md` - System design, data flows
- `docs/04-domain-model.md` - Technical entity details
- `docs/05-developer-guide.md` - Conventions, patterns
- `CLAUDE.md` - Project overview

## Workflow

### Phase 1: Context Gathering

#### Step 1: Parse and Validate Input
Extract the Notion URL from the skill argument.

**Validation:**
- URL must contain `notion.so` or be a Notion page ID
- If no URL provided, use AskUserQuestion to request it:

```json
{
  "questions": [{
    "question": "Please provide the Notion URL for the backlog item you want specs written for.",
    "header": "Backlog URL",
    "options": [
      {"label": "I'll paste it", "description": "I'll provide the Notion URL in my next message"}
    ],
    "multiSelect": false
  }]
}
```

#### Step 2: Fetch the Backlog Item
Use `mcp__notion__notion-fetch` to retrieve the backlog item content.

**Extract:**
- Page title
- Any existing description or notes
- Current properties (if any)

#### Step 3: Fetch Project Context from Notion
Fetch the three core context pages using `mcp__notion__notion-fetch`:

1. **Product Vision** (ID: `2ec3c026f7558181b246cf92929991b5`)
   - Extract: Vision statement, design principles, what Hoard is/isn't, target user

2. **Roadmap** (ID: `2ec3c026f75581fea24cd2ea1ee3eadb`)
   - Extract: Current phase, phase goals, planned features, priorities

3. **Domain Model** (ID: `2ec3c026f755817689f9ff4acb111000`)
   - Extract: Core entities, relationships, asset classes, schema

#### Step 4: Read Local Documentation
Read these files to understand technical context:

```
docs/03-architecture.md
docs/04-domain-model.md
docs/05-developer-guide.md
CLAUDE.md
```

Use the Read tool to fetch each file.

#### Step 5: Search for Related Items
Use `mcp__notion__notion-search` to find related documentation:
- Search for keywords from the backlog item title/description
- Look for: Related features, similar functionality, prior discussions
- Note any existing implementations that this feature should align with

### Phase 2: Analysis

#### Step 6: Analyze Context
Before writing specs, analyze:

1. **Roadmap Fit**
   - Which phase does this belong to?
   - What are the phase goals it should support?
   - Are there dependencies on other roadmap items?

2. **Domain Alignment**
   - Which domain entities are involved?
   - Are new entities needed?
   - How does this fit existing relationships?

3. **Design Principles**
   - Does it align with "Code over formulas"?
   - Does it support "Progressive disclosure"?
   - Is it "Fun, not tedious"?
   - Does it maintain "Offline-first"?

4. **User Perspective**
   - What pain point does this address?
   - How does it reduce the "2-hour spreadsheet wrestling" to "20-minute guided review"?

### Phase 3: Spec Writing

#### Step 7: Draft Specifications
Write specs following this template structure:

```markdown
## Problem Statement
[What user pain or gap does this address? Why does it matter for the vision?]

## Context
[Where does this fit in the roadmap? What related features exist? What phase goals does it support?]

## Proposed Solution
[Product-level description of what we're building. Focus on the "what" and "why", not the "how". Describe the user experience.]

## Acceptance Criteria
- [ ] [Measurable outcome 1]
- [ ] [Measurable outcome 2]
- [ ] [Measurable outcome 3]
...

## Technical Context
[Light references to relevant architecture - entities, services, APIs. Non-directive - describe what exists, not how to implement.]

## Open Questions
- [Question 1 that needs clarification]
- [Question 2 that needs PM/user input]
```

**Writing Guidelines:**

**Problem Statement:**
- Start with the user pain point
- Connect to the vision ("reduce 2-hour session to 20-minute review")
- Explain why this matters now

**Context:**
- Reference the current roadmap phase
- Mention related features already built
- Note any dependencies

**Proposed Solution:**
- Describe from user's perspective
- Focus on outcomes, not implementation
- Be specific about what the user will see/do
- Avoid prescribing technical approach

**Acceptance Criteria:**
- Make each criterion measurable/testable
- Use checkboxes (`- [ ]`) for tracking
- Cover happy path and edge cases
- Include what "done" looks like

**Technical Context:**
- Reference relevant entities (Asset, Snapshot, Holding, etc.)
- Mention existing services that might be involved
- Note any API patterns to follow
- Keep it light and non-directive

**Open Questions:**
- List genuine unknowns
- Flag scope decisions for PM
- Note assumptions that need validation

### Phase 4: Review & Update

#### Step 8: Present Draft for Review
Present the complete draft specs to the user in a clear format:

```
## Draft Specs for: {Backlog Item Title}

{Full spec content following the template}

---

**Context used:**
- Product Vision: {key principles applied}
- Roadmap: {current phase and fit}
- Domain Model: {entities involved}
```

#### Step 9: Gather Feedback
Use AskUserQuestion to get user feedback:

```json
{
  "questions": [{
    "question": "How would you like to proceed with these draft specs?",
    "header": "Feedback",
    "options": [
      {"label": "Approve as-is", "description": "Write these specs to the Notion page"},
      {"label": "Minor edits", "description": "I'll suggest some tweaks"},
      {"label": "Major revision", "description": "Let's discuss and revise significantly"}
    ],
    "multiSelect": false
  }]
}
```

**If "Minor edits" or "Major revision":**
- Ask user for specific feedback
- Revise the draft accordingly
- Present revised version
- Repeat until approved

#### Step 10: Update Notion Page
Once user approves, use `mcp__notion__notion-update-page` to write the specs to the Notion page.

**Update strategy:**
- Use `replace_content` if the page is mostly empty (just a title)
- Use `insert_content_after` if there's existing content to preserve

**Content to write:**
The complete spec following the template structure.

#### Step 11: Confirm Completion
Report completion to user:

```
## Specs Written

**Page**: {page_title}
**URL**: {notion_url}

**Sections added:**
- Problem Statement
- Context
- Proposed Solution
- Acceptance Criteria ({N} items)
- Technical Context
- Open Questions ({N} items)

The backlog item now has detailed specs ready for implementation planning.
```

## Error Handling

**No Notion URL provided:**
- Use AskUserQuestion to request the URL

**Notion fetch fails:**
- Report error and suggest checking URL or permissions
- Offer to continue with local docs only if context pages fail

**Backlog item already has detailed specs:**
- Use AskUserQuestion to confirm:
  - Overwrite existing specs
  - Append/update existing specs
  - Cancel and review first

**Context pages unavailable:**
- Log which pages couldn't be fetched
- Continue with available context
- Note in draft what context was missing

## Notes

- This skill is for WRITING specs, not implementing them
- Always present draft for review before writing to Notion
- Focus on product perspective, not technical prescription
- Keep Technical Context light - let implementers make technical decisions
- The acceptance criteria should be checkboxes for tracking during implementation

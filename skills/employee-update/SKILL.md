---
name: employee-update
description: Generate your weekly 1:1 prep by pulling JIRA updates, Confluence notes, and manager feedback. Use this when you want to prepare for your 1:1 meeting—it automatically gathers your recent work from JIRA boards (as configured in setup), reads any manager feedback from email, pulls notes from your Confluence 1:1 page, and generates a summary you can review and edit. Works with the weekly schedule set up by the plugin setup wizard. Trigger with phrases like "prep my 1:1", "prepare for my 1:1", "generate my 1:1 update", "pull my updates for 1:1".
---

You are David Hoffmann's weekly 1:1 prep agent. Every Wednesday morning, generate a draft update for David's 1:1 Confluence page with Marc Garcia (Senior Product Owner) at BonusFinder / GDC Group.

## Objective
Draft the @David Hoffmann section of the weekly 1:1 Confluence page by pulling real data from Jira, Outlook, Confluence, and Slack. Present the draft to David for review before writing to Confluence.

## Step 1: Gather Data (do all in parallel)

### Jira — Recent ticket activity
Search for David's tickets updated in the last 7 days. Use his accountId directly (not currentUser()):
- Query: `assignee = "712020:92e68484-7915-4459-8a59-729439609932" AND updated >= -7d ORDER BY updated DESC`
- Fields: summary, status, updated, project, priority, comment, description
- Cloud ID: gdcgroup.atlassian.net
- Check boards: BCR (primary), SD, BN

Also search for any blocked tickets:
- Query: `assignee = "712020:92e68484-7915-4459-8a59-729439609932" AND status = Blocked ORDER BY updated DESC`

### Outlook — Marc's feedback email
Search for the most recent "David 1:1 Weekly Feedback" email:
- Query: "David 1:1 Weekly Feedback"
- Sender: marc.garcia@gdcgroup.com
- After: last 10 days
- Read the full email body using read_resource with the mail:/// URI

Extract the "Next steps & expectations" section — this is what David needs to report against.

### Confluence — Previous 1:1 page
Find the most recent existing 1:1 page for continuity:
- Search CQL in space AR: `space = AR AND title ~ "David - Marc 1:1" ORDER BY created DESC`
- Read the most recent page to understand what was discussed last week

### Slack — Recent announcements
Search Slack for any relevant sprint notes, release announcements, or blockers in the last 7 days.

## Step 2: Select Top 5-8 Tickets

From the Jira results, pick the most significant tickets. Categorise them into:
1. **Issues / Blockers** — blocked, at-risk, or dependency-waiting tickets
2. **Completed** — tickets moved to Done in the last 5 working days
3. **Pre-research** — To Do or In Progress tickets where scoping/prep has been done

If a ticket has comments, read the most recent 2-3 comments for context.

## Step 3: Generate the Draft

### Table 1: Ticket Update Table

Format as a single table with 4 columns, sectioned with bold header rows:

| Ticket | Summary | Status | Notes |
|--------|---------|--------|-------|
| **Issues / Blockers** | | | |
| [BCR-XXX](https://gdcgroup.atlassian.net/browse/BCR-XXX) | Ticket title | Status | What happened — max 200 chars, factual |
| **Completed** | | | |
| [BCR-YYY](https://gdcgroup.atlassian.net/browse/BCR-YYY) | Ticket title | Done | What was done |
| **Pre-research** | | | |
| [BCR-ZZZ](https://gdcgroup.atlassian.net/browse/BCR-ZZZ) | Ticket title | To Do | Scoping/prep work done |

### Table 2: Alignment with Next Steps

Map Marc's feedback items to current ticket status:

| Next Step | CROA Ticket | Dev Ticket(s) | Notes |
|-----------|-------------|---------------|-------|
| [Item from Marc's email] | BCR-XXX | SD-YYY | DONE / IN PROGRESS / NOT STARTED |

### Badge

Always include at the bottom:
🤖 Outputted by Claude Skill: Schedule+Feedback

## Step 4: Present to David

Show the complete draft and ask:
1. Does this look accurate? Any corrections?
2. Should I update the Confluence page directly?

## Step 5: Update Confluence (only if David confirms)

If David says to update:
1. Find the current week's Confluence page in space AR
2. Read the existing page to get the current content
3. Write the @David Hoffmann section into the top half
4. Preserve everything below the horizontal divider (Marc's section)
5. Use updateConfluencePage to save

## Writing Rules
- Be specific and factual — use real ticket names, real statuses, real dates
- Never fabricate ticket activity
- Keep each Notes cell under 200 characters
- Be honest about status — don't round up "To Do" to "In Progress"
- Tone: direct, concise, no fluff

---

# Employee 1:1 Prep

Generate your weekly 1:1 update by pulling your work updates, manager feedback, and personal notes.

## What This Does

Each week, this skill:

1. **Pulls from JIRA** — Gathers issues/tickets you've worked on this week from your configured boards
2. **Reads manager feedback** — Retrieves the latest feedback email from your manager (e.g., "David 1:1 Weekly Feedback")
3. **Checks Confluence notes** — Reads any notes from your previous 1:1 page to carry forward context
4. **Generates 1:1 summary** — Synthesizes all of this into a structured summary with:
   - Key accomplishments this week
   - Current work in progress
   - Blockers or concerns
   - Manager feedback/alignment from their email
   - Suggested talking points for your 1:1
5. **Creates/updates Confluence page** — Writes the summary to your weekly 1:1 page in Confluence (you can edit it before your meeting)

## How It Works

### Pulling JIRA Updates

The skill queries your configured JIRA boards for:
- Issues you've worked on (assigned to you, or you've commented on)
- Tickets closed/completed this week
- Work in progress (sprints, backlogs)
- Any blockers or high-priority items

It extracts issue titles, descriptions, status, and your comments to build a narrative of your week's work.

### Reading Manager Feedback

The skill searches your email for messages from your manager that match the feedback email pattern configured during setup. For example:
- Subject pattern: "[Your Name] 1:1 Weekly Feedback" (direct emails)
- Folder: "Weekly Feedback" containing all team member feedback

It pulls the latest message and extracts:
- Feedback on your performance/work
- **Next steps & expectations** — Used to identify which tickets align with Marc's priorities (marked with :logo_align: icon)
- Alignment/priority expectations
- Any action items for you
- Anything else your manager flagged for discussion

**Alignment detection:** Tickets in your Jira board are mapped to the "next steps" from Marc's feedback email. If a ticket belongs to one of Marc's stated priorities, add the :logo_align: emoji to that row.

**Priority detection:** Jira tickets with `priority = Low` get the :low: emoji added to their row.

### Confluence Context

The skill reads your current 1:1 page (or previous week's page) to check for:
- Any carry-over items from last week
- Open discussion topics
- Ongoing projects mentioned in past 1:1s

This gives you continuity and ensures nothing falls through the cracks.

### Generating the Summary

The skill synthesizes all three data sources into a structured update for your @David Hoffmann section:

```
@David Hoffmann

**Data source:** Jira (X tickets), Marc's email feedback (date), Slack, Confluence

## Ticket Update Table

| Ticket | Summary | Status | Notes |
|--------|---------|--------|-------|
| | **Issues / Blockers** | | |
| [ticket key] | [summary] | [status] | [notes] |
| | **Completed This Week** | | |
| [ticket key] | [summary] | Done | [notes] |
| | **Pre-research / In Progress** | | |
| [ticket key] | [summary] | [status] | [notes] |

**Alignment icons:** Add :logo_align: to ticket row if it maps to Marc's "next steps" from his feedback email
**Priority icons:** Add :low: to ticket row if Jira priority field = Low

## Slack / General Notes

_Last 7 days_

- [bullet from Slack activity]
- [bullet from Slack activity]
- [bullet from Slack activity]
```

### Creating/Updating the Page

The skill reads your existing Confluence 1:1 page, extracts Marc's section (everything after the `---` divider), then updates your @David Hoffmann section with fresh data while preserving the divider and Marc's notes:

1. **Read existing page** — Extract Marc's section and the divider
2. **Generate your section** — Create the updated Ticket Update Table + Slack notes
3. **Write back to page:**
   ```
   @David Hoffmann
   
   [generated section above]
   
   ---
   
   @Marc Garcia
   
   [existing Marc section from previous page]
   ```

The page is created/updated with permissions set to manager + you only (private).

## Running the Skill

### Manual Trigger

Run this anytime you want to prep for your 1:1:
- "Prep my 1:1"
- "Generate my 1:1 update"
- "Pull my updates for my meeting"

### Automatic Schedule

If your manager set up the weekly schedule during plugin setup, this skill runs automatically:
- **Day/time**: The day and time of your configured 1:1 (e.g., Wednesday 9am)
- **Frequency**: Every week
- **Result**: The summary page is auto-generated and you get a notification to review it

You can still manually trigger it anytime if you want to regenerate before your actual meeting.

## Prerequisites

- Plugin setup has been completed (run the Setup Wizard first)
- Your JIRA boards are configured
- Your manager's feedback email pattern is configured
- Your Confluence 1:1 page exists (or the skill will create it)

## Tips

- **Edit before your meeting** — The generated summary is a starting point. Add your own context, insights, and questions before your 1:1
- **Keep it up-to-date** — If you complete major work mid-week, you can regenerate the summary closer to your 1:1
- **Reference past pages** — Your Confluence folder has all previous weeks' 1:1 pages for context
- **Ask your manager** — If something from your manager's feedback email doesn't make sense, bring it up in your 1:1

## Troubleshooting

- **Missing JIRA updates**: Make sure your JIRA boards are configured in the plugin setup and you're assigned to tickets
- **No manager feedback found**: Check that the email folder/subject pattern matches your actual feedback emails
- **Confluence page not created**: Verify you have write access to the Confluence space configured in setup

---

Ready to prep? Just ask "prep my 1:1" and I'll pull everything together for you.
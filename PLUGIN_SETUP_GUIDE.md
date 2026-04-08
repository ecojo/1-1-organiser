# Weekly 1:1 Updates Plugin — Setup Guide

## Overview

This plugin automates your team's weekly 1:1 prep. It pulls JIRA updates, manager feedback emails, and previous 1:1 notes to generate structured summaries—saving 30–45 minutes per week per person.

**Two modes:**
- **Manager mode**: Pull all your direct reports' updates before back-to-back 1:1s
- **Employee mode**: Prep your own 1:1 update before your meeting with your manager

---

## What You Need Before Starting

### Required Connectors (Must Be Connected in Cowork)
1. **JIRA** — to pull assigned work/issues
2. **Confluence** — to create and read 1:1 pages
3. **Outlook/Email** — to read manager feedback emails

### Optional Connectors
- **Slack** — for team notifications (optional)
- **Teams** — for team notifications (optional)

**Check these are connected before running Setup Wizard:**
- Go to your Cowork workspace settings
- Verify JIRA, Confluence, and Outlook appear in your connected tools
- If any are missing, connect them first

---

## Installation

1. Download the `weekly-1-1-updates.plugin` file
2. In **Cowork** → **Plugins** → **Install Plugin** → select the file
3. The plugin appears in your installed plugins list
4. Click the plugin to view skills

---

## Quick Start

### For Managers (Do This First)

**Run the Setup Wizard** (one-time setup):
1. Click the plugin → select **"Setup Wizard"** skill
2. Answer these questions:
   - **Team name** (e.g., "Engineering")
   - **Your email** (manager email)
   - **Your team members** (list each person's name + email)
   - **JIRA boards** (which boards each person works on)
   - **Email feedback** (folder where you send feedback emails, or subject line pattern)
   - **Confluence space** (where 1:1 pages live)
   - **Meeting times** (day + time for each person's 1:1; auto-discover from Outlook or manual)
   - **Timezone** (for scheduling)

3. The wizard validates your connectors and creates Confluence folders automatically
4. Configuration is saved and reused by all other skills

### For Employees

Wait for your manager to complete setup, then:

**Prep your 1:1** (weekly):
- Ask: **"Prep my 1:1"** or **"Generate my 1:1 update"**
- The skill pulls your JIRA updates, reads manager feedback, gathers previous notes
- Creates a Confluence page you can review + edit before your meeting
- Or set it to run automatically on your 1:1 day/time (scheduled by manager during setup)

### For Managers (Weekly)

**Pull all your reports' updates** (before your 1:1s):
- Ask: **"Pull all my reports' updates"** or **"Get team 1:1 updates"**
- Creates individual 1:1 prep pages for each person
- Run 30–60 minutes before your first 1:1
- Or set it to run automatically on each person's 1:1 day morning (scheduled during setup)

### Automatic Features

**Monthly page scaffolding:**
- On the 1st of each month (or your configured date), new placeholder 1:1 pages are auto-created for next quarter
- Pages are named: `[Name] - Manager 1:1 - [Date]`
- No action needed—just happens automatically

---

## What Gets Created

After setup, your Confluence space looks like:

```
Weekly Feedback (Space)
├── David Hoffmann 1:1s
│   └── 2026
│       ├── David Hoffmann - Manager 1:1 - 01 Apr 2026
│       ├── David Hoffmann - Manager 1:1 - 08 Apr 2026
│       └── ...
├── Sarah Chen 1:1s
│   └── 2026
│       └── ...
└── Jordan Smith 1:1s
    └── 2026
        └── ...
```

Pages are visible to manager + that employee only (permissions set automatically).

---

## Each Skill Explained

| Skill | Trigger | For Whom | Frequency |
|-------|---------|----------|-----------|
| **Setup Wizard** | Run manually | Manager only | One-time (initial setup) |
| **Employee Update** | "Prep my 1:1" | Each employee | Weekly (manual or auto-scheduled) |
| **Manager Updates** | "Pull my reports' updates" | Manager | Weekly (manual or auto-scheduled) |
| **Scaffolder** | Auto-runs | Automatic | Monthly (creates next quarter pages) |

---

## Example: First Week

**Monday, January 15 — Manager runs Setup Wizard**

Answers:
- Team: Engineering
- Reports: David, Sarah, Jordan
- David's 1:1: Monday 9am
- Sarah's 1:1: Wednesday 9am
- Jordan's 1:1: Friday 2pm
- Confluence space: "Weekly Feedback"
- Email feedback folder: "Weekly Feedback"

System creates:
- Confluence folder structure (Weekly Feedback > David Hoffmann 1:1s > 2026 > pages)
- Scheduled tasks for each employee + manager

**Monday 9am — Plugin auto-triggers**
- David's Employee Update runs → creates his 1:1 page (JIRA work, feedback, notes)
- Manager Updates runs for David → Marc reviews page in Confluence
- David reviews his page, edits notes, meets with Marc

**Wednesday 9am — Sarah's turn**
- Sarah's page auto-generated
- Marc reviews + meets with Sarah

**Friday 2pm — Jordan's turn**
- Jordan's page auto-generated
- Marc reviews + meets with Jordan

**Monthly (e.g., Feb 1) — Scaffolder auto-runs**
- Creates all Q2 2026 placeholder pages for David, Sarah, Jordan
- Pages ready weeks in advance

---

## Adjusting Your Setup

**Need to change something?** (e.g., add team member, change JIRA boards)

Simply re-run **Setup Wizard** and answer the questions again. It updates the configuration; all other skills pick up the changes automatically.

---

## Troubleshooting

### "Connector not found"
- Ensure JIRA, Confluence, and Outlook are connected in your Cowork settings
- Re-run Setup Wizard to re-validate

### "Confluence page not created"
- Verify the Confluence space exists
- Check you have write access to the space
- Re-run Setup Wizard

### "No JIRA updates showing"
- Confirm each person has issues assigned to them in their JIRA boards
- Check that issues are from the current week
- Verify JIRA connector is connected and has board access

### "Email feedback not found"
- Confirm the email folder/subject pattern matches your actual emails
- Check Outlook connector is connected
- Re-run Setup Wizard to adjust the email pattern

### "Scheduled tasks not running"
- Confirm Setup Wizard completed successfully
- Check that your workspace allows scheduled tasks
- Try running the skill manually first: "Prep my 1:1" or "Pull my reports' updates"

---

## Tips & Best Practices

### For Managers
- Review 1:1 pages 10 minutes before each meeting
- Look for team patterns (shared blockers, capacity issues)
- Add your notes/feedback to pages during meetings
- Use the monthly scaffolder—pages are ready weeks ahead

### For Employees
- The summary is a starting point—add your own context + goals
- Check your manager's feedback email before the meeting
- Review previous 1:1 pages for continuity
- Add talking points + discussion topics to the page
- Ask clarifying questions in Confluence if needed

### Team Best Practices
- Keep 1:1 schedule consistent (same time each week) so automation runs reliably
- Use consistent JIRA board names across the team
- Store feedback emails in a shared folder or use consistent subject lines
- Review 1:1 pages regularly to identify trends/issues

---

## Privacy & Permissions

- **Employee pages**: Visible to manager + that employee only
- **Config**: Stored securely, used only by this plugin
- **Data**: All processing happens in your Cowork workspace—no data leaves your organization
- **Connectors**: Plugin uses only the permissions you've granted to JIRA, Confluence, Outlook

---

## Questions?

1. Check the **Troubleshooting** section above
2. Re-run **Setup Wizard** to validate your configuration
3. Try running the skill manually to test (e.g., "Prep my 1:1")

---

**Ready to start?**

Managers: Run **Setup Wizard** to configure your team (takes ~10 minutes).

Employees: Ask **"Prep my 1:1"** once your manager has completed setup.

Everyone: Let the plugin run on schedule and focus on your 1:1 conversations!

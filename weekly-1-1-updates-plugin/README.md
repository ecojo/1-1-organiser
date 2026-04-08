# Weekly 1:1 Updates Plugin

Automate your team's weekly 1:1 updates. Pull JIRA, Confluence, and manager feedback automatically to generate employee 1:1 prep or consolidate all team reports for manager review.

## Quick Install

1. Download `weekly-1-1-updates.plugin` from this repo
2. Drag & drop into your Cowork chat
3. Click "Install"
4. Run Setup Wizard to configure for your team

[Full setup guide →](../PLUGIN_SETUP_GUIDE.md)

## What It Does

For employees: Automatically gathers your JIRA updates, manager feedback email, and notes from past 1:1s, then generates a summary you can review and edit before your meeting.

For managers: Pulls all direct reports' updates (each person's JIRA work, notes, and feedback) and generates individual 1:1 prep pages so you're ready for back-to-back meetings.

Automatic infrastructure: Creates your Confluence folder structure (Weekly Feedback space, employee subfolders, year folders, placeholder pages) and pre-scaffolds next quarter's pages monthly.

## How to Install

1. Download the `weekly-1-1-updates.plugin` file
2. In Claude Cowork, go to Plugins → Install Plugin → select this file
3. The plugin will appear in your installed plugins list

## Quick Start

### Step 1: Run Setup Wizard (Manager Only)

The manager should run the Setup Wizard skill first:

1. Click the plugin → select "Setup Wizard" skill
2. Answer questions about your team:
   * Team name, manager email, timezone
   * Each team member's name, email, JIRA boards
   * How manager feedback emails are organized
   * Which Confluence space to use
   * Each person's 1:1 meeting time (auto-discover from Outlook or manual entry)
3. The wizard will validate your connectors and create Confluence infrastructure
4. Your team config is saved and reused by all other skills

**Required connectors before setup:**
* JIRA (to pull work updates)
* Confluence (to create 1:1 pages)
* Outlook/Email (to read feedback emails)
* Slack (optional, if your team uses it)
* Teams (optional, if your team uses it)

### Step 2: Employee Prep Their 1:1 (Weekly)

For each employee, trigger the Employee Update skill to prep for their 1:1:

* **Manual:** Ask "Prep my 1:1" or "Generate my 1:1 update"
* **Automatic (if scheduled during setup):** Runs on their 1:1 day/time each week, creates their Confluence page automatically

The skill:
* Pulls their JIRA updates (assigned issues, closed work, blockers)
* Reads manager feedback email
* Gathers notes from previous 1:1 pages
* Generates a summary page in Confluence
* They can review, edit, and add notes before the meeting

### Step 3: Manager Reviews All Reports (Weekly)

For the manager, trigger the Manager Updates skill to see all team members' prep:

* **Manual:** Ask "Pull all my reports' updates" or "Get team 1:1 updates"
* **Automatic (if scheduled during setup):** Runs on each employee's 1:1 day (morning), creates their page before the meeting

The skill:
* Pulls each person's JIRA, notes, and feedback
* Creates individual 1:1 pages for each team member
* Provides a summary view so you're prepared for all 1:1s

### Step 4: Auto-Scaffold Next Quarter (Monthly)

The Scaffolder runs automatically every month:

* Creates year folders (2026, 2027, etc.)
* Pre-creates blank 1:1 pages for next quarter (or half-year)
* Uses format: `[Name] - Manager 1:1 - [Date]`
* Pages are ready weeks in advance

You can also manually trigger: "Create next quarter pages"

## Configuration

All configuration happens in the Setup Wizard. Key settings:

* Team members — Who reports to you
* JIRA boards — Which boards each person works on (can be different per person)
* Email feedback — How feedback is organized (folder or direct emails)
* Confluence space — Where 1:1 pages live
* Meeting times — Day/time of each 1:1 (auto-discover from Outlook or manual)
* Timezone — For scheduling (e.g., America/Los_Angeles)
* Scaffold frequency — Quarterly or half-yearly (how far ahead to create pages)

To update config later, re-run the Setup Wizard.

## Skills Reference

| Skill | Trigger | For Whom | Frequency |
|-------|---------|----------|-----------|
| **Setup Wizard** | "Set up my team" | Manager (once) | One-time setup |
| **Employee Update** | "Prep my 1:1" | Employees | Weekly (manual or scheduled) |
| **Manager Updates** | "Pull my reports' updates" | Manager | Weekly (manual or scheduled) |
| **Scaffolder** | "Create next quarter pages" | Auto-runs | Monthly (auto or manual) |

## Example Workflow

**Monday, January 15, 2026**

Manager Marc runs Setup Wizard:
* Team: Engineering
* Reports: David (JIRA: BCR, BonusFinder Dev), Sarah (JIRA: BonusFinder Dev), Jordan (JIRA: Infrastructure)
* David's 1:1: Monday 9am
* Sarah's 1:1: Wednesday 9am
* Jordan's 1:1: Friday 2pm
* Confluence space: "Weekly Feedback"

**Monday 9am, January 15:**

* Plugin auto-triggers David's Employee Update → generates his Monday 1:1 page
* Plugin auto-triggers Manager Updates for David → sends Marc a summary
* Marc reviews David's page in Confluence (JIRA work, feedback, talking points)
* David reviews his own page, edits as needed, meets with Marc

**Wednesday 9am, January 17:**

* Plugin auto-triggers Sarah's Employee Update → generates her Wednesday 1:1 page
* Plugin auto-triggers Manager Updates for Sarah → sends Marc a summary
* Marc meets with Sarah

**Friday 2pm, January 19:**

* Plugin auto-triggers Jordan's Employee Update → generates his Friday 1:1 page
* Plugin auto-triggers Manager Updates for Jordan → sends Marc a summary
* Marc meets with Jordan

**Monthly (e.g., Feb 1 at 12am):**

* Scaffolder runs → creates Q1 pages (Jan–Mar) for David, Sarah, Jordan
* Pages are ready for the next quarter

## Troubleshooting

### "Connector not found"

Make sure you have JIRA, Confluence, and Outlook/Email connected in your workspace before running Setup Wizard.

### "Confluence page not created"

* Verify the Confluence space exists and you have write access
* Check that employee subfolders are created (Setup Wizard should do this)
* Re-run Setup Wizard to validate/fix the space

### "No JIRA updates showing"

* Make sure each person is assigned to issues in their configured JIRA boards
* Check that the issue date range matches "this week"
* Verify JIRA connector is connected and has access to those boards

### "Email feedback not found"

* Confirm the email folder/subject pattern matches your actual emails
* Check that the Outlook/Email connector is connected
* Re-run Setup Wizard to adjust the feedback email pattern

### "Scheduled tasks not running"

* Confirm setup was completed and config was saved
* Check your workspace settings for task scheduling
* Manually trigger the skill to test (e.g., "Prep my 1:1")

## Tips & Best Practices

### For Managers

* Review 1:1 pages 5–10 minutes before each meeting to prepare talking points
* Look for patterns across your team (shared blockers, capacity issues)
* Add your own notes/feedback to pages during or after meetings
* Use the monthly scaffolder to stay ahead—pages are ready in advance

### For Employees

* The generated summary is a starting point—personalize it with your context
* Check your manager's feedback email before the meeting
* Review previous 1:1 pages for continuity
* Ask clarifying questions in the Confluence page if something is unclear
* Add your own talking points and discussion topics

### Team Best Practices

* Set a consistent 1:1 schedule (same time each week) so automation runs reliably
* Use consistent JIRA board naming across your team
* Store feedback emails in a shared folder or with consistent subject lines
* Review 1:1 pages regularly to identify trends or issues needing escalation

## Privacy & Permissions

* Employee pages: Visible to manager + that employee only (set during setup)
* Config: Stored securely and used only by this plugin's skills
* JIRA/Confluence/Email access: Requires the connectors you authorize during setup
* No data leaves your workspace: All processing happens locally in Claude

## Ready to Get Started?

For managers: Run the Setup Wizard skill to configure your team.

For employees: Ask "Prep my 1:1" to generate your first update.

For everyone: Let the skills run on schedule and enjoy your prepared 1:1 meetings!

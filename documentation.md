# PulseRook for Jira — User Documentation

## Getting Started

### Installation

1. Go to the **Atlassian Marketplace** and search for "PulseRook for Jira"
2. Click **Install** and authorize the required Jira permissions
3. Once installed, you'll see PulseRook in your Jira project sidebar
4. Click **PulseRook** to open the app
5. Select your project from the dropdown and click **Get Started**

### First-Time Setup (30-second onboarding)

1. Go to **Settings** tab
2. Under **SLA Rules**, set your SLA hours per priority level:
   - Highest: e.g., 4 hours
   - High: e.g., 8 hours
   - Medium: e.g., 24 hours
   - Low: e.g., 48 hours
   - Lowest: e.g., 72 hours
3. Click **Save SLA Rules**
4. (Optional) Scroll down to **Slack Integration** and paste a webhook URL if you want alerts
5. Done. Your SLA dashboard is now live.

---

## Tabs Explained

### 1. Overview Tab

**Your executive dashboard — the most important view.**

**Executive Health Score (top):** A single 0–100 score and letter grade (A–F) that blends:
- SLA compliance % (met vs. breached)
- Risk (% of tickets at risk)
- Mean time to resolution (MTTR)
- Reopen rate (how often closed tickets re-open)
- Workload (how many open tickets per team member)

**Metric Cards:** Below the gauge, see:
- **Total** = all issues in the project
- **Healthy** = on track to meet SLA
- **Moderate** = within 75% of SLA time
- **At Risk** = within 25% of SLA time, will breach soon
- **Breached** = SLA time already passed
- **Compliance %** = (Healthy + Moderate) / Total

**SLA Health by Group:** A table showing SLA metrics per Jira group (if your team members are added to Jira groups). Filter by group to drill into a specific team's health.

**7-Day Trend Chart:** Shows your compliance % over the last 7 days — is health improving or declining?

**How to use:** Share the screenshot of this tab with stakeholders. The health score tells the whole story instantly. Click any metric card to jump to that filtered list of issues.

---

### 2. Issues Tab

**Every issue in your project, with SLA data.**

Columns shown:
- **Issue Key** (clickable) — opens the issue in Jira
- **Summary** — issue title
- **Status** — current workflow status (To Do, In Progress, In Review, Done, etc.)
- **Priority** — Highest/High/Medium/Low/Lowest
- **Assignee** — who it's assigned to
- **SLA Status** — Met / Moderate / At Risk / Breached
- **Time Remaining** — hours left before breach (e.g., "3.2h remaining")
- **Time Elapsed** — how long it's been in the current status

**Sorting:** Click any column header to sort (e.g., click "Time Remaining" to see the closest-to-breach issues first).

**Filtering:** Use the Status / Priority dropdowns above the table to narrow the list.

**How to use:** Check this tab daily. Sort by "Time Remaining" to find what needs immediate attention. Click any issue to jump to Jira and take action.

---

### 3. SLA Tab

**Dedicated breach prediction view.**

**Breach Prediction Panel:**
- Shows all issues grouped by risk level: Healthy (green) / Moderate (blue) / At Risk (orange) / Breached (red)
- Each group shows count + % of total
- Click into a group to see the specific issues

**Risk-Scored Table:**
- List of all issues sorted by urgency (At Risk first)
- Shows issue key, summary, priority, assignee, time remaining
- Color-coded pills (green/blue/orange/red) for instant visual scanning
- Click any issue to open in Jira

**Root Cause Hints:** If available, shows a brief hint about why this ticket is at risk (e.g., "Status: In Review for 2 days").

**How to use:** Every morning, check the "At Risk" section. Assign resources to unblock the top 3–5 issues. Use this to prevent breaches, not respond to them.

---

### 4. Reports Tab

**Understand why you're missing SLAs.**

**"Why Are We Missing SLAs?" Diagnosis:**
- **Root Cause Analysis:** Automatically surfaces the top 3 drivers behind breaches:
  - "Status bottleneck: 8 tickets stuck in In Review" → Recommendation: increase review capacity
  - "Assignee overload: Jane has 14 open items, SLA avg 1.2h" → Recommendation: rebalance work
  - "Priority misclassification: 6 Medium items acting as Highest" → Recommendation: audit priority rules
  - "Slow first response: avg 6h to start work" → Recommendation: triage SLA
  - "Chronic backlog: 23 Lowest items never started" → Recommendation: capacity planning

**Priority Breakdown:**
- Count of Met / Breached / At Risk per priority level
- Helps you see if specific priorities are problematic (e.g., "Medium is failing, High is fine")

**Export:**
- **CSV Export:** Issue list with all SLA data for use in Excel or Slack
- **PDF Export:** Formatted report for stakeholder presentations (includes charts, metrics, top issues)

**How to use:** Review diagnoses weekly. Use the recommendations to guide team discussions. Export the PDF for monthly status reports to leadership.

---

### 5. Insights Tab

**Trends, patterns, and team health.**

**Weekly SLA Trend:** Chart showing compliance % for the past 4 weeks. Trending up = improving, trending down = risk.

**Risk Hotspots:**
- Which statuses have the most at-risk issues? (e.g., "In Review" is a bottleneck)
- Which priorities are underperforming? (e.g., "Highest has 80% breach rate")
- Which assignees have the most at-risk work? (early warning for overload)

**Assignee Performance Table:**
- Total issues, % met, % breached, average time-to-completion
- Helps identify who needs support or unblocking

**Reopen Rate:** % of closed issues that were re-opened. High reopen % suggests quality issues or incomplete work.

**How to use:** Use this in team retrospectives. If "Code Review" is a hotspot, discuss ways to speed up reviews. If one person has high reopen %, invest in pair programming or mentoring.

---

### 6. Settings Tab

**Configuration and permissions.**

**SLA Rules (Jira admin only):**
- Editable per-priority SLA hours (Highest / High / Medium / Low / Lowest)
- Click the number to edit; click **Save SLA Rules** when done
- Changes apply immediately to all issues

**Slack Integration (admin only):**
- **Webhook URL field:** Paste a Slack webhook URL (get this from Slack app management)
- **Test Connection:** Sends a test message to verify the webhook works
- **Enable Alerts:** Toggle to send near-breach and breach notifications to Slack (real-time)
- **Enable Daily Digest:** Toggle to send a daily summary at 9 AM in your timezone

**Manual Actions (admin only):**
- **Send Alerts Now:** Manually trigger breach/near-breach alerts (useful for testing or immediate escalation)
- **Send Digest Now:** Manually trigger the daily summary

**Permissions:**
- If you're not a Jira admin, the Settings tab shows read-only. You'll see a banner: "Read-only view. Jira admin permission required to change settings."

**How to use:** Jira admins: set up SLA rules on day one, then review quarterly. Connect Slack early so the team gets alerts. Non-admins: reference SLA rules here to understand the expectations.

---

## Common Workflows

### "I need to show SLA health to my boss"
→ Go to **Overview** → take a screenshot of the Health Score and Metrics → attach to your status report. Done.

### "We're missing SLAs. What do we do?"
→ Go to **Reports** → read the "Why Are We Missing SLAs?" diagnosis → act on the top recommendation (e.g., "unblock Code Review"). Recheck in 1 week.

### "Which issues will breach in the next hour?"
→ Go to **SLA** tab → sort by "Time Remaining" → look at the orange/red pills.

### "Jane's team is struggling. Which issues are theirs?"
→ Go to **Overview** → filter by the group in "SLA Health by Group" → see their metrics and breached items.

### "I want a report for stakeholders"
→ Go to **Reports** → click **PDF Export** → email it.

### "Slack isn't alerting us"
→ Go to **Settings** → Slack Integration section → click **Test Connection** → if red error appears, check your webhook URL. If green success, webhook is good.

---

## FAQ

**Q: How often is SLA data updated?**
A: In real time. Every time an issue status or priority changes, the SLA calculations update instantly.

**Q: Can I change SLA rules mid-project?**
A: Yes. Go to Settings, edit the hours, and click Save. The new rules apply to all issues from that point forward. Older issues keep their original thresholds for consistency.

**Q: What if an issue isn't in a Jira group?**
A: It won't appear in the "SLA Health by Group" panel. But it still counts toward overall project metrics.

**Q: Does PulseRook work with Service Desk?**
A: Yes. If you have Service Desk requests, they appear in PulseRook alongside standard issues.

**Q: Can I export SLA data for integration with other tools?**
A: Yes, use the CSV export in the Reports tab. You can then import into Excel, Tableau, Looker, etc.

**Q: What if I uninstall PulseRook?**
A: All your configuration (SLA rules, Slack webhook) is deleted within 30 days. Your Jira data is untouched.

**Q: Is there a mobile app?**
A: Not yet. The dashboard is responsive and works on mobile, but the experience is optimized for desktop.

**Q: Who can edit SLA rules?**
A: Only Jira admins and project admins. Regular team members see the Settings tab in read-only mode.

---

## Getting Help

- **Email:** support@pulserook.com
- **Response time:** We aim to respond within 24 hours
- **Status page:** Check [status.pulserook.com](https://status.pulserook.com) for any known issues

---

## Version

**PulseRook v1.0.0** — January 2026

Last updated: January 2026

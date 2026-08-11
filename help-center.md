# PulseRook Help Center & FAQ

---

## Installation & Setup

### How do I install PulseRook?

1. Go to the [Atlassian Marketplace](https://marketplace.atlassian.com)
2. Search for "PulseRook for Jira"
3. Click **Install**
4. Authorize the required Jira permissions
5. Open PulseRook in your Jira project sidebar
6. Select your project and go to **Settings** to configure SLA rules

### What permissions does PulseRook need?

PulseRook requests the following Jira scopes:
- **read:jira-work** — read issue data (status, priority, timestamps, assignee)
- **read:jira-user** — read user profiles and group membership
- **read:servicedesk-request** — read Service Desk requests (if applicable)
- **storage:app** — store your configuration (SLA rules, webhook URLs)

These permissions are required for the app to function. PulseRook does not access issue descriptions, comments, or other Atlassian products.

### Can I use PulseRook with multiple projects?

Currently, PulseRook monitors one project per Jira Cloud instance. Multi-project monitoring is on the v2.0 roadmap.

**Workaround:** If you need to monitor multiple projects, you'll need to install the app separately for each project.

### How long is the free trial?

30 days, with full access to all features. After 30 days, billing begins at $9/month per instance. You can cancel anytime.

---

## SLA Configuration

### How do I set up SLA rules?

1. Go to **Settings** tab (Jira admin access required)
2. Under **SLA Rules**, you'll see priority levels: Highest, High, Medium, Low, Lowest
3. Click on the hours for each priority to edit
4. Set your team's SLA hours (e.g., Highest = 4 hours, High = 8 hours, etc.)
5. Click **Save SLA Rules**

Rules apply immediately to all issues.

### Can I set different SLA rules per project?

Currently, SLA rules are global per Jira Cloud instance. If you need project-specific rules, this feature is planned for v2.0.

**Workaround:** Use priority-based rules as a proxy. If Project A always prioritizes differently, have your team adjust priority assignments.

### Can I have different SLA rules for Service Desk vs. regular issues?

Not yet. All SLA calculations use the same rules regardless of issue type. This is on the roadmap.

### What happens if I change SLA rules mid-project?

New rules apply immediately to all issues going forward. Issues that were already created use the rules in effect when they were created (for consistency).

---

## Health Score & Metrics

### How is the Executive Health Score calculated?

The score (0–100) blends five factors:
1. **SLA Compliance %** (40% weight) — % of issues that met their SLA
2. **Risk %** (20% weight) — % of issues currently at risk of breach
3. **MTTR** (15% weight) — mean time to resolution (lower is better)
4. **Reopen Rate** (15% weight) — % of closed issues that were reopened (lower is better)
5. **Workload** (10% weight) — average open issues per team member (lower is better)

**Grade scale:**
- 90–100: A
- 80–89: B
- 70–79: C
- 60–69: D
- 0–59: F

### What does "Moderate" mean in the metrics?

**Moderate** = the issue is within 75% of its SLA time but hasn't breached yet. It's on track, but monitor it.

Example: if an issue has a 24-hour SLA, "Moderate" means it has between 6–24 hours remaining.

### Why is my compliance % different from the Overview card and the trend chart?

They should match. If they don't, refresh the page. If the discrepancy persists, email support@pulserook.com.

---

## Group Filtering

### What is "SLA Health by Group"?

It shows SLA compliance metrics for each Jira group (team). You can filter the Overview dashboard by group to see one team's health in isolation.

### How do I add users to Jira groups?

In Jira, go to **Settings** → **User Management** → **Groups** and add users. PulseRook detects group membership and automatically surfacees the groups in the Overview tab.

### What if a user is in multiple Jira groups?

PulseRook assigns each user to their first group alphabetically. This ensures consistent, deterministic reporting.

Example: if Jane is in both "dev-team" and "qa-team", her issues count toward "dev-team" only.

---

## Slack Integration

### How do I connect Slack?

1. In Slack, create a Slack app (or use an existing one)
2. Under **Incoming Webhooks**, create a new webhook for a channel (e.g., #sla-alerts)
3. Copy the webhook URL
4. In PulseRook Settings, go to **Slack Integration**
5. Paste the URL and click **Test Connection**
6. If the test succeeds (green checkmark), enable **Alerts** and **Daily Digest**

### What gets sent to Slack?

- **Breach alerts:** When an issue breaches its SLA (real-time)
- **Near-breach alerts:** When an issue enters "At Risk" (within 25% of SLA time)
- **Daily digest:** Each morning, a summary of the previous day's SLA performance

Messages include issue key, priority, and breach status only — no sensitive comment data.

### Can I customize Slack messages?

Not yet. Messages are formatted automatically. Custom message templates are on the v2.0 roadmap.

### What if my Slack webhook stops working?

Slack may deactivate webhooks if they're unused for 30 days. If alerts stop, go to **Settings**, click **Test Connection**, and regenerate the webhook if needed.

### Can I send alerts to multiple Slack channels?

Currently, one webhook per PulseRook instance. To alert multiple channels, you can set up a Slack workflow to re-post messages from the primary channel.

---

## Reports & Exports

### How do I export SLA data?

1. Go to **Reports** tab
2. Scroll to the bottom
3. Click **CSV Export** (for Excel/analytics) or **PDF Export** (for presentations)
4. The file downloads immediately

### What's included in the CSV export?

- Issue key, summary, status, priority, assignee
- SLA status (Met / Moderate / At Risk / Breached)
- Time remaining (or time elapsed if breached)
- Priority level
- One row per issue

### What's included in the PDF export?

- Executive summary with health score and key metrics
- Priority breakdown chart
- SLA compliance trend (7-day)
- Top breached issues
- Root-cause diagnosis
- Assignee performance table

### Can I schedule automated exports to email?

Not yet. Export manually and email the PDF. Scheduled reports are planned for v2.0.

---

## Troubleshooting

### The dashboard shows "No data" or very low numbers. Why?

1. **Did you set SLA rules?** Go to Settings and configure SLA hours per priority. Without rules, no analysis runs.
2. **Do you have issues in your project?** If the project has 0 issues, there's nothing to monitor.
3. **Are you looking at the right project?** Check the project selector at the top of PulseRook.

### The Slack test shows an error. What do I do?

**Common errors:**
- "Invalid webhook URL" → Check that you copied the full URL from Slack (should start with https://hooks.slack.com/)
- "Channel not found" → Make sure the webhook points to a channel that exists and you have permission to post to
- "Unauthorized" → Check that the webhook is still active in Slack (webhooks can expire if unused for 30 days)

Try **Test Connection** again after fixing the URL.

### Why aren't my changes saving in Settings?

1. **Are you a Jira admin?** Only admins can edit SLA rules and Slack settings. If you see a "Read-only view" banner, you don't have permission.
2. **Are you clicking Save?** Changes don't persist until you click the Save button.
3. **Is there a red error message?** Read the message — it may explain what went wrong.

### The group dropdown is empty. Why?

**SLA Health by Group** only shows groups that have at least one user with an assigned ticket. If your groups exist but don't appear:
1. Make sure users in the group have open or closed issues assigned to them
2. Refresh the page
3. Check that users are actually added to the Jira group (Settings → User Management → Groups)

### Metrics aren't updating. The data looks stale.

1. Refresh the page (Ctrl+R or Cmd+R)
2. Wait a few seconds if you just made a change in Jira (PulseRook updates in real time, but may take a few seconds to reflect)
3. Check if there's a browser console error (F12, Console tab)

If issues persist, email support@pulserook.com with your project key and browser details.

---

## Account & Billing

### How do I upgrade after my free trial ends?

Nothing — billing begins automatically on day 31 of your trial. Charges are billed to your Atlassian account monthly.

### How do I cancel my subscription?

1. Go to your **Atlassian Marketplace** account
2. Find PulseRook under "Installed apps"
3. Click **Manage** or **Uninstall**
4. Follow the prompts

Cancellation takes effect at the end of your current billing cycle. No refunds for partial months.

### Can I get a refund?

Refunds are not available. However, you can cancel anytime, and charges stop at the end of your current cycle.

### Do you offer discounts for annual billing?

Not yet. We bill monthly at $9/instance. Annual pricing is on the roadmap.

### What happens to my data if I uninstall?

All PulseRook configuration (SLA rules, Slack webhook) is deleted within 30 days per Atlassian's retention policy. Your Jira data is untouched.

---

## Permissions & Security

### Who can use PulseRook?

Anyone with access to the project can view the dashboards (Overview, Issues, SLA, Reports, Insights). Only **Jira admins and project admins** can edit SLA rules and notification settings.

### How is my data secured?

- All data is stored in Atlassian Forge, which encrypts data in transit and at rest
- PulseRook does not store Jira issue descriptions, comments, or attachments
- Slack webhook URLs are stored securely and only used to post notifications you control
- No data is shared with third parties (only Slack, if you enable it)

### Does PulseRook access my password?

No. PulseRook uses Jira OAuth for authentication — you never provide your password.

### Is PulseRook GDPR compliant?

Yes. PulseRook complies with GDPR and only processes data necessary for SLA monitoring. See our [Privacy Policy](/privacy) for details.

---

## Performance & Limits

### Will PulseRook slow down my Jira?

No. PulseRook runs on Atlassian Forge, which isolates its compute from your Jira instance. You'll see no performance impact.

### How many issues can PulseRook handle?

PulseRook works with projects of any size. We've tested with 10,000+ open issues with no performance degradation.

### What's the maximum SLA hours I can set?

There's no hard limit, but we recommend staying under 1,000 hours (about 40 days) for practical purposes.

---

## Feature Requests & Roadmap

### How do I request a feature?

Email support@pulserook.com with your idea. We review all requests and include popular ones on the roadmap.

### What's coming in v2.0?

- Multi-project dashboard (one view across all projects)
- Health score trends over time
- Email digest option (in addition to Slack)
- Dark mode
- Per-project SLA rule isolation
- Scheduled report exports

### When is v2.0 releasing?

We don't have a confirmed date yet. Join our mailing list for updates.

---

## Contact & Support

**Email:** support@pulserook.com  
**Response time:** 24 hours (best effort)  
**Status page:** [status.pulserook.com](https://status.pulserook.com)

Still stuck? Email us with:
- Your Jira project key
- What you were trying to do
- What happened instead
- Any error messages shown

We'll get back to you within 24 hours.

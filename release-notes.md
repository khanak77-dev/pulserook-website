# PulseRook v1.0.0 — Release Notes

**Release Date:** January 2026

---

## Overview

PulseRook v1.0 is the inaugural release of a real-time SLA monitoring and breach prediction plugin for Jira Cloud. It delivers a complete, feature-rich dashboard for teams that need to monitor SLA compliance, diagnose root causes, and improve incident response.

**Status:** Production-ready, tested, stable.

---

## What's Included

### 1. Executive Dashboards (6 Tabs)

#### Overview Tab
- **Executive Health Score:** Single 0–100 score (A–F grade) blending compliance, risk, MTTR, reopen rate, and workload
- **Metric Cards:** Total / Healthy / At Risk / Breached / Compliance %
- **7-Day Trend Chart:** Compliance % trend (is your team improving?)
- **SLA Health by Group:** Filter by Jira group to drill into team-level performance
- **Color-coded UI:** Green (healthy) / Blue (moderate) / Orange (at risk) / Red (breached) for instant visual scanning

#### Issues Tab
- **Full issue list** with sortable columns: Key, Summary, Status, Priority, Assignee, SLA Status, Time Remaining
- **Filtering by Status and Priority** to narrow focus
- **Clickable rows:** Jump from the table to the actual Jira issue

#### SLA Tab (Breach Prediction)
- **Breach Prediction Panel:** Issues grouped by risk level with counts and percentages
- **Risk-Scored Table:** All issues sorted by urgency (At Risk first), color-coded risk pills
- **Time-to-Breach Indicator:** Hours remaining before each issue breaches its SLA

#### Reports Tab (Root-Cause Diagnosis)
- **Automatic Root-Cause Analysis:** Identifies the top 3 drivers behind missed SLAs (status bottlenecks, assignee overload, priority misclassification, slow first response, chronic backlog)
- **Actionable Recommendations:** Each root cause comes with a concrete suggestion to fix it
- **Priority Breakdown:** Met / Breached / At Risk counts per priority level
- **CSV Export:** Issue data for Excel or analytics tools
- **PDF Export:** Formatted report for stakeholder presentations (includes charts, metrics, top issues)

#### Insights Tab (Trends & Patterns)
- **Weekly SLA Trend:** 4-week compliance history
- **Risk Hotspots:** Which statuses and priorities are problematic
- **Assignee Performance:** Total issues, % met, % breached, average time-to-completion
- **Reopen Rate:** % of closed issues that were reopened (quality indicator)

#### Settings Tab (Configuration)
- **SLA Rules Editor:** Set custom SLA hours per priority level (Highest / High / Medium / Low / Lowest)
- **Slack Integration:** Webhook URL configuration, test connection, toggle alerts and digests
- **Manual Actions:** Send alerts now / send digest now (useful for testing or escalation)
- **Admin-Only Access:** Permission gating ensures only Jira admins can edit settings

### 2. SLA Rules Engine

- **Custom Per-Priority Rules:** Set your own SLA hours for each priority level
- **Instant Application:** Rules apply to all issues immediately after save
- **No Coding Required:** Simple numeric input, no custom expressions
- **Deterministic:** All calculations are rule-based, explainable logic (no AI, no black boxes)

### 3. Real-Time Breach Prediction

- **Risk Scoring:** Every issue gets a risk level based on elapsed time, priority, and status
- **Risk Levels:** Healthy / Moderate / At Risk / Breached (color-coded)
- **Time-to-Breach Countdown:** Shows hours remaining before each ticket breaches
- **Near-Breach Alerts:** Issues within 25% of SLA time are flagged as "At Risk"

### 4. Root-Cause Diagnosis

Automatic analysis that surfaces why SLAs are being missed:
- **Status Bottleneck:** Issues stuck in a specific status (e.g., "In Review") for too long
- **Assignee Overload:** Team members with too many open items relative to their SLA targets
- **Priority Misclassification:** Items marked as lower priority acting as higher priority
- **Slow First Response:** First response time is a bottleneck
- **Chronic Backlog:** Low-priority items never getting started

Each diagnosis includes a recommendation (e.g., "increase review capacity").

### 5. Slack Integration

- **Webhook-Based Alerts:** Configure a Slack webhook URL (no Slack app installation required)
- **Breach Alerts:** Real-time notification when an issue breaches its SLA
- **Near-Breach Alerts:** Warning when an issue enters "At Risk" status
- **Daily Digest:** Morning summary of the previous day's SLA performance (9 AM in your timezone)
- **Manual Triggers:** Send alerts or digests on demand for testing or escalation
- **Test Connection:** Verify the webhook works with a test message

### 6. SLA Health by Group

- **Jira Group Filtering:** Drill into SLA metrics for a specific Jira group (team)
- **Group-Level Metrics:** Total / Healthy / At Risk / Breached / Compliance % per group
- **Automatic Discovery:** PulseRook detects all groups and shows only those with tickets assigned
- **Multi-Group Membership:** Uses alphabetical tie-break for deterministic assignment

### 7. Reporting & Export

- **CSV Export:** Raw issue data (key, summary, status, priority, SLA status, time remaining)
- **PDF Export:** Formatted report with charts, metrics, top issues, recommendations
- **No Manual Formatting:** Exports are ready to share with stakeholders

### 8. Admin-Only Permissions

- **Settings Protection:** Only Jira admins and project admins can edit SLA rules and Slack settings
- **Read-Only Mode:** Non-admin users see all dashboards but cannot edit configuration
- **Clear UI:** Admins see full controls; non-admins see a "Read-only view" banner
- **Server-Side Enforcement:** Permissions are enforced on the backend, not just the UI

---

## Technical Details

### Architecture
- **Platform:** Atlassian Forge (React 16, Node.js)
- **Storage:** Atlassian Forge storage API (encrypted at rest)
- **Scopes Used:** read:jira-work, read:jira-user, read:servicedesk-request, storage:app
- **External Services:** None (except optional Slack webhooks for notifications)
- **No External AI:** All analysis is rule-based, deterministic JavaScript

### Performance
- **Real-Time Updates:** Issue changes reflect in dashboards within seconds
- **Lightweight:** Runs on Forge with no performance impact on your Jira instance
- **Scalability:** Tested with 10,000+ issues per project

### Security & Privacy
- **Data Encryption:** Atlassian Forge handles encryption in transit and at rest
- **No Data Extraction:** Issue descriptions, comments, and attachments are not accessed
- **Admin-Only Config:** Settings changes require Jira admin permission
- **Slack URLs Secured:** Webhook URLs are stored securely and only used for notifications
- **GDPR Compliant:** See Privacy Policy for details

---

## Known Limitations

1. **Single-Project Monitoring:** Currently monitors one project per Jira Cloud instance. Multi-project dashboard is on the v2.0 roadmap.
2. **Global SLA Rules:** Rules are global per instance, not per-project. Per-project rules are planned for v2.0.
3. **Slack Webhook Manual Setup:** Webhook URLs must be created manually in Slack. Slack OAuth app integration is planned for v2.0.
4. **No Service Desk Customization:** Service Desk issues are supported but use the same SLA rules as standard issues.
5. **Email Digest Not Yet Available:** Daily digest is Slack-only in v1.0. Email digest is planned for v2.0.

---

## What We Learned Building v1.0

We built this plugin to solve a real problem: teams using Jira don't know they're missing SLAs until it's too late. Existing solutions are expensive, opaque (AI-driven), or require moving data off Atlassian's cloud.

PulseRook is different:
- **Simple:** No configuration beyond SLA hours and (optionally) a Slack webhook
- **Fast:** All logic is rule-based, so calculations are instant
- **Trustworthy:** No external API calls, no data extraction, no black boxes
- **Fair:** Flat pricing per instance, no per-user seats, no per-call metering

This v1.0 is the foundation. Future versions will add multi-project support, trends, and deeper analytics. But the core—knowing your SLA risk in real time—is here and ready to use.

---

## v2.0 Roadmap (Coming 2026)

We're planning the following for v2.0:

- **Multi-Project Dashboard:** One view across all Jira projects in your instance
- **Health Score Trends:** See how your health score is improving (or declining) week over week
- **Per-Project SLA Rules:** Different SLA thresholds for different projects
- **Email Digest:** In addition to Slack, send daily summaries via email
- **Dark Mode:** For users who prefer low-light interfaces
- **Slack OAuth Integration:** Easier setup without manual webhook copy-paste
- **Quantified Recommendation Outcomes:** Track how recommendations impact your SLA performance
- **Advanced Scheduling:** Schedule when alerts and digests should fire
- **Custom Reports:** Build your own reports with saved filters and export templates

---

## How to Get Started

1. **Install:** Go to the Atlassian Marketplace, search "PulseRook," and click Install
2. **Configure:** Go to Settings, set your SLA hours per priority, save
3. **Monitor:** Open the Overview tab and start watching
4. **(Optional) Connect Slack:** Paste a webhook URL in Settings to enable alerts
5. **Share:** Take a screenshot of the Health Score and send it to stakeholders

**Free 30-day trial. Then $9/month. Cancel anytime.**

---

## Support & Feedback

- **Questions?** Email support@pulserook.com
- **Found a bug?** Email support@pulserook.com with details
- **Feature request?** Email support@pulserook.com with your idea
- **Documentation:** Full user guide at [docs.pulserook.com](https://docs.pulserook.com)
- **Status page:** Check [status.pulserook.com](https://status.pulserook.com) for any incidents

We read every email and prioritize based on customer feedback.

---

## Thank You

Thank you for trying PulseRook. We hope it helps your team master SLA compliance and deliver better incident response.

Questions or ideas? We're here to help.

**PulseRook Team**

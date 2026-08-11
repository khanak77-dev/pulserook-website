# Privacy Policy — PulseRook for Jira

**Last updated: January 2026**

## 1. What this app does

PulseRook for Jira ("the App") is a Jira Cloud plugin that monitors SLA compliance for issues in projects where it is installed. It runs entirely within Atlassian's Forge platform and processes data on your Jira instance.

## 2. Data we access

The App requests the following Jira scopes:

- `read:jira-work` — read issue data (key, status, priority, timestamps, assignee)
- `read:jira-user` — read user profiles and group membership
- `read:servicedesk-request` — read Service Desk request data (if applicable)
- `storage:app` — store your configuration (SLA rules, notification settings, webhook URLs)

This allows the App to calculate SLA compliance, predict breaches, diagnose root causes, and store your settings using Atlassian Forge's built-in storage API.

## 3. Data we do NOT access

- Issue description text, comments, or attachments (unless needed for status/priority)
- Other Atlassian products (Confluence, Bitbucket, etc.)
- Personal data beyond what's needed to identify assignees and groups
- Any external AI or machine-learning services — all analysis runs as deterministic logic inside the App

## 4. Where data is stored

All configuration data (SLA rules, Slack webhook URLs, notification preferences) is stored using Atlassian Forge's `storage:app` API. This keeps data within Atlassian's infrastructure, scoped to your Jira instance. We do not operate our own database or servers.

Issue data (status, priority, assignee, timestamps) is read from your Jira instance on demand and is not stored by the App beyond the duration of the request.

## 5. Third-party sharing

The only external service the App communicates with is **Slack**, and only if you explicitly configure a Slack webhook URL in Settings. In that case:

- SLA alert and digest messages are sent to the webhook URL you provide
- Messages include issue keys, priorities, and breach status
- No personal data is sent to Slack unless included in issue metadata
- You control the webhook entirely — if you delete it, messages stop

**We do not sell, share, or transfer your data to any other third party.**

## 6. Data retention & deletion

Configuration data persists only as long as the App is installed on your Jira site. Uninstalling the App removes its stored configuration data via Forge's storage lifecycle.

Issue data is never stored — it is read from Jira on each analysis and discarded after the analysis completes.

## 7. Your rights

You have the right to:
- Request a copy of the data the App has stored (your SLA rules and settings)
- Request deletion of all configuration data by uninstalling the App
- Disable the Slack integration at any time by removing the webhook URL
- Disable email or daily digest notifications at any time in Settings

To exercise these rights, email **support@pulserook.com** with your request.

## 8. Security

PulseRook relies on Atlassian Forge's built-in security, which includes:
- Data encryption in transit (TLS/HTTPS)
- Data at rest encryption managed by Atlassian
- Authentication via Jira user accounts
- Role-based access control (Jira admins only for Settings)

We do not store passwords or authentication tokens.

## 9. Changes to this policy

We may update this policy from time to time. Changes take effect immediately upon posting to this page. Continued use of the App after changes constitutes your acceptance of the updated policy.

## 10. Contact

Questions about this policy or your data? Email **support@pulserook.com**.

For Atlassian-related privacy concerns, see [Atlassian's Privacy Policy](https://www.atlassian.com/legal/privacy-policy).

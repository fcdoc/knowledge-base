---
brief: Through the use of webhooks, synchronize Jira Issue events with Kuaimao Nebula to collect change events.
---

# Jira Integration

## Usage Restrictions

### In Jira

- You must have the authority to modify **Settings => System => Webhooks**.
- (For on-premises deployment) Your Jira server must be able to access the domain api.flascat.cloud.

## Supported Versions
---

This guide is compatible with **Jira Cloud and On-Premises** versions.

## Operation Steps
---

### In Flashduty

1. Enter the Flashduty console, select **Integration Center => Change Events**, and navigate to the integration selection page.
2. Choose the **Jira** integration:
- **Integration Name**: Define a name for the current integration.
3. Click **Save**, then copy the newly generated **Push Address** on the current page for future reference.
4. Completed.

### In Jira

<div id="!"><ol><li>Login your Jira</li><li> Enter **Settings = >System = >Webhooks** page, click Create button</li><li> Fill in the callback address as the push address corresponding to the current integration, and check Issue Created/Updated/Deleted three types of events</li><li> You can choose to fill in JQL to further narrow down (such as specific Projects ) the scope of events to be synchronized</li><li> Click the Save button to submit the configuration</li></ol>![drawing](https://fcdoc.github.io/img/B6IhBdbjTowcYF9BrtI8yg1Zd8GUkJkCmDOleGUd7PE.avif)<ol start="5"><li> Finish</li></ol></div>

## Status Mapping
---

<div class="md-block">

| Jira        | Flashduty   | state               |
| ----------- | ---------- | ------------------ |
| planned     | planned    | Bill Submitted             |
| to do       | planned    | Bill Submitted             |
| ready       | ready      | Soon to Start (or Planned) |
| processing  | processing | In Progress             |
| open        | processing | In Progress             |
| reopen      | processing | In Progress             |
| in progress | processing | In Progress             |
| canceled    | canceled   | Canceled (or Rolled Back)   |
| aborted     | canceled   | Canceled (or Rolled Back)   |
| done        | done       | Completed             |
| resolved    | done       | Completed             |
| closed      | done       | Completed             |

If you wish to modify this mapping, please reach out to Flashduty for assistance.</p>
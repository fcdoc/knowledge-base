---
brief: A fault in Flashduty represents an ongoing issue or an item requiring attention. Faults are typically initiated by alarms, often in conjunction with a series of related alarms.
---

# What Is a Fault

---

A fault signifies an ongoing issue or an item requiring attention. Faults are generally set off by alarms, frequently accompanied by a sequence of similar alarms.

## Faults, Alarms, and Events
---

When Flashduty receives an alarm event (such as an alarm notification from Zabbix), the system will automatically trigger an alarm, and this alarm will trigger a fault. Multiple similar active alarms may be aggregated into the same fault and dispatched, notified, and processed together.

We can simply understand that **a fault is a compilation of similar alarms**. Without noise reduction, a fault is equivalent to an alarm. Conversely, in a noise-reduction scenario, a fault is equivalent to the associated multiple alarms. For more information on the alarm noise reduction model, please refer to [Understanding the Noise Reduction Process](doc-4185939).

## Fault Severity, Status, and Progress
---

### Severity

- **Info**: Minor; the service is still operating normally; this is merely a service status alert, and no immediate action is required.
- **Warning**: Caution; the service may be experiencing issues or is on the verge of problems; early intervention is recommended to prevent escalation.
- **Critical**: Severe; the service is widely affected or even disrupted; users are impacted, and immediate intervention is necessary.

Faults, alarms, and events all utilize the above three severity levels. **The first letter of the severity level is capitalized**. Pay close attention to this when using the API. The rules for generating the severity levels for the three are as follows:

- **Event Severity**: Alarm events from various integration sources (such as Zabbix and Nightingale) have different severity enumeration values. Flashduty maps them to the above three standard severity levels according to specific rules. For the specific mapping relationships, please consult the access documentation for the relevant integration.
- **Alarm Severity**: Equivalent to the highest severity level among the associated events.
- **Fault Severity**: Equivalent to the highest severity level among the associated alarms.

### Processing Progress

- **Pending**: After a fault is triggered, the default processing status is "Pending". The system will automatically dispatch, assign handlers, and notify them.
- **Processing**: If anyone clicks **Claim Fault**, the processing status will immediately change to "Processing". In this scenario, the fault handler may be in the **Claimed** or **Unclaimed** state, but at least one person must be in the "Claimed" state. When all handlers **cancel the claim**, the fault handling progress will revert to "Pending".
- **Closed**: If anyone clicks **Close Fault** or **Fault Auto-Recovery**, the processing status will immediately change to "Closed".

### Fault Status

The status of an alarm represents the status of the fault in the original monitoring system, i.e., "Recovered" or "Unrecovered". The status of a fault is entirely determined by its associated alarms.

- **Recovered**: All associated alarms have been resolved, and the fault will automatically recover.
- **Unrecovered**: At least one associated alarm has not been resolved, and the fault will remain in an unrecovered state.


:::🔹 Highlight: Orange 💡
Automatic fault recovery will automatically close the (processing progress); however, manual fault closure has no effect on the fault status.
:::


## Fault Tag
---

Labels are a very important basic concept in Flashduty. Different labels describe information about alarms and faults in different dimensions, and are widely used in filtering, retrieval, aggregation and other scenarios.

**How are tags generated?**

Alarm tags are extracted from the event message body reported by the original alarm system. Different sources employ different extraction methods. Generally, we adhere to the principle of **extracting as much as possible**. For instance, for alarm events from Prometheus, Flashduty extracts the Labels and Annotations information from the Payload.

Tags can only be obtained through event reporting and cannot be manually modified or added. The label of an automatically triggered fault is always equal to the label of the first associated alarm. A manually triggered fault's label will always be empty.

Flashduty offers a label enhancement solution for automated label generation. For more information, visit [Configure Label Enhancement](http://docs.flashcat.cloud/zh/flashduty/label-enrichment-settings).

## Fault Life Cycle
---

**1. Trigger a New Fault**

**Automatic Triggering**: When Flashduty receives an alarm event reported by an integration (such as a Zabbix notification), the event automatically triggers an alarm, which then automatically triggers a fault.

**Manual Triggering**: Manually create a fault in the Flashduty console by clicking the **Create Fault** button, filling in the title, description, severity, and other information to trigger a new fault.

**2. Distribution and Notification**

After a new fault is triggered, Flashduty will sequentially match the dispatch strategy under the relevant collaboration space. Once a dispatch strategy is matched, the system will assign the fault to individuals, team members, or on-duty personnel and notify them. **If no dispatch strategy is matched, the fault will not be assigned to anyone, and no notification will be sent**.

You can set different dispatch strategies for different time periods or types of faults to achieve flexible distribution. The system allows you to set up multiple dispatch stages within a single dispatch strategy. If the assigned personnel for the current stage do not complete the confirmation and processing of the fault within the specified time, the system will automatically escalate to the next stage. Escalation is equivalent to reassigning the fault to another person.

You can flexibly arrange notification methods within the dispatch strategy. Flashduty supports a wide range of group chat and one-on-one notification channels. One-on-one chat is a direct push channel (such as voice, text message, and email), while group chat pushes messages to a message group (such as Feishu, DingTalk, and Slack) and provides additional reminders to the assigned personnel.

:::🔹 Highlight: Orange 💡
Note that **notifications will only be sent after a fault is dispatched**. Without dispatch, there will be no notifications.
:::

If a fault is assigned to a duty list (rota) with no on-call personnel, the system will not notify any individual. However, if a group chat channel is configured, messages will still be sent to the group chat.

**3. Claim and Resolve**

On-call personnel can immediately claim the fault after receiving the notification. You can claim the fault via **voice call** or **instant message**. After claiming, the fault handling progress will change to **Processing**.

:::🔹 Highlight: Orange 💡
Flashduty currently does not limit faults to only being claimed by "assigned handlers". Anyone who can see the fault can click to claim it.
:::

**Closing a fault** will change the processing progress to **Closed**. If the associated alarms are automatically recovered, the fault will also be automatically closed. Conversely, if a fault is manually closed, all associated alarms will be automatically closed. This means that these alarms will no longer be merged into any new events.


## Fault Timeline
---

Each fault has a timeline that allows you to trace the changes and operations that have occurred at different times in the fault's history. For example, at what time the fault occurred, who was notified through which channel, and the outcome of the notification.

![](https://fcdoc.github.io/img/7vOIcjGm9D-jdoK4WtKCTV63KSPRW6vXBCpZwzU3vNo.avif)

## Trigger Fault
---

### Trigger Fault via Integration

Flashduty supports most common monitoring systems, including Prometheus, Zabbix, Nightingale, and cloud monitoring, among others. For specific steps, please refer to [Alarm Integration](https://docs.flashcat.cloud/zh/flashduty/nightingale-integration-guide).

:::🔹 Highlight: Orange 💡
Flashduty supports both dedicated integration and shared integration models. Alarms delivered to dedicated integrations within a collaboration space will trigger faults within that space.
Alternatively, alarms can be delivered to the shared integration in the integration center, and then configured to route alarms to different collaboration spaces according to rules.
:::

### Triggering Faults via API

Flashduty provides a custom event standard that allows you to report alarms via a standard protocol, suitable for any unadapted monitoring system. For detailed documentation, please read [Custom Events](https://docs.flashcat.cloud/zh/flashduty/custom-alert-integration-guide).

:::🔹 Highlight: Orange 💡
To ensure the stability of the entire system, Flashduty currently imposes a **200qps** frequency limit on API reporting. Exceeding this limit will result in the rejection of reports.
:::

:::🔹 Highlight: Orange 💡
Please ensure that you actively close alarms, or set the fault timeout to automatically close in the collaboration space. An excessive number of faults can significantly degrade console search performance. In such cases, the system may close historical faults without any notification.
:::

### Trigger Fault via Email

Flashduty provides an email integration that allows you to report alarms by sending emails. It is suitable for all monitoring systems that support email reminders. For detailed documentation, please read [Custom Events](https://docs.flashcat.cloud/zh/flashduty/email-integration-guide).

:::🔹 Highlight: Orange 💡
You can set specific email prefixes for each integration. You can also contact us to set an easy-to-remember exclusive domain name for your main account. For example, order-service@tesla.flashcat.cloud.
:::


### Trigger Fault via Console

Click the **Create** button on the console to initiate fault creation.

| Field | Is it necessary | Description |
| :---: | :---:   | ---- |
| Fault title | yes | A brief statement indicating what has occurred |
| Fault description | no | Detailed description of the fault, supporting Markdown syntax |
| Severity | yes | Select one of the three enumeration values: Critical, Warning, and Info |
| Collaborative space | no | Fault attribution; if not selected, it represents a global fault. In this case, the fault must be assigned directly to a person to notify |
| Assign personnel | no | Troubleshooting personnel; if not selected, will be matched and assigned according to the collaboration space they belong to, otherwise they will be notified directly according to personal preferences |
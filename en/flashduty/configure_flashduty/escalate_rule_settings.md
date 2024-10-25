---
brief: Alarm events from various businesses or teams can be assigned to the corresponding handling groups through dispatch strategies, ensuring that the relevant handlers are reached via different communication channels
---

# Configure Dispatch Strategy

---

Each collaborative workspace should have at least one dispatch policy in place. Through this policy, alarms from different businesses or teams can be directed to the appropriate handling groups, and the responsible members can be notified through various means such as IM apps, SMS, voice messages, and robots. Additionally, it supports multi-stage notification configurations and automatic progression between stages. If no dispatch policy is configured for a collaborative workspace, incoming alarms will not trigger any notifications.

## Policy Configuration
---
### Time Filtering
- By default, all faults are notified according to this policy at any time.
- It supports selecting whether to dispatch based on specific days of the week, for instance, only handling faults from Monday to Friday, with Saturday and Sunday exceptions.
- It supports dispatch selection based on the service calendar (which needs to be created beforehand), allowing configuration according to holidays or working days, such as notifying only on trading days, which is common in the securities industry.

![rilitongzhi.png](https://fcdoc.github.io/img/gsUqruaXsUQO8Vbb-QgEIJb23EQ3jUZDMWBvtOYSEBs.avif)

### Fault Filtering
- By default, all faults are notified in accordance with this policy.
- It supports conditional matching of faults by title, level, and tags, for example, following the dispatch for alarms with a level of "Info."

![tiaojian.png](https://fcdoc.github.io/img/WyGIe6d3UjoWaGg4Y8KCZ87KCalIEM3cdR1YMRI6RVc.avif)

Visit [How to Configure Filter Conditions](https://docs.flashcat.cloud/zh/flashduty/how-to-filter) for more information.

## Dispatch configuration
---

### Dispatch Object
- **Individual:** Specify certain members to receive the alarm, with support for multiple selections and no duplicates allowed.
- **Team:** Specify a team to receive the alarm, with support for multiple selections. If there are duplicate team members, only one notification will be sent to each member.
- **Duty:** Specify a duty schedule to receive the alarm, with the specific recipients determined by the duty rules. Multiple selections are supported, and duplicate duty personnel will only receive one notification.
- **Combination:** Select a combination of individuals, teams, and duty schedules.

:::tip
Looking to integrate with internal self-developed systems for dynamic dispatching?

Refer to [Dynamically Setting Dispatch Personnel](https://docs.flashcat.cloud/zh/flashduty/dynamic-notifications).
:::

### Single Chat Channel
Single chat refers to one-on-one notifications, such as through email, SMS, voice, and certain IM applications.

- **Follow Personal Preferences:** Notification methods are determined by members based on their [account settings for each alarm category's receiving channels and methods](https://docs.flashcat.cloud/zh/flashduty/preference-settings).
- **Follow Unified Settings:** Notification recipients' channels and methods are configured uniformly by the policy setter.

### Group Chat Channel

Group chat involves sending notifications to a group with special mentions for dispatch personnel, including various webhook robots and some IM applications.

- In group chats, you can choose how to reach recipients through different applications and group robots. **When selecting IM app notifications**, the notification recipient must first link to the corresponding application. See [Instant Messaging Integration](https://docs.flashcat.cloud/zh/flashduty/lark-integration-guide) for details

:::tip

Select at least one notification channel for personal and group chats. If you prefer not to notify individuals, only groups, you can set an empty team as the dispatch target.

:::

### Cyclic Notification

- Cyclic notifications are disabled by default, meaning that the same event is notified only once. If enabled, configure the number of notifications appropriately. Note that you must enter a value of at least `2` to receive additional cyclic notifications.
- If a fault is claimed, cyclic notifications will cease.


### Upgrade Dispatch

- To ensure that faults are addressed, set automatic upgrades for faults that are not closed or claimed within a timeout. This involves setting up multiple stages.
- You can choose to automatically upgrade when a fault is `not closed within the timeout` or `not claimed within the timeout`.
- Typical scenarios include hierarchical upgrades between primary and backup duty personnel, between superiors and subordinates, and between first and second lines of support.

You can also manually upgrade faults; visit [Upgrade and Dispatch Faults](https://docs.flashcat.cloud/zh/flashduty/escalate-incidents) for more information.

### Strategy Sequence Adjustment
- When multiple dispatch strategies are in place, notifications are matched sequentially and stop once a match is found. Consider the relevant dispatch conditions thoroughly when configuring.
- Different strategies can be adjusted by dragging and dropping to change the notification order, with changes taking effect immediately. Please proceed with caution.

:::tip
If you need to set up multiple dispatch strategies in a collaborative workspace and ensure that every fault is notified, it's advisable to have a fallback strategy with no filtering criteria.
:::

:::caution
We do not recommend setting up an overly large collaborative workspace, especially when managing alerts for a large-scale business. This can lead to the maintenance of numerous dispatch strategies, increasing the long-term maintenance burden, confusion, and the likelihood of errors.
:::


## Policy Configuration Principles
---
General principles for configuring dispatch strategies should consider the following aspects:

1. **Matching Notification Object Capabilities:** Ensure that notification objects have the ability and authority to handle alerts within the space. This means that only relevant individuals or teams should receive alerts related to their work, avoiding the delivery of irrelevant alerts to unrelated individuals.
2. **Multi-channel Notification:** Utilize multiple notification methods to ensure that notification objects receive alerts promptly. For example, use various channels such as SMS, email, and instant messaging tools to improve the timeliness and reliability of notifications. However, different notification methods are recommended for different alert levels to prevent information overload.
3. **Alarm Escalation Mechanism:** When an alert remains unclaimed or unhandled for an extended period, an escalation mechanism should be in place. This could involve automatically escalating the alert to the next level of handler or team or sending the alert to multiple handlers to ensure timely resolution.


## FAQs
---

<details><summary>How to troubleshoot if an alarm occurs but no notification is received</summary>Go to Fault Details => Timeline to check the status of each channel in the notification process. If a failure occurs, there will be a failure message for reference. For more reasons, you can contact technical support for assistance with troubleshooting.</details>

<details><summary>Why don't my notification methods match my personal preferences?</summary> Flashduty The single chat notification channel supports two settings, one is "Follow personal preferences" and the other is "Follow unified settings". Only in the "Follow personal preferences" setting, notifications will be personalized according to your settings.<p> Go to Collaboration Space Details = > Policy to view your specific settings.</p></details>
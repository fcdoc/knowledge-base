---
brief: Push proprietary system alert events to Flashduty via standard protocols to automate noise reduction processing for these alerts.
---

# Custom Alert Event Integration Guide

---

Push proprietary system alert events to Flashduty via standard protocols to automate noise reduction processing for these alerts.

:::tips
Flashduty is compatible with the webhook protocols of most commonly used alert systems. For these systems, you should use the corresponding integration first, as it is simpler and more convenient. This integration provides a standard HTTP interface, allowing you to develop adaptations. The benefit is that you can push any alert event you wish to be handled by oncall.
:::

## Operation Steps
---

### In Flashduty

You can obtain a push address for integration through the following two methods, choose one that suits you.

#### Use a Dedicated Integration

Choose this method if you do not need to route alert events to different collaboration spaces, as it is more straightforward.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</li><li> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</li><li> Select **Prometheus** Integrate, click **Save** , and generate the card.</li><li> Click on the generated card to view **the push address** , copy it for later use, and complete.</li></ol></details>

#### Use a Shared Integration

Opt for this method when you need to route alerts to different collaboration spaces based on the payload information of the alert event.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **custom event** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>


## Implement Protocol
---

Please refer to [the development documentation](https://developer.flashcat.cloud/zh/flashduty/custom-alert) to complete the protocol development.

## Best Practices
---

1. When an alert status changes, send an event to Kuaimao Nebula
2. When an alert is resolved, send an event with a status of "Ok" to close the alert. Otherwise, the alert will remain open. If your alert system does not have a resolution event, it is recommended that you manually send a resolution event
3. The label is a description of the event. Enrich the label content as much as possible (specified when sending, or generated through configuration enrichment rules), such as:
- The source of the alert, such as host, cluster, check, or metric, etc
- Ownership information of the alert, such as team, owner, etc
- Category information of the alert, such as class (API, database, network)


## FAQs
---

<details><summary>Why didn't I receive the alert Flashduty !?</summary><h4> exist Flashduty</h4><ol><li> Check if the integration shows **the latest event time** ? If not, it means Flashduty has not received the push, and your system will be prioritized directly.</li><li> If you are using **shared integration** , first confirm whether you have configured **routing rules** . If you do not set routing rules, the system will directly reject new pushes because there is no collaboration space to receive your alerts. In this case, just configure the routing rules directly to the space you want.</li></ol><h4> in your system</h4><ol><li> Confirm that the address you requested exactly matches the address in the integration details.</li><li> Confirm that your service can access the external network api.flashcat.cloud domain name. If not, you first need to open an external network for server , or separately enable external network access for the Flashduty domain name.</li><li> Print the response result of the Flashduty service to see if there is clear information.</li></ol><p> If the root cause of the problem is still not found after performing the above steps, please contact us **with the request_id in the request response** .</p></details>
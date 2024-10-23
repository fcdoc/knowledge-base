---
brief: Push proprietary system change events to Flashduty via standard protocols. Most failures are caused by these changes, and the correlation between change and alert events aids in swiftly identifying the root causes of failures.
---

# Custom Change Event Integration Guide

---

Push proprietary system change events to Flashduty via standard protocols. Most failures are caused by these changes, and the correlation between change and alert events aids in swiftly identifying the root causes of failures.

:::tips
Flashduty has already adapted to the webhook protocols of some common ticketing and deployment systems. For these systems, you should first utilize the corresponding integrations, which are more straightforward and convenient. This integration provides a standard HTTP interface, allowing you to develop custom adaptations. The advantage is that you can integrate with any deployment system.
:::

## Operation Steps
---

### In Flashduty

1. Enter the Flashduty console, select **Integration Center => Change Events**, and navigate to the integration selection page.
2. Select the **Custom Event** integration:
- **Integration Name**: Define a name for the current integration.
3. Click **Save**, then copy the newly generated **Push Address** on the current page for future reference.
4. Completed.


## Implement Protocol
---

Please refer to [the development documentation](https://developer.flashcat.cloud/zh/flashduty/custom-change) to complete the protocol development.

## Best Practices
---

Tags are descriptive elements of events and should be as detailed as possible, including:
1. The scope of the change, such as host, cluster, etc
1. Ownership information of the change, such as team, owner, etc

## FAQs
---

<details><summary>Why didn't I receive the changes in Flashduty ?</summary><h4> exist Flashduty</h4><ol><li> Check if the integration shows **the latest event time** ? If not, it means that Flashduty has not received the push, and the Nightingale part will be directly checked first.</li></ol><h4> in your system</h4><ol><li> Confirm that the address you requested exactly matches the address in the integration details.</li><li> Confirm that your service can access the external network api.flashcat.cloud domain name. If not, you first need to open an external network for server , or separately enable external network access for the Flashduty domain name.</li><li> Print the response result of the Flashduty service to see if there is clear information.</li></ol><p> If the root cause of the problem is still not found after performing the above steps, please contact us **with the request_id in the request response** .</p></details>
---
brief: Synchronize Influxdata alert events to Kuaimao Xingyun via webhook to automate noise reduction processing of alerts
---

# Influxdata Integration

---

Synchronize Influxdata alert events to Flashduty via webhook to automate noise reduction processing of alerts.


## Within Flashduty
---
You can obtain an integrated push address using two methods; you may choose either one.

### Use Exclusive Integration

When there is no need to route alert events to different collaboration spaces, this method is recommended for its simplicity.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Influxdata** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integration

When you need to route alerts to different collaboration spaces based on the payload information of the alert event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Influxdata** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## In Influxdata
---
<div id="!"><ol><li>Log in to your Influxdata console and go to the Alerting > Alert Rules page</li><li> Click on the alarm rule that needs to be synchronized, enter the Alert Rule Builder page, and start editing the rules.</li><li> Alert Handlers Part, Select Add Another Handler , select post as type, HTTP endpoint fill in the integrated push address, as shown in the figure below:</li></ol><p>![influxdb-alert-rule](/0)</p><ol start="4"><li> Save Rule the button to save. Wait for the event to be triggered. If the latest event time is displayed in the integration list, it means the configuration is successful and the event is received.</li><li> Finish</li></ol><h2> Status comparison</h2><hr><div id="!"><p> Influxdata relationship between alarm Flashduty and alarm levels:</p>

| Influxdata |  Flashduty  | Status |
| ---------- | -------- | ---- |
| CRITICAL   | Critical | Critical |
| WARNING    | Warning  | Warning |
| INFO       | Info     | Reminder |

</div>
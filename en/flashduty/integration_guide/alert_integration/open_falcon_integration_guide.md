---
brief: Synchronize Open-Falcon alert events to Flashduty via webhook to automate noise reduction processing
---

# Open Falcon Integration

---

Synchronize Open-Falcon alert events to Flashduty via webhook to automate noise reduction processing.
## In Flashduty
---
You can obtain an integrated push address using two methods; choose either one.

### Use a dedicated integration

When there's no need to route alert events to different collaboration spaces, this method is recommended for its simplicity.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Falcon** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use a shared integration

When you need to route alerts to different collaboration spaces based on the alert's payload information, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Falcon** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## In Falcon
---
Select alert rules and configure webhooks one by one.

<div id="!"><ol><li>Log in to your Falcon console and select Templates to enter the alarm rule template list page</li><li> Open any alarm rule template and fill in the callback address as the push address corresponding to the current integration.</li><li> Click the Save button to save the alarm rules</li><li> Repeat steps 2 and 3 for all alert rule templates that want to send events</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/K8WaMj6aJuvE6gB_F7OMBexypNErGAVawIwmAlCr64Y.avif"><img alt="drawing" width="600" src="https://fcdoc.github.io/img/BO_Ai0Y13E8v87DBBXD5IOD16hvspuJGBLxdpAkq7uY.avif"><p> Similarly, for Expressions alarm rules), you can also configure the same push address.</p><ol start="5"><li> Return to the integration list. If the latest event time is displayed, the configuration is successful and the event is received.</li><li> Finish</li></ol></div>

## Status Correspondence
---
<div class="md-block">

| Open-Falcon |  Flashduty  | Status |
| ----------- | -------- | ---- |
| 0           | Critical | Serious |
| 1           | Critical | Serious |
| 2           | Warning  | Warning |
| 3           | Warning  | Warning |
| 4           | Info     | Reminder |
| 5           | Info     | Reminder |
| 6           | Info     | Reminder |

</div>
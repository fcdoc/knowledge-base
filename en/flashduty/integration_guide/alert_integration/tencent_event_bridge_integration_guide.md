---
brief: Synchronize Tencent Cloud Event Bus EB events with Kuaimao Nebula via webhook to automate noise reduction processing for alarm events
---

# Tencent Cloud EventBridge

---

Synchronize Tencent Cloud Event Bus EB events with Flashduty via webhook to automate noise reduction processing for alarm events.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Tencent Cloud EventBridge** integration, click **Save** , and generate a card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Tencent Cloud EventBridge** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## In Tencent Cloud EventBridge
---
<div id="!"><ol><li>Log in to your Tencent Cloud console and select the event bus product</li><li> Enter the event rules page, click the New button to start editing rules</li><li> Fill in the name as FlashDuty as shown in the figure below:</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/3xdEpRnxM31nV5t8REeGxRbhRhwfQpwFooG7q6L6JhA.avif"><ol start="4"><li> In the event matching part, you can select specific events through the form mode, or you can customize the following JSON content to match all events:</li></ol><pre> `{
"source": [
{
"suffix": ".cloud.tencent"
}
]
}
`</pre><p> The diagram is as follows:</p><img alt="drawing" width="600" src="https://fcdoc.github.io/img/pRBjDtOVtl4b6YmKAVF8EJ9RoOAIPGgt4m2hRWWaMzk.avif"><ol start="5"><li> Next, configure the event target, select "Message Push", "Universal Notification Template", "English", "Interface Callback" and "Custom webhook " respectively, webhook fill in the integrated push address for the address</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/ha120gZ2uvDk4brSB4_OqEoYRM751-TesVi4cmOYQ-0.avif"><ol start="6"><li> Click the Save button, return to the event set page, select an event set, click Send event, and test</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/gh3xRQXvARrh7BWDz_le-dLR-0TMS4vblvXZbSu7NkM.avif"><ol start="7"><li> Return to the integration list. If the latest event time is displayed, the configuration is successful and the event is received.</li><li> Finish</li></ol></div>

## Status Comparison
---
<div id="!"><p>All events in the Tencent Cloud event bus correspond to "warning ( warning )" level alarms Flashduty</p></div>
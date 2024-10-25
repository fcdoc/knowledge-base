---
brief: Synchronize Alibaba Cloud Monitoring Event Center alerts to Kuaimao Xingyun via webhook to automate noise reduction processing for alert events
---

# Alibaba Cloud Monitoring CM Event Integration

---

Synchronize Alibaba Cloud Monitoring Event Center alerts to Flashduty via webhook to automate noise reduction processing for alert events.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Alibaba Cloud CM Event** Integration, click **Save** , and generate a card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Alibaba Cloud CM event** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>


## Configure Alibaba Cloud Monitoring CM Events
---
**Step 1: Add a Push Channel**

<div id="!"><ol><li>Log in to your Alibaba Cloud console and select cloud monitoring products</li><li> Enter **the Event Center -> Event Subscription** page, switch to **the Push Channel** tab, click the Create Push Channel button, and start editing content</li><li> As shown in the figure, select **POST** **for the request method** , and fill in the integrated push address **for the address.**</li><li> Click the Confirm button to submit the update</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/seOk8MgkEvjJCNzrDUEr8i0bnprzJyM5bb7-V_I3lqs.avif"></div>

**Step 2: Add a Subscription Policy**

<div id="!"><ol><li>Log in to your Alibaba Cloud console and select cloud monitoring products</li><li> Enter **the Event Center -> Event Subscription** page, switch to **the Subscription Strategy** tab, click the Create Subscription Strategy button, and start editing content</li><li> Fill in the subscription name, select the event type and scope, and configure the push channel at the bottom to be the Flashduty created previously.</li><li> Click the Confirm button to submit the update</li><li> The figure below shows the subscription results of two types of events: threshold and system.</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/yyNAM2bu8Z8ppbnnUX_irJpODrosO8QqejhB8egEojw.avif"></div>

## Status Comparison
---
<div class="md-block">

| Alibaba Cloud Monitoring |  Flashduty  | state |
| ------------ | -------- | ---- |
| CRITICAL     | Critical | serious |
| WARNING      | Warning  | warn |
| INFO         | Info     | remind |

</div>
---
brief: Synchronize Graylog alert events to Kuaimao Nebula via webhook to automate noise reduction processing for these alerts
---

# Graylog Alert Event

---

Synchronize Graylog alert events to Kuaimao Nebula via webhook to automate noise reduction processing for these alerts.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Graylog** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Graylog** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>



## In Graylog
---
<div id="!"><h2>Graylog Alarm push configuration</h2><h3> Step 1: Configure alarm channel</h3><ol><li> Login to Graylog .</li><li> Find Alerts in the menu and select Notifications .</li><li> created Create Notification .</li><li> Enter Title and Description .</li><li> Notification Type Select **HTTP Notification** , as shown below.</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/eWI2dwAH-u6NiXImb2P94U6PLQwwqJ874Z-9dTEnG8U.avif"><ol start="6"><li> Input FlashDuty The obtained URL (you need to whiten URL for the first input).</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/lkx7VzY3ZZqF9K-qUu469azcTPzOeOevMdLD1b5Q9cU.avif"><ol start="7"><li> Click Save to save the whitened URL</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/99FRplZHwxawFUPjKweW08evg86CU7O26tKNkjuwANk.avif"><ol start="8"><li> After saving, commit Create .</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/LWGvCpNBZ1fE2ILfxZ9-COnwvCXk806KviB6KQ_B4fg.avif"><h3> Step 2: Use FlashDuty alarm channels in alarm events</h3><ol><li> Create or edit an existing Event Definition .</li><li> Other alarm configurations are omitted here (configure alarm conditions according to business requirements).</li><li> Configure channel in Notifications .</li><li> Add Notifition channel FlashDuty .</li><li> Click Done .</li><li> Just complete the next step.</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/FBEZ5WZwmS1KOXauhVJ_PCxKzhnwgCfeWVriVNKUqsA.avif"></div>

## Status Comparison

<div class="md-block">

|Graylog|Kuaimao Nebula|state|
|---|---|---|
|3|Critical|serious|
|2|Warning|warn|
|1|Info|remind|

</div>
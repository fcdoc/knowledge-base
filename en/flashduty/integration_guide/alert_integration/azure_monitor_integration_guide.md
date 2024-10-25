---
brief: Synchronize Azure Monitor alert events to Kuaimao Xingyun via webhook to automate noise reduction processing of alerts
---

# Azure Monitor Integration

---

Synchronize Azure Monitor alert events to Flashduty via webhook to automate noise reduction processing of alerts.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Azure Monitor** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Azure Monitor** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>


## The process is now complete
---
**Step 1: Configure Webhook**

<div id="!"><ol><li>Log in to your Azure portal and select Monitor ;</li><li> Enter page `Alerts -> Action groups` , click the Create button to start editing;</li><li> As shown in the figure, option `Actions` chooses `Action type` as `Webhook` ;</li><li> Fill in the name, copy and write the `URI` parts into the integrated push address, pay attention to the `Enable` general alert structure;</li><li> Click the Create button to submit and save.</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/4gzLFt9GChD5e3f_GYsfB0c4VwgFWvEtl4oBrNyvKzs.avif"><p> **Step 2: Configuration Alert rule**</p><ol><li> Enter page `Alerts -> Alert rules` , click Create or select an existing policy to edit;</li><li> As shown in the figure below, on page `Actions` , select the created one Action group ;</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/b-vF-yP22lZacuG_Q9t4J7xx0uPFYqYcILv3Fc3vI3k.avif"><ol start="3"><li> Submit and save, waiting for the alarm to be triggered.</li></ol></div>

## Status Comparison
---
<div class="md-block">

| Azure Monitor  |  Flashduty  | state |
| ------------ | -------- | ---- |
| Sev0     | Critical | serious |
| Sev1     | Warning  | warn |
| Sev2     | Warning  | warn |
| Sev3     | Info     | remind |
| Sev4     | Info     | remind |

</div>
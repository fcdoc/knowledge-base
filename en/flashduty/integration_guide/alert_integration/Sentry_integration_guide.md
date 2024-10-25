---
brief: Synchronize Sentry alert events to Kuaimao Xueyun via webhook to automate noise reduction processing for these alerts
---

# Sentry Alert Event

---

Synchronize Sentry alert events to Kuaimao Xueyun via webhook to automate noise reduction processing for these alerts.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Sentry** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Sentry** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>



## In Sentry
---
<div id="!"><h2>1. Preliminary instructions</h2><p> Sentry Provides two types of alarm mechanisms: Issue Alerts and Metric Alerts . Issue Alerts Supports the notification function through WebHooks in Integrations , while Metric Alerts is limited to use Internal Integration alarm notification. Worth noting Internal Integration not only compatible with Metric Alerts , but also Issue Alerts . In view of the wide applicability of Internal Integration , we decided to adopt this method uniformly and no longer rely solely on WebHooks to simplify the configuration of alarm notifications.</p><h2> 2. Sentry Alarm push configuration</h2><h3> Step 1: Add FlashDuty Custom Integrations</h3><ol><li> Log in to the Sentry management console.</li><li> In the left navigation bar, find **Settings = > Custom Integrations** .</li><li> Click Create New Integration and select **Internal Integration** .</li><li> on the edit page. **Fill in FlashDuty at Name WebhookURL copy and write the integrated push address at** ;.</li><li> Turn on **Alert Rule Action** , refer to the following configuration:</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/WsTxnddIFxx3K9TzO9oeQdeGe4_uvFdAMKD_8ZZbt38.avif"><ol start="5"><li> **Configure Read permissions for Issue & Event** in the PERMISSIONS .</li><li> In the WEBHOOKS configuration, check **issue** , **please do not check error and comment**</li><li> After the configuration is complete, click Save Changes to complete the creation.</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/QLbhF_ak80OpOZK3z4SOdT46MBmuS29kneZWyT4zZzk.avif"><p> **Special notes on WEBHOOKS configuration:**</p><ol><li> After checking **issue** FlashDuty can receive the resolved event of issue , that is, when resolved is manually triggered for a problem in the issue list, we will automatically restore the associated fault in FlashDuty</li><li> Other events of issue , such as create , assigned , archived , and unresolved , are not supported.</li><li> If error and comment are checked at the same time, FlashDuty will not receive and process such events.</li></ol><h3> Step 2: Use FlashDuty Integration in Alerts</h3><ol><li> In the left navigation bar, find **Alerts = > Create Alert**</li><li> Select the Alert to create, such as Issue .</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/JByBizu05Z4bxPUlUtnsmePcvjUBA0zMKC75mJX6qyo.avif"><ol start="3"><li><p> Please configure the trigger conditions as needed.</p></li><li><p> **Add action at THEN perform these actions** and select **Send a notification via** .</p></li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/n9LGTYqFuUmJEPlP-3sHQI-zy0TF8HpY7sQvtOLJ9cA.avif"><ol start="5"><li><p> For the notification channel, select **FlashDuty** added above.</p></li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/rtUTpFhDO_-3FKalrhFBZJg3aVRb8c7YBnkwXj42KQI.avif"><ol start="6"><li><p> After configuring other options, click **Save Rule** to save.</p></li></ol><h2> 3. Status comparison</h2><div id="!">

|Sentry|Kuaimao Nebula|state|
|---|---|---|
|critical|Critical|serious|
|warning|Warning|warn|
|triggered|Warning|warn|
|resolved|Ok|Recovered|

</div>
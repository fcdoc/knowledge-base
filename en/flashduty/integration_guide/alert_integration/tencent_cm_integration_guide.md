---
brief: Synchronize Tencent Cloud Monitoring CM alarm events to Kuaimao Xingyun via webhook to automate noise reduction processing of the alarm events
---

# Tencent Cloud Monitoring CM Integration

---

Synchronize Tencent Cloud Monitoring CM alarm events to Flashduty via webhook to automate noise reduction processing of the alarm events.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Tencent Cloud Monitoring CM** Integration, click **Save** , and generate a card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Tencent Cloud Monitoring CM** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## In Tencent Cloud Monitoring CM
---
<div id="!"><ol><li>Log in to your Tencent Cloud console and select cloud monitoring products</li><li> Enter the Alarm Management -> Notification Template page, click the New button to start editing the notification template</li><li> Fill in the callback address as the integrated push address, and select English as the notification language.</li><li> Click the Save button to save the template</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/Mx0ptF5_sB39VvPufOJofjlLXjqmecyBt8CYNIPXM3c.avif"><ol start="5"><li> Enter the Alarm Configuration -> Alarm Policy page, select the alarm policy for all events to be sent, enter the details, and add the notification template created in the previous step.</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/wmSUn2CyyOZJ-kktoTUMQ3jtGgD2GqNx51IVcZdafIk.avif"><ol start="6"><li> Return to the integration list. If the latest event time is displayed, the configuration is successful and the event is received.</li><li> Finish</li></ol></div>

## Status Comparison
---
<div id="!"><p>All indicator alarms in Tencent Cloud Monitoring correspond to "Warning ( warning )" level alarms Flashduty</p></div>
---
brief: Synchronize Huawei Cloud Monitoring CES alarm events with Kuaimao Xinyun via webhook to automate noise reduction processing of alarm events"
---

# Huawei Cloud Monitoring CES Integration

---

Synchronize Huawei Cloud Monitoring CES alarm events with Flashduty via webhook to automate noise reduction processing of alarm events.

## In Flashduty
---
You can obtain an integrated push address using the following two methods, choose one as preferred.

### Use Exclusive Integration

When there's no need to route alarm events to different collaboration spaces, this method is recommended for its simplicity.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Huawei Cloud Monitoring CES** Integration, click **Save** , and generate a card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integration

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Huawei Cloud Monitoring CES** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## In Huawei Cloud Monitoring CES
---
<div id="!"><ol><li>Log in to your Huawei Cloud console, retrieve `云监控` products, and enter the corresponding product console</li><li> Enter page `告警-告警通知-通知对象` and click button `创建通知对象`</li><li> Select `HTTPS` for the protocol, fill in `flashduty` for the name, and fill in the integration address for the terminal (fill in the integration name on the current page, and the address can be generated after saving)</li><li> Click the `确定` button to complete the notification object creation</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/tgH1UDKys17VJAMsXbifQp-qYjXBKKOpusNdIiZJYbE.avif"><ol start="5"><li> Enter page `告警-告警通知-通知组` and click button `创建通知组`</li><li> Fill in `FlashDuty` for the group name, and check `flashduty` created previously for the notification object.</li><li> Click the `确定` button to complete the notification group creation</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/un2_U8J_auion76Ks570Tt6OQj1_akTliX0oX-a3QUQ.avif"><p> Note that when creating a notification group, Huawei Cloud will initiate a request to Flashduty verify the push address, and view the notification object list of the notification group. Only when the status of the notification object is `已确认` , the alarm will be pushed normally.</p><ol start="8"><li> Enter page `告警-告警规则` , select an existing alarm rule to edit, or create a new alarm rule, and open page `告警规则详情`</li><li> Among them, select `FlashDuty` for `通知组` , and select `出现告警` and `恢复正常` for trigger conditions. Click the `确定` button to save changes</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/XNjNCWbTfuFnsmavwkCyhMtG9DJNykfjqsIQiLG4Sj4.avif"><ol start="10"><li> Return to the Flashduty integration list page. If the latest event time is displayed, it means the configuration is successful and the event is received.</li><li> Finish</li></ol></div>

## Status Correspondence
---
<div class="md-block">

| CES  |  Flashduty  | Status |
| ---- | -------- | ---- |
| Urgent | Critical | Serious |
| Important | Critical | Serious |
| Minor | Warning  | Warning |
| Hint | Info     | Reminder |

</div>
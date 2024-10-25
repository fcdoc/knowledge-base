---
brief: Synchronize AWS CloudWatch alarm events with Flashduty via webhook to automate noise reduction processing for these events
---

# AWS CloudWatch Integration

---

Synchronize AWS CloudWatch alarm events with Flashduty via webhook to automate noise reduction processing for these events.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **AWS CLoudWatch** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **AWS CloudWatch** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## In AWS CloudWatch
---
<div id="!"><ol><li>Log in to your AWS console, retrieve `Simple Notification Service` products, and enter the corresponding product console</li><li> Enter page `Topics` , click button `Create topic` to start creating a theme</li><li> `Type` `Standard` and fill in the name as `FlashDuty`</li><li> Click button `Create Topic` to complete theme creation</li><li> Enter page `Subscriptions` and click button `Create subscription` to create a subscription for the topic</li><li> `Topic ARN` Select `FlashDuty` , `Protocal` select `HTTPS` , and `Endpoint` fill in the integrated push address (fill in the integration name on the current page, and the address can be generated after saving)</li><li> Click the `Create subscription` button to complete the subscription creation</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/gwmuAGU9LJLBtiGACTpOAzBVZeYcAhCPSPh7HFKmdJ0.avif"><ol start="8"><li> Return to the `Subscriptions` page. When the subscription status is `Confirmed` , it means the subscription address verification is successful. Otherwise, please contact Flashduty</li><li> Retrieve `CloudWatch` products and enter the corresponding product console</li><li> Enter the `All alrams` page and choose to create or edit an existing alarm policy.</li><li> For the `Notification` step, `FlashDuty` is selected as the push target `SNS topic` for the three states `In alarm` , `OK` and `Insufficient data` , as shown in the following figure:</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/ZWmshP-7A7IaZw8z1v9mLjFZQQc_4Z6zNv9EyxJFvY0.avif"><ol start="12"><li> Return to the integration list. If the latest event time is displayed, the configuration is successful and the event is received.</li><li> Finish</li></ol></div>

## Status Comparison
---
<div id="!"><p>CloudWatch All monitoring indicator alarms correspond to Flashduty "warning ( warning )" level alarms.</p></div>
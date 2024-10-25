---
brief: Synchronize Blue Whale Cloud monitoring events with Flashduty via webhook to automate noise reduction for alarm events
---

# Blue Whale Zhiyun Integration

---

Synchronize Blue Whale Cloud monitoring events with Flashduty via webhook to automate noise reduction for alarm events.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Blue Whale Zhiyun** integration, click **Save** to generate a card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Choose **Blue Whale Zhiyun** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## In Blue Whale Zhiyun
---
The following content has been verified in `Blue Whale V6/7 versions`. Versions V5 and below are no longer officially supported. It is recommended that you upgrade.

Blue Whale alarm policies can trigger `processing packages`, which can be integrated with surrounding systems to perform complex functions. First, create a processing package, configure FlashDuty's callback address, then edit the alarm policy to associate actions with the processing package, enabling automatic alarm updates to be pushed to FlashDuty. Specific steps are as follows:

#### Step 1: Create a Processing Package

<div id="!"><ol><li>Log in to your Blue Whale Zhiyun desktop and enter `监控平台` ;</li><li> Enter page `配置-处理套餐` and click button `添加套餐` to start creating a processing package;</li><li> Fill in the name as `Send To FlashDuty` , choose `HTTP回调` as the package type, choose `POST` as the push method, and fill in the integrated push address (obtained after saving the integration), as shown in the figure below:</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/PZqbJNifhVKQj9FQNUw3DmVq8JGPf0sug4nfwFxVEjQ.avif"><ol start="4"><li> Switch to `主体` , select type `JSON` , copy the message body and fill in the following information (when an alarm is actually generated, Blue Whale will render the variable content as Payload and push it to the target callback address):</li></ol><pre> `{{alarm.callback_message}}
`</pre><ol start="5"><li> Save the package to complete creation.</li></ol></div>

#### Step 2: Edit Alarm Policy

<div id="!"><ol><li>Enter the `配置-告警策略` page, select an existing policy to edit, or create a new alarm policy;</li><li> Scroll down to Part `告警处理` , select `Send To FlashDuty` processing package for all three scenarios, and turn off `防御规则` , as shown below:</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/yeCaYyAFIHIaZZL6z7_gTPHz-vjF6nCl5Yw8rv1t9SI.avif"><ol start="3"><li> Submit and save, complete;</li><li> For other alarms that you want to push to FlashDuty repeat the above steps.</li></ol></div>

## Status Comparison
---
<div class="md-block">

| Blue Whale Zhiyun |  Flashduty  | state |
| -------- | -------- | ---- |
| Fatal     | Critical | serious |
| Early Warning     | Warning  | warn |
| remind     | Info     | remind |

</div>
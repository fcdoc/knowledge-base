---
brief: Synchronize Baidu Cloud BCM alarm events with Flashduty via webhook to automate noise reduction processing for alarm events
---

# Baidu Cloud BCM Monitoring Integration

---

Synchronize Baidu Cloud BCM alarm events with Flashduty via webhook to automate noise reduction processing for alarm events.
## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Baidu Cloud Monitoring BCM** Integration, click **Save** , and generate a card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Baidu Cloud Monitoring BCM** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## In Baidu Cloud Monitoring BCM
---
<div id="!"><ol><li>Log in to your Baidu Cloud console, retrieve `云监控` products, and enter the corresponding console</li><li> Baidu Cloud provides a variety of ways to configure alarm callbacks. For details, please refer to [the official documentation](/0) . The following only demonstrates the `报警管理-报警策略` entry configuration method.</li><li> Enter page `报警管理-报警策略` and choose to edit an existing or create a new alarm policy.</li><li> In the `回调地址` column of the alarm policy, fill in the integrated push address (fill in the integration name on the current page, and the address can be generated after saving)</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/YNQKnmj1FuILvVEkkDliHTFfRCgRUxWDDNsctXsp12Q.avif"><ol start="5"><li> Finish</li></ol></div>

## Status Comparison
---
<div class="md-block">

| BCM  |  Flashduty  | state |
| ---- | -------- | ---- |
| serious | Critical | serious |
| Important | Critical | serious |
| warn | Warning  | warn |
| Notification | Info     | remind |

</div>
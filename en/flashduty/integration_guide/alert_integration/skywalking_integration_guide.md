---
brief: Synchronize Skywalking alert events to Kuaimao Nebula via webhook to automate noise reduction processing for these alerts
---

# Skywalking Alert Event

---

Synchronize Skywalking alert events to Kuaimao Nebula via webhook to automate noise reduction processing for these alerts.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Skywalking** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Skywalking** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>



## In Skywalking
---
<div id="!"><h2>1. Skywalking the configuration file of the service</h2><ol><li> Login to Skywalking .</li><li> Find configuration files for Skywalking . /config/alarm-settings.yml .</li><li> Add tags of Level in the alarm rule.</li></ol><pre> `# v8.6.0+ 及以上版本才支持tags标签，其他版本可以不添加。
# Level 的对应 value ：Critical、Warning、Info。
# 请注意大小写。
rules:
endpoint_relation_resp_time_rule:
expression: sum(endpoint_relation_resp_time > 1000) >= 2
period: 10
message: Response time of endpoint relation {name} is more than 1000ms in 2 minutes of last 10 minutes
tags:
Level: Warning
`</pre><ol start="4"><li> Add FlashDuty 's webhook address.</li></ol><pre> `# 在配置文件底部添加
# v8.8.0 ~ v9.5.0 的添加方式
webhooks:
- url: https://api.flashcat.cloud/event/push/alert/skywalking?integration_key=18c7f1551df55fa28a1a87f0846d9d1e131

# v10.0.0 的添加方式
hooks:
webhook:
default:
is-default: true
urls:
- https://api.flashcat.cloud/event/push/alert/skywalking?integration_key=18c7f1551df55fa28a1a87f0846d9d1e131
`</pre><ol start="5"><li><p> After editing is completed, save and restart the Skywalking to make the configuration file take effect.</p></li></ol><h2> 2. Status comparison</h2><div id="!">

|Skywalking|Kuaimao Nebula|state|
|---|---|---|
|Critical|Critical|serious|
|Warning|Warning|warn|
|Info|Info|remind|
|Other or Empty|Info|remind|


</div>
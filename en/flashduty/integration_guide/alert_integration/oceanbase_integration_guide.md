---
brief: Synchronize OceanBase alarm events to Kuaimao Nebula via webhook to automate noise reduction processing for alarm events
---

# OceanBase Alarm Event

---

Synchronize OceanBase alarm events to Kuaimao Nebula via webhook to automate noise reduction processing for alarm events

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **OceanBase** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **OceanBase** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>



## At OceanBase
---

<div id="!"><h2>OceanBase Alarm push configuration</h2><h3> Step 1: Configure alarm channel</h3><ol><li> Log in to your OceanBase and select Alarm Center.</li><li> Enter **the alarm channel** and click the **New Channel** button to start creating a new channel.</li><li> Select **custom script** for channel type.</li><li> The basic configuration content is as shown in the figure below:</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/IQVsfNMP7URm0FvPQlnMRB7JFUTPrgKlUw96ylc3Udc.avif"><ol start="5"><li> Copy the following script content in the configuration channel, and **please add the integration_key parameter in the script with the value FlashDuty in the push address integration_key** .</li></ol><pre> `#!/usr/bin/env bash

function sendToFlashDuty() {
URL="${address}/event/push/alert/standard?integration_key=${integration_key}"
curl -s -X POST ${URL} -H 'Content-Type: application/json' -d '{
"event_status": "'${alert_level}'",
"alert_key": "'${alarm_id}'",
"description": "'"${alarm_description//\"/\\\"}"'",
"title_rule": "$app_types::$name::$alarm_targets",
"event_time":'${timestamp}',
"labels": {
"app_types":"'${app_type}'",
"id":"'${alarm_id}'",
"name":"'${alarm_name}'",
"alarm_level":"'${alarm_level}'",
"alarm_status":"'${alarm_status}'",
"alarm_active_at":"'${alarm_active_at}'",
"alarm_threshold":"'${alarm_threshold}'",
"alarm_type":"'${alarm_type}'",
"alarm_targets":"'${alarm_target}'",
"ob_cluster_group":"'${ob_cluster_group}'",
"ob_cluster":"'${ob_cluster}'",
"hostIP":"'${host_ip}'",
"app_cluster":"'${app_cluster}'",
"alarm_description":"'"${alarm_description//\"/\\\"}"'",
"alarm_url":"'${alarm_url}'"
}
}'

return $?
}

alarm_name=$(echo ${alarm_name}
`</pre> | sed  "s/ /_/g")
alarm_target=$(echo ${alarm_target} | sed  "s/ /_/g" )</p><p> # the alarm update time as the alarm generation time timestamp = $ ( TZ = UTC date -d "${alarm_updated_at}" + %s)</p><p> #OceanBase The status and level of the alarm notification are in Chinese, so turn to , first Md5 and then make a judgment levelMd5 = $ ( echo ${alarm_level} | md5sum | awk '{print$1}')
statusMd5=$(echo ${alarm_status} | md5sum | awk ' {print$1} ')</p><p> # status Md5
active = "048d106318302b41372b4292b5696ad4"
Inactive = "bf7da164d431439fe9668fbc964110c4"</p><p> # Alarm level Md5
down = "2e1558b0a152fae2dd15884561b1508d"
critical = "59b9b38574ca2ee4f5e264b56f49a83f"
alert = "723931b03a5d1cec59eac40cf0703580"
caution = "abf4d55ba8926eff32cb44065e634ed3"
info = "6aae3f4254789d72aa0cc8ed55b8f11f"</p><p> address = " [https://api.flashcat.cloud](https://api.flashcat.cloud) "
integration_key = ""</p><p> # Convert the alarm level definition of OceanBase if [[ ${statusMd5} == ${Inactive} ]] ;then
alert_level = "Ok"
timestamp = $ ( TZ = UTC date -d "${alarm_resolved_at}" + %s) elif [[ ${statusMd5} == "${active}" ]] ;then
if [[ ${levelMd5} == ${down} || ${levelMd5} == ${critical} ]];then
alert_level="Critical"
elif [[ ${levelMd5} == ${alert} ]];then
alert_level="Warning"
elif [[ ${levelMd5} == ${caution}  ||  ${levelMd5} == ${info} ]] ;then
alert_level = "Info"
fi
fi</p><p> # Notification will be sent only when the status is in alarm or alarm is restored. No notification will be sent if the status is blocked or suppressed if [[ ${statusMd5} == ${active} || ${statusMd5} == ${Inactive} ]] ;then
sendToFlashDuty
fi</p><pre> `
6. Response 校验信息填写 {} 即可。
7. 消息配置中的告警消息格式选择 Markdown。
8. 告警消息模板 **选择简体中文**，并填写以下内容并提交。

`</pre><p> OCP notification - Single alarm</p><ul><li> Alert ID : ${alarm_id}</li><li> Name: ${alarm_name}</li><li> Level: ${alarm_level}</li><li> Alarm objects: ${alarm_target}</li><li> Services: ${service}</li><li> Overview: ${alarm_summary}</li><li> Generation time: ${alarm_active_at}</li><li> Update time: ${alarm_updated_at}</li><li> Recovery time: ${alarm_resolved_at}</li><li> Details: ${alarm_description}</li><li> Status: ${alarm_status}</li><li> Alarm type: ${alarm_type}</li><li> Alarm threshold: ${alarm_threshold}</li><li> Cluster group: ${ob_cluster_group}</li><li> Cluster: ${ob_cluster}</li><li> Host: ${host_ip}</li><li> Application cluster: ${app_cluster}</li><li> OCP Link: ${alarm_url}</li></ul><pre> `
### 步骤2：配置告警推送

1. 新建推送配置，路径：**告警中心=>告警推送=>新建推送配置**。
2. 推送类型、指定对象按需配置即可。


<img alt="drawing" id="!">

3. 推送语言选择 **简体中文**。
4. 告警通道选择 **FlashDuty** 。
5. 开启 **恢复通知**。
6. 提交。


<img alt="drawing" id="#">
</div>
`


## Status Comparison

<div class="md-block">

|OceanBase|Kuaimao Nebula|state|
|---|---|---|
|Service Suspension|Critical|serious|
|serious|Warning|serious|
|warn|Warning|warn|
|Notice|Info|remind|
|remind|Info|remind|

</div>


## Status Comparison
---
<div class="md-block">

|OceanBase|Kuaimao Nebula|state|
|---|---|---|
|Service Suspension|Critical|serious|
|serious|Warning|serious|
|warn|Warning|warn|
|Notice|Info|remind|
|remind|Info|remind|

</div>
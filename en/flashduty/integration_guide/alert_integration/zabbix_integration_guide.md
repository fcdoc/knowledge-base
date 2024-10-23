---
brief: >-
  Synchronize Zabbix events to Flashduty through webhook (support Zabbix 3.x ~ 6.x
  version (the configuration of different versions is different) to realize automatic noise reduction processing of alarm events.
---

# Utilize dedicated integrations in Flashduty

---

Through webhook, synchronize Zabbix alarm events to Flashduty (supports Zabbix 3.x to 6.x versions; configurations differ between versions) to automate the noise reduction of alarm events.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Zabbix** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Zabbix** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## For versions 5.x to 6.x
---
<span id="v5"></span>

### Use Shared Integrations

#### 使用共享集成

<div id="!"><ol><li>media type is the transmission channel used in Zabbix to send notifications and alarms. Enter the terminal and download the complete configuration through the following command</li></ol><pre> `// 5.x版本 XML配置：
wget https://download.flashcat.cloud/flashduty/integration/zabbix/zbx_mediatype_flashcat_v5.xml

// 6.x 版本 YAML 配置：
wget https://download.flashcat.cloud/flashduty/integration/zabbix/zbx_mediatype_flashcat_v6.yml
`</pre><ol start="2"><li> Log in to the Zabbix console, select `Administration > Media Types` , click the Import button in the upper right corner to enter the editing page, select the configuration file downloaded above, and click the Import button to complete the import.</li><li> Return to the Media Types page and you can see media type that has been imported. Click on the name to enter the editing page, complete the content such as URL , zabbix_url and HTTPProxy</li></ol><ul><li> `URL` : webhook Push request address, just copy the integrated push address</li><li> `zabbix_url` : Zabbix console address, just copy it (if your page is configured with tomcat/nginx forwarding path, please bring it with it at the same time), the system will splice trigger_id and other parameters after the path to generate the alarm details page connection</li><li> `HTTPProxy` : If your Zabbix Server cannot directly access the Flashduty service, you can set this parameter to a proxy address</li></ul><img alt="drawing" width="600" src="https://fcdoc.github.io/img/Wa1lJ6E3soYLZa2u6CJUpyAbJsVvqjqDuTl2m5pyK-g.avif"><ol start="4"><li> Click Update to save the configuration</li></ol></div>

#### Step 2: Associate media type to user

<div id="!"><p>media type Must be associated with a user to send events. user has at least permission to host of read . It is recommended to link directly to Admin users. Take Admin user as an example:</p><ol><li> Log in Zabbix console, select `Administration > Users` , select Admin User, select media , select Add , enter the editing window:</li></ol><ul><li> Type : Select Flashduty  media type created above</li><li> Send To : Fill in N/A</li><li> Other configurations use the default configuration and remain unchanged.</li></ul><img alt="drawing" width="600" src="https://fcdoc.github.io/img/NQZGtjnDMgN5oBrDr-I7TfOtAVCihNKlxVsahULxRMg.avif"><ol start="2"><li> Click the Add button to exit the Add media window</li><li> Click the Update button to exit the editing user page</li></ol></div>

#### Integration Name: Define a name for the current integration

<div id="!"><p>Sending a notification is one of the operations performed by the action ( actions ) in Zabbix . So, to set up a notification, log into Zabbix console, select `Configuration > Actions` , then:</p><ol><li> Click `Create action` to enter action edit page</li></ol><ul><li> Name : Fill in as " Send To FlashDuty "</li></ul><ol start="2"><li> Select `Operations` to add notification sending configurations for three scenarios:</li></ol><ul><li> In the Operations configuration item, Add the button to enter the configuration window</li><li> Send to users : Select the newly created or configured one above user</li><li> Send only to : Select Flashduty  media type</li><li> Keep other configurations as default</li><li> Click the Add button to complete the configuration of this configuration item</li><li> Repeat the above steps to complete the configuration of `Recovery operations` and `Update operations`</li></ul><img alt="drawing" width="600" src="https://fcdoc.github.io/img/eBJqunprfGJYQKJ843YcyuGkeEtykZmW2n9Wme-xqTc.avif"><img alt="drawing" width="600" src="https://fcdoc.github.io/img/EPSOBfH6Q2QrVkBSqKBj5rEJxsrnm7VD2gaoczsAl00.avif"></div>

#### Step 4: Send Events to Flashduty

<div id="!"><p>Log in Zabbix Console, select `Monitoring > Problems` to view the latest alarm list.</p><ol><li> Click Actions , you can see the message notification results in the pop-up window</li><li> Find the corresponding log of Flashduty . If Status is `Sent` , it means the notification is successful. Otherwise, check the reason according to the prompts.</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/OXyBJbDkZ1sj4otE-Is2dYelUR6ggs6rHPr-VtC3JGk.avif"><ol start="3"><li> Return to the integration list. If the latest event time is displayed, the configuration is successful and the event is received.</li><li> Finish</li></ol></div>

<span id="v4"></span>

### 5.x ~ 6.x

#### 5. 完成

<div id="!"><ol><li>Log in Zabbix Console, select `Administration > Media Types` , click the `Create media type` button in the upper right corner to enter the editing page</li><li> On the editing page, Type `Script` , Parameter fill in the following contents in order (do not adjust the order, leave blank if there is no value, the script obtains parameter values in order):</li></ol><ul><li><p> `{ALERT.SUBJECT}` : Alarm title, kept in the first parameter</p></li><li><p> `{ALERT.MESSAGE}` : Alarm information, kept in the second parameter</p></li><li><p> `FlashDuty webhook 推送请求地址` Just copy the integrated push address and keep it in the third parameter.</p></li><li><p> `Zabbix 控制台地址` Just copy it (if your page is configured with tomcat/nginx forwarding path, please bring it at the same time), it is used to generate the alarm details page connection. If it is not empty, keep it in the fourth parameter</p></li><li><p> `HTTPProxy` : If your Zabbix Server cannot directly access the Flashduty service, you can set this parameter to a proxy address. If it is not empty, keep it in the fifth parameter</p></li></ul><img alt="drawing" id="#"><ol start="3"><li> `Script name` in `send-to-flashduty.sh`</li><li> Click Update to save the configuration</li><li> Log Zabbix server to the server and execute the following command:</li></ol><pre> ```
#1. 进入告警脚本加载目录（具体地址配置在 Zabbix Server 配置文件中 `AlertScriptsPath` 变量，一般为`/usr/lib/zabbix/alertscripts`）
cd /usr/lib/zabbix/alertscripts

#2. 下载脚本
wget https://download.flashcat.cloud/flashduty/integration/zabbix/send-to-flashduty.sh

#3. 更改脚本为可执行状态
chmod +x send-to-flashduty.sh

```</pre><ol start="6"><li> Note, `脚本中使用了 curl 和 jq 命令` , make sure this Zabbix server process can find and execute these two commands, if not you need to install it according to the situation</li></ol></div>

#### 在 Zabbix

<div id="!"><p>media type Must be associated with a user to send events. user has at least permission to host of read . It is recommended to link directly to Admin users. Take Admin user as an example:</p><ol><li> Log in Zabbix console, select `Administration > Users` , select Admin User, select media , select Add , enter the editing window:</li></ol><ul><li> Type : Select Flashduty  media type created above</li><li> Send To : Fill in N/A</li><li> Other configurations use the default configuration and remain unchanged.</li></ul><img alt="drawing" width="600" src="https://fcdoc.github.io/img/GWCfInrRqnlRwvapcrtU-olJfugWnKPWNB6ZZ7BLpsY.avif"><ol start="2"><li> Click the Add button to exit the Add media window</li><li> Click the Update button to exit the editing user page</li></ol></div>

#### 步骤 1:定义 Flashduty  media type

<div id="!"><p>Sending a notification is one of the operations performed by the action ( actions ) in Zabbix . So, to set up a notification, log into Zabbix console, select `Configuration > Actions` , then:</p><ol><li> Click `Create action` to enter action edit page</li></ol><ul><li> Name : Fill in as " Send To FlashDuty "</li></ul><ol start="2"><li> Select `Operations` to update the notification user configurations for the three scenarios:</li></ol><ul><li> In the Operations configuration item, Add the button to enter the configuration window</li><li> Send to users : Select the newly created or configured one above user</li><li> Send only to : Select Flashduty  media type</li><li> Keep other configurations as default</li><li> Click the Add button to complete the configuration of this configuration item</li><li> Repeat the above steps to complete the configuration of `Recovery operations` and `Update operations`</li></ul><img alt="drawing" width="600" src="https://fcdoc.github.io/img/HlbY6VbtYAM28b-HLPawASZgS_QHOMmhsx0V2X9QabQ.avif"><ol start="3"><li> Select `Operations` to update the notification content configurations of the three scenarios respectively:</li></ol><ul><li> **In the Default Message configuration item, copy the following content completely and paste it after the default content** . FlashDuty After receiving the event, the corresponding text will be parsed to find the alarm attribute information:</li></ul><pre> `
-----FlashDuty Required Starts-----event_severity={TRIGGER.SEVERITY}
`</pre>||event_name={TRIGGER.NAME}||event_id={EVENT.ID}||event_tags={EVENT.TAGS}||event_ack={EVENT.ACK.STATUS}||event_value={EVENT.VALUE}||trigger_id={TRIGGER.ID}||trigger_desc={TRIGGER.DESCRIPTION}||trigger_expr={TRIGGER.EXPRESSION}||host_group={TRIGGER.HOSTGROUP.NAME}||host_ip={HOST.IP}||host_name={HOST.NAME}||item_name={ITEM.NAME}||item_value = {ITEM.VALUE}-----FlashDuty Required Ends-----</p><pre> ```
- 重复以上步骤，完成对 `Recovery operations` 和 `Update operations` 的配置

<img alt="drawing" id="!">

</div>
```

#### Step 4: Send events to Flashduty

<div id="!"><p>Log in Zabbix Console, select Monitoring > Problems to view the latest alarm list.</p><ol><li> Click Actions , you can see the message notification results in the pop-up window</li><li> If the found Flashduty corresponding log, if Status is Sent , it means the notification is successful. Otherwise, troubleshoot the cause according to the prompts.</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/ZWiq1b69iYwn2zoaaTSqjHCvFiIkRe68itpXEnQes1A.avif"><ol start="3"><li> Return to the integration list. If the latest event time is displayed, the configuration is successful and the event is received.</li><li> Finish</li></ol></div>

## Status Comparison
---
<div class="md-block">

| Zabbix         |  Flashduty  | state |
| -------------- | -------- | ---- |
| Disaster       | Critical | serious |
| High           | Critical | serious |
| Average        | Warning  | warn |
| Warning        | Warning  | warn |
| Information    | Info     | remind |
| Not classified | Info     | remind |

</div>
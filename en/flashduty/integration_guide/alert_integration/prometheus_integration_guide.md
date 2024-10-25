---
brief: >-
  Push Prometheus alert events to Flashduty via AlertManager using a webhook. When an alert is triggered, send a trigger event to
  Flashduty, and when the alert is resolved, send a recovery event to Flashduty.
---

# Prometheus Alert Integration

---

Push Prometheus alert events to Flashduty via AlertManager using a webhook. When an alert is triggered, send a trigger event to Flashduty, and when the alert is resolved, send a recovery event to Flashduty.


## Usage Restrictions
---

### In AlertManager

- You must have the permission to modify the AlertManager configuration file.
- Your AlertManager server must be able to access the domain api.flascat.cloud to push alerts to the external network.

## Supported Versions
---

This article is compatible with **Alertmanager version 0.16.0 and above**.

## Operation Steps
---

### In Flashduty

使用专属集成

#### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</li><li> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</li><li> Select **Prometheus** Integrate, click **Save** , and generate the card.</li><li> Click on the generated card to view **the push address** , copy it for later use, and complete.</li></ol></details>

#### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select ** Prometheus** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

### In AlertManager

#### Step 1: Configure Alertmanager

<div id="!"><ol><li>Log into your Alertmanager instance</li><li> Find and open the configuration file, usually alertmanager.yml in the Alertmanager root directory</li><li> In the receivers configuration section, add a Flashduty  webhook type receiver , as follows</li></ol><pre> <code class="language-receiver">receivers:
- name: 'flashcat'
webhook_configs:
- url: '您的集成推送地址'
send_resolved: true
http_config:
proxy_url: 'http://proxyserver:port'
</code></pre><p> You need to url the corresponding parameter value with the integrated push address. Note query string the parameter part needs to be carried integration_key</p><p> If you need to request Flashduty through a proxy, you can additionally set the http_config to proxy_url parameters as the proxy address.</p><ol start="4"><li> In the route configuration section, change the default route and specify receiver to webhook just configured, as follows:</li></ol><pre> <code class="language-route">route:
...
receiver: 'flashcat'
</code></pre><p> You can also add receiver to the non-default route , but then you will only synchronize the alarm events corresponding to route to Flashduty not all alarm events.</p><ol start="5"><li> Save configuration file</li><li> Make changes take effect by reloading the configuration file (sending a SIGHUP signal, or POST request /-/reload api to the process)</li><li> Finish</li></ol></div>

#### Step 2: Configure Timestamp

By default, the system uses the current time as the event trigger time. If you wish to customize the time, you can set an additional timestamp field to indicate the exact time of each alert occurrence.

<div id="!"><ol><li>Log into your Prometheus Server instance</li><li> Open the configuration file related to the alarm rule</li><li> For each alarm rule, change the annotations part and add the timestamp field, as follows:</li></ol><pre> `annotations:
timestamp: '{{ with query "time()" }}{{ .
`</pre> | first | value }}{{ end }} '...</p><pre> `
4. 保存配置文件
5. 通过重新加载配置文件（向进程发送 SIGHUP 信号，或 POST 请求/-/reload api），使更改生效
6. 完成

</div>
`

## Severity Level Mapping
---

The system sequentially extracts the `severity`, `priority`, and `level` tags from the alert event. The corresponding values will be used as Prometheus's own alert levels. If none are extracted, the system will automatically set the Prometheus alert level to `Warning`.

Prometheus to Flashduty Alert Level Mapping:

| Prometheus   |  Flashduty  | state |
| ------------ | -------- | ---- |
| critical     | Critical | serious |
| warning      | Warning  | warn |
| warn         | Warning  | warn |
| info         | Info     | remind |
| acknowledged | Info     | remind |
| unknown      | Info     | remind |
| unk          | Info     | remind |
| ok           | Ok       | Recovered |

## FAQs
---

<details><summary>Why didn't I receive the alert Flashduty !?</summary><h4> exist Flashduty</h4><ol><li> Check if the integration shows **the latest event time** ? If not, it means that Flashduty has not received the push, so you can directly check it first AlertManager Part.</li><li> If you are using **shared integration** , first confirm whether you have configured **routing rules** . If you do not set routing rules, the system will directly reject new pushes because there is no collaboration space to receive your alerts. In this case, just configure the routing rules directly to the space you want.</li></ol><h4> exist AlertManager</h4><ol><li><p> First, confirm whether the AlertManager generates new alarms. If no new alarm is generated, please continue to wait for a new alarm to be triggered before re-verifying.</p></li><li><p> Open the AlertManager configuration file. If you have set up a sub-route, please make sure that your routing settings are correct (for example, the previous route is set to continue AlertManager will skip matching subsequent sub-routes. We recommend that you always only set a default route to Flashduty ). Also verify whether the target callback address exactly matches the integrated push address. If they do not match, please modify **the alarm rules** and re-verify.</p></li><li><p> If it matches, please continue to confirm that AlertManager instance can access the external network api.flashcat.cloud domain name. If not, you first need to open an external network for it, or separately enable external network access for the domain name Flashduty .</p></li><li><p> If there is no problem with the network, you need to continue troubleshooting AlertManager to find whether there are relevant error logs.</p></li></ol><p> If you still cannot find the root cause of the problem after performing the above steps, please contact us directly.</p></details>
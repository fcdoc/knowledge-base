---
brief: >-
  Push Nightingale (Nightingale/n9e) or Flashcat alert events to Flashduty via webhook. When an alert is triggered, send a trigger event to Flashduty; when the alert is resolved, send a recovery event to Flashduty
  Flashduty sends a trigger event when an alert is activated, and sends a recovery event when the alert is resolved
---

# Nightingale/Flashcat Integration

---

Push Nightingale (Nightingale/n9e) or Flashcat alert events to Flashduty through a webhook. When an alert is triggered, send a trigger event to Flashduty; when the alert is resolved, send a recovery event to Flashduty.


## Usage Restrictions
---

### In Nightingale,

- You must have the permission to modify **System Configuration > Global Notification** or **Alert Management > Alert Rules**.
- Your Nightingale server must be able to access the domain api.flascat.cloud to push alerts to the external network.

## Supported Versions
---

This article is compatible with **Nightingale V5 and V6** versions.

## Operation Steps
---

### In Flashduty

使用专属集成

#### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</li><li> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</li><li> Select **Nightingale /Flashcat** integration, click **Save** , and generate the card.</li><li> Click on the generated card to view **the push address** , copy it for later use, and complete.</li><li> (Optional) Click the generated card, click the **Edit** button, select **the console address** , and enter the Nightingale console address (only the domain name part). Flashduty A Nightingale details jump link will be generated for the new alarm.</li></ol></details>

#### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Nightingale /Flashcat** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li><li> **Console address** : (Optional) Enter the Nightingale console address (only the domain name part). Flashduty A Nightingale details jump link will be generated for new alarms.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

### In Nightingale/Flashcat,

Choose one of the two configuration methods.

#### Method 1: Configure by Policy

<div id="!"><p>Select alarm rules in batches and configure them webhook .</p><ol><li> Log in to your n9e , select Alarm Management > Alarm Rules, and enter the alarm rule list page</li><li> Select the alarm rules you want to import in batches, and select Batch Update Alarm Rules in the upper right corner.</li><li> Select the "Callback Address" field in the pop-up window and fill in the integrated push address in the new input box, as shown in the figure below:</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/UjmNaNKJ88MKM2yEVC51LPmB0PoC2jve-WRDdLKvsjk.avif"><ol start="4"><li> Return to the integration list. If the latest event time is displayed, the configuration is successful and the event is received.</li><li> Finish</li></ol></div>

#### Method 2: Global Configuration

<div id="!">Nightingale supports configuring global webhook in pages and configuration files to push all alarm events. You can choose one of the following two methods.<h5> V6 and above version</h5><ol><li> Log into your n9e console</li><li> Enter page `系统配置-通知设置-回调地址`</li><li> As shown in the figure below, enable a new webhook , fill in part `URL` of the integrated push address</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/KlaBAhQQ7VXvE2gal3qgIgbV0nuXhUjcu7ERu8Tg948.avif"><ol start="4"><li> Finish</li></ol><h5> V5.4 ~ 5.15 version</h5><ol><li> Log into your n9e server instance</li><li> Find and open the configuration file, usually etc/server.conf</li><li> Alerting the configuration section and write Webhook as follows</li></ol><pre> <code class="language-receiver">[Alerting.Webhook]
Enable = true
Url = "{api_host}/event/push/alert/n9e?integration_key=$integration_key"
BasicAuthUser = ""
BasicAuthPass = ""
Timeout = "5s"
Headers = ["Content-Type", "application/json", "X-From", "N9E"]
</code></pre><p> You need to replace the parameter value corresponding to Url with the integrated push address.</p><ol start="4"><li> Save configuration file</li><li> Restart n9e server to make the configuration take effect</li><li> Return to the integration list. If the latest event time is displayed, the configuration is successful and the event is received.</li><li> Finish</li></ol></div>

## Severity Level Mapping
---

Nightingale/Flashcat to Flashduty alert level mapping:

| n9e |  Flashduty  | state |
| --- | -------- | ---- |
| 1   | Critical | serious |
| 2   | Warning  | warn |
| 3   | Info     | remind |

## FAQs
---

<details><summary>Why didn't I receive the alert Flashduty !?</summary><h4> exist Flashduty</h4><ol><li> Check if the integration shows **the latest event time** ? If not, it means that Flashduty has not received the push, and the Nightingale part will be directly checked first.</li><li> If you are using **shared integration** , first confirm whether you have configured **routing rules** . If you do not set routing rules, the system will directly reject new pushes because there is no collaboration space to receive your alerts. In this case, just configure the routing rules directly to the space you want.</li></ol><h4> in the nightingale /Flashcat</h4><ol><li><p> First, confirm whether the Nightingale test has generated new alarms: Go to **alarm management = > historical alarms** and check whether new alarms have been generated after configuring webhook . Note that the new alarm status must be **Triggered** . If no new alarm is generated, please continue to wait for a new alarm to be triggered before re-verifying.</p></li><li><p> After finding the alarm, go to the alarm details and view **the callback address** section. Verify whether the real callback address exactly matches the integrated push address. If they do not match, please modify **the alarm rules** and re-verify.</p></li><li><p> If it matches, you need to log in to Nightingale server confirm that it can access the external network api.flashcat.cloud domain name. If not, you first need to open an external network for server , or separately enable external network access for the domain name of Flashduty .</p></li><li><p> If there is no problem with the network, you need to continue troubleshooting server to find whether there are relevant error logs.</p></li></ol><p> If you still cannot find the root cause of the problem after performing the above steps, please contact us directly.</p></details>
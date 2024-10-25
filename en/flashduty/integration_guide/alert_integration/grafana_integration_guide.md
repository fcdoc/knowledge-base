---
brief: Synchronize Grafana alert events with Kuaimao Nebula via webhook to automate noise reduction processing for these alerts.
---

# Grafana Integration

---

Synchronize Grafana alert events with Flashduty via webhook to automate noise reduction processing for these alerts.


## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Grafana** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Grafana** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## Within Grafana
---
Grafana versions V4 to V8 have the Legacy Alerting feature enabled by default, while V9 and later versions have the Grafana Alerting feature enabled by default. For the differentiation of features and activation methods, please refer to [the official documentation](https://grafana.com/docs/grafana/v8.4/alerting/unified-alerting/opt-in/#opt-in-to-grafana-alerting). Please integrate according to the version you have deployed, following the steps below.

### Legacy Alerting

<div id="!"><ol><li>Open your Grafana Console and select Alerting > Notification channels</li><li> Click Add Channel to open the configuration Channel pop-up page</li><li> Configure the name, Type select webhook , Url fill in the integrated push address, Method select POST , as shown in the figure below:</li></ol><img alt="drawing" id="#"><ol start="4"><li> Save, return to the integration list, and wait for the alarm to be generated. If the latest event time is displayed, the configuration is successful and the event is received.</li><li> Finish</li></ol></div>

### Grafana Alerting

<div id="!"><ol><li>Open your Grafana Console and select Alerting > Contact points</li><li> Click New contact point to open the configuration pop-up page</li><li> Configuration name, Type select webhook , Url fill in the integrated push address, Method select POST as shown in the figure below:</li></ol><img alt="drawing" id="#"><ol start="4"><li> Open the Notification policies page, edit or add according to the situation policy and select contact point as the sending channel created in the previous step, as shown in the following figure:</li></ol><img alt="drawing" id="$"><ol start="5"><li> Save, return to the integration list, and wait for the alarm to be generated. If the latest event time is displayed, the configuration is successful and the event is received.</li><li> The default alarm level is warning If you need to customize it, you can configure the severity label on the alarm details page (for enumeration, please refer to the status comparison below). The specific operation is as shown in the figure below:</li></ol><img alt="drawing" id="("><ol start="7"><li> Finish</li></ol><h2> Status comparison</h2><hr><div id="!"><p> Alarm level Legacy Alerting to Flashduty mapping relationship:</p>

| Legacy Alerting |  Flashduty  | state |
| --------------- | -------- | ---- |
| alerting        | Warning  | warn |
| no_data         | Critical | serious |
| ok              | Ok       | Recovered |

Grafana Alerting to Flashduty level mapping relationship:</p><p> The system extracts `severity` , `priority` and `level` in the alarm event tags in sequence, and the corresponding values will be used as Prometheus s own alarm level. If not extracted, the system will automatically set it Prometheus the alarm level is `warning` ).

| Grafana Alerting |  Flashduty  | state |
| ---------------- | -------- | ---- |
| critical         | Critical | serious |
| warning          | Warning  | warn |
| warn             | Warning  | warn |
| info             | Info     | remind |
| acknowledged     | Info     | remind |
| unknown          | Info     | remind |
| unk              | Info     | remind |
| ok               | Ok       | Recovered |

</div>
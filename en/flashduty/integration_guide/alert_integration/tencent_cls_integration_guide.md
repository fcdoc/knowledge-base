---
brief: 1	Synchronize Tencent Cloud Log Service CLS monitoring alarm events to Kuaimao Nebula via webhook, achieving automated noise reduction processing for alarm events
---

# 2	Integration of Tencent Cloud Log Service CLS

---

3	Synchronize Tencent Cloud Log Service CLS monitoring alarm events to Flashduty via webhook, realizing automated noise reduction processing for alarm events.

## In Flashduty
---
使用专属集成

### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Tencent Cloud CLS** integration, click **Save** , and generate a card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Tencent Cloud CLS** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

## CLS in Tencent Cloud
---

**Step 1: Configure Notification Channel Group**

<div id="!"><ol><li>Log in to your Tencent Cloud console, select the Log Service CLS product, and enter Monitoring Alarm - Notification Channel Group</li><li> Click `新建` to start new</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/9TVvjInBRsJOGHYptzIJmMgCaYUTRTohbSwENzk9_bg.avif"><ol start="3"><li><p> As shown in the figure, `名称` fill in the specific channel group name, `渠道类型` select "custom interface callback", `回调地址` fill in the integrated push address, `请求方法` select POST</p></li><li><p> Click `确定` to save, `添加` to add multiple channels</p></li></ol></div>

**Step 2: Configure Alarm Policy**

<div id="!"><ol><li>Log in to your Tencent Cloud console, select the Log Service CLS product, and enter Monitoring Alarm - Alarm Policy</li><li> Click `新建` to start new</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/FCfCmqlCwhjze8nSa88mkVt3nUX1myHyDFygJd8_lIc.avif"><ol start="3"><li><p> As shown in the figure, `告警名称` fill in the specific alarm name and select a specific log topic for the log topic.</p></li><li><p> `执行语句` Fill in the specific query statement, select the time range for the query time range, click Preview to view the execution results, and enter specific trigger conditions for the trigger conditions</p></li><li><p> `告警级别` , divided into emergency, alarm and reminder, the program is selected according to the severity of the alarm, and the execution cycle is selected according to needs</p></li><li><p> `多维分析` When an alarm is triggered, additional retrieval and analysis can be performed on the original log, and the results are appended to the alarm notification to assist in locating the cause of the alarm. Multidimensional analysis will not affect alarm triggering conditions.</p></li><li><p> Alarm notification, `通知渠道组` , can be associated with a specific channel group</p></li></ol></div>


**Step 3: Configure Custom Callback**

<div id="!"><ol><li><p>After associating the channel group, you can see the callback content configuration</p></li><li><p> Request header, you can add specific requests headers</p></li><li><p> Request content, return specific request data format, refer to:</p></li></ol><pre> <code class="language-json">{
"uin": "{{escape .UIN}}",
"nickname": "{{escape .Nickname}}",
"region": "{{escape .Region}}",
"alarm": "{{escape .Alarm}}",
"alarm_id": "{{escape .AlarmID}}",
"condition": "{{escape .Condition}}",
"happen_threshold": "{{escape .HappenThreshold}}",
"alert_threshold": "{{escape .AlertThreshold}}",
"topic": "{{escape .Topic}}",
"topic_id": "{{escape .TopicId}}",
"level": "{{escape .Level}}",
"label": {{.Label}},
"start_time": "{{escape .StartTime}}",
"start_time_unix": "{{escape .StartTimeUnix}}",
"notify_time": "{{escape .NotifyTime}}",
"notify_time_unix": "{{escape .NotifyTimeUnix}}",
"notify_type": "{{escape .NotifyType}}",
"consecutive_alert_nums": "{{escape .ConsecutiveAlertNums}}",
"duration": "{{escape .Duration}}",
"trigger_params": "{{escape .TriggerParams}}",
"record_group_id": "{{escape .RecordGroupId}}",
"detail_url": "{{escape .DetailUrl}}",
"query_url": "{{escape .QueryUrl}}",
"message": {{.Message}},
"query_result": {{.QueryResult}},
"query_log": {{.QueryLog}},
"analysis_result": {{.AnalysisResult}}
}
</code></pre></div>


## Status Comparison
---
9	<div class="md-block">

| Tencent Cloud CLS Monitoring |  Flashduty    | state
| ------------- | --------- | --- |
| Info          |  Info     | remind
| Warn          |  Warning  | warn
| Critical      |  Critical | urgent</p> </
---
brief: Synchronize Alibaba Cloud Log Service SLS monitoring alarm events with Kuaimao Xinyun via webhook, achieving automated noise reduction for alarm events
---

# Alibaba Cloud SLS Integration

---

Synchronize Alibaba Cloud Log Service SLS monitoring alarm events with Flashduty via webhook, achieving automated noise reduction for alarm events.

## In Flashduty
---
You can obtain an integrated push address using the following two methods, choosing one as preferred.

### Use Exclusive Integration

When there is no need to route alarm events to different collaboration spaces, this method is recommended for its simplicity.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Alibaba Cloud SLS** Integration, click **Save** , and generate a card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integration

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is recommended.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Alibaba Cloud SLS** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>


## In Alibaba Cloud SLS
---
**Step 1: Configure Webhook**

<div id="!"><ol><li>Log in to your Alibaba Cloud console, select Log Service SLS product, and select a Project</li><li> Enter the `告警` -> `告警管理` -> `Webhook集成` page, click the `新建` button to start editing</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/do6Aljc-9776gTE_GTxT9gsVkAEejjOPvjVOZjEMs8U.avif"><ol start="3"><li> As shown in the figure, `类型` select "Universal Webhook ", `请求方法` select POST , `请求地址` fill in the integrated push address (obtained after saving)</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/l7QslDgInVpUwfNHW6GyVdSgdLrHiblCHY8-Zq1YR4M.avif"><ol start="4"><li> Click button `确认` to submit and save</li></ol></div>

**Step 2: Configure Content Template**

<div id="!"><ol><li>Switch to page `内容模板` , click the `添加` button to start editing</li><li> Enter `Webhook-自定义` configuration items, `发送方式` select "Send one by one", `发送内容` copy the following content:</li></ol><pre> `{{ alert
`</pre> | to_json}}</p><pre> ```
<img alt="drawing" id="!">

3. 点击`确认`按钮，提交保存

</div>
```

**Step 3: Configure Action Strategy**

<div id="!"><ol><li>Switch to page `行动策略` , click the `添加` button to start editing</li><li> Enter the `第一行动列表` configuration item and click to add a `行动组` node.</li><li> `渠道` Select "Universal Webhook ", `选择Webhook` and `内容模板` use the object created previously, `发送时段` select "Any"</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/Dl-kqzyg53lz-hqYR8rZw8wC-cVpK4103tdtDLESOzU.avif"><ol start="4"><li> Click `结束` to complete the creation of the first action list</li><li> Click button `确认` to submit and save</li></ol></div>

**Step 4: Configure Monitoring Rules**

<div id="!"><ol><li>Switch to the `规则/事务` page, click the `新建告警` button or select an existing alarm to update and edit.</li><li> Enter the `告警规则` editing page, `告警策略` .</li><li> `告警策略` "Normal Mode", `行动策略` the object created previously</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/TQ-mllhuKcn6FKPy11GIPpGB8GvwiJ17ZSraCR-IPCg.avif"><ol start="4"><li> Click button `确定` to submit and save</li><li> Repeat the above steps for all other rules to push all alarms to FlashDuty</li></ol></div>

## Status Comparison
---
<div id="!"><p>Alibaba Cloud SLS Monitors the Flashduty level mapping relationship:</p>

| Alibaba Cloud SLS Monitoring |  Flashduty  | Status |
| --------------- | -------- | ---- |
| 10              | Critical | Serious |
| 8               | Critical | Serious |
| 6               | Warning  | Warning |
| 4               | Warning  | Warning |
| 2               | Info     | Reminder |

</div>
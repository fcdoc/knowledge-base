---
brief: 通过 webhook 的方式同步腾讯云日志服务 CLS 监控告警事件到快猫星云，实现告警事件自动化降噪处理
---

# 腾讯云日志服务CLS集成

---

通过 webhook 的方式同步腾讯云日志服务 CLS 监控告警事件到 Flashduty，实现告警事件自动化降噪处理。

## 在 Flashduty
---
您可通过以下2种方式，获取一个集成推送地址，任选其一即可。

### 使用专属集成

当您不需要将告警事件路由到不同的协作空间，优先选择此方式，更简单。

<details>
<summary>展开</summary>

1. 进入 Flashduty 控制台，选择 **协作空间**，进入某个空间的详情页面
2. 选择 **集成数据** tab，点击 **添加一个集成**，进入添加集成页面
3. 选择 **腾讯云CLS** 集成，点击 **保存**，生成卡片。
4. 点击生成的卡片，可以查看到 **推送地址**，复制备用，完成。


</details>

### 使用共享集成

当您需要根据告警事件的 Payload 信息，将告警路由到不同的协作空间，优先选择此方式。

<details>
<summary>展开</summary>

1. 进入 Flashduty 控制台，选择 **集成中心=>告警事件**，进入集成选择页面。
2. 选择 **腾讯云CLS** 集成：
- **集成名称**：为当前集成定义一个名称。
3. 点击 **保存** 后，复制当前页面的新生成的 **推送地址** 备用。
4. 点击 **创建路由**，为集成配置路由规则。您可以按条件匹配不同的告警到不同的协作空间，也可以直接设置默认协作空间作为兜底，后续再按需调整。
5. 完成。

</details>

## 在腾讯云的 CLS
---

**步骤 1：配置 通知渠道组**

<div class="md-block">

1. 登录您的腾讯云控制台，选择日志服务 CLS 产品，进入 监控告警 - 通知渠道组
2. 单击 __新建__ 开始新建

<img alt="drawing" width="600" src="https://fcdoc.github.io/img/9TVvjInBRsJOGHYptzIJmMgCaYUTRTohbSwENzk9_bg.avif" />

3. 如图，__名称__ 填写具体的渠道组名称，__渠道类型__选择“自定义接口回调”，__回调地址__ 填写集成的推送地址，__请求方法__ 选择POST

4. 点击 __确定__ 保存， __添加__ 可以添加多个渠道

</div>

**步骤 2：配置 告警策略**

<div class="md-block">


1. 登录您的腾讯云控制台，选择日志服务 CLS 产品，进入 监控告警 - 告警策略
2. 单击 __新建__ 开始新建

<img alt="drawing" width="600" src="https://fcdoc.github.io/img/FCfCmqlCwhjze8nSa88mkVt3nUX1myHyDFygJd8_lIc.avif" />

3. 如图，__告警名称__填写具体的告警名称，日志主题选择具体的日志主题

4. __执行语句__ 填写具体的查询语句，查询时间范围选择时间范围，点击预览可以查看执行的结果，触发条件输入具体的触发条件

5. __告警级别__，分为紧急、告警和提醒，根据告警的严重程序选择，执行周期根据需要选择

6. __多维分析__，触发告警时可针对原始日志进行额外的检索分析，将结果附加在告警通知中，以辅助定位告警原因。多维分析不会影响告警触发条件。

7. 告警通知，__通知渠道组__，可以关联到具体的渠道组

</div>


**步骤 3：配置 自定义回调**

<div class="md-block">

1. 关联渠道组后，可以看到回调内容配置

2. 请求头，可以添加具体的请求的headers

3. 请求内容，返回具体的请求数据格式，参考：

```json
{
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
```

</div>


## 状态对照
---
<div class="md-block">

腾讯云CLS监控告警级别到 Flashduty 映射关系：

| 腾讯云 CLS 监控 |  Flashduty    | 状态
| ------------- | --------- | --- |
| Info          |  Info     | 提醒
| Warn          |  Warning  | 警告
| Critical      |  Critical | 紧急

</div>
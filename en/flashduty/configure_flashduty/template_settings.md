---
brief: By customizing configuration templates, you can fulfill the need for personalized notification content
---

# Configure Notification Template

---

## In what scenarios would templates be utilized?
---
When the system encounters a `dispatched fault`, it employs template rendering for the [Incident](#Incident) and initiates notifications. Distribution can take place in the following scenarios:

1. Manually create and dispatch faults
2. Report an alarm event, and the system will automatically generate a fault, dispatching it based on the matched dispatch strategy
3. After a fault is created, manually alter the dispatch, i.e., re-dispatch
4. According to the dispatch policy settings, the system will automatically escalate the dispatch
5. After a fault is closed and reopened, re-dispatch according to the previous settings

We utilize `Golang template syntax` [template/html](https://pkg.go.dev/html/template@go1.18.1) to parse data, allowing for the completion of any complex rendering requirements.

- Please refer to the Chinese documentation [here](https://www.topgoer.com/%E5%B8%B8%E7%94%A8%E6%A0%87%E5%87%86%E5%BA%93/template.html#%E6%A8%A1%E6%9D%BF%E8%AF%AD%E6%B3%95) which supports logical judgments, loops, pipelines, and common functions;
- We have referenced the open-source library [sprig](https://github.com/flashcatcloud/sprig/tree/flashcat), which includes hundreds of commonly used functions that can be directly called in the template;
- If you wish to introduce additional functions, please submit a merge request

## What variables can be referenced?
---
**Example of referenced variable** :

```
// 引用标题
{{.Title}}

// 引用发起人名称
{{.Creator.PersonName}}

// 引用resource标签值
{{.Labels.resource}}

// 引用命名中带”.“的标签值
{{index .Labels "A.B"}}
```

**Complete list of variables** (direct quotes):
<span id="Incident"></span>
Field|type|Must contain|Definition
:-:|:-:|:-:|:---
ID | string | yes | Fault ID
`Title` | string | yes | Fault title
`Description` | string | yes | Fault description, may be empty
DetailUrl | string | yes | Fault details page address
Num | string | yes | Short fault identifier, used for easy visual recognition and may be duplicated
`IncidentSeverity` | string | yes | Severity, enumeration values: Critical, Warning, Info
IncidentStatus | string | yes | Fault status, enumeration values: Critical, Warning, Info, Ok
`Progress` | string | yes | Processing progress, enumeration values: Triggered, Processing, Closed
`StartTime` | int64 | yes | Trigger time, Unix seconds timestamp
LastTime | int64 | no | Latest event time, the latest combined event time in the associated alarm, Unix second timestamp, default is 0
EndTime | int64 | no | Recovery time, when all associated alarms are recovered, the fault will automatically recover and close. Unix seconds timestamp, default is 0
SnoozedBefore | int64 | no | Blocking deadline, Unix seconds timestamp, default is 0
AckTime | int64 | no | First claim time, Unix seconds timestamp, default is 0
CloseTime | int64 | no | The shutdown time, end_time is the fault recovery time, close_time is the shutdown time of the processing progress, it will be automatically closed when the fault is restored, and the fault recovery will not be affected when the fault is closed manually. Unix Second timestamp, default is 0
Creator | [Person](#Person) | no | Sponsor information does not exist when the system automatically generates it
Closer | [Person](#Person) | no | Close the person information and it will not exist when the fault automatically recovers
AssignedTo | [Assignment](Assignment) | no | Dispatch configuration
Responders | [][Responder](#Responder) | no | The list of handlers is initialized according to the dispatch configuration. If a non-dispatched person claims the fault, there will also be a corresponding record
ChannelID | int64 | no | Collaboration space ID, value is 0 when manually creating a global fault
ChannelName | string | no | Collaboration space name
GroupMethod | string | no | Aggregation method, enumeration value: n: no aggregation, p: aggregation according to rules, i: intelligent aggregation
`Labels` | map[string]string | no | Tags KV, Key and Value are all strings. There is no such information when created manually. When created automatically, it is the label information of the first alarm aggregated
AlertCnt | int64 | yes | Number of associated alarms
Alerts | [][Alert](#Alert) | no | Associated alarm details, this information is not available when manually created
FireType | string | no | Notification type, enumeration value: fire: notification, refire: circular notification
IsFlapping | bool | no | Whether it is in a jittering state, that is, occurs and recovers frequently, is related to the convergence configuration
Impact | string | no | Impact of the fault, fill in after the fault is closed
RootCause | string | no | Root cause of the fault, fill it in after the fault is closed
Resolution | string | no | Troubleshooting method, fill it out after the fault is closed

<span id="Person"></span>
**Person** (indirect reference) :
Field|type|Must contain|Definition
:-:|:-:|:-:|:---
person_id | int64 | yes | Person ID
person_name | string | yes | Personnel name
email | string | yes | Email address

<span id="Assignment"></span>
**Assignment** (indirect reference) :
Field|type|Must contain|Definition
:-:|:-:|:-:|:---
PersonIDs | []string| no | List of person IDs, only exists when assigned by person
EscalateRuleID | string | no | Dispatch policy ID, present only when dispatching according to policy
EscalateRuleName | string | no | Dispatch policy name
LayerIdx | string | no | Dispatch link, corresponding to the hierarchical index of the dispatch strategy, starting from 0
Type | string | yes | Dispatch type, enumeration value: assign: assign, reassign: reassign, escalate: upgrade assignment, reopen: reopen assignment

<span id="Responder"></span>
**Responder** (indirect reference) :
Field|type|Must contain|Definition
:-:|:-:|:-:|:---
PersonID | int64 | yes | Person ID
PersonName | string | yes | Personnel name
Email | string | yes | Email address
AssignedAt | int64 | yes | Dispatch time, Unix seconds timestamp, default is 0
AcknowledgedAt | int64 | no | Claim time, Unix seconds timestamp, default is 0

<span id="Alert"></span>
**Alert** (indirect reference) :
Field|type|Must contain|Definition
:-:|:-:|:-:|:---
Title | string | yes | Alarm title
Description | string | yes | Alarm description, may be empty
AlertSeverity | string | yes | Severity, enumeration values: Critical, Warning, Info
AlertStatus | string | yes | Alarm status, enumeration values: Critical, Warning, Info, Ok
Progress | string | yes | Processing progress, enumeration values: Triggered, Processing, Closed
StartTime | int64 | yes | Trigger time, Unix seconds timestamp
EndTime | int64 | no | Recovery time, Unix seconds timestamp, default is 0
CloseTime | int64 | no | Closing time, EndTime is the alarm recovery time, CloseTime is the closing time of the processing progress, the alarm will be closed automatically when it is restored, and the alarm recovery will not be affected when the alarm is manually closed. Unix seconds timestamp, default is 0
`Labels` | map[string]string | no | Tags KV, Key and Value are all strings

## FAQs
---
1. **How do I know what specific tag information `Labels` has?**

- Manually created faults do not have labels;
- The automatically created fault has a label, which is the same as the label of the first alarm that is merged. Go to the `故障列表` page, find a fault and view the fault details. You can see all label information

2. **I configure rendering according to a custom template, but the actual content sent uses `默认模板` ?**

- When creating a custom template, the system uses mock data to render the template to check for syntax errors;
- Mock data coverage scenarios are limited and may not match some of the logical branches in your template. During actual operation, rendering may fail;
- After rendering fails, the system will use the default template to ensure that the message is reachable;
- It is recommended that you use logical judgment to avoid rendering exceptions when you are not sure whether the reference variable exists, such as the `resource` tag:

```
// 错误做法：直接读取标签
{{.Labels.resource}}

// 推荐做法：先判断，再读取标签
{{if .Labels.resource}}{{.Labels.resource}}{{end}}
```

3. **The fault title contains `字符转义` such as " > "?**

```
// 使用toHtml函数
{{toHtml .Title}}

// 使用第一个不为空的值进行渲染，避免写复杂的if逻辑
{{toHtml .Title .TitleEnglish}}
```

4. **Time variables are all timestamp type, how about `转换时间格式` ?**

```
// date函数，将时间戳转换可读格式
// "2006-01-02 15:04:05"是一种常见格式，更多格式请检索网络
{{date "2006-01-02 15:04:05" .StartTime}}

// ago函数，将时间差转换为可读格式
{{ago .StartTime}}
```

5. **How to reference external variables inside for loop?**
```
// 在外部变量前增加”$“
{{range .Responders}}
{{if eq $.Progress "Triggered"}}
【待处理】{{.Email}}
{{end}}
{{end}}
```
6. **How to extract the field value with "." in the name, such as the information of " obj.instance " in the label?**

```
// 使用index函数
{{index .Labels "obj.instance"}}
```

7. **How to extract the information of a certain label in the fault-related alarm and remove duplicates?**

```
// 使用alertLabels函数，得到去重后的数组
{{alertLabels . "resource"}}

// 使用joinAlertLabels函数，得到去重后的数组，然后按照“sep”来拼接为字符串
{{joinAlertLabels . "resource" "sep"}}
```

8. **How to loop through and print labels ?**

```
// 完整遍历
{{range $k, $v := .Labels}}
{{$k}} : {{toHtml $v}}
{{end}}

// 排除单个label
{{range $k, $v := .Labels}}
{{if ne $k "resource"}}
{{$k}} : {{toHtml $v}}
{{end}}
{{end}}

// 排除多个labels
{{range $k, $v := .Labels}}
{{if not (in $k "resource" "body_text")}}
{{$k}} : {{toHtml $v}}
{{end}}
{{end}}

```


9. **How can I view more functions and examples of their use?**
- Function list: https://github.com/flashcatcloud/sprig/blob/master/functions.go#L97
- Usage example: View the corresponding _test.go file, such as date function test cases can be found at https://github.com/flashcatcloud/sprig/blob/master/date_test.go

The following is a detailed description of each notification channel.


## Feishu Application
---
You need to pre-configure `集成中心-即时消息-飞书` integration to send message cards. If no custom content is set, the system default template will be used to render all label information:

```
{{if .Description}}**description** :{{toHtml .Labels.body_text .Description}}{{end}}
{{if .Labels.resource}}**resource** : {{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{range $k, $v := .Labels}}
{{if not (in $k "resource" "body_text")}}**{{$k}}** : {{toHtml $v}}{{end}}{{end}}
```

As shown in the figure below:

<img src="https://fcdoc.github.io/img/J98dSP86cWqCChp7NGPy5yWabfG66jrDlLFIgzpMjYw.avif" alt="drawing" style="display: block; margin: 0 auto;" width="500"/>

If you want to display only key tag information, you can refer to the following code snippet:

- We have listed some common tags that you can delete at your own pace;
- In the Feishu app, the system will automatically delete empty rendering lines (caused by the non-existence of tags) for you, and you can configure it with confidence

```
{{if (index .Labels "resource")}}resource：{{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{if (index .Labels "check")}}check：{{toHtml (index .Labels "check")}}{{end}}
{{if (index .Labels "metric")}}metric：{{index .Labels "metric"}}{{end}}
{{if (index .Labels "prom_ql")}}prom_ql：{{toHtml (index .Labels "prom_ql")}}{{end}}
{{if (index .Labels "host_ql")}}host_ql：{{toHtml (index .Labels "host_ql")}}{{end}}
{{if (index .Labels "trigger_value")}}trigger_value：{{index .Labels "trigger_value"}}{{end}}
{{if (index .Labels "region")}}region：{{index .Labels "region"}}{{end}}
{{if (index .Labels "cluster")}}cluster：{{index .Labels "cluster"}}{{end}}
{{if (index .Labels "business")}}business：{{index .Labels "business"}}{{end}}
{{if (index .Labels "service")}}service：{{index .Labels "service"}}{{end}}
{{if (index .Labels "env")}}env：{{index .Labels "env"}}{{end}}
{{if (index .Labels "type")}}type：{{index .Labels "type"}}{{end}}
{{if (index .Labels "topic")}}topic：{{index .Labels "topic"}}{{end}}
{{if (index .Labels "cpu")}}cpu：{{index .Labels "cpu"}}{{end}}
{{if (index .Labels "device")}}device：{{index .Labels "device"}}{{end}}
{{if (index .Labels "path")}}path：{{index .Labels "path"}}{{end}}
{{if (index .Labels "fstype")}}fstype：{{index .Labels "fstype"}}{{end}}
{{if (index .Labels "name")}}name：{{index .Labels "name"}}{{end}}
{{if (index .Labels "mode")}}mode：{{index .Labels "mode"}}{{end}}
{{if (index .Labels "runbook_url")}}runbook_url：{{toHtml (index .Labels "runbook_url")}}{{end}}
```



## DingTalk Application
---
You need to pre-configure `集成中心-即时消息-钉钉` integration to send message cards. If no custom content is set, the system default template will be used to render all label information:

```
{{if .Description}}**description** :{{toHtml .Labels.body_text .Description}}{{end}}
{{if .Labels.resource}}**resource** : {{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{range $k, $v := .Labels}}
{{if not (in $k "resource" "body_text")}}**{{$k}}** : {{toHtml $v}}{{end}}{{end}}
```

As shown in the figure below:

<img src="https://fcdoc.github.io/img/weJqFl22lWcHW3KZo4lFHKRadEvGUclE7OL3W8BM2F0.avif" alt="drawing" style="display: block; margin: 0 auto;" width="500"/>

If you want to display only key tag information, you can refer to the following code snippet:

- We have listed some common tags that you can delete at your own pace;
- In the DingTalk application, the system will automatically delete empty rendering lines (caused by the non-existence of labels) for you, and you can configure it with confidence

```
{{if (index .Labels "resource")}}**resource**：{{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{if (index .Labels "metric")}}**metric**：{{index .Labels "metric"}}{{end}}
{{if (index .Labels "prom_ql")}}**prom_ql**：{{toHtml (index .Labels "prom_ql")}}{{end}}
{{if (index .Labels "trigger_value")}}**trigger_value**：{{index .Labels "trigger_value"}}{{end}}
{{if (index .Labels "host_ql")}}**host_ql**：{{toHtml (index .Labels "host_ql")}}{{end}}
{{if (index .Labels "region")}}**region**：{{index .Labels "region"}}{{end}}
{{if (index .Labels "cluster")}}**cluster**：{{index .Labels "cluster"}}{{end}}
{{if (index .Labels "business")}}**business**：{{index .Labels "business"}}{{end}}
{{if (index .Labels "service")}}**service**：{{index .Labels "service"}}{{end}}
{{if (index .Labels "env")}}**env**：{{index .Labels "env"}}{{end}}
{{if (index .Labels "type")}}**type**：{{index .Labels "type"}}{{end}}
{{if (index .Labels "topic")}}**topic**：{{index .Labels "topic"}}{{end}}
{{if (index .Labels "cpu")}}**cpu**：{{index .Labels "cpu"}}{{end}}
{{if (index .Labels "device")}}**device**：{{index .Labels "device"}}{{end}}
{{if (index .Labels "path")}}**path**：{{index .Labels "path"}}{{end}}
{{if (index .Labels "fstype")}}**fstype**：{{index .Labels "fstype"}}{{end}}
{{if (index .Labels "name")}}**name**：{{index .Labels "name"}}{{end}}
{{if (index .Labels "mode")}}**mode**：{{index .Labels "mode"}}{{end}}
{{if (index .Labels "runbook_url")}}**runbook_url**：{{index .Labels "runbook_url"}}{{end}}
```


## Enterprise WeChat Application
---

You need to pre-configure `集成中心-即时消息-企业微信` integration to send message cards. If no custom content is set, the system default template will be used and only common tag information will be rendered:

- We have listed some common tags that you can delete at your own pace;
- In the enterprise WeChat application, the system will automatically delete the rendering blank lines (caused by the non-existence of the label) for you, and you can configure it with confidence

```
{{if (index .Labels "resource")}}resource：{{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{if (index .Labels "metric")}}metric：{{index .Labels "metric"}}{{end}}
{{if (index .Labels "prom_ql")}}prom_ql：{{toHtml (index .Labels "prom_ql")}}{{end}}
{{if (index .Labels "trigger_value")}}trigger_value：{{index .Labels "trigger_value"}}{{end}}
{{if (index .Labels "host_ql")}}host_ql：{{toHtml (index .Labels "host_ql")}}{{end}}
{{if (index .Labels "region")}}region：{{index .Labels "region"}}{{end}}
{{if (index .Labels "cluster")}}cluster：{{index .Labels "cluster"}}{{end}}
{{if (index .Labels "business")}}business：{{index .Labels "business"}}{{end}}
{{if (index .Labels "service")}}service：{{index .Labels "service"}}{{end}}
{{if (index .Labels "env")}}env：{{index .Labels "env"}}{{end}}
{{if (index .Labels "type")}}type：{{index .Labels "type"}}{{end}}
{{if (index .Labels "topic")}}topic：{{index .Labels "topic"}}{{end}}
{{if (index .Labels "cpu")}}cpu：{{index .Labels "cpu"}}{{end}}
{{if (index .Labels "device")}}device：{{index .Labels "device"}}{{end}}
{{if (index .Labels "path")}}path：{{index .Labels "path"}}{{end}}
{{if (index .Labels "fstype")}}fstype：{{index .Labels "fstype"}}{{end}}
{{if (index .Labels "name")}}name：{{index .Labels "name"}}{{end}}
{{if (index .Labels "mode")}}mode：{{index .Labels "mode"}}{{end}}
{{if (index .Labels "runbook_url")}}runbook_url：{{toHtml (index .Labels "runbook_url")}}{{end}}
```

As shown in the figure below:

<img src="https://fcdoc.github.io/img/kc9K5HzTgAu_MmhpaEV9CWqmg5AZwDmV6X4g_T10mnc.avif" alt="drawing" style="display: block; margin: 0 auto;" width="500"/>

**Note that Enterprise WeChat limits the length of the card. In the template rendering area, you can render no more than 8 lines of content, and the part exceeding 8 lines will be hidden.**



## Slack App
---
You need to pre-configure `集成中心-即时消息- Slack` integration to send message cards. If no custom content is set, the system default template will be used and only common tag information will be rendered:

```
{{if .Description}}*description* :{{toHtml .Labels.body_text .Description}}{{end}}
{{if .Labels.resource}}*resource* : {{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{range $k, $v := .Labels}}
{{if not (in $k "resource" "body_text")}}*{{$k}}* : {{toHtml $v}}{{end}}{{end}}
```


As shown in the figure below:

<img src="https://fcdoc.github.io/img/0m3LAvve_fgFH8cVvhTk6Z4Qwpw5SUFee7hf7XliCAs.avif" alt="drawing" style="display: block; margin: 0 auto;" width="600"/>

If you want to display only key tag information, you can refer to the following code snippet:

- We have listed some common tags that you can delete at your own pace;
- Messages can be sent with a length of about 15,000 characters, and will be truncated if exceeded;
- In the Slack application, the system will automatically delete the rendering empty lines (caused by the non-existence of the label) for you, and you can configure it with confidence

```
{{if (index .Labels "resource")}}*resource*：{{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{if (index .Labels "metric")}}*metric*：{{index .Labels "metric"}}{{end}}
{{if (index .Labels "prom_ql")}}*prom_ql*：{{toHtml (index .Labels "prom_ql")}}{{end}}
{{if (index .Labels "trigger_value")}}*trigger_value*：{{index .Labels "trigger_value"}}{{end}}
{{if (index .Labels "host_ql")}}*host_ql*：{{index .Labels "host_ql"}}{{end}}
{{if (index .Labels "region")}}*region*：{{index .Labels "region"}}{{end}}
{{if (index .Labels "cluster")}}*cluster*：{{index .Labels "cluster"}}{{end}}
{{if (index .Labels "business")}}*business*：{{index .Labels "business"}}{{end}}
{{if (index .Labels "service")}}*service*：{{index .Labels "service"}}{{end}}
{{if (index .Labels "env")}}*env*：{{index .Labels "env"}}{{end}}
{{if (index .Labels "type")}}*type*：{{index .Labels "type"}}{{end}}
{{if (index .Labels "topic")}}*topic*：{{index .Labels "topic"}}{{end}}
{{if (index .Labels "cpu")}}*cpu*：{{index .Labels "cpu"}}{{end}}
{{if (index .Labels "device")}}*device*：{{index .Labels "device"}}{{end}}
{{if (index .Labels "path")}}*path*：{{index .Labels "path"}}{{end}}
{{if (index .Labels "fstype")}}*fstype*：{{index .Labels "fstype"}}{{end}}
{{if (index .Labels "name")}}*name*：{{index .Labels "name"}}{{end}}
{{if (index .Labels "mode")}}*mode*：{{index .Labels "mode"}}{{end}}
{{if (index .Labels "runbook_url")}}*runbook_url*：{{index .Labels "runbook_url"}}{{end}}
```



## Microsoft Teams App
---
You need to pre-configure `集成中心-即时消息- Microsoft Teams` integration to send message cards. If no custom content is set, the system default template will be used and only common tag information will be rendered:

```
{{if .Description}}**description** :{{toHtml .Labels.body_text .Description}}{{end}}
{{if .Labels.resource}}**resource** : {{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{range $k, $v := .Labels}}
{{if not (in $k "resource" "body_text" "body_text_with_table")}}**{{$k}}** : {{toHtml $v}}{{end}}{{end}}
```


As shown in the figure below:

<img src="https://fcdoc.github.io/img/BAqnlzAiIJTgO4QpAvulu4fB62HIMfiWSXjldSxB5Uk.avif" alt="drawing" style="display: block; margin: 0 auto;" width="300"/>

If you want to display only key tag information, you can refer to the following code snippet:

- We have listed some common tags that you can delete at your own pace;
- The message can be sent with a length of about 28KB bytes, and an error will be reported if it exceeds;
- In the Microsoft Teams application, the system will automatically delete the rendering blank lines (caused by the non-existence of the label) for you, and you can configure it with confidence

```
{{if (index .Labels "resource")}}**resource**：{{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{if (index .Labels "metric")}}**metric**：{{index .Labels "metric"}}{{end}}
{{if (index .Labels "prom_ql")}}**prom_ql**：{{toHtml (index .Labels "prom_ql")}}{{end}}
{{if (index .Labels "trigger_value")}}**trigger_value**：{{index .Labels "trigger_value"}}{{end}}
{{if (index .Labels "host_ql")}}**host_ql**：{{index .Labels "host_ql"}}{{end}}
{{if (index .Labels "region")}}**region**：{{index .Labels "region"}}{{end}}
{{if (index .Labels "cluster")}}**cluster**：{{index .Labels "cluster"}}{{end}}
{{if (index .Labels "business")}}**business**：{{index .Labels "business"}}{{end}}
{{if (index .Labels "service")}}**service**：{{index .Labels "service"}}{{end}}
{{if (index .Labels "env")}}**env**：{{index .Labels "env"}}{{end}}
{{if (index .Labels "type")}}**type**：{{index .Labels "type"}}{{end}}
{{if (index .Labels "topic")}}**topic**：{{index .Labels "topic"}}{{end}}
{{if (index .Labels "cpu")}}**cpu**：{{index .Labels "cpu"}}{{end}}
{{if (index .Labels "device")}}**device**：{{index .Labels "device"}}{{end}}
{{if (index .Labels "path")}}**path**：{{index .Labels "path"}}{{end}}
{{if (index .Labels "fstype")}}**fstype**：{{index .Labels "fstype"}}{{end}}
{{if (index .Labels "name")}}**name**：{{index .Labels "name"}}{{end}}
{{if (index .Labels "mode")}}**mode**：{{index .Labels "mode"}}{{end}}
{{if (index .Labels "runbook_url")}}**runbook_url**：{{index .Labels "runbook_url"}}{{end}}
```





## Microsoft Teams App
---
You need to pre-configure `集成中心-即时消息- Microsoft Teams` integration to send message cards. If no custom content is set, the system default template will be used and only common tag information will be rendered:

```
{{if .Description}}**description** :{{toHtml .Labels.body_text .Description}}{{end}}
{{if .Labels.resource}}**resource** : {{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{range $k, $v := .Labels}}
{{if not (in $k "resource" "body_text" "body_text_with_table")}}**{{$k}}** : {{toHtml $v}}{{end}}{{end}}
```


As shown in the figure below:

<img src="https://fcdoc.github.io/img/BAqnlzAiIJTgO4QpAvulu4fB62HIMfiWSXjldSxB5Uk.avif" alt="drawing" style="display: block; margin: 0 auto;" width="300"/>

If you want to display only key tag information, you can refer to the following code snippet:

- We have listed some common tags that you can delete at your own pace;
- The message can be sent with a length of about 28KB bytes, and an error will be reported if it exceeds;
- In the Microsoft Teams application, the system will automatically delete the rendering blank lines (caused by the non-existence of the label) for you, and you can configure it with confidence

```
{{if (index .Labels "resource")}}**resource**：{{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}
{{if (index .Labels "metric")}}**metric**：{{index .Labels "metric"}}{{end}}
{{if (index .Labels "prom_ql")}}**prom_ql**：{{toHtml (index .Labels "prom_ql")}}{{end}}
{{if (index .Labels "trigger_value")}}**trigger_value**：{{index .Labels "trigger_value"}}{{end}}
{{if (index .Labels "host_ql")}}**host_ql**：{{index .Labels "host_ql"}}{{end}}
{{if (index .Labels "region")}}**region**：{{index .Labels "region"}}{{end}}
{{if (index .Labels "cluster")}}**cluster**：{{index .Labels "cluster"}}{{end}}
{{if (index .Labels "business")}}**business**：{{index .Labels "business"}}{{end}}
{{if (index .Labels "service")}}**service**：{{index .Labels "service"}}{{end}}
{{if (index .Labels "env")}}**env**：{{index .Labels "env"}}{{end}}
{{if (index .Labels "type")}}**type**：{{index .Labels "type"}}{{end}}
{{if (index .Labels "topic")}}**topic**：{{index .Labels "topic"}}{{end}}
{{if (index .Labels "cpu")}}**cpu**：{{index .Labels "cpu"}}{{end}}
{{if (index .Labels "device")}}**device**：{{index .Labels "device"}}{{end}}
{{if (index .Labels "path")}}**path**：{{index .Labels "path"}}{{end}}
{{if (index .Labels "fstype")}}**fstype**：{{index .Labels "fstype"}}{{end}}
{{if (index .Labels "name")}}**name**：{{index .Labels "name"}}{{end}}
{{if (index .Labels "mode")}}**mode**：{{index .Labels "mode"}}{{end}}
{{if (index .Labels "runbook_url")}}**runbook_url**：{{index .Labels "runbook_url"}}{{end}}
```



## Feishu Robot
---
Feishu Robot only supports sending plain text messages.

- message0 `Maximum length is 4000 bytes, truncated and sent if exceeded`;
- If the text contains `<br>`, it will `first remove empty lines and then replace <br> with newline characters` during rendering;
- If custom content is not set, the system default template will be used, displaying only key information:

```
{{fireReason .}}INC #{{.Num}} {{toHtml .Title}}
-----
协作空间：{{if .ChannelName}}{{.ChannelName}}{{else}}无{{end}}
严重程度：{{.IncidentSeverity}}
触发时间：{{date "2006-01-02 15:04:05" .StartTime}}
持续时长：{{ago .StartTime}}{{if gt .AlertCnt 1}}
聚合告警：{{.AlertCnt}}条{{end}}{{if .Labels.resource}}
告警对象：{{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}{{if .Description}}
故障描述：{{toHtml .Description}}{{end}}{{if gt (len .Responders) 0}}
分派人员：{{range .Responders}}@{{.PersonName}} {{end}}{{end}}
<br>详情：{{.DetailUrl}}
```



## DingTalk Robot
---
DingTalk Robot only supports sending Markdown messages ([grammar restrictions](https://open.dingtalk.com/document/robots/custom-robot-access#title-7ur-3ok-s1a)).

- message0 `Maximum length is 4000 bytes, truncated and sent if exceeded`;
- If the text contains `<br>`, it will `first remove empty lines and then replace <br> with newline characters` during rendering;
- If custom content is not set, the system default template will be used, displaying only key information:

```
{{fireReason .}}INC [#{{.Num}}]({{.DetailUrl}}) {{toHtml .Title}}

---
- 协作空间：{{if .ChannelName}}{{.ChannelName}}{{else}}无{{end}}
- 严重程度：{{$s := colorSeverity .IncidentSeverity}}{{toHtml $s}}
- 触发时间：{{date "2006-01-02 15:04:05" .StartTime}}
- 持续时长：{{ago .StartTime}}{{if gt .AlertCnt 1}}
- 聚合告警：{{.AlertCnt}}条{{end}}{{if .Labels.resource}}
- 告警对象：{{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}{{if .Description}}
- 故障描述：{{toHtml .Description}}{{end}}{{if gt (len .Responders) 0}}
- 分派人员：{{range .Responders}}@{{.PersonName}} {{end}}{{end}}
---
<br>[详情]({{.DetailUrl}})|[认领]({{.DetailUrl}}?ack=1)
```



## Enterprise WeChat Robot
---
Qiwei Robot only supports sending Markdown messages ([grammar restrictions](https://developer.work.weixin.qq.com/document/path/91770#markdown%E7%B1%BB%E5%9E%8B)).

- message0 `Maximum length is 4000 bytes, truncated and sent if exceeded`;
- If the text contains `<br>`, it will `first remove empty lines and then replace <br> with newline characters` during rendering;
- If custom content is not set, the system default template will be used, displaying only key information:

```
{{fireReason .}}**INC [#{{.Num}}]({{.DetailUrl}}) {{toHtml .Title}}**
> 协作空间：<font color="warning">{{if .ChannelName}}{{.ChannelName}}{{else}}无{{end}}</font>
> 严重程度：<font color="warning">{{.IncidentSeverity}}</font>
> 触发时间：{{date "2006-01-02 15:04:05" .StartTime}}
> 持续时长：{{ago .StartTime}}{{if gt .AlertCnt 1}}
> 聚合告警：{{.AlertCnt}}条{{end}}{{if .Labels.resource}}
> 告警对象：{{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}{{if .Description}}
> 故障描述：{{toHtml .Description}}{{end}}{{if gt (len .Responders) 0}}
> 分派人员：{{range .Responders}}@{{.PersonName}} {{end}}{{end}}
<br>[详情]({{.DetailUrl}})|[认领]({{.DetailUrl}}?ack=1)
```



## Telegram Bot
---
- Configure the Telegram service address that can be accessed in China;
- message0 `Maximum length is 4096 characters, not sent if exceeded`;
- If the text contains `<br>`, it will `first remove empty lines and then replace <br> with newline characters` during rendering;
- If custom content is not set, the system default template will be used, displaying only key information:

```
{{fireReason .}}INC [#{{.Num}}]({{.DetailUrl}}) {{toHtml .Title}}
-----
协作空间：{{if .ChannelName}}{{.ChannelName}}{{else}}无{{end}}
严重程度：{{.IncidentSeverity}}
触发时间：{{date "2006-01-02 15:04:05" .StartTime}}
持续时长：{{ago .StartTime}}{{if gt .AlertCnt 1}}
聚合告警：{{.AlertCnt}}条{{end}}{{if .Labels.resource}}
告警对象：{{toHtml (joinAlertLabels . "resource" ", ")}}({{.Labels.resource}}){{end}}{{if .Description}}
故障描述：{{toHtml .Description}}{{end}}{{if gt (len .Responders) 0}}
分派人员：{{range .Responders}}@{{.PersonName}} {{end}}{{end}}

<br>[详情]({{.DetailUrl}})|[认领]({{.DetailUrl}}?ack=1)
```



## Slack Bot
---
- The message `can be sent with a character length of about 15000, and will be truncated if exceeded`;
- If the text contains `<br>`, it will `first remove empty lines and then replace <br> with newline characters` during rendering;
- If custom content is not set, the system default template will be used, displaying only key information:

```
{{fireReason .}}INC <{{.DetailUrl}}|#{{.Num}}> {{toHtml .Title}}
-----
协作空间：{{if .ChannelName}}{{.ChannelName}}{{else}}无{{end}}
严重程度：{{.IncidentSeverity}}
触发时间：{{date "2006-01-02 15:04:05" .StartTime}}
持续时长：{{ago .StartTime}}{{if gt .AlertCnt 1}}
聚合告警：{{.AlertCnt}}条{{end}}{{if .Labels.resource}}
告警对象：{{toHtml (joinAlertLabels . "resource" ", ")}}{{end}}{{if .Description}}
故障描述：{{toHtml .Description}}{{end}}{{if gt (len .Responders) 0}}
分派人员：{{range .Responders}}@{{.PersonName}} {{end}}{{end}}
-----
<br><{{.DetailUrl}}|详情>|<{{.DetailUrl}}?ack=1|认领>
```

## Zoom Robot
---
- The message `can be sent with a character length of about 4000, and will be truncated if exceeded`;
- If the text contains `<br>`, it will `first remove empty lines and then replace <br> with newline characters` during rendering;
- Message format `遵循Zoom消息格式` , the current robot application does not support Markdown other formats can refer to the official website : [https://developers.zoom.us/docs/team-chat-apps/customizing-messages/](https://developers.zoom.us/docs/team-chat-apps/customizing-messages/)
- If custom content is not set, the system default template will be used, displaying only key information:

```
{"head": {
"text": "{{fireReason .}}INC [#{{.Num}}] {{toHtml .Title}}",
"style": {
"bold": true,
"italic": false,
"color": "{{$s := serverityToColor .IncidentSeverity}}{{toHtml $s}}"
}
},
"body": [
{
"type": "message",
"text": "协作空间：{{if .ChannelName}}{{.ChannelName}}{{else}}无{{end}}",
"style": {
"bold": false,
"italic": false
}
},
{
"type": "message",
"text": "严重程度：{{.IncidentSeverity}}",
"style": {
"bold": false,
"italic": false,
"color": "{{$s := serverityToColor .IncidentSeverity}}{{toHtml $s}}"
}
},
{
"type": "message",
"text": "持续时长：{{ago .StartTime}}{{if gt .AlertCnt 1}}",
"style": {
"bold": false,
"italic": false
}
},
{
"type": "message",
"text": "聚合告警：{{.AlertCnt}}条{{end}}{{if .Labels.resource}}",
"style": {
"bold": false,
"italic": false
}
},
{
"type": "message",
"text": "告警对象：{{.Labels.resource}}{{end}}{{if .Description}}",
"style": {
"bold": false,
"italic": false
}
},
{
"type": "message",
"text": "故障描述：{{toHtml .Description}}{{end}}{{if gt (len .Responders) 0}}",
"style": {
"bold": false,
"italic": false
}
},
{
"type": "message",
"text": "分派人员：{{range .Responders}}@{{.PersonName}}{{end}}{{end}}",
"style": {
"bold": false,
"italic": false
}
},
{
"type": "message",
"text": "查看详情",
"link": "{{.DetailUrl}}{{if .IsFlapping}}"
},
{
"type": "message",
"text": "注意：当前故障状态变化频繁，将收敛通知{{.Flapping.MuteMinutes}}分钟，建议您优化告警策略。{{end}}{{if .IsInStorm}}",
"style": {
"bold": true,
"italic": false
}
},
{
"type": "message",
"text": "注意：当前故障已聚合{{.AlertCnt}}条告警，触发告警风暴，请加急处理！{{end}}",
"style": {
"bold": true,
"italic": false
}
}
]
}
```



## Short Message
---
If custom content is not set, the system default template will be used to render the notification:

```
您有故障待处理：{{toHtml .Title}}，协作空间：{{.ChannelName}}，等级：{{.IncidentSeverity}}{{if gt .AlertCnt 1}}，共聚合{{.AlertCnt}}条告警{{end}}
```



## Mail
---
If custom content is not set, the system default template will be used to render the notification:

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
<title>{{.Title}}</title>
<html lang="zh">

<head data-id="__react-email-head">
<style>
.bg-Critical { background-color: #C80000; }
.bg-Warning { background-color: #FA7D00; }
.bg-Info { background-color: #FABE00; }
.bg-Ok { background-color: rgb(132 204 22); }
.text-Critical { color: #C80000; }
.text-Warning { color: #FA7D00; }
.text-Info { color: #FABE00; }
.text-Ok { color: rgb(132 204 22); }
.text-title {font-weight:500;width:6rem;flex-shrink:0}
.text-content {color:rgb(55,65,81)}
</style>
</head>

<body data-id="__react-email-body" style="background-color:rgb(255,255,255);border-radius:0.25rem;margin-top:2.5rem;margin-bottom:2.5rem;margin-left:auto;margin-right:auto;padding:1rem;min-width:400px;max-width:660px;font-family:ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Helvetica Neue, Arial, Noto Sans, sans-serif, Apple Color Emoji, Segoe UI Emoji, Segoe UI Symbol, Noto Color Emoji">
<div style="width:100%;height:0.375rem;margin-bottom:2rem" class="bg-{{.IncidentSeverity}}"></div>
<div style="display:flex;align-items:center;margin-bottom:1.5rem">
<div style="display:flex;align-items:flex-end;gap:1rem"><img witdh="120" data-id="react-email-img" src="https://fcdoc.github.io/img/5sp7YaSh-LnDzReB0Qnd3HSfrGRY6X8Amie5S-FmmNc.avif" height="40" style="display:block;outline:none;border:none;text-decoration:none" /><span style="font-size:1.25rem;line-height:1.75rem;font-weight:600">您有故障待处理</span></div>
</div>
<div style="background-color:rgb(243,244,246);padding:2rem;margin-top:1rem;border-radius:0.5rem">
<div style="display:flex;flex-direction:column;gap:0.75rem">
<div style="display:flex">
<div class="text-title">故障标题</div>
<div class="text-content">{{.Title}}</div>
</div>
<div style="display:flex">
<div class="text-title">严重程度</div>
<div class="text-{{.IncidentSeverity}}">{{.IncidentSeverity}}</div>
</div>
<div style="display:flex">
<div class="text-title">协作空间</div>
<div class="text-content">{{if .ChannelName}}{{.ChannelName}}{{else}}无{{end}}</div>
</div>
<div style="display:flex">
<div class="text-title">触发时间</div>
<div class="text-content">{{date "2006-01-02 15:04:05" .StartTime}}</div>
</div>
{{if .CreatorID}}
<div style="display:flex">
<div class="text-title">发起人员</div>
<div class="text-content">{{.Creator.PersonName}}</div>
</div>
{{end}}
{{if gt (len .Responders) 0}}
<div style="display:flex">
<div class="text-title">分派人员</div>
<div class="text-content">{{range .Responders}}@{{.PersonName}} {{end}}</div>
</div>
{{end}}
<div style="display:flex">
<div class="text-title">处理进度</div>
<div class="text-content">{{.Progress}}</div>
</div>
<div style="display:flex">
<div class="text-title">故障描述</div>
<div style="color:rgb(55,65,81);margin-top:0.125rem">
<div data-id="react-email-markdown">{{toHtml .Description}}</div>
</div>
</div>
{{if .Labels.resource}}
<div style="display:flex;margin-bottom:0.5rem;">
<div style="color:#000;font-weight:500;width:6rem;margin-right:1rem;">告警对象</div>
<div style="color:rgb(55,65,81);margin-top:0.125rem">
<div data-id="react-email-markdown">{{toHtml (joinAlertLabels . "resource" ", ")}}</div>
</div>
</div>
{{end}}
</div>
<div style="display:flex;gap:1rem;margin-top:2rem"><a href="{{.DetailUrl}}?ack=1" data-id="react-email-button" target="_blank" style="line-height:100%;text-decoration:none;display:inline-block;max-width:100%;padding:0px 0px"><span></span><span style="max-width:100%;display:inline-block;line-height:120%;mso-padding-alt:0px;mso-text-raise:0"><div style="padding-left:2rem;padding-right:2rem;padding-top:0.5rem;padding-bottom:0.5rem;background-color:rgb(108,83,177);border-radius:0.25rem;font-size:1rem;line-height:1.5rem;color:rgb(255,255,255);font-weight:600;transition-property:color, background-color, border-color, text-decoration-color, fill, stroke, opacity, box-shadow, transform, filter, backdrop-filter;transition-timing-function:cubic-bezier(0.4, 0, 0.2, 1);transition-duration:150ms">立即认领</div></span><span></span></a><a href="{{.DetailUrl}}" data-id="react-email-button" target="_blank" style="color:#61dafb;line-height:100%;text-decoration:none;display:inline-block;max-width:100%;padding:0px 0px"><span></span><span style="max-width:100%;display:inline-block;line-height:120%;mso-padding-alt:0px;mso-text-raise:0"><div style="padding-left:2rem;padding-right:2rem;padding-top:0.5rem;padding-bottom:0.5rem;background-color:rgb(255,255,255);border-width: 1px;border-style:solid;border-color:rgb(229,231,235);border-radius:0.25rem;font-size:1rem;line-height:1.5rem;color:rgb(0,0,0);font-weight:600">查看详情</div></span><span></span></a></div>
</div>
<div style="display:flex;justify-content:flex-end;align-items:flex-end;margin-top:2rem">
<div style="font-size:0.875rem;line-height:1.25rem;font-weight:500">ALL RIGHTS RESERVED © 北京快猫星云科技有限公司</div>
</div>
</body>

</html>
```

As shown in the figure below:

<img src="https://fcdoc.github.io/img/t84afsCGAkRd_qtwBXqtWMEseQIZRcdCoeRYViFtl8Y.avif" alt="drawing" style="display: block; margin: 0 auto;" width="500"/>
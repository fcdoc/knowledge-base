---
brief: 通过分派策略可以将不同业务或不同团队的告警事件分派到相应的处理组，且能够通过不同渠道触达到相应的处理成员
---

# 配置分派策略

---

每个协作空间应至少有一个分派策略，通过分派策略可以将不同业务或不同团队的告警事件分派到相应的处理组，且能够通过不同渠道触达到相应的处理成员，如常见的IM应用、短信语音、机器人等方式。同时支持多环节的通知配置以及环节之间的自动升级；当协作空间没有配置分派策略时，接入到该协作空间告警将不会触发通知。

## 策略配置
---
### 时间过滤
- 默认所有时间的故障均按该策略通知。
- 支持按星期中的某天进行选择是否分派，比如只有星期一到星期五的故障才进行分派处理，星期六星期日的故障不处理。
- 支持按服务日历进行选择是否分派（服务日历需提前创建），可根据假期或工作日进行配置，如只有交易日的故障才需要通知，一般适用于证券行业。

![rilitongzhi.png](https://fcdoc.github.io/img/gsUqruaXsUQO8Vbb-QgEIJb23EQ3jUZDMWBvtOYSEBs.avif)

### 故障过滤
- 默认全部故障均按该策略通知。
- 支持按标题、级别和标签等条件匹配故障，如告警级别为 Info 的遵循该分派分派。

![tiaojian.png](https://fcdoc.github.io/img/WyGIe6d3UjoWaGg4Y8KCZ87KCalIEM3cdR1YMRI6RVc.avif)

前往 [如何配置过滤条件](https://docs.flashcat.cloud/zh/flashduty/how-to-filter)，了解更多。

## 分派配置
---

### 分派对象
- **个人：** 指定某些成员接收该告警，支持多选，不可重复选择。
- **团队：** 指定某团队接收该告警，支持多选，团队成员有重复时，只向该成员发送一次通知。
- **值班：** 指定某值班表接收该告警，具体接收成员按值班规则中的值班人进行接收，支持多选，值班人员重复时，只向值班人发送一次通知。
- **组合：** 即个人、团队、值班表一起选择。

> [!NOTE]
> 想与内部自研系统打通，实现动态分派？
>
> 请参考 [动态设置分派人员](https://docs.flashcat.cloud/zh/flashduty/dynamic-notifications)。

### 单聊渠道
单聊即一对一的进行推送。如邮件、短信、语音以及部分 IM 应用。

- **遵循个人爱好：** 通知方式由成员自行在[账户配置](https://docs.flashcat.cloud/zh/flashduty/preference-settings)各个告警类别的接收渠道与方式。
- **遵循统一设置：** 由策略配置人员统一配置通知对象中成员的接收告警的渠道和方式。

### 群聊渠道

群聊即推送到群，并针对分派人员进行特别提醒。包括各类 Webhook 机器人，以及部分 IM 应用。

- 群聊中可以选择各个应用以及群机器人的方式进行触达到接收人，**选择IM应用通知时**，通知对象需要先与对应的应用进行关联，具体可以参考[即时消息集成](https://docs.flashcat.cloud/zh/flashduty/lark-integration-guide)

> [!NOTE]
> 个人与群聊通知渠道请至少选择一个。如果您不期望通知到任何个人，仅通知到群，您可以设置一个空团队作为分派对象。

### 循环通知

- 循环通知默认关闭，即相同事件默认通知一次，如需开启，请合理配置通知次数。注意，您输入的值，至少为`2`次，才能获得额外的循环通知。
- 如果故障被认领，将终止循环通知。


### 升级分派

- 为了确保故障一定有人处理，我们可以设置故障超时未关闭，自动升级。即设置多个环节。
- 您可以选择故障__超时未关闭__或__超时未被认领__时，自动升级。
- 典型场景是：主备值班人员之间，上下级之间，一二线之间进行层层升级。

您也可以手动升级故障，前往 [升级与分派故障](https://docs.flashcat.cloud/zh/flashduty/escalate-incidents) 了解更多。

### 策略顺序调整
- 多个分派策略时，分派通知时是按顺序依次匹配，匹配到即终止，请在配置时充分考虑相关分派条件。
- 不同策略之间支持以拖拽的方式进行调整通知顺序，调整即生效，请慎重操作。

> [!NOTE]
> 如果您需要在一个协作空间下，设置多个分派策略，且需要确保每一个故障都得到通知。设置一个没有筛选条件的分派策略作为兜底，是一个好主意。

> [!WARN]
> 我们不建议您，将一个协作空间设置的过大。尤其是，使用一个协作空间来管理某个大型业务的所有告警。这会导致您维护很多不同的分派策略，使得长期维护工作负担加重，更混乱也更易出错。


## 策略配置原则
---
常规的分派策略配置应该考虑以下几个方面：

1. **通知对象能力匹配：** 确保通知对象具有处理该空间告警的能力和权限。这意味着只有相关人员或团队能够接收到与其工作相关的告警，避免将无关的告警发送给不相关的人员。
2. **多渠道通知：** 采用多种通知方式确保通知对象能够及时接收到告警信息。例如，通过短信、邮件、即时通讯工具等多种渠道发送通知，以提高通知的及时性和可靠性，但不同级别的告警建议采用不同通知方式，避免消息过载。
3. **告警升级机制：** 当告警长时间没有被认领或处理时，应该有相应的升级机制。这可以是自动将告警升级到下一级别的处理人员或团队，或者将告警发送给多个环节的处理人员以确保及时处理。


## 常见问题
---

<details>
<summary>有告警产生，但没有收到通知怎么排查</summary>
前往 故障详情=>时间线, 查看触发通知流程中的各个渠道通知状态是否正常，如果失败会有失败信息供参考，更多原因可以联系技术支持进行协助排查。
</details>

<details>
<summary>为什么通知方式与我的个人偏好设置不符？</summary>
Flashduty单聊通知渠道支持两种设定，一种是“遵循个人偏好”，一种是“遵循统一设定”。仅在“遵循个人偏好”设定下，会按照您的设置进行个性化通知。

前往 协作空间详情=>分派策略 中，查看您的具体设定。
</details>
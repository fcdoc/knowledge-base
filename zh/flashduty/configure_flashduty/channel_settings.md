---
brief: 协作空间是什么，都有哪些功能，以及如何管理
---

# 协作空间

---

协作空间作为一个组织和管理故障排查的核心载体，旨在将不同团队、不同业务系统或不同服务模块的告警进行分别管理，每个协作空间通常对应于团队日常运营和维护的一个特定范围。

## 创建协作空间
---

### 空间规划要领

&check;  建议以业务系统、团队职责等某一个维度进行合理的创建协作空间，比如创建一个订单管理系统的协作空间，该空间接收订单处理流程相关的故障事件；这样可以确保信息聚焦与高效协同。可以让相关团队成员迅速获取到与自己工作直接相关的信息，提升处理效率，同时减少跨领域干扰，有利于职责清晰和任务追踪，促进项目管理和问题解决的时效性。

&cross; 应避免将不同类型或互不相关的告警接入到同一个协作空间，比如某空间即接入订单相关的告警又接入了硬件资源或网络相关的告警事件，这样处理、分派以及分析时都将变得混乱，会使团队难以准确识别和优先处理问题，从而降低工作效率。


### 开始创建
登录控制台进行创建，路径：**故障管理=>协作空间=>创建协作空间**。

- **空间名称：** 建议以部门、小组、业务类型进行命名和规划，以便更直观的了解该空间的用途。
- **描述信息：** 建议简单概述该空间所承接的业务以及接入哪种类型的告警。
- **管理团队：** 创建时可以设置该空间的管理团队，**团队所属成员对该空间有全部操作权限**，非创建者对该空间的配置只读。
- **超时自动关闭：** 即超过N分钟未关闭的故障**系统会将其自动关闭**（对该空间下所有新故障生效），超时关闭的故障也**会有相应的关闭通知**（通知渠道取决于[分派策略](https://docs.flashcat.cloud/zh/flashduty/escalate-rule-settings)的配置）。
- 未规划好该空间的故障如何分派时，可以**跳过设定分派策略**，创建完成后可以继续配置分派策略。
- 创建时接入的集成类型**属于专属集成**，仅对该空间生效，同样可以忽略且创建完成后进行配置。


## 管理协作空间
---
### 空间概览
- 账户成员可以看到全部协作空间，但只能操作其负责的协作空间。
- 鼠标悬放在某个协作空间处，点击五角星即可完成**收藏和取消收藏**。
- 默认看到的是全部协作空间，可以**通过"我管理的"、"我收藏的"查看与“我”有关的协作空间**。
- 当协作空间很多，但自己关注的空间排序比较靠后时，可以**通过右上角的排序功能将自己关注的协作空间往前排序**。
- 排序时可以自由编排，且**只对当前用户生效，不影响其他用户**。


### 变更信息
- 空间名称、描述、超时自动关闭、管理团队支持变更，可在空间详情->基础设置中进行修改。
- 协作空间禁用后不再接收告警，可以继续操作该空间的故障和相关配置。
- 删除空间并不会删除已接入该空间的故障数据，但删除空间后该空间不可恢复，请谨慎操作。

### 故障列表
- 展示接入该空间的所有故障，默认只展示未关闭故障，可以通过**处理进度**进行筛选。
- 筛选条件中可根据故障状态、处理人员、时间、标题等条件进行筛选显示。
- 选择多条**相同状态的故障**，可以进行批量关闭、认领等操作。
- **合并**即将多条故障合并为一条进行处理，支持跨协作空间的故障合并。
- **更多详解请参考[检索与查看故障](https://docs.flashcat.cloud/zh/flashduty/view-incidents)**。


### 集成数据
- 在协作空间下创建的集成属于**专属集成，即只应用于此空间**。
- 每种类型集成创建完成后都会生成相应的 webhook 地址，**不同类型的集成互不兼容**。
- 排除规则是将设定符合条件的事件进行丢弃，支持按集成类型、严重程度等条件配置。
- 多条排除规则时，优先级从高到低依次匹配，匹配上即终止，即时还有其他规则未匹配。
- 排除后的事件，**系统将不会在任何地方显示** ，属于无感知的，如果有收不到告警的情况，可以先看下是否有配置排除规则。

### 分派策略
- 可管理故障的通知规则、通知渠道、升级规则等。
- 故障通知会按照每个策略的先后顺序进行依次匹配，匹配到后不再进行往下匹配。
- 多个策略时可以自由拖动调整分派策略的顺序，调整前请确保通知规则符合业务需求。
- 更多**分派策略**相关请参考[分派策略](https://docs.flashcat.cloud/zh/flashduty/escalate-rule-settings)部分。

### 降噪配置
- 聚合降噪是将相似或相关联的告警进行合并为一个故障。
- 可以根据告警标题、告警级别、标签维度进行配置聚合。
- 故障收敛可以将某段时间内相同的故障自动屏蔽通知。
- 更多**降噪配置**相关请参考[降噪配置](https://docs.flashcat.cloud/zh/flashduty/noise-reduction-settings)部分。
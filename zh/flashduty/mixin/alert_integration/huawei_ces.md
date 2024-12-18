---
brief: 通过 webhook 的方式同步华为云监控 CES 告警事件到快猫星云，实现告警事件自动化降噪处理"
---

# 华为云监控 CES集成

通过 webhook 的方式同步华为云监控 CES 告警事件到 Flashduty，实现告警事件自动化降噪处理。

## 在 Flashduty
您可通过以下2种方式，获取一个集成推送地址，任选其一即可。

### 使用专属集成

当您不需要将告警事件路由到不同的协作空间，优先选择此方式，更简单。

|+| 展开

    1. 进入 Flashduty 控制台，选择 **协作空间**，进入某个空间的详情页面
    2. 选择 **集成数据** tab，点击 **添加一个集成**，进入添加集成页面
    3. 选择 **华为云监控CES** 集成，点击 **保存**，生成卡片。
    4. 点击生成的卡片，可以查看到 **推送地址**，复制备用，完成。

### 使用共享集成

当您需要根据告警事件的 Payload 信息，将告警路由到不同的协作空间，优先选择此方式。

|+| 展开

    1. 进入 Flashduty 控制台，选择 **集成中心=>告警事件**，进入集成选择页面。
    2. 选择 **华为云监控CES** 集成：
    - **集成名称**：为当前集成定义一个名称。
    3. 点击 **保存** 后，复制当前页面的新生成的 **推送地址** 备用。
    4. 点击 **创建路由**，为集成配置路由规则。您可以按条件匹配不同的告警到不同的协作空间，也可以直接设置默认协作空间作为兜底，后续再按需调整。
    5. 完成。

## 在华为云监控 CES

1. 登录您的 华为云 控制台，检索 __云监控__ 产品，并进入对应产品控制台
2. 进入 __告警-告警通知-通知对象__ 页面，单击 __创建通知对象__ 按钮
3. 协议选择 `HTTPS`，名称填写 `flashduty`，终端填写集成地址（当前页面填写集成名称，保存后即可生成地址）
4. 点击 __确定__ 按钮，完成通知对象创建

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/huawei_ces/1.avif" />

5. 进入 __告警-告警通知-通知组__ 页面，单击 __创建通知组__ 按钮
6. 组名称填写 `FlashDuty`，通知对象勾选前边创建的 `flashduty`
7. 点击 __确定__ 按钮，完成通知组创建

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/huawei_ces/2.avif" />

注意，创建通知组时，华为云会发起请求到 Flashduty，验证推送地址，查看通知组的通知对象列表，仅当通知对象状态为 __已确认__ 时，才会正常推送告警

8. 进入 __告警-告警规则__ 页面，选择已有的告警规则进行编辑，或者创建新的告警规则，打开 __告警规则详情__ 页面
9. 其中 __通知组__ 选择 `FlashDuty`，触发条件勾选 __出现告警__ 和 __恢复正常__。点击 __确定__ 按钮，保存修改

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/huawei_ces/3.avif" />

10. 回到 Flashduty 控制台集成列表页面，如果展示了最新事件时间，说明配置成功且收到事件
11. 完成

## 状态对照

华为云监控到 Flashduty 告警等级映射关系：

| CES  |  Flashduty  | 状态 |
| ---- | -------- | ---- |
| 紧急 | Critical | 严重 |
| 重要 | Critical | 严重 |
| 次要 | Warning  | 警告 |
| 提示 | Info     | 提醒 |
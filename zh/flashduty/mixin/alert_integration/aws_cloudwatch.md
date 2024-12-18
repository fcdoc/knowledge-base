---
brief: 通过 webhook 的方式同步 AWS CloudWatch 告警事件到 Flashduty，实现告警事件自动化降噪处理
---

# AWS CloudWatch集成

通过 webhook 的方式同步 AWS CloudWatch 告警事件到 Flashduty，实现告警事件自动化降噪处理。

## 在 Flashduty
您可通过以下2种方式，获取一个集成推送地址，任选其一即可。

### 使用专属集成

当您不需要将告警事件路由到不同的协作空间，优先选择此方式，更简单。

|+| 展开

    1. 进入 Flashduty 控制台，选择 **协作空间**，进入某个空间的详情页面
    2. 选择 **集成数据** tab，点击 **添加一个集成**，进入添加集成页面
    3. 选择 **AWS CLoudWatch** 集成，点击 **保存**，生成卡片。
    4. 点击生成的卡片，可以查看到 **推送地址**，复制备用，完成。

### 使用共享集成

当您需要根据告警事件的 Payload 信息，将告警路由到不同的协作空间，优先选择此方式。

|+| 展开

    1. 进入 Flashduty 控制台，选择 **集成中心=>告警事件**，进入集成选择页面。
    2. 选择 **AWS CloudWatch** 集成：
    - **集成名称**：为当前集成定义一个名称。
    3. 点击 **保存** 后，复制当前页面的新生成的 **推送地址** 备用。
    4. 点击 **创建路由**，为集成配置路由规则。您可以按条件匹配不同的告警到不同的协作空间，也可以直接设置默认协作空间作为兜底，后续再按需调整。
    5. 完成。

## 在 AWS CloudWatch

1. 登录您的 AWS 控制台，检索 `Simple Notification Service` 产品，并进入对应产品控制台
2. 进入 `Topics` 页面，单击 `Create topic` 按钮，开始创建主题
3. `Type` 选择 `Standard`，填写名称为 `FlashDuty`
4. 点击 `Create Topic` 按钮，完成主题创建
5. 进入 `Subscriptions` 页面，单击 `Create subscription` 按钮，为主题创建订阅
6. `Topic ARN` 选择 `FlashDuty`，`Protocal` 选择 `HTTPS`，`Endpoint` 填写集成的推送地址（当前页面填写集成名称，保存后即可生成地址）
7. 点击 `Create subscription` 按钮，完成订阅创建

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/aws_cloudwatch/1.avif" />

8. 回到 `Subscriptions` 页面，当订阅状态为 `Confirmed`，说明订阅地址校验成功，否则请联系 Flashduty
9. 检索 `CloudWatch` 产品，并进入对应产品控制台
10. 进入 `All alrams` 页面，选择创建或编辑已有的告警策略
11. 对于 `Notification` 这一步，`In alarm`、`OK` 和 `Insufficient data` 三种状态推送目标 `SNS topic` 均选择 `FlashDuty`，如下图所示：

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/aws_cloudwatch/2.avif" />

12. 回到集成列表，如果展示了最新事件时间，说明配置成功且收到事件
13. 完成

## 状态对照

CloudWatch 监控所有指标告警均对应到 Flashduty “警告（warning）”级别告警。
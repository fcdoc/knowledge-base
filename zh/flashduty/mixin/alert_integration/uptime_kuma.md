---
brief: 通过 webhook 的方式同步 Uptime Kuma 告警事件到快猫星云，实现告警事件自动化降噪处理
---

# Uptime Kuma 集成

通过 webhook 的方式同步 Uptime Kuma 告警事件到 Flashduty，实现告警事件自动化降噪处理。

## 在 Flashduty
您可通过以下2种方式，获取一个集成推送地址，任选其一即可。

### 使用专属集成

当您不需要将告警事件路由到不同的协作空间，优先选择此方式，更简单。

|+| 展开

    1. 进入 Flashduty 控制台，选择 **协作空间**，进入某个空间的详情页面
    2. 选择 **集成数据** tab，点击 **添加一个集成**，进入添加集成页面
    3. 选择 **Uptime Kunma** 集成，点击 **保存**，生成卡片。
    4. 点击生成的卡片，可以查看到 **推送地址**，复制备用，完成。

### 使用共享集成

当您需要根据告警事件的 Payload 信息，将告警路由到不同的协作空间，优先选择此方式。

|+| 展开

    1. 进入 Flashduty 控制台，选择 **集成中心=>告警事件**，进入集成选择页面。
    2. 选择 **Uptime Kunma** 集成：
    - **集成名称**：为当前集成定义一个名称。
    3. 点击 **保存** 后，复制当前页面的新生成的 **推送地址** 备用。
    4. 点击 **创建路由**，为集成配置路由规则。您可以按条件匹配不同的告警到不同的协作空间，也可以直接设置默认协作空间作为兜底，后续再按需调整。
    5. 完成。

## 在 Uptime Kuma
**步骤 1：设置通知渠道**

1. 进入 `Settings -> Notifications` 页面，单击 Setup 进行编辑，如下图所示；
2. `Notification Type` 选择 __FlashDuty（ Flashduty ）__；
3. `Integration Key` 复制写入集成推送地址中的 integration_key 参数值；
4. `Severity` 为严重程度，按需选择；
5. 提交保存

<img alt="drawing" width="400" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/uptime_kuma/1.avif" />

**步骤 2：配置监控项**

1. 点击 `Add New Monitor` 或编辑已有的监控项，按需完成监控配置；
2. 如图，右侧 `Notifications` 部分启用上一步创建的通知方式；
3. 如需设置标签，可以添加 `Tags`，注意仅同时存在 Key/Value 的标签才会推送到 FlashDuty；
4. 提交保存，等待告警触发。

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/uptime_kuma/2.avif" />

## 状态对照

Uptime Kuma 到 Flashduty 告警等级映射关系：

| Uptime Kuma  |  Flashduty  | 状态 |
| ------------ | -------- | ---- |
| Critical     | Critical | 严重 |
| Warning     | Warning  | 警告 |
| Info     | Info     | 提醒 |
---
brief: 通过 webhook 的方式同步腾讯云事件总线 EB 事件到快猫星云，实现告警事件自动化降噪处理
---

# 腾讯云EventBridge

---

通过 webhook 的方式同步腾讯云事件总线 EB 事件到 Flashduty，实现告警事件自动化降噪处理。

## 在 Flashduty
---
您可通过以下2种方式，获取一个集成推送地址，任选其一即可。

### 使用专属集成

当您不需要将告警事件路由到不同的协作空间，优先选择此方式，更简单。

<details>
<summary>展开</summary>

1. 进入 Flashduty 控制台，选择 **协作空间**，进入某个空间的详情页面
2. 选择 **集成数据** tab，点击 **添加一个集成**，进入添加集成页面
3. 选择 **腾讯云EventBridge** 集成，点击 **保存**，生成卡片。
4. 点击生成的卡片，可以查看到 **推送地址**，复制备用，完成。


</details>

### 使用共享集成

当您需要根据告警事件的 Payload 信息，将告警路由到不同的协作空间，优先选择此方式。

<details>
<summary>展开</summary>

1. 进入 Flashduty 控制台，选择 **集成中心=>告警事件**，进入集成选择页面。
2. 选择 **腾讯云EventBridge** 集成：
- **集成名称**：为当前集成定义一个名称。
3. 点击 **保存** 后，复制当前页面的新生成的 **推送地址** 备用。
4. 点击 **创建路由**，为集成配置路由规则。您可以按条件匹配不同的告警到不同的协作空间，也可以直接设置默认协作空间作为兜底，后续再按需调整。
5. 完成。

</details>

## 在腾讯云 EventBridge
---
<div class="md-block">

1. 登录您的腾讯云控制台，选择事件总线产品
2. 进入 事件规则 页面，单击 新建 按钮，开始编辑规则
3. 填写名称为 FlashDuty，如下图所示：

<img alt="drawing" width="600" src="https://fcdoc.github.io/img/3xdEpRnxM31nV5t8REeGxRbhRhwfQpwFooG7q6L6JhA.avif" />

4. 事件匹配部分可以通过表单模式选择特定事件，也可以自定义填写以下 JSON 内容，匹配全部事件：

```
{
"source": [
{
"suffix": ".cloud.tencent"
}
]
}
```

图示如下：

<img alt="drawing" width="600" src="https://fcdoc.github.io/img/pRBjDtOVtl4b6YmKAVF8EJ9RoOAIPGgt4m2hRWWaMzk.avif" />

5. 下一步，配置事件目标，分别选择”消息推送“、”通用通知模板“、”英文“，”接口回调“和”自定义 webhook“，webhook 地址填写集成的推送地址

<img alt="drawing" width="600" src="https://fcdoc.github.io/img/ha120gZ2uvDk4brSB4_OqEoYRM751-TesVi4cmOYQ-0.avif" />

6. 点击 保存 按钮，回到 事件集 页面，选择一个事件集，点击 发送事件，进行测试

<img alt="drawing" width="600" src="https://fcdoc.github.io/img/gh3xRQXvARrh7BWDz_le-dLR-0TMS4vblvXZbSu7NkM.avif" />

7. 回到集成列表，如果展示了最新事件时间，说明配置成功且收到事件
8. 完成

</div>

## 状态对照
---
<div class="md-block">

腾讯云事件总线所有事件均对应到 Flashduty “警告（warning）”级别告警。

</div>
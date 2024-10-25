---
brief: 通过 webhook 的方式同步蓝鲸智云监控事件到 Flashduty，实现告警事件自动化降噪处理
---

# 蓝鲸智云集成

---

通过 webhook 的方式同步蓝鲸智云监控事件到 Flashduty，实现告警事件自动化降噪处理。

## 在 Flashduty
---
您可通过以下2种方式，获取一个集成推送地址，任选其一即可。

### 使用专属集成

当您不需要将告警事件路由到不同的协作空间，优先选择此方式，更简单。

<details>
<summary>展开</summary>

1. 进入 Flashduty 控制台，选择 **协作空间**，进入某个空间的详情页面
2. 选择 **集成数据** tab，点击 **添加一个集成**，进入添加集成页面
3. 选择 **蓝鲸智云** 集成，点击 **保存**，生成卡片。
4. 点击生成的卡片，可以查看到 **推送地址**，复制备用，完成。


</details>

### 使用共享集成

当您需要根据告警事件的 Payload 信息，将告警路由到不同的协作空间，优先选择此方式。

<details>
<summary>展开</summary>

1. 进入 Flashduty 控制台，选择 **集成中心=>告警事件**，进入集成选择页面。
2. 选择 **蓝鲸智云** 集成：
- **集成名称**：为当前集成定义一个名称。
3. 点击 **保存** 后，复制当前页面的新生成的 **推送地址** 备用。
4. 点击 **创建路由**，为集成配置路由规则。您可以按条件匹配不同的告警到不同的协作空间，也可以直接设置默认协作空间作为兜底，后续再按需调整。
5. 完成。

</details>

## 在蓝鲸智云
---
以下内容已经在__蓝鲸V6/7版本__完成验证，V5 及以下版本官方已不再支持，建议您升级。

蓝鲸告警策略可以触发__处理套餐__，处理套餐可与周边系统打通，来完成复杂功能。我们首先创建一个处理套餐，配置 FlashDuty 的回调地址，然后编辑告警策略，关联动作到该处理套餐，实现告警变更自动推送到 FlashDuty。具体步骤如下：

#### 步骤 1、创建处理套餐

<div class="md-block">

1. 登录您的蓝鲸智云桌面，进入__监控平台__；
2. 进入__配置-处理套餐__页面，单击__添加套餐__按钮，开始创建处理套餐；
3. 填写名称为`Send To FlashDuty`，套餐类型选择__HTTP回调__，推送方式选择`POST`，并填写集成的推送地址（保存集成后获得），如下图所示：

<img alt="drawing" width="600" src="https://fcdoc.github.io/img/PZqbJNifhVKQj9FQNUw3DmVq8JGPf0sug4nfwFxVEjQ.avif" />

4. 切换到__主体__，选择`JSON`类型，消息体复制并填入以下信息（实际产生告警时，蓝鲸会渲染变量内容作为 Payload 推送到目标回调地址）：

```
{{alarm.callback_message}}
```

5. 保存套餐，完成创建。
</div>

#### 步骤 2、编辑告警策略

<div class="md-block">

1. 进入__配置-告警策略__页面，选择一个已有的策略进行编辑，或新建一个告警策略；
2. 下拉到__告警处理__部分，三种场景均选择`Send To FlashDuty`处理套餐，并关闭__防御规则__，如下图：

<img alt="drawing" width="600" src="https://fcdoc.github.io/img/yeCaYyAFIHIaZZL6z7_gTPHz-vjF6nCl5Yw8rv1t9SI.avif" />

3. 提交保存，完成；
4. 对于其他想要推送到 FlashDuty 的告警，重复以上步骤。

</div>

## 状态对照
---
<div class="md-block">

蓝鲸智云到 Flashduty 告警等级映射关系：

| 蓝鲸智云 |  Flashduty  | 状态 |
| -------- | -------- | ---- |
| 致命     | Critical | 严重 |
| 预警     | Warning  | 警告 |
| 提醒     | Info     | 提醒 |

</div>
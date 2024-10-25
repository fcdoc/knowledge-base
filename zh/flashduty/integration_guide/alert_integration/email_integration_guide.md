---
brief: 在 Flashduty 生成唯一的邮件地址，通过邮件的方式将告警的发生与恢复同步到 Flashduty
---

# 邮件Email集成

---

在 Flashduty 生成唯一的邮件地址，通过邮件的方式将告警的发生与恢复同步到 Flashduty。

## 操作步骤
---

### 创建邮件集成

您可通过以下2种方式，获取一个邮件地址，任选其一即可。

#### 使用专属集成

当您不需要将告警事件路由到不同的协作空间，优先选择此方式，更简单。

<details>
<summary>展开</summary>

1. 进入 Flashduty 控制台，选择 **协作空间**，进入某个空间的详情页面
2. 选择 **集成数据** tab，点击 **添加一个集成**，进入添加集成页面
3. 选择 **邮件 Email** 集成，点击 **保存**，生成卡片。
4. 点击生成的卡片，可以查看到 **邮件地址**，复制备用，完成。

</details>

#### 使用共享集成

当您需要根据告警事件的 Payload 信息，将告警路由到不同的协作空间，优先选择此方式。

<details>
<summary>展开</summary>

1. 进入 Flashduty 控制台，选择 **集成中心=>告警事件**，进入集成选择页面。
2. 选择 **邮件 Email** 集成：
- **集成名称**：为当前集成定义一个名称。
- **邮件地址**：为邮件设定一个方便记忆的前缀，需要保证在账户下唯一。
- **推送模式**：选择邮件在何种情况下触发或恢复告警。
3. 复制当前页面的 **邮件地址** 备用。
4. 点击 **创建路由**，为集成配置路由规则。您可以按条件匹配不同的告警到不同的协作空间，也可以直接设置默认协作空间作为兜底，后续再按需调整。
5. 完成。

</details>

### 定制邮件集成

#### 邮件地址

默认系统会帮您生成一个唯一的邮件地址。您可以进行修改，但需要注意，**邮件前缀只能由字母和数字组成**，且要在您的账户下保持唯一。

#### 推送模式

默认系统总是为每一封邮件创建新的告警，但您可以切换模式为：

1. **根据邮件标题触发或更新告警**：该模式下，每当接收到新邮件，系统会根据邮件标题查找未关闭告警。如果找到告警则进行更新，否则系统会触发一条新的告警。
2. **根据规则触发或关闭告警**：该模式下，每当接收到新邮件，系统会根据您的规则进行邮件匹配，匹配到的邮件按照规则去触发新告警或关闭已有告警。

- 您至少需要填写一条**触发**规则；
- 您必须设置 Alert Key 的正则提取规则。系统使用该字段来查找历史告警，以便对其进行更新或关闭；**如果正则提取失败，系统将使用邮件标题来生成 Alert Key**，以确保告警不会因为配置错误而丢失；
- 您可以选择，当所有的规则都不匹配时，是否丢弃邮件。

配置示例：

- 接收所有邮件，当邮件内容中包含 **RESOVED** 字样时，关闭告警，否则触发新告警；
- Alert Key 从邮件标题中提取，规则为 **/(.\*)/**。

<img src="https://fcdoc.github.io/img/UzSAxxB8q30joMRUlGUldv2u9iiYGCNCXG0uJmiRvtA.avif" alt="drawing" width="800"/>

### 注意事项

1. 如果邮件消息体大于 5MB，系统会直接拒绝接收。
2. 如果邮件文字内容长度超过 32KB，系统会进行截断，并在故障详情中增加标签提示：

```
body_cut = true
```

3. 如果邮件中包含附件，系统会直接丢弃附件，并在故障详情中增加标签提示：

```
attachment_stripped = true
```

4. 邮件触发的新告警中，**标题即邮件标题，描述即邮件内容**。

5. 如果您修改了账户域名，此邮件地址也会变更，务必记得更新推送地址。



## 严重程度映射关系
---

当前邮件集成推送到 Flashduty 的告警等级均为Warning。
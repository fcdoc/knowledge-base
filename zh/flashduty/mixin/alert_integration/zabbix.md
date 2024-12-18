---
brief: >-
  通过 webhook 的方式同步 Zabbix 告警事件到 Flashduty（支持 Zabbix 3.x ~ 6.x
  版本，不同版本配置有差异），实现告警事件自动化降噪处理
---

# Zabbix集成

通过 webhook 的方式同步 Zabbix 告警事件到 Flashduty（支持 Zabbix 3.x ~ 6.x 版本，不同版本配置有差异），实现告警事件自动化降噪处理。

## 在 Flashduty
您可通过以下2种方式，获取一个集成推送地址，任选其一即可。

### 使用专属集成

当您不需要将告警事件路由到不同的协作空间，优先选择此方式，更简单。

|+| 展开

    1. 进入 Flashduty 控制台，选择 **协作空间**，进入某个空间的详情页面
    2. 选择 **集成数据** tab，点击 **添加一个集成**，进入添加集成页面
    3. 选择 **Zabbix** 集成，点击 **保存**，生成卡片。
    4. 点击生成的卡片，可以查看到 **推送地址**，复制备用，完成。

### 使用共享集成

当您需要根据告警事件的 Payload 信息，将告警路由到不同的协作空间，优先选择此方式。

|+| 展开

    1. 进入 Flashduty 控制台，选择 **集成中心=>告警事件**，进入集成选择页面。
    2. 选择 **Zabbix** 集成：
    - **集成名称**：为当前集成定义一个名称。
    3. 点击 **保存** 后，复制当前页面的新生成的 **推送地址** 备用。
    4. 点击 **创建路由**，为集成配置路由规则。您可以按条件匹配不同的告警到不同的协作空间，也可以直接设置默认协作空间作为兜底，后续再按需调整。
    5. 完成。

## 在 Zabbix
<span id="v5"></span>

### 5.x~6.x 版本

#### 步骤 1：定义 Flashduty  media type

1. media type 是 Zabbix 中用于发送通知和告警的传输通道。进入终端，通过以下命令，下载完整配置

```i18n
// 5.x版本 XML配置:
wget https://download.flashcat.cloud/flashduty/integration/zabbix/zbx_mediatype_flashcat_v5.xml

// 6.x 版本 YAML 配置:
wget https://download.flashcat.cloud/flashduty/integration/zabbix/zbx_mediatype_flashcat_v6.yml
```

2. 登录 Zabbix 控制台，选择 `Administration > Media Types`，点击右上角 Import 按钮，进入编辑页面，选择上边下载的配置文件，点击 Import 按钮完成导入
3. 回到 Media Types 页面，可以看到已经导入的 media type。点击名称，进入编辑页面，补全 URL、zabbix_url 以及 HTTPProxy 等内容：

- `URL`：webhook 推送请求地址，复制集成的推送地址即可
- `zabbix_url`：Zabbix 控制台地址，直接复制即可（如果您的页面配置了 tomcat/nginx 转发路径，请同时携带），系统会在路径后拼接 trigger_id 等参数来生成告警详情页面连接
- `HTTPProxy`：如果您的 Zabbix Server 不能直接访问 Flashduty 服务，可以将该参数设置为一个代理地址

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/zabbix/1.avif" />

4. 点击 Update，保存配置

#### 步骤 2：关联 media type 至 user

media type 必须关联至某个 user 才能发送事件。user 至少拥有对 host 的 read 权限。建议直接关联到 Admin 用户。以 Admin 用户为例：

1. 登录 Zabbix 控制台，选择 `Administration > Users`，选择 Admin 用户，选择 media，选择 Add，进入编辑窗口：

- Type： 选择以上创建的 Flashduty  media type
- Send To：填写 N/A
- 其他配置使用默认配置，保持不变

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/zabbix/2.avif" />

2. 点击 Add 按钮，退出添加 media 窗口
3. 点击 Update 按钮，退出编辑 user 页面

#### 步骤 3：创建 action

发送通知是 Zabbix 中动作（actions）执行的操作之一。因此，为了建立一个通知，登录 Zabbix 控制台，选择 `Configuration > Actions`，然后：

1. 点击 `Create action`，进入 action 编辑页面

- Name：填写为“Send To FlashDuty”

2. 选择 `Operations`，分别添加三种场景的通知发送配置：

- 在 Operations 配置项，点击 Add 按钮，进入配置窗口
- Send to users：选择以上新建或配置的 user
- Send only to：选择 Flashduty  media type
- 其他配置保持默认
- 点击 Add 按钮，完成该配置项配置
- 重复以上步骤，完成对 `Recovery operations` 和 `Update operations` 的配置

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/zabbix/3.avif" />
<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/zabbix/4.avif" />

#### 步骤 4：发送事件到 Flashduty

登录 Zabbix 控制台，选择 `Monitoring > Problems`，查看最新的告警列表。

1. 点击 Actions，弹窗内可以看到消息通知结果
2. 找到 Flashduty 对应日志，如果 Status 为 `Sent`，代表通知成功。否则根据提示排查原因

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/zabbix/5.avif" />

3. 回到集成列表，如果展示了最新事件时间，说明配置成功且收到事件
4. 完成

<span id="v4"></span>

### 3.x~4.x 版本

#### 步骤 1：定义 Flashduty  media type

1. 登录 Zabbix 控制台，选择 `Administration > Media Types`，点击右上角 `Create media type` 按钮，进入编辑页面
2. 在编辑页面，Type 选择`Script`，Parameter 依次填写以下内容（不要调整顺序，没有值的也要留空，脚本按顺序获取参数值）：

- `{ALERT.SUBJECT}`：告警标题，保持在第一个参数
- `{ALERT.MESSAGE}`：告警信息，保持在第二个参数

- __FlashDuty webhook 推送请求地址__，复制集成的推送地址即可，保持在第三个参数
- __Zabbix 控制台地址__，直接复制即可（如果您的页面配置了 tomcat/nginx 转发路径，请同时携带），用于生成告警详情页面连接。如果没有空着即可，保持在第四个参数
- `HTTPProxy`：如果您的 Zabbix Server 不能直接访问 Flashduty 服务，可以将该参数设置为一个代理地址。如果没有空着即可，保持在第五个参数

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/zabbix/6.avif"/>

3. `Script name` 填写 `send-to-flashduty.sh`
4. 点击 Update，保存配置
5. 登录 Zabbix server 所在服务器，执行以下命令：

```i18n

#1. 进入告警脚本加载目录(具体地址配置在 Zabbix Server 配置文件中 `AlertScriptsPath` 变量, 一般为`/usr/lib/zabbix/alertscripts`)
cd /usr/lib/zabbix/alertscripts

#2. 下载脚本
wget https://download.flashcat.cloud/flashduty/integration/zabbix/send-to-flashduty.sh

#3. 更改脚本为可执行状态
chmod +x send-to-flashduty.sh

```

6. 注意，__脚本中使用了 curl 和 jq 命令__，确保这个 Zabbix server 进程可以找到并执行这两个命令，如果没有您需要根据情况安装

#### 步骤 2：关联 media type 至 user

media type 必须关联至某个 user 才能发送事件。user 至少拥有对 host 的 read 权限。建议直接关联到 Admin 用户。以 Admin 用户为例：

1. 登录 Zabbix 控制台，选择 `Administration > Users`，选择 Admin 用户，选择 media，选择 Add，进入编辑窗口：

- Type： 选择以上创建的 Flashduty  media type
- Send To：填写 N/A
- 其他配置使用默认配置，保持不变

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/zabbix/7.avif" />

2. 点击 Add 按钮，退出添加 media 窗口
3. 点击 Update 按钮，退出编辑 user 页面

#### 步骤 3：创建 action

发送通知是 Zabbix 中动作（actions）执行的操作之一。因此，为了建立一个通知，登录 Zabbix 控制台，选择 `Configuration > Actions`，然后：

1. 点击`Create action`，进入 action 编辑页面

- Name：填写为“Send To FlashDuty”

2. 选择 `Operations`，分别更新三种场景的通知用户配置：

- 在 Operations 配置项，点击 Add 按钮，进入配置窗口
- Send to users：选择以上新建或配置的 user
- Send only to：选择 Flashduty  media type
- 其他配置保持默认
- 点击 Add 按钮，完成该配置项配置
- 重复以上步骤，完成对 `Recovery operations` 和 `Update operations` 的配置

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/zabbix/8.avif" />

3. 选择 `Operations`，分别更新三种场景的通知内容配置：

- **在 Default Message 配置项，完整复制以下内容，粘贴在默认内容之后**，FlashDuty 收到事件后将解析对应文字，找到告警属性信息：

```

-----FlashDuty Required Starts-----event_severity={TRIGGER.SEVERITY}||event_name={TRIGGER.NAME}||event_id={EVENT.ID}||event_tags={EVENT.TAGS}||event_ack={EVENT.ACK.STATUS}||event_value={EVENT.VALUE}||trigger_id={TRIGGER.ID}||trigger_desc={TRIGGER.DESCRIPTION}||trigger_expr={TRIGGER.EXPRESSION}||host_group={TRIGGER.HOSTGROUP.NAME}||host_ip={HOST.IP}||host_name={HOST.NAME}||item_name={ITEM.NAME}||item_value={ITEM.VALUE}-----FlashDuty Required Ends-----

```

- 重复以上步骤，完成对 `Recovery operations` 和 `Update operations` 的配置

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/zabbix/9.avif" />

#### 步骤 4：发送事件到 Flashduty

登录 Zabbix 控制台，选择 Monitoring > Problems，查看最新的告警列表。

1. 点击 Actions，弹窗内可以看到消息通知结果
2. 找到 Flashduty 对应日志，如果 Status 为 Sent，代表通知成功。否则根据提示排查原因

<img alt="drawing" width="600" src="https://fc.3ti.site/zh/flashduty/mixin/alert_integration/zabbix/10.avif" />

3. 回到集成列表，如果展示了最新事件时间，说明配置成功且收到事件
4. 完成

## 状态对照

Zabbix 到 Flashduty 告警等级映射关系：

| Zabbix         |  Flashduty  | 状态 |
| -------------- | -------- | ---- |
| Disaster       | Critical | 严重 |
| High           | Critical | 严重 |
| Average        | Warning  | 警告 |
| Warning        | Warning  | 警告 |
| Information    | Info     | 提醒 |
| Not classified | Info     | 提醒 |
---
brief: 通过修改推送参数，实现对故障的严重程度和标题等信息的定制
---

# 定制故障标题和严重程度

通过修改推送参数，定制故障的严重程度和标题等信息。

## 定制严重程度

**在推送地址中增加Query参数severity，覆盖故障的严重程度。**

> [!NOTE]
> 适配所有通过 webhook 上报告警的集成。

部分告警集成（比如 AWS CloudWatch）是不支持严重程度区分的，这种情况下我们可以在集成推送地址中进行指定。不同的告警策略配置不同的推送地址，以此实现对告警严重程度的区分。

示例：以下地址指定了 severity 参数，值为 Info（**注意首字母大写**）。通过此地址推送的告警，严重程度一定会覆盖为 Info。
```
https://api.flashcat.cloud/event/push/alert/aws/cloudwatch?integration_key=your-integration-key?severity=Info
```

## 定制故障标题

> [!NOTE]
> 适配所有通过 webhook 上报告警的集成。

**在推送地址中增加Query参数title_rule，动态生成故障标题。**

### 通过简化语法生成

用::分割子串，每一个子串可以是一个固定字符串或用\$作为前缀的变量，变量内容将从标签中提取，提取不到不进行变量替换。

示例：

| 规则 | 标签值 | 生成内容 |
| --- | ---| ---- |
|\$resource::\$check | {"resource": "127.0.0.1", "check": "cpu idle low"} | 127.0.0.1 / cpu idle low |
|\$resource::\$check | {"resource": "127.0.0.1"} | 127.0.0.1 / \$check |
|\$resource::主机宕机 | {"resource": "127.0.0.1"} | 127.0.0.1 / 主机宕机 |

### 通过\${var}引用标签生成

以[TPL]作为前缀，使用\${}来引用变量，变量内容将从标签中提取，提取不到使用\<no value\>替代。

示例：

| 规则 | 标签值 | 生成内容 |
| --- | ---| ---- |
|[TPL]\${resource} / \${check}| {"resource": "127.0.0.1", "check": "cpu idle low"} | 127.0.0.1 / cpu idle low |
|[TPL]\${resource} / \${check} | {"resource": "127.0.0.1"} | 127.0.0.1 / \<no value\> |
|[TPL]\${resource} / 主机宕机 | {"resource": "127.0.0.1"} | 127.0.0.1 / 主机宕机 |

### 通过Golang模版语法生成

以[TPL]作为前缀，使用{{}}来引用变量（可以引用标签以及其他变量），提取不到使用\<no value\>替代。变量范围参考[告警事件定义](#AlertEvent)。

示例：

| 规则 | 标签值 | 生成内容 |
| --- | ---| ---- |
|[TPL]{{.Labels.resource}} / {{.Labels.check}}| {"resource": "127.0.0.1", "check": "cpu idle low"} | 127.0.0.1 / cpu idle low |
|[TPL]{{.Labels.resource}} / {{.Labels.check}} | {"resource": "127.0.0.1"} | 127.0.0.1 / \<no value\> |
|[TPL]{{.Labels.resource}} / 主机宕机 | {"resource": "127.0.0.1"} | 127.0.0.1 / 主机宕机 |

## 常见问题

|+| 使用标签动态生成标题，如果标签不存在怎么办？

    取决于您使用哪一种变量获取方式，标题可能会保留原始的变量信息或使用\<no value\>替代。

    即使获取不到变量，也不影响告警的生成，您可放心调试。
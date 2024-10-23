---
brief: Realize dynamic dispatch of alerts based on tags and integrate with your proprietary system
---

# Dynamically set dispatch personnel

---

Realize dynamic dispatch of alerts based on tags and integrate with your proprietary system.

## Adaptation scenarios
---

**The responsible party for the alert is maintained and frequently adjusted in the source monitoring system, with the hope of timely synchronization to Flashduty.**

Scenario 1:

Customer A has a self-developed big data task system where internal personnel can create various batch processing tasks, assigning primary and secondary responsible individuals to each task. If a batch processing task fails, the system will first notify the primary responsible individual. If the alert is not resolved within 30 minutes, it will escalate to the secondary responsible individual.

Scenario 2:

Customer B uses Zabbix for host monitoring and assigns a responsible person tag to each host. The customer wants to be able to notify the corresponding responsible person based on this tag when an alert for the host occurs.

Scenario 3:

Customer C has a self-developed monitoring system with many alerting policies, each set to notify a specific WeChat group. The customer decided to migrate incident response to Flashduty but wants to retain the relationship between the original monitoring system's policies and the WeChat groups, and to dynamically notify the WeChat groups of alerts based on this relationship.


## Implementation methods
---

**Add specific tags or Query parameters to override the dispatch targets in Flashduty for dynamic dispatching.**

Parameter format as follows:

- **Replace dispatch personnel**:
- **Parameter name**: Must match the regex: ^layer_person_reset_(\d)_emails$. The link number starts from 0. For example, layer_person_reset_0_emails represents replacing the dispatch personnel in the first link of the dispatch strategy.
- **Parameter value**: Email addresses of the dispatch personnel, separated by commas. For example, zhangsan@flashcat.cloud, lisi@flashcat.cloud, replacing the personnel with Zhang San and Li Si.
- **Parameter location**: Query parameter or tag value. For example, set this tag in the nightingale alert or automatically generate a tag through tag enhancement.
- **Replace the WeChat group chat bot**:
- **Parameter name**: Must match the regex: ^layer_webhook_reset_(\d)_wecoms$. The link number starts from 0. For example, layer_webhook_reset_0_wecoms represents replacing the WeChat group chat bot in the first link of the dispatch strategy.
- **Parameter value**: Target group chat bot token, separated by commas for multiple tokens. For example, bbb025a0-e2e8-4b79-939d-82c91a275b06, replacing the group chat bot with the corresponding bot for this token.
- **Parameter location**: Query parameter or tag value. For example, set this tag in the nightingale alert or automatically generate a tag through tag enhancement.

:::tip
In the event of a fault trigger, Flashduty matches against the existing dispatch strategy. After matching a dispatch strategy, dispatch or escalate according to the links in the strategy. If the above parameters are set, the system will automatically replace the dispatch targets or group chat channels.

In the matched dispatch strategy, only the dispatch targets and group chat destinations change, while other content remains the same, similar to a template dispatch strategy.
:::

## Push example
---

### Set a template dispatch policy

Configure a dispatch policy for the collaboration space. As shown in the figure below, the space is set up with one dispatch link, with the dispatch target being Toutie Technology, and simultaneously pushing to a WeChat group with a token ending in 5b96.

![](https://fcdoc.github.io/img/BzEFtRd9mmTNVjjnF7f_AcO7kcjSqdKamWmET3Dxwjw.avif)

### Set labels for alerts

For example, using custom alert event integration, we push a sample alert to the target collaboration space. The layer_person_reset_0_emails tag is set to replace the dispatch personnel of the first link with guoyuhang and yushuangyu. The layer_webhook_reset_0_wecoms tag is set to replace the WeChat group chat token of the first link with a token ending in d9c0.

Request content as follows:

```
curl --location --request POST 'https://api.flashcat.cloud/event/push/alert/standard?integration_key=your-integration-key' \
--header 'Content-Type: application/json' \
--data-raw '{
"event_status": "Warning",
"alert_key": "lasdfl2xzasd0262",
"description": "cpu idle lower than 20%",
"title_rule": "$cluster::$resource::$check",
"labels": {
"service": "engine",
"cluster":"nj",
"resource":"es.nj.01",
"check":"cpu.idle<20%",
"metric":"node_cpu_seconds_total",
"layer_person_reset_0_emails": "guoyuhang@flashcat.cloud,yushuangyu@flashcat.cloud",
"layer_webhook_reset_0_wecoms":"90dbb66b-af39-4235-956c-636a9c1ed9c0"
}
}'
```

### View the fault dispatch timeline

As shown in the figure below, the target fault is normally triggered and dispatched. The dispatch personnel and target group chat have been replaced as expected.

![](https://fcdoc.github.io/img/WHCu6fjd-r-vUtUeAhxzLsFFwBNaf5gIG_gQ4lcHAZ4.avif)


## FAQs
---
<details><summary>What should I do if my monitoring system does not have these tags?</summary><ol><li> If your system supports active label addition, such as Prometheus or Nightingale, it is recommended that you add specific labels directly to the alarm policy.</li><li> If your system already has the relevant tags, but the format or naming is different. For example, if your host has a team tag, you need to find the corresponding person in charge based on the team. In this case, you can use the tag enhancement function to generate tags related to the person in charge based on the team tag. For details, please refer to [Configuring Tag Enhancement](/0) .</li></ol></details>
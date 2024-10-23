---
brief: Access alarms through exclusive or shared integration, and what is the difference between exclusive and shared integration?
---

# Various alarm access methods

---


FlashDuty serves as a unified alarm processing platform, which itself does not generate alarm data. It is necessary to integrate alarm events from third-party monitoring platforms into FlashDuty to achieve unified alarm reception, noise reduction, dispatching, notification, resolution, analysis, and automation, such as alarms from monitoring platforms like Nightingale/FlashCat, Zabbix, Prometheus, and alerts from major cloud service providers. For more types, please refer to [Alarm Integration](https://docs.flashcat.cloud/zh/flashduty/custom-alert-integration-guide).


## Access methods
---

### Exclusive Integration
Exclusive integration addition path: **Collaboration Space Details => Integration Data => Exclusive Integration**.
- Exclusive integration can be added when creating a collaboration space or within an already created collaboration space.
- In exclusive integration, alarms accessed in a collaboration space **do not require configuration of routing rules, meaning all alarms will be distributed to this space** (excluding filtered alarms) and cannot be shared with other collaboration spaces.
- Exclusive integration should be chosen when alarms do not need to be distributed to multiple different spaces.

![zhuanshujicheng1.png](https://fcdoc.github.io/img/OjUArE19Yq2a3UdlhEmLR_3NvXfy2pvEnGf2ZYBpIxE.avif)

### Shared Integration
Shared integration addition path: **Integration Center => Alarm Events**.
- Alarm event types created in the Integration Center are global and must **be directed to specific collaboration spaces or multiple collaboration spaces using routing rules**.
- Each integration **must be configured with at least one collaboration space to receive alarms; otherwise, the integration will not be effective, meaning it cannot receive alarm events**.


![jichengzhongxin.png](https://fcdoc.github.io/img/Ag1OnefntjpAjD-qq6fCgotIHvpQl1F-G2kc9VC7WAs.avif)

:::tip

- Exclusive or shared integration will generate a push address after a new alarm integration is added. Copy the modified address to the corresponding platform.
- Each alarm event source accesses different data types. For specific methods, refer to the access instructions in the [Integration Guide](https://docs.flashcat.cloud/zh/flashduty/custom-alert-integration-guide).

:::

:::caution
To ensure the overall system's stability, we have imposed frequency limits on event requests reported by each integration. The current limits are a request limit per second (`qps`) of `100` and a request limit per minute (`qpm`) of `1000`.

If your request volume exceeds this frequency, you will receive a response with status code `429`. In this case, you should wait for a period before resubmitting.

We may adjust these limits in the future. If you need to increase these limits, please contact us.
:::

## FAQs
---

<details><summary>The integration created in the integration center's alarm event doesn't receive alarms?</summary> 1. Please confirm if routing is configured. 2. Please confirm if the source platform is triggering alarm events and generating alarms.</details>

<details><summary>Is there a limit to the number of integrations I can create?</summary> There are currently no restrictions.</details>

<details><summary>How are alarm labels generated?</summary> Flashduty adopts an all-inclusive approach for each integration, incorporating all crucial information into tags, descriptions, or titles. If you wish to dynamically generate additional labels based on this, please configure tag enrichment rules. For detailed instructions, refer to: https://docs.flashcat.cloud/zh/flashduty/label-enrichment-settings</details>

<details><summary>How is the alarm title determined? Can I customize it?</summary> Flashduty employs a specific title generation method for each integration, typically combining "policy name / alarm object". If you want to customize the title generation rules, please refer to: https://docs.flashcat.cloud/zh/flashduty/customize-incident-attrs</details>

<details><summary>How can I determine the integration type of an alarm event?</summary> Click "Fault" -> Enter Fault Details -> Associated Alarm -> Alarm Source.</details>
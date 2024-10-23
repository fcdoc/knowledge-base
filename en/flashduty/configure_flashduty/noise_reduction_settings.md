---
brief: Through alarm aggregation, multiple similar active alarms can be consolidated into a single fault for joint dispatching, notification, and handling, which significantly reduces notification frequency and enhances response efficiency
---

# Configure Alarm Noise Reduction

---

## Set Alarm Aggregation
---
Go to [Collaboration Space Details] - [Alarm Noise Reduction], you can set the **alarm aggregation** strategy. When creating a new collaboration space, alarm aggregation is turned off by default. It is recommended that you manually enable it and set aggregation policies as needed.

:::tip
When alarm aggregation is not enabled, each alarm will create a separate fault, with identical basic information.
:::

- Aggregation dimensions: A space can set multiple default aggregation dimensions. If any dimension set matches, the alarm and fault are considered similar and can be merged.

- If you wish to manage different alarms separately, please enable `Fine-Grained Control`.
- Fine-Grained Control allows you to filter faults and specify a particular aggregation dimension.
- The system always prioritizes fine-grained control matching. If no match is found, the default aggregation dimensions will be used.
- You can visit [Configure Filter Conditions](https://docs.flashcat.cloud/zh/flashduty/how-to-filter) to understand how to set up filters.

- Aggregation window: You can choose to aggregate only alarms that occur in close succession (indicating stronger relevance), while alarms beyond the time window will trigger new faults. **Note that this is a sliding window, which extends as new alarms are incorporated**.

- It is generally advised to use the average arrival time of alarms as the aggregation window, for instance, 10 minutes.

- Storm Alert: After a fault is triggered, the system will immediately dispatch and notify (unless a delayed notification is set). Subsequently, it will continuously incorporate new alarms, **but no additional notifications will be sent**. This may prevent timely detection of an alarm storm. Therefore, we provide a threshold. When the number of incorporated alarms reaches this threshold, the system will trigger a storm alert, prompting you to address the issue promptly.

- We always suggest enabling storm alerts.

- Preview: You can use the preview feature to retrieve recent events and render the noise reduction results in real-time, thus assessing the noise reduction effect. The system can retrieve up to `666` historical events.

<img src="https://fcdoc.github.io/img/V7G1hZj1IPX10Fsa_ekHR77oKs8POHsib5y2zg-Yjdw.avif" style="display: block; margin: 0 auto;" height="400">


## View Aggregation Examples
---

When the space is set to aggregate by **alarm check items**, the system receives five alarm notifications sequentially, each triggering an alarm and a fault:

```
故障：cpu idle < 20% / es.nj.03，Critical

- 告警cpu idle < 20% / es.nj.03：
- 事件1：es.nj.03，cpu.idle = 10%，Critical
- 事件2：es.nj.03，cpu.idle = 18%，Warning
- 事件4：es.nj.03，cpu.idle = 10%，Ok

- 告警cpu idle < 20% / es.nj.01：
- 事件3：es.nj.01，cpu.idle = 15%，Warning

- 告警cpu idle < 20% / es.nj.02：
- 事件5：es.nj.02，cpu.idle = 19%，Warning
```

We can see the final [fault-alarm-event] correlation relationship through the console fault details page:
- Click on the alarm title to view the details of the associated alarm, including its timeline and related events
- Click on the event point to view the specific content reported by the event, including tags and descriptions

![](https://fcdoc.github.io/img/jAkbujzJKD3war7mV4EyzsYvd-TZB1BX_wJ1PUGZKTM.avif)

## FAQs
---
<details><summary>Will the fault title change when the alarm is merged?</summary> No, the default fault title remains the same as the first alarm that triggered it. You can manually modify the fault title at any time. This title will not change when new alarms are merged. </details>
<details><summary>Will the fault label change when the alarm is merged?</summary><ul><li> Manually created alerts: No, their label list will always be empty</li><li> Automatically triggered alarm: It is possible that the label of the fault will be consistent with the label of the first alarm that triggered the fault. If the label of the alarm changes, the label of the fault will also change synchronously.</li></ul></details>
<details><summary>Will the alarm label change as the event is merged?</summary> Yes, the alarm label will always align with the newly added event. For example, if you receive an alarm "CPU idle is low" at 10:00 AM with a trigger value of 10%, as more events are merged, the trigger value label may dynamically change. However, if the new event is a recovery event, the alarm will retain its existing labels and add any new, relevant labels. Our aim is to keep the displayed alarm label as close as possible to its initial state when triggered. </details>
<details><summary>Is there an upper limit on the number of alarms that can be merged into faults?</summary> Yes, we have set a maximum of 1000 alarms for a single fault. This is primarily to optimize the rendering time of the console page. However, as Flashduty is a high-performance event processing system with extensive concurrent logic in the background, seeing fault aggregation exceed 1000 alarms is a normal occurrence. </details>
<details><summary>Is there an upper limit on the number of events that can be combined into alarms?</summary> There is no limit. However, the maximum window for an alarm to aggregate events is 24 hours. This means that if an alarm is triggered and remains unresolved after 24 hours, no further events will be merged. If Flashduty receives new events, a new alarm will be generated. </details>
<details><summary>Why do the number of events I push and the number of events associated with the alarm not match?</summary> The merging of events into alarms is a noise reduction process. If Flashduty determines that a newly reported event does not significantly differ from the existing alarm (for example, the status, severity, or description remain unchanged), Flashduty will discard the new event and use the labels from the new event to overwrite any existing labels. </details>
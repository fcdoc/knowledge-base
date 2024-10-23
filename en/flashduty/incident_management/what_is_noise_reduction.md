---
brief: Understand how Flashduty mitigates noise in alarms
---

# Learn about alarm noise reduction

---

Grasp how Flashduty reduces noise in alarms.

---

When Flashduty receives an alarm event (e.g., a Zabbix alert notification), the system automatically triggers an alarm, which in turn initiates a fault. Multiple similar active alarms may be consolidated into a single fault, allowing for joint dispatching, notification, and handling, which significantly reduces notification frequency and enhances response efficiency.


## Noise Reduction Model
---

### Basic Concepts

- **Event (Event)**: An event originating from the original monitoring system (such as Zabbix), with each trigger and recovery notification constituting an event.
- **Alarm (Alert)**: Automatically triggered by events, where alarms from the same event in the original monitoring system, occurring at different times, are consolidated into a single alert by Flashduty.
- **Fault (Incident)**: The primary object processed by the Flashduty platform, usually automatically triggered by alarms but can also be manually created. A fault is a grouping of similar alarms, with Flashduty aggregating similar alarms based on user-configured policies for dispatching and handling.

### Noise Reduction Process

Faults can be triggered in two ways: manually or automatically. Alarm noise reduction is effective only in the automatic triggering scenario. The general process of noise reduction is as follows:

1. The monitoring system generates an alarm and pushes it to Flashduty
2. Flashduty determines if the new event can be incorporated into an existing active alarm; if not, a new alarm is triggered, otherwise, it is incorporated
3. Flashduty determines if the new alarm can be incorporated into an existing active fault; if not, a new fault is triggered, otherwise, it is incorporated
4. Flashduty assigns personnel according to the dispatching strategy and notifies them
5. Personnel receive the notification and begin to address the fault

![Flashduty-Alarm Noise Reduction.png](https://fcdoc.github.io/img/162SjbaT8JsHNjwpD1lTkMqYHD9AafLsUB1CvUKGVV0.avif)

## Set Alarm Aggregation
---

Go to [Collaboration Space Details] - [Alarm Noise Reduction], you can set the **alarm aggregation** strategy. When creating a new collaboration space, alarm aggregation is turned off by default. It is recommended that you manually enable it and set aggregation policies as needed.

:::tip
When alarm aggregation is not enabled, each alarm will create a separate fault, with identical basic information.
:::

- Aggregation Dimensions: A space can set multiple sets of aggregation conditions; if any set matches, the alarm and fault are considered similar and can be incorporated.
- Aggregation Window: You can choose to aggregate only alarms that occur close together (indicating stronger correlation), with alarms outside the time window triggering new faults. Note that this window is sliding and extends as new alarms are incorporated.
- Storm Alert: After a fault is triggered, the system immediately dispatches and notifies (unless a delay notification is set). Subsequent alarms are incorporated without triggering new notifications, which may prevent timely detection of an alarm storm. Therefore, we provide a threshold; when the number of incorporated alarms reaches this threshold, a storm alert is triggered to prompt urgent handling.
- Preview: Use the preview function to pull recent events and render the noise reduction results in real-time to assess the effectiveness of the noise reduction

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
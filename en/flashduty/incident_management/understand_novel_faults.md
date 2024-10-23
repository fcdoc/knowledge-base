---
brief: Novel fault detection, swift handling of emerging issues
---

# Understanding novel faults

---

Distinguish between common and novel faults to expedite troubleshooting

---

so-called novel faults refer to those that have not occurred within a certain period in the past. If a fault is identified as a novel fault, the fault responder should be vigilant. This is crucial for OnCall engineers, as the impact of novel faults may be unknown, and their resolution may require immediate judgment. Some engineers may focus only on novel faults, developing standardized processes or SOPs for addressing such issues.

:::tip
This feature is currently in beta and is available only in the professional version and above subscriptions. If you need to enable this feature, please contact us at any time.
:::


## View novel faults
---

### Console

1. On the fault list page, novel faults will be marked with a distinct **Novelty** label;
2. On the fault details page, novel faults will be clearly labeled with **Novelty** at the top, along with an explanation.

<img src="https://fcdoc.github.io/img/xqtBsH90jOXzcppNlKqXij4peIRPbV51UKC2dJ3JjnU.avif" alt="新奇" style="display: block; margin: 0 auto;" width="600">

### IM Tool

For example, on Feishu, when a fault is identified as a novel alert, the system will enhance the notification:

<img src="https://fcdoc.github.io/img/gngVyQEuu-kSTV7uje3XUNK6objwAnF7b1KkiEgIK4g.avif" alt="新奇-feishu" style="display: block; margin: 0 auto;" width="500">

### How to identify

The system employs a machine learning model to assess the similarity between faults. When the similarity exceeds 90%, we consider the two faults to be similar.

In assessing similarity, we primarily consider the following factors:

1. Fault title
2. Detailed description of the fault
3. The service affected by the fault (usually extracted from the 'service' tag)
4. Alarm objects included in the fault (usually extracted from the 'resource' tag)

If the system detects no similar faults within the past **30** days, it will mark the fault as novel.


## FAQs
---

<details><summary>Do novelty faults need to be enabled separately?</summary> There is no need to set up and turn it on. By default, the system will trigger novel fault identification for all professional and above subscription versions.</details>
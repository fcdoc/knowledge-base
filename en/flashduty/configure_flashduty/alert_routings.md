---
brief: Configure routing rules to route alarm events of the same type or related business to the corresponding collaboration spaces for categorized information processing and analysis
---

# Configure Routing Rules

---

When integrating alarm events via shared integration, routing rules can be set to distribute events of the same type or related business to the respective collaboration spaces for categorized processing, analysis, etc.

## How to Configure
---
Configuration path: **Integration Center => Alarm Events => Specific Integration Type => Create Route**

**1. Add Route:** Multiple routes can be added without a current limit, but it's advisable to keep them concise to maintain readability.
**2. Adjust Order:** With two or more routing rules, you can adjust the activation order using the up and down arrows.
**3. Routing Rules:** Support for multiple conditions and rules for logical operations (including both match and non-match operations). Various matching patterns are available, such as exact matches, wildcards, and regular expressions. Visit [Configure Filter Conditions](https://docs.flashcat.cloud/zh/flashduty/how-to-filter) to learn how to set up constraints.
**4. Process Control:** In the presence of two or more routing rules, the option to **terminate or proceed** with the matching of subsequent rules is available. By default, the system **continues matching**, ensuring that subsequent routes remain active. Conversely, selecting **termination** will deactivate any subsequent rules.
**5. Preview Rules:** After configuring the rules, you can view the configuration expressions.
**6. Insert Route:** When there are two or more routing rules, you can insert a new route before or after an existing one, saving the need to reorder.
**7. Default Route:** At least one routing rule is required for shared integration to receive alarm events. A default route is provided, which will distribute events to the corresponding collaboration space if no other rules match.
**8. Delivery Space:** You can select multiple collaboration spaces to deliver matching alarms.

<img src="https://fcdoc.github.io/img/6OTNxniH4889Qyk8SdVuF3-vrYcF9bxAE2CGG329U0s.avif"  width="800">

## Configuration Example
---

### 1. Distribute the Same Business Group to the Same Space
**Scenario:** Route alarms from the same business group in the FlashCat monitoring platform to a unified collaboration space.
**Rule:** Match based on the Labels.group_name tag.

<img src="https://fcdoc.github.io/img/6zBXABVJ4xFMBJd7MQ7oT8Sla6LZa19rMPbUjXJ4IT4.avif"  width="800">



## FAQs
---
<details><summary>Routing rules not taking effect?</summary> Please check if the alarm events match the rules and if the rules are correctly configured.</details>

<details><summary>What happens when multiple routing rules are the same and deliver to the same collaboration space?</summary> A corresponding issue will be generated for each collaboration space. It is recommended to select multiple collaboration spaces in the same rule.</details>


<details><summary>Not receiving alarms after configuring routing rules?</summary> Please confirm whether the reported alarm events match the configured routing rules. It is suggested to set up a default fallback route to capture unmatched events.</details>

<details><summary>Will the default route be matched if the routing rule flow control is set to Stop?</summary> It will match. The default route serves as a catch-all and is not subject to the flow control restrictions.</details>
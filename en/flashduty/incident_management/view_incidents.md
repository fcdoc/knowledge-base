---
brief: Understand the usage of fault lists, detail pages, including aggregate views, filtering, and timelines
---

# Search and view faults

---

Connect all company alarm events to Flashduty to monitor and manage alarms centrally.

## Fault List
---

Flashduty offers two entry points for viewing the fault list: one within the collaboration space and another under the fault management menu. The difference lies in the fact that under the fault management menu, you can view faults across multiple collaboration spaces, even those of the entire company.


![](https://fcdoc.github.io/img/HHHZag1gZSDUdLUUapF-diTesLEySgjEC5azLRzY8Ys.avif)

1. **Assignees**: By default, it focuses on faults **assigned to me**, but can be switched to view faults across the entire account.
2. **Processing Progress**: Filter faults by processing progress, with the default set to **All**.
3. **Time Filtering**: Supports relative time and custom range filtering. Note that for performance reasons, **the query's start and end times must not exceed one month**. To query data older than one month, adjust the start and end times accordingly.
4. **Search by Input**: Supports searching for fault IDs, and if the assignee is switched to "assigned to me", it also supports fuzzy matching of the "fault title".
5. **Common Filters**: Allows saving frequently used filter conditions, such as "My Collaboration Space", as "Common Filters" to enhance daily processing efficiency.
6. **Advanced Filters**: Supports a variety of filtering dimensions, including severity, tags, or custom fields.
7. **View Settings**: Offers a range of rendering options, including the ability to introduce **custom display attributes** and aggregate views.
8. **Pagination Settings**: Adjust pagination and the number of items per page.

:::highlight orange 💡
2	In order to enhance performance, when the search criteria match over **1000** faults, the system displays 1000+ only, rather than the exact number. Consequently, you can only view 1000 faults by navigating through pages. If you wish to see more, please adjust your search time frame. Alternatively, you can access all data via the [Fault Query](https://developer.flashcat.cloud/api-110655782) API.
:::

### Use Aggregate Views

Aggregate views provide a different perspective for viewing faults, allowing you to define various aggregation dimensions. The essence of aggregation dimensions is real-time grouping, such as aggregating by severity.

![](https://fcdoc.github.io/img/J7MizvU-Gd2gBNItJuE5kbo0FeypSzo74DxQSwGZm_8.avif)

:::highlight orange 💡
For performance reasons, the system will match up to **100 pieces of** data for aggregation in the aggregate view. Thus, the list page you see may not include all matching data. If this is a concern, switch to the list view.
:::

### Use Advanced Filters

Flashduty provides various filtering capabilities and offers ample flexibility. A typical scenario is:

- Search for related faults triggered by the "Host Down" alarm policy based on the check tag.
- Search for related faults marked as "false positive" based on the false positive field.

:::highlight orange 💡
Flexibility often comes at the cost of performance, and this is also true for Flashduty, despite our extensive performance optimizations. We always recommend narrowing your search time range and using conditions like **assigned to me** and **processing progress** to limit the scope of your query.
:::


### Custom Rendering

Under the **Settings** tab, select or disable the display of the following content to customize the fault list display:

1. **Basic Attributes**: Define whether to display basic information such as duration and handler.
2. **Custom Fields**: You can select custom fields defined by the platform. If a fault does not have this field set, it will display as "–".
3. **Tags**: You can filter and select tags. If a fault does not have a particular tag, it will display as "–".


## Fault Details
---

Fault details are the primary entry point for fault investigation, presenting all available information. Especially on the fault overview page, Flashduty highlights the most essential information you need.

![](https://fcdoc.github.io/img/Z2yap9_v7IRgltiWTpayQTnNy8bR1RZsI6ay3DE2Gj4.avif)

1. **Key Information**: The fault's title, severity, processing progress, ID number, collaboration space, and duration.
2. **Detailed Information**: The fault's description, impact, and tags. Both the description and impact support Markdown formatting.
3. **Action Area**: Various frequently used action buttons, including additional custom and infrequent action buttons.
4. **Assignment Information**: Current handler information and method of assignment. If using strategic assignment and there is a subsequent step, an upgrade countdown will be displayed here.
5. **Custom Fields**: The area for configuring custom fields.

You can switch to the top tabs to view more detailed **related alarms**, **timelines**, and **historical changes** for fault root cause analysis. For closed faults, the system also displays a **problem resolution** page to show the fault's root cause and solution.

### FAQs
---

<details><summary>Console error: Due to the large volume of data , we are unable to respond to your request in a timely manner. ..</summary><p> This error often appears on fault, alarm list query, analysis dashboard and other pages. Mainly because the system matches too much data and the query times out.</p><p> In this case, please narrow the query scope, such as time interval, or use precise query conditions. If you still have questions, please contact us.</p></details>
---
brief: Flashduty's dispatch strategies, silencing, suppression, routing, and label enhancement features extensively utilize conditional matching to filter specific alerts or incidents. This article introduces how to configure these conditions
---

# Configure Filter Conditions

---


Filter conditions in Flashduty are used to match different alerts, incidents, or events. By using filter conditions, we can selectively operate on specific targets. This article will guide you through the design and configuration of filter conditions.

## Where to Use Filter Conditions?
---

Filter conditions are applied in the following scenarios:

1. **Dispatch Strategy**: Multiple dispatch strategies can be created within the same collaboration space, each with its own set of filter conditions. You can assign different dispatch targets for different incidents.
2. **Silence Rules**: Set filter conditions to match specific incidents, which will be silenced if they meet the criteria.
3. **Suppression Rules**: Set filter conditions to match newly triggered incidents and existing active incidents separately. New incidents that meet the conditions will be suppressed.
4. **Alert Aggregation**: Alert aggregation supports default dimensions, but for finer control, you need to set filter conditions to match specific alerts and define new aggregation dimensions for those incidents.
5. **Routing Rules**: When using the alert integration of the integration center, global routing matching rules can be set. Different alerts can be matched with different filter conditions and routed to specific collaboration spaces.
6. **Label Enhancement**: Set filter conditions to match specific alerts, which will have labels generated according to the rules if they meet the conditions.


## How to Configure Filter Conditions?
---

### Design of Rules

Flashduty abstracts the entire filtering conditions to achieve minimal configuration while meeting the needs of most scenarios.

The overall judgment logic is divided into multiple sets of conditions:
- Conditions within a group are in an **`AND`** relationship, meaning that all conditions must be met for the group to be considered a match.
- Groups of conditions are in an **`OR`** relationship, meaning that if any group matches, the entire set is considered a match.

Each condition is divided into fields, operators and target values. Among them, there are only two situations for operators:
- **`Match`**: The target can have multiple values, and if any value meets the condition, the condition is considered a match.
- **`No Match`**: The target can have multiple values, and if none of the values meet the condition, the condition is considered a match.


:::tip
Condition target values are all strings and support various matching methods, including **Exact**, **Regular**, **Wildcard**, **IP Range**, and **Numerical Size**.
:::

<img src="https://fcdoc.github.io/img/-Vf5HeXq1VMVm1O5j6DdBa2sqiWJKeYxnCN3b9ZTt84.avif" style="display: block; margin: 0 auto;" height="300">

As shown in the diagram above, there are two sets of conditions, each with two conditions and multiple matching values. If the severity is "Critical" or "Warning" and the check label equals "Binlog Synchronization Delay", the overall condition is met. Otherwise, if the check label contains "cpu", "io", or "disk" and the value label's numerical value is greater than 90, the overall condition is also met. The filter conditions can also be described intuitively using an expression:

```
( severity == Critical|Warning && labels.check == Binlog同步延迟 )
or
( labels.check == /cpu/|/io/|/disk/ && labels.value == num:gt:90 )
```

### Filter by Regular Expression

When the value string is both prefixed and suffixed with `/`, the entire value is recognized as a `regular expression`. In this case, the target value must conform to this regular expression for the match to be considered successful.

For example:
- labels.check:/Downtime/, which matches when the check label contains "Downtime".

:::tip
Flashduty uses the `RE2` regular expression specification across all platforms, and some `Perl` syntax may not be compatible. You can use an AI Chatbot to generate expressions and verify them at [RE2 Playground](https://re2js.leopard.in.ua/).
:::

### Filter by Wildcard

When the value string contains `*` or `?` but lacks the `/` prefix or suffix, the entire value is treated as a `wildcard`. Note that currently, only `*` and `?` are supported; `*` can match zero or more arbitrary characters, while `?` can match a single arbitrary character. The target value must match this wildcard string for the match to be successful.

For example:
- labels.check: Downtime*, which matches when the check label starts with "Downtime".

:::tip
You can use `*` to determine whether a field `存在(Exist)` or `不存在(NotExsit)` .

If a field is marked as `match *`, it indicates that the field is required to be present. Conversely, if a field is marked as `not match *`, it signifies that the field should not exist.
:::

### Filter by IP Range

When the value is prefixed with `cidr`, the entire value is interpreted as an `IP range`.

For example:
- labels.host: cidr:10.0.0.206/24, which matches if the IP label is within the "10.0.0.206/24" IP range.

### Filter by Numerical Value

When the value is prefixed with `num: [gt|ge|lt|le]:`, the entire value is recognized as `value size matching`. The rules for size comparison are as follows:
- **ge**: Greater than or equal to
- **lt**: Less than
- **le**: Less than or equal to
- **le**: Less than or equal to

For example:
- Filter by Exact Value


### Filtering by Exact Value

When the value does not conform to any of the aforementioned formats, it is considered an `exact match`. In this instance, the match is successful only when the strings are an exact match.

## FAQs
---

<details><summary>Why am I not prompted for optional tags?</summary> Flashduty Accepts a large amount of data reporting. In order to ensure the stability of the system, the system only searches for up to 500 alarm events in the past 24 hours to deduplicate labels. Therefore, the range of extracted tags may change dynamically, and even no tags can be extracted when there is no new data in the past 24 hours).<p> In this case, **you can enter the tag manually** .</p></details>

<details><summary>My regular expression has passed offline verification, why can't it be matched in the system?</summary> Flashduty All platforms use the ` RE2 ` regular specification, and some ` Perl ` syntax may not match. You can use AI Chatbot generate expression, and go to RE2 Playground to verify.</details>
---
brief: By modifying push parameters, you can customize the severity level and title information for faults
---

# Customize fault titles and severity levels

---

By adjusting push parameters, you can tailor the severity and title details of faults.

## Customize severity levels
---

**Add a query parameter 'severity' to the push URL to override the fault severity.**

:::tip
Compatible with all integrations reporting alerts via webhooks.
:::

Some alarm integrations (such as AWS CloudWatch) do not support severity differentiation. In this case, we can specify it in the integration push address. Different alarm policies are configured with different push addresses to differentiate the severity of alarms.

Example: The following URL specifies a 'severity' parameter with the value 'Info' ( **note the capitalization of the first letter** ). Alerts pushed through this URL will have their severity level overridden to 'Info'.
```
https://api.flashcat.cloud/event/push/alert/aws/cloudwatch?integration_key=your-integration-key?severity=Info
```

## Customize fault titles
---

:::tip
Compatible with all integrations reporting alerts via webhooks.
:::

**Add a query parameter 'title_rule' to the push URL to dynamically generate fault titles.**

### Generated using simplified syntax

Use '::' to separate substrings, where each substring can be a fixed string or a variable prefixed with '$'. The variable content will be extracted from the tags; if extraction fails, no variable substitution will occur.

Example:

| rule | tag value | generated content |
| --- | ---| ---- |
|\$resource::\$check | {"resource": "127.0.0.1", "check": "cpu idle low"} | 127.0.0.1 / cpu idle low |
|\$resource::\$check | {"resource": "127.0.0.1"} | 127.0.0.1 / \$check |
|$resource:: Host Down | {"resource": "127.0.0.1"} | 127.0.0.1 / Host Down |


### Referencing tags to generate content using ${var}

Use '[TPL]' as the prefix and '${}' to reference variables. The variable content will be extracted from the tags; if extraction fails, use '<no value\>' as a substitute.

Example:

| rule | tag value | generated content |
| --- | ---| ---- |
|[TPL]\${resource} / \${check}| {"resource": "127.0.0.1", "check": "cpu idle low"} | 127.0.0.1 / cpu idle low |
|[TPL]\${resource} / \${check} | {"resource": "127.0.0.1"} | 127.0.0.1 / \<no value\> |
|[TPL]${resource} / Host Down | {"resource": "127.0.0.1"} | 127.0.0.1 / Host Down |


### Generated using Golang template syntax

Use '[TPL]' as the prefix and '{{}}' to reference variables (which can include tags and other variables). If extraction fails, use '<no value\>' as a substitute. Refer to [Alarm Event Definition](#AlertEvent) for the variable scope.

Example:

| rule | tag value | generated content |
| --- | ---| ---- |
|[TPL]{{.Labels.resource}} / {{.Labels.check}}| {"resource": "127.0.0.1", "check": "cpu idle low"} | 127.0.0.1 / cpu idle low |
|[TPL]{{.Labels.resource}} / {{.Labels.check}} | {"resource": "127.0.0.1"} | 127.0.0.1 / \<no value\> |
|[TPL]{{.Labels.resource}} / Host Down | {"resource": "127.0.0.1"} | 127.0.0.1 / Host Down |

## FAQs
---

<details>
<summary>What should be done if tags are missing when dynamically generating titles?</summary>

Depending on the variable retrieval method used, the title may retain the original variable information or use '<no value\>' as a substitute.

Even if variables cannot be retrieved, the generation of alerts will not be affected, allowing for confident debugging.
</details>
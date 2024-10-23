---
brief: Understand, configure, and utilize custom fields
---

# Custom Fields

---

Understand, configure, and utilize custom fields.

## Usage Scenarios
---

FlashDuty has already integrated with most common alert systems, placing the majority of push content information into Labels for display. Nevertheless, our users still have some needs for expansion or customization, such as manually marking a fault as a false alarm. Therefore, we have introduced the **Custom Fields** feature to further enhance fault descriptions.

Custom fields enable you to add personalized metadata, record specific fault-related information, and utilize this information throughout the fault resolution process. Here are some common scenarios for using custom fields:

- **Flexible Definition**: You can create multiple custom fields as needed, defining field names, types, optional choices, and default values.

![field_list.png](https://fcdoc.github.io/img/cvylIK7Sjff1ob1ZMisQH_yeUeEviyzie3RiMU2b59c.avif)

- **Information Association**: Custom fields can be used to associate faults with other relevant data. For example, you can add custom fields to indicate affected systems, geographic locations, associated clients, or whether it's a false alarm.

![reset_field.png](https://fcdoc.github.io/img/4TczIamyUJycZfUIZWU_fTAAROBC3p7o1e96Ejcku9I.avif)

- **Filtering and Categorization**: The fault list supports filtering and categorizing views based on custom fields. You can create common filter options based on the values of custom fields to better organize and manage faults.

![card_view.png](https://fcdoc.github.io/img/qgzMUmesZeZzn3VDyYPdiwAcNxkJzd7czJX92cR_np8.avif)

## Configure Custom Fields
---

### Create Fields

:::highlight orange 💡
An account can support the creation of up to 15 custom fields.
:::

1. Enter the console **Fault Management => Custom Fields**
2. Click **Create Custom Field**
3. Enter the following information:

- **Field Name**: Identifies the field in the API and cannot be modified after creation.
- **Display Name**: The field name displayed on the fault details page, which can be modified after creation.
- **Field Description**: Helps those handling faults to understand and use the field effectively.

4. Select the field type and add optional choices and default values as necessary. The following field types are available:

- **Text**: A plain text input box that can accommodate up to 500 characters.
- **Single Choice**: A single selection dropdown allowing for up to ten options, with each option not exceeding 200 characters.
- **Multiple Choice**: A multi-selection dropdown allowing for up to ten options, with each option not exceeding 200 characters.
- **Checkbox**: A checkbox input.

5. Click **Submit** to complete the process

:::highlight orange 💡
If a field has a default value set, the system will automatically populate this field with the default value when a fault is created. Note that this only applies to new faults and will not affect existing ones.
:::

### Update Fields

Only the following content can be updated:

1. 3	display name
2. 4	Field description
3. 5	Field options (available for single-select and multi-select types only)
4. 6	default value

:::highlight orange 💡
Any updates to fields will only apply to new faults and will not impact existing ones.
:::

### Delete Field

You can initiate a deletion at any time from the console. However, be aware that deletion is a time-consuming process. When a field is deleted, the system will scan historical faults and update the associations asynchronously. You will not be able to recreate a field with the same name until the deletion process is complete.


## FAQs
---
<details><summary>Why can't I retrieve the fault by the field I created?</summary><p> Please confirm whether the field type you want to retrieve is **text** type. In order to ensure the stability of the system, the system currently does not support retrieving text type fields, please understand.</p></details>
---
brief: What is a collaboration space, what are its features, and how is it managed?
---

# Collaborative space

---

As a core vehicle for organizing and managing troubleshooting, the collaboration space aims to manage separately the alerts from different teams, business systems, or service modules. Typically, each collaboration space corresponds to a specific operational and maintenance scope within the team's daily activities.

## Create a Collaboration Space
---

### Principles of Space Planning

✓ It is recommended to create collaboration spaces logically based on dimensions such as business systems or team responsibilities, for example, establishing a collaboration space for an order management system that handles故障 events related to the order processing workflow. This ensures focused information and efficient collaboration, enabling team members to quickly access information directly related to their work, enhancing processing efficiency, and reducing cross-domain interference, which is beneficial for clarifying responsibilities, tracking tasks, and improving the timeliness of project management and problem resolution.

✗ It should be avoided to integrate different types of or unrelated alerts into the same collaboration space. For instance, a space should not simultaneously handle both order-related alerts and those related to hardware resources or networks, as this would lead to confusion in handling, dispatching, and analyzing alerts, making it difficult for teams to accurately identify and prioritize issues, thus decreasing work efficiency.


### Begin Creation
Login to the console to create, path: **Fault Management => Collaboration Space => Create Collaboration Space**.

- **Space Name:** It is suggested to name and plan based on departments, teams, or business types to gain a clearer understanding of the space's purpose.
- **Description:** A brief summary of the business handled by the space and the types of alerts it receives is recommended.
- **Management Team:** The management team for the space can be set upon creation. **Team members have full operational permissions for the space**, while non-creators have read-only access to the space's configuration.
- **Automatic Timeout Closure:** After N minutes of inactivity, the system will automatically close the fault **(applicable to all new faults in this space)**. Faults that are closed due to timeout will **receive corresponding notification messages** (the notification channel depends on the configuration of the [dispatch policy](https://docs.flashcat.cloud/zh/flashduty/escalate-rule-settings)).
- If the distribution of faults within the space has not been planned, you can **skip setting the dispatch policy**. After creation, you can continue to configure the dispatch policy.
- During creation, the type of integration connected is **exclusive to that space** and only effective within it. It can also be overlooked and configured after creation.


## Manage Collaboration Space
---
### Space Overview
- Account members can view all collaboration spaces but can only operate the ones they are responsible for.
- by hovering over a collaboration space and clicking the star icon, you can **favorite or unfavorite** it.
- By default, all collaboration spaces are displayed. You can **view collaboration spaces related to "me" by selecting "Managed by Me" or "My Favorites"**.
- When there are many collaboration spaces and the ones you are interested in are ranked low, you can **use the sorting feature in the upper right corner to bring your preferred collaboration spaces to the forefront**.
- Sorting can be freely arranged and **will only affect the current user, not others**.


### Change Information
- The space name, description, automatic timeout closure, and management team can be changed, which can be modified in the Space Details -> Basic Settings section.
- Once a collaboration space is disabled, it will no longer receive alerts but can still be used to manage existing faults and related configurations.
- Deleting a space will not delete the fault data that has been integrated into it, but the space cannot be restored after deletion, so please proceed with caution.

### Fault List
- Displays all faults integrated into this space, with the default view showing only unresolved faults. You can filter by **processing status**.
- Filter conditions can be set based on fault status, handler, time, title, and other criteria.
- Select multiple **faults with the same status** to perform batch operations such as closing or claiming.
- **Merging** allows multiple faults to be combined into one for handling, supporting merging across different collaboration spaces.
- **For more details, please refer to [Searching and Viewing Faults](https://docs.flashcat.cloud/zh/flashduty/view-incidents)**.


### Integrated Data
- Integrations created under a collaboration space are **exclusive to that space**.
- Each type of integration, once created, generates a corresponding webhook address, and **different types of integrations are not compatible with each other**.
- Exclusion rules are used to discard events that meet certain criteria and can be configured based on integration type, severity, and other conditions.
- When multiple exclusion rules are present, they are matched in order of priority from highest to lowest, and matching stops once a rule is triggered.
- Events that are excluded **will not be displayed anywhere in the system**, making them invisible. If alerts are not received, check first to see if exclusion rules have been configured.

### Distribution Strategy
- Manage notification rules, channels, and escalation policies for faults.
- Fault notifications are matched sequentially according to the order of each policy, and no further matching occurs after a match is found.
- When multiple policies exist, you can freely drag and adjust the order of the distribution policies, ensuring that notification rules align with business needs before making changes.
- For more information on **distribution strategies**, please refer to the [Distribution Strategies](https://docs.flashcat.cloud/zh/flashduty/escalate-rule-settings) section.

### Noise Reduction Configuration
- Aggregation noise reduction combines similar or related alerts into a single fault.
- Aggregation can be configured based on alert title, level, and label dimensions.
- Fault convergence automatically suppresses notifications for the same fault within a certain time frame.
- For more information about **noise reduction configuration**, please refer to the [Noise Reduction Configuration](https://docs.flashcat.cloud/zh/flashduty/noise-reduction-settings) section.
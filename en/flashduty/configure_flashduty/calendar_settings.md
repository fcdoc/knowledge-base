---
brief: By configuring the service calendar, you can manage allocation strategies and silent rules using either the working day or rest day mode
---

# Configure Service Calendar

---

## Application Scenarios
---
- When assigning faults, the calendar mode can be used to dispatch them according to rest or working days.
- When it is necessary to silence alerts during a specific time period, the calendar mode can be employed for periodic silencing.

## Create Calendar
---
**Navigate to Console => Fault Management => Service Calendar => Add Calendar to create.**
- It is recommended to name the calendar based on the business dimension, for example, "Settlement Business System."
- The calendar description should provide an overview of the business characteristics and logic, allowing team members to quickly grasp the information.
- After configuring team members to manage the calendar, they will have full permissions for that calendar.
- Newly created calendars are set to all working days by default. It is generally advised to link them directly to national holidays to automatically incorporate holiday schedules, thus saving the manual marking process. Even after linking, manual adjustments can still be made as needed.

![Service Calendar](https://fcdoc.github.io/img/GG_lye0HJBxjFs54noT-0OrrOiUBH8NPZqkny2qYXl4.avif)

## Edit Calendar
---
- Only the creator and team members have the right to edit the calendar; other members have read-only access.
- Basic information such as the calendar name, description, and management team can be modified.
- Rest days can be quickly marked based on the weekday.

![](https://fcdoc.github.io/img/6we-QRWfJKvBVRJZC2rF7JdF73fg6ntjNLDnw0A5GSg.avif)


:::caution

Deleting a calendar is irreversible. Please ensure no business is using it before deletion.

:::

## FAQs
---
<details><summary>What is the difference between calendar and duty labels?</summary> The biggest difference between the service calendar and the duty schedule is that the positioning and application scenarios of the two are different. When the duty schedule is used for receiving, it belongs to the receiving object of fault events and is responsible for receiving and processing the faults assigned to the duty; while the service calendar is used for dispatching time, that is, it is responsible for assigning faults in which time periods, and belongs to the upper layer of the receiver ; The service calendar is generally used in the securities industry. For example, only business that trades on weekdays needs attention.</details>
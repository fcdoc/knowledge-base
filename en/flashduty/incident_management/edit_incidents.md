---
brief: Learn how to modify information such as the title of the incident and how to address the issue
---

# Handle and update incidents

---

Invesitigate incidents, update key information, and synchronize with others.

## Modify information
---

When an incident is triggered and its symptoms become clearer over time, you can update key details like the incident title to make it more precise than the original alert information.

### Modify incident title

1. Open the incident details on the console, locate the title section, and click the "Modify" button.
2. Enter a new title and finish.

:::highlight orange 💡
The modified title will not change with the integration of new alerts.
:::

### Modify incident severity

1. Open the incident details on the console, navigate to the severity section, and select a new severity level.
2. Remove the mouse focus to complete.

:::highlight orange 💡
The modified severity will not change with the integration of new alerts.
:::

### Modify incident description and impact

1. Open the incident details on the console, go to the description and impact section, and enter new information directly.
2. The system will automatically save the changes.

**You can use Markdown syntax to update the description and impact of the incident, or you can directly copy and paste images!**

:::highlight orange 💡
The modified description will not change with the integration of new alerts.
:::

## Claim an incident
---

You have three methods to claim a newly triggered incident.

### Claim incidents through the console

- 4	**Single Claim**: Click the fault details on the console and click the **Claim** button to complete the claim.
- 5	**Batch Operation**: In the console fault list, select multiple faults to be processed, and click the **Claim** button to complete batch claiming.

### Claim incidents through an IM application

- 6	**Application Messages**: The main card of application messages features a **Claim** button. Click the card to complete the claim. If the card does not respond upon clicking, it may indicate that you have not associated your login account within the app or for other reasons. For details, please refer to the [Feishu Lark Integration Guide](http://docs.flashcat.cloud/zh/flashduty/lark-integration-guide).
- 7	**Robot Messages**: Most robot channels deliver messages in Markdown format. You can modify the notification template to include a **Claim** link that directs to the console for the claim process. Please consult the default template for more information.

### Claim incidents through a voice call

8	Flashduty's voice alarm notifications will prompt you to **press 1 for one-click claim** at the end of the voice broadcast. Press button 1, and the system will complete the fault claim on your behalf.

### Cancel the claim on an incident

Once someone claims an incident, the status will change from "Pending" to "Closed." Subsequent claims by others will not alter the incident's handling progress.

9	After a single individual claims a fault, they can opt to **Unclaim** it, which is applicable in cases of mistaken claim. When all claimants have withdrawn their claims, the fault will revert to the **Pending** status.


### Handling progress and MTTA

You can view each person's assignment and claim times in the console. We calculate the MTTA of an incident based on the following rules:

- MTTA (Mean Time to Acknowledge) is defined as the average time to acknowledge, which is the average difference between the claim time and the trigger time.
- For the same incident, each person may have different assignment and claim times. Therefore, each person's MTTA calculation will vary.
- For the overall MTTA of an incident, only the difference between the incident's trigger time and the time of its first claim is considered.

## Postpone handling
---

10	After a fault has been claimed, the handler may require time to investigate and address the issue. The **Suspension** action can temporarily halt the fault's progression according to the anticipated dispatch strategy. You can set a suspension period after claiming the fault, such as 2 hours, 4 hours, or define a custom expiration time within 24 hours.


:::highlight orange 💡
12	Should you initiate a suspension and the suspension period expire without completing the fault handling, the system will automatically revert the fault to the **Pending** status and reinitiate the dispatch notification.
:::

### Postpone incidents through the console

13	Click the fault details on the console, select the **Suspension** button, choose the suspension duration, and proceed.

### Postpone incidents through an IM application

14	On the fault message card, click the **Suspension** button, select the delay duration, and complete the action.

## Close an incident
---

You have multiple ways to close an incident.

### Close an incident through the console

- 15	**Single Shutdown**: Click the fault details on the console and click the **Close** button to complete the shutdown.
- 16	**Batch Operation**: In the console fault list, select multiple pending faults and click the **Close** button to complete batch closure.

### Close an incident through an IM application

17	The application message main card includes a **Close** button. Click the card to complete the claim. If the card does not respond upon clicking, it may indicate that you have not associated your login account within the app or for other reasons. For details, please refer to the [Feishu Lark Integration Guide](http://docs.flashcat.cloud/zh/flashduty/lark-integration-guide).

### Reopen an incident

Manually closing a fault will change its processing status to **Closed**. You can click the **Close** button at any time. After a fault is manually closed, its associated alarms will also stop incorporating new events. If the alarm is not restored in the original alarm system, a new notification event may be generated, potentially triggering new alarms and faults in Flashduty.

19	You can reopen a fault after accidentally closing it. Upon reopening, the fault will revert to the **Pending** status, and dispatch and notification will be reinitiated.

## Merge handling
---

You can manually merge incidents with each other or with alerts. Merging similar alerts and incidents can converge information into a single incident, accelerating the handling process.

**Merge incidents**: You can select multiple incidents on the console and merge them into a target incident. You can also select other target incidents to merge under specific incident details.

20	**Merge Alarms into Faults**: Alarms may be aggregated into a fault due to aggregation policies, but you may wish to adjust the relationship between the fault and the alarm. Access the alarm details, click the **Merge** button to transfer the alarm to the target fault.

**The essence of merging is to change the relationship between alerts and incidents. If all alerts associated with an incident are merged into another incident, the original incident will be closed directly. You will only need to handle the target incident moving forward.**

The timeline will fully record your modification process.

## FAQs
---

<details><summary>I suspended the fault, why did the system still trigger a new similar fault?</summary><p> You may misunderstand **the suspend function** as **the silent function** , but there is a big difference between the two.</p><ul><li> The silent function requires you to fill in the matching policy. When a newly triggered fault matches the silent policy, no notification will be issued. Quiet policies can affect the triggering of notifications for new faults.</li><li> The suspension function does not require you to fill in any policies. It only buys you a period of time to deal with the fault after you claim it, preventing the fault from being escalated to the next handler.</li></ul><p> If you need to suppress an alert policy, use **silence** instead of **suspend** .</p></details>
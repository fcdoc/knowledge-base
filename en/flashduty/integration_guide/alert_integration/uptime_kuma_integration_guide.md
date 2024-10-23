---
brief: Synchronize Uptime Kuma alert events to Kuaimao Xingyun via webhook to automate noise reduction processing of alerts
---

# Uptime Kuma Integration

---

Synchronize Uptime Kuma alert events to Flashduty via webhook to automate noise reduction processing of alerts.

## In Flashduty
---
You can obtain an integrated push address using two methods; select either one.

### Use Exclusive Integration

When there's no need to route alert events to different collaboration spaces, choose this method for its simplicity.

<details><summary>Expand</summary><ol><li><p> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</p></li><li><p> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</p></li><li><p> Select **Uptime Kunma** Integrate, click **Save** , and generate the card.</p></li><li><p> Click on the generated card to view **the push address** , copy it for later use, and complete.</p></li></ol></details>

### Use Shared Integrations

When routing alarms to various collaboration spaces based on the payload information of alarm events is required, this approach is the preferred choice.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Uptime Kunma** integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li></ul><ol start="3"><li> After clicking **Save** , copy the newly generated **push address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>


## The process is now complete
---
**Step 1: Set up notification channels**

1. Access the `Settings -> Notifications` page, click on "Setup" to edit, as illustrated in the figure below;
2. Select `Notification Type` as `FlashDuty (Flashduty)`;
3. Copy and paste the `Integration Key` from the integrated push address into the corresponding field;
4. Choose the appropriate `Severity` as needed;
5. Submit the changes to save

<img alt="drawing" width="400" src="https://fcdoc.github.io/img/qhNB9d5__aqCBTrcBAcfGYP5YeeaAAdrSxF3KlQjg6M.avif" />

**Step 2: Configure monitoring items**

<div id="!"><ol><li>Click `Add New Monitor` or edit existing monitoring items to complete monitoring configuration as needed;</li><li> As shown in the figure, part `Notifications` on the right enables the notification method created in the previous step;</li><li> If you need to set a label, you can add `Tags` Note that only labels that exist at the same time Key/Value will be pushed to FlashDuty ;</li><li> Submit and save, waiting for the alarm to be triggered.</li></ol><img alt="drawing" width="600" src="https://fcdoc.github.io/img/MhOsvqHsYIku4nGsClITGQNGpNqg1ceKLBKd6xcN_P0.avif"></div>

## Status Comparison
---
<div class="md-block">

| Uptime Kuma  |  Flashduty  | State |
| ------------ | -------- | ---- |
| Critical     | Critical | Severe |
| Warning     | Warning  | Warning |
| Info     | Info     | Reminder |

</div>
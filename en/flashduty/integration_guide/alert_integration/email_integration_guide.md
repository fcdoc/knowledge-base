---
brief: Generate a unique email address in Flashduty and synchronize alarm occurrences and recoveries to Flashduty via email
---

# Email Integration

---

Generate a unique email address in Flashduty and synchronize alarm occurrences and recoveries to Flashduty via email.

## Operation Steps
---

### Create Email Integration

You can obtain an email address using either of the following two methods.

#### Use Proprietary Integrations

When you do not need to route alarm events to different collaboration spaces, this method is preferred because it is simpler.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **the collaboration space** , and enter the details page of a certain space</li><li> Select **Integration Data** tab and click **Add an Integration** to enter the Add Integration page.</li><li> Select **Mail Email** Integration, click **Save** , and generate the card.</li><li> Click on the generated card to view **the email address** , copy it for later use, and complete.</li></ol></details>

#### Use Shared Integrations

When you need to route alarms to different collaboration spaces based on the payload information of the alarm event, this method is preferred.

<details><summary>Expand</summary><ol><li> Enter the Flashduty console, select **Integration Center = > event** , and enter the integration selection page.</li><li> Select **Mail Email** Integration:</li></ol><ul><li> **Integration Name** : Define a name for the current integration.</li><li> **Email address** : Set a prefix for the email that is easy to remember and needs to be unique under the account.</li><li> **Push mode** : Select the situation under which the email triggers or restores the alarm.</li></ul><ol start="3"><li> Copy **the email address** of the current page for later use.</li><li> Click **Create Route** to configure routing rules for the integration. You can match different alarms to different collaboration spaces based on conditions, or you can directly set the default collaboration space as a fallback, and then adjust it as needed.</li><li> Finish.</li></ol></details>

### Customize Email Integration

#### Email address

By default, the system generates a unique email address for you. You can customize it, but note that **the email prefix must consist only of letters and numbers** and remain unique within your account.

#### Push Mode

By default, the system creates a new alert for each email, but you can switch to:

1. **Trigger or Update Alerts Based on Email Titles**: In this mode, upon receiving a new email, the system searches for open alerts based on the email title. If an alert is found, it is updated; otherwise, a new alert is triggered.
2. **Trigger or Close Alerts Based on Rules**: In this mode, upon receiving a new email, the system matches the email against your rules, triggering new alerts or closing existing ones accordingly.

- You must define at least one **trigger** rule
- You must set the regular expression for extracting the Alert Key. The system uses this field to find historical alerts for updates or closures; **if the regular expression fails, the system uses the email title to generate the Alert Key**, ensuring alerts are not lost due to configuration errors
- You can opt to discard emails when no rules match.

Configuration Example:

- Receive all emails; when the content includes the word **RESOLVED**, close the alert, otherwise trigger a new one
- Extract the Alert Key from the email title using the rule **/(.*)/**.

<img src="https://fcdoc.github.io/img/UzSAxxB8q30joMRUlGUldv2u9iiYGCNCXG0uJmiRvtA.avif" alt="drawing" width="800"/>

### Notes

1. The system will reject emails larger than 5MB.
2. If the text content of an email exceeds 32KB, the system will truncate it and add a label prompt in the fault details

```
body_cut = true
```

3. If an email contains an attachment, the system will discard the attachment and add a label prompt in the fault details

```
attachment_stripped = true
```

4. In new alerts triggered by email, **the title is the email's subject, and the description is the email's content**.

5. If you change your account's domain name, the email address will also change. Be sure to update the push address accordingly.



## Severity Level Mapping
---

The current email integration pushes alerts to Flashduty at a Warning level.
---
brief: Learn how to quickly get started with Flashduty
---

# Quick Start Guide

---

## Demonstration Video
---

<Video src="https://fcdoc.github.io/img/demo.mp4"></Video>


## Get Started for Free
---

1. Visit [Flashduty Console](https://console.flashcat.cloud/) via your browser, enter your **mobile number** or **work email**, read and agree to our [Terms of Service](https://docs.flashcat.cloud/zh/flashduty/user-aggrement) and [Privacy Policy](https://docs.flashcat.cloud/zh/flashduty/privacy-policy), then click "Next." The system will send a verification code to your mobile or email.
2. Enter the name of your **company or organization**, along with the verification code received in the previous step, click "Next," and complete the registration.
3. The system will guide you through the process of completing your information and will send you a custom alert event to experience voice, SMS, or email notifications.

:::tip
Due to security considerations, the system only allows registration via work email. This means that if you use an email with a suffix like qq.com, gmail.com, 163.com, etc., your registration will be rejected.
:::


## Basic Workflow
---

![](https://fcdoc.github.io/img/ou5ipHtxUCsHg62yRMA8mRHHPtwemssZ5PAlcsAG2MY.avif)

### Create a Collaboration Space

A collaboration space serves as a container for related incidents. We typically use the services owned, managed, and monitored by a team as the collaboration space, such as order systems, recommendation services, MySQL components, Client A, etc.

Enter the [collaboration space](https://console.flashcat.cloud/channel) list page, click **Create Collaboration Space**, and provide an intuitive and concise name along with a description. Associate a management team with the collaboration space to facilitate future multi-person management.

:::caution
Collaboration spaces are managed through data permissions rather than by role.

**Only the account owner, collaboration space creator, and members of the management team** have the authority to modify the collaboration space configuration; others can only view it. This means anyone can create a collaboration space, but only modify those they are managing.

**Even as an account administrator, you cannot modify the configuration of a collaboration space you are not managing.**
:::


### Integration of Alert Events

Collaboration spaces can only store incidents and require external integration to receive alert event reports.

1. Navigate to the collaboration space details, click on **Integrated Data**, select **Add New Integration**, choose the alarm system your company uses, and then save the changes.
2. The new integration will generate a unique push address, and any alerts sent to this address will be directly added to the current collaboration space. You will need to complete the alert push configuration according to the integration details documentation.

- To route alerts to different collaboration spaces based on conditions, go to **Integration Center - Alert Events**, add a shared integration, and set up routing rules based on those conditions. This method is particularly useful for integrations like Zabbix and Prometheus that do not easily support webhook policy management.

3. If the integration receives an alert event, the integration card will display the **latest event time**. Otherwise, it will show **no alerts received yet**. You can check if your monitoring system has generated new alerts and if the network is functioning properly.


:::tip
Flashduty is compatible with most daily-used monitoring systems and can be used right away. If you have a custom alert system, use **Custom Events** or **Email Integration**. If you have other monitoring system needs, feel free to contact us.
:::

### Configure Notification Methods

When an incident occurs, how will you be notified?

1. Access the collaboration space details, click **Distribution Strategy**, and either add a new strategy or modify an existing one.
2. Access the first step of the configuration to specify the distribution personnel, i.e., the respondents after an incident is triggered, and specify their notification methods.
- Choose a shift, team, or individual as the distribution target. It is recommended to use shifts, so that only the current on-duty personnel are notified when an incident occurs.
- Single chat refers to one-on-one notifications, such as via text message, voice call, or email. IM applications like Feishu and DingTalk also support one-on-one chat notifications.
- Group chat refers to notifications sent to an IM group, with @mentions for the assigned personnel.
4. To ensure incidents are addressed, you can add an escalation step. For example, if an incident is not resolved within 30 minutes, it can be escalated to the Team Leader.

:::tip
How to set up incident notifications according to personal preferences?
Go to **Account Settings > Notification Settings** to configure how you are notified when assigned or during shift rotations. Note that these settings only apply when assigned directly or when using policy-based assignments that follow personal preferences.
:::

## Official Subscription
---

:::tip
Only individuals with **Subscription Management** permissions can perform this action.
:::

Newly registered businesses automatically receive a 2-week free trial. After testing, you can visit the **Payment Center** to choose between the Professional or Standard editions for an upgrade.

- You can compare the feature differences between different versions at the bottom of the page.
- Only members who handle incidents daily need a license. If you only receive alert notifications passively, there is no need to purchase a license.
- If there are insufficient licenses, members without a license will not be able to view or handle incidents. You can purchase additional licenses in the console at any time, which will take effect immediately.
- Each license comes with a certain amount of free communication credit, which is shared among all members.
- Five days before the subscription expires, the system will remind the primary account holder via text message daily. Please renew in a timely manner to avoid disruption to alert reception.
---
brief: Through the integration of third-party applications in Microsoft Teams, enable the capability to receive and respond to alerts within Microsoft Teams
---

# Microsoft Teams Integration

---

Through the integration of third-party applications in Microsoft Teams, enable the capability to receive and respond to alerts within Microsoft Teams.
## 1. Install the Application
---

The Microsoft Teams integration is currently in the Beta phase. Before proceeding with the association, you need to complete the following actions:

::: caution
This step must be completed by a Microsoft Teams administrator
:::

### 1. Download the Application Package
Download [FlashDutyBot.zip](https://fcpub-1301667576.cos.ap-nanjing.myqcloud.com/flashduty/integration/microsoft-teams/FlashDutyBot.zip) to your local machine

### 2. Upload the Application Package
Enter **Microsoft Teams jump to [ +Apps ] - [ Manage your apps ] - [ Upload an app ] - [ Upload an app to your org ' s app catalog ]** to upload the application package FlashDutyBot.zip


![](https://fcdoc.github.io/img/4H1BjgL-F76QJ7e_BvGHE9JSdClYYtFcqgibEjjaeeM.avif)

### 3. Configure Application Visibility
Enter the Microsoft Teams admin center, locate the FlashDuty app, and adjust the visibility scope of the app to everyone (or to your custom scope)

::: tip
If you encounter a status of [Blocked] for the application, please wait a moment, refresh the page, or make changes manually
:::
![](https://fcdoc.github.io/img/jNLXwWgaj5dxyxxgtyWjdSjJIF4XJpq1x4cBSQ4eAb4.avif)

### 4. Check if the addition was successful
Wait a few minutes, and organization members will be able to find this app integration under [+Apps] - [Built for your org]

![](https://fcdoc.github.io/img/mDDLIqPv8lNm_zqQrh9qHQZc3SCtgyARuN5wDaODyEs.avif)

## 2. Associate Teams

### 1. Add the FlashDuty app to the target Team

#### 1.1 Locate the FlashDuty app
If the app is not available, please contact your Microsoft Teams organization administrator
![](https://fcdoc.github.io/img/mDDLIqPv8lNm_zqQrh9qHQZc3SCtgyARuN5wDaODyEs.avif)

#### 1.2 Add to the target Team
::: caution
Note: This step requires selecting the General Channel of the target Team; otherwise, the alerts will not be sent to the Team
:::

![](https://fcdoc.github.io/img/yGkKFnJa_bt0FwUNfYNz_HoaDD7RbQUnrm2vuSGceW0.avif)

### 2. Send the Association Command
@FlashDuty and send linkTeam {ID} to the added Team, then click to associate immediately

![](https://fcdoc.github.io/img/3ncB4ZFRKrXfiFI9mY1_dWgRQSlaiFWdjYLozZtc5t8.avif)

## 3. Associate Users

### 1. Add the FlashDuty app

#### 1.1 Locate the FlashDuty app
If the app is not available, please contact your Microsoft Teams organization administrator
![](https://fcdoc.github.io/img/mDDLIqPv8lNm_zqQrh9qHQZc3SCtgyARuN5wDaODyEs.avif)

#### 1.2 Click the Add button
::: caution
Note: This step requires selecting the General Channel of the target Team; otherwise, the alerts will not be sent to the Team
:::

![](https://fcdoc.github.io/img/BxbYezkSRzMseDCvtFvLuNCVzAj5TUTOexiKGkSpo04.avif)

### 2. Send the Association Command
Copy the command: linkUser {} and send it to the chat, then click to associate immediately

![](https://fcdoc.github.io/img/cpsWE8YB5hTfUdPnNl4x6T8p7uq40Ew_6763QVKxIqU.avif)

## FAQs
<details><summary>Team or Individual Fails to Receive Messages</summary> Please go to the Integration Center => Instant Messaging => Check if the team and user in Microsoft Teams are successfully associated.</details>

<details><summary>How to View Associated Teams and Users</summary> Please go to the Integration Center => Instant Messaging => View the associated Teams and users in Microsoft Teams.</details>

<details><summary>How to Cancel Associated Teams and Users</summary> This feature is not supported yet.</details>
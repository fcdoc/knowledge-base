---
brief: By integrating third-party enterprise WeChat applications, the ability to receive and respond to alerts within the enterprise WeChat client is realized
---

# Enterprise WeChat Integration

---

By integrating third-party enterprise WeChat applications, the ability to receive and respond to alerts within the enterprise WeChat client is realized.

## 1. Install the Application
---

1. Visit [the Enterprise WeChat Management Backend](https://work.weixin.qq.com/wework_admin/frame#apps) - `Application Management` - `Third-Party`, and select to add a third-party application

<img src="https://fcdoc.github.io/img/IgG_9fMWOSStyP-Mfy34i03HFthJ3GNqJhQ0h0wYKE8.avif" alt="drawing" width="400"/>

2. Enter `flashduty` in the search bar, locate the application, and click the `Add` button

<img src="https://fcdoc.github.io/img/FIPgCZNwraqFTID3vXd6xBQ2KpLSF6ba4IzwPLx-0EI.avif" alt="drawing" width="400"/>

3. Adjust the application's `Visibility Scope`, recommending it for all members or specific department nodes to avoid modifying the scope when new members are added. Click `Agree to the Above Authorization and Add` to complete the installation

<img src="https://fcdoc.github.io/img/q-OMKvZ372VP_Z9Ym2g63seLWgZjyfrmGQzZG27uJkA.avif" alt="drawing" width="400"/>

4. Access [the Enterprise WeChat Management Background](https://work.weixin.qq.com/wework_admin/frame#apps) - `My Enterprise` page, copy the `Enterprise ID` as the `Corp ID` for the current page, and fill it into the integration configuration. Click Save to complete the integration setup

<img src="https://fcdoc.github.io/img/DZu7yYB2CXNegJm6ZkFdR3TcARZnoBvKY_LPgOPsIv0.avif" alt="drawing" width="400"/>

5. **Note: Flashduty, as an enterprise WeChat service provider, offers you a long-term free version of the `FlashDuty` application. This application requires an enterprise WeChat interface calling license to be used (password-free login + sending messages). This license currently supports a `60-day` free trial. Afterward, we must purchase an enterprise WeChat license for you to continue using it.**

## 2. Common Issues
---

1. **Upon clicking the integrated save button, an error `authorize app first` appears?**

- Please check if you have completed the application installation steps, such as whether you can see the `FlashDuty` application in the workspace
- Please check if you have correctly configured the `Corp ID`

2. **How to complete account linking? Or message sending prompt `未关联应用` ?**

- Login to the enterprise WeChat client (desktop or mobile), navigate to the `Workspace`, find and enter the `FlashDuty` application
- You will need to log in upon first entering the application. Choose member account - Password or Single Sign-On. After successful login, the association between `Flashduty` and the `Enterprise WeChat` account is established
- Subsequent entries into the application will be password-free

3. **How to send fault notifications?**

- You must first complete the account association as described in question 1 before sending notifications
- Enter the details page of a specific collaboration space - Dispatch Strategy, and under the personal channel section, select to notify the enterprise WeChat integration to complete the notification configuration
- Support for customizing the content of enterprise WeChat notifications is available. You can go to the template management page to set a custom template. Note: **The custom area can display a maximum of 8 lines. Content exceeding this limit will be truncated by enterprise WeChat.**

<img src="https://fcdoc.github.io/img/YJ3cNz2YnnC8zi44MUfat7CNuti0ntKvxzXD4eB2XlM.avif" alt="drawing" width="400"/>

4. **How to handle alerts within WeChat?**

- Click on the card message to directly go to the alert details page
- Click `Start Processing` to immediately set the alarm to `In Progress` status
- Click `Directly Close` to immediately set the alarm to `Closed` status
- Click `Block for 2 Hours` to immediately block the alarm for a period of 2 hours. For longer blocking periods, click the `...` in the upper right corner of the card for additional blocking options

5. **Why is a `Refresh Status` button provided in the card message?**

- Enterprise WeChat limits card interactions to one update every 72 hours. Each button operation counts as an interaction
- When the status of an alert changes, Flashduty will request an update to the card content
- When the alert status changes frequently, it may exceed the update limit, preventing the card from updating in real time. In such cases, you can click the refresh button to get one opportunity to update the card status

6. **How to open a click card message on the Mac desktop using the `System Default Browser`?**

- By default, the Mac desktop uses the in-app browser to open links
- You can try using the shortcut keys `ctrl` + `command` + `shift` + `d` to enable debugging mode, then select `Debug - Browser, webView Related - Open Web Page with System Browser` to change the link opening mode. The same shortcut keys can be used to turn off debugging mode and maintain the settings.

7. **Fault notification failed, prompt `未开通企微许可` ?**

- Contact Flashduty customer service or dedicated support to purchase and activate the license for you
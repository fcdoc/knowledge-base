---
brief: By integrating a self-built Feishu application, the ability to receive and respond to alerts within the Feishu platform is achieved
---

# Feishu Lark Integration

---

By integrating a self-built Feishu application, the ability to receive and respond to alerts within the Feishu platform is achieved.

## 1. Create a Feishu Application
---

### 1. Create a Self-Built Application

Visit [Feishu Developer Backend](https://open.feishu.cn/app) to create a self-built application within the enterprise. (For details, refer to the Feishu Development Documentation - [Creating an Enterprise Self-Built Application](https://open.feishu.cn/document/uYjL24iN/uMTMuMTMuMTM/development-guide/step1#132c1aac))

<img src="https://fcdoc.github.io/img/YyRTmgwY7nfhtcBdhnk4SVQW2v1Km27PNshoKZia7Yw.avif" alt="drawing" width="400"/>

The application icon can use the [Flashduty Official Icon](https://download.flashcat.cloud/flashcat_logo_circular.png).

### 2. Copy Credential Information

Go to the **Credentials and Basic Information** page and copy the `App ID` and `App Secret` for later use.

<img src="https://fcdoc.github.io/img/z3fOjBTA6HK4fTigqDUyb3oXjWI1itwz_5SeS96zDQk.avif" alt="drawing" width="800"/>

### 3. Copy the Event Callback Token Information

Go to the **Development Configuration - Events and Callbacks - Encryption Policy** page and copy the `Encrypt Key` (recommended for enhanced security) and `Verification Token` for backup.

<img src="https://fcdoc.github.io/img/pCfnVRk1nPAjLQU-ReDmX-ab7TfqtNRZnGdOKkiVYyY.avif" alt="drawing" width="800"/>

## 2. Add Feishu Integration
---

Return to the Flashduty **Integration Center** page, select **Instant Messaging > Feishu**, fill in the `Name` and the previously copied `App ID`, `App Secret`, `Verification Token`, and `Encrypt Key` in the form, then click Save to create.

<img src="https://fcdoc.github.io/img/fwuJqwfdijVN9SdQVmADOOZuuqEZBUa_9w-vaOZn4V4.avif" alt="drawing" width="800"/>

After creation, the newly added Feishu integration will appear in the list. Click on the name to enter the details, where you will find the **Web Configuration** address, **Redirect URL**, and **Message Card Request URL** which will be used in the subsequent steps.

<img src="https://fcdoc.github.io/img/F_i05Wj-itHzUr_HJJGEASuvJImXIDN_15RDfqWPeIQ.avif" alt="drawing" width="800"/>

## 3. Configure the Feishu Application
---

### 1. Enable and Configure Application Capabilities

1). Return to the Feishu Developer Backend, enter the Feishu application you just created, navigate to the **Add Application Capabilities - Add by Capability** page, and simultaneously enable the **Web Application** and **Robot** capabilities.

<img src="https://fcdoc.github.io/img/ir5Q7y1bQ4oCNy2Z2Un_tHuh8d00NAsw4YZKzKd4dug.avif" alt="drawing" width="800"/>

2). Go to the **Web Application** page and configure the `Desktop Home Page` and `Mobile Home Page` with the **Web Configuration** address from the integration details.

<img src="https://fcdoc.github.io/img/PuSpN5HtcTATlbeBd_CLiTgQ06xUuxsDzJ6ubNpqIdI.avif" alt="drawing" width="800"/>

(For more details, refer to the Feishu Development Documentation - [Configuring the Application Home Page Address](https://open.feishu.cn/document/uYjL24iN/uMTMuMTMuMTM/development-guide/step1#8366b844))

3). Navigate to the **Event Callback - Callback Configuration** page, configure the `Message Card Request URL` (the content should be the **Message Card Request URL** as specified in the integration details) and set up the callback.

<img src="https://fcdoc.github.io/img/EmV7D9wKA1BibAIiHRT8EcZ05PyiUpoJ5RDH0LPTuCc.avif" alt="drawing" width="800"/>
<img src="https://fcdoc.github.io/img/SiHDL4kj75gd6l529pmDkUOOtfGm8O8J_yuG2WruQuM.avif" alt="drawing" width="800"/>

### 2. Add a Redirect URL to the Feishu Application

Access the **Security Settings** page, and configure the `Redirect URL`. The content should be the **Redirect URL** as provided in the integration details.

<img src="https://fcdoc.github.io/img/JJvHuqySxpuNGYcLyuyTFPRC_p0BgdowNwt7sSyP2sg.avif" alt="drawing" width="800"/>

(For more details, refer to the Feishu Development Documentation - [Configuring Redirect URL](https://open.feishu.cn/document/uYjL24iN/uYjN3QjL2YzN04iN2cDN?lang=zh-CN#c863e533))

### 3. Apply for Application Permissions

Enter the **Permission Management** page and apply for the `im:chat` and `im:message` permissions. These two permissions will allow the current application to access information about the groups it belongs to and to send messages to groups or individuals.

<img src="https://fcdoc.github.io/img/t03fu8HgE8UB5ahuhxHv4Yej7bSMSCjpTeI1V6YJRI4.avif" alt="drawing" width="800"/>

## 4. Application Release and Usage
---

After completing the above steps, proceed with the application release and usage. The application can be used after it is reviewed by the administrator.
Note: The **Available Scope** requires special configuration, and it is recommended to set it to **All Employees**.

<img src="https://fcdoc.github.io/img/5kFssMPTFMc3DOqNxf2RJkE_Mt2XPr9XiMBHioEeQNU.avif" alt="drawing" width="800"/>

For more details, refer to the Feishu Development Documentation - [Application Release and Usage](https://open.feishu.cn/document/uYjL24iN/uMTMuMTMuMTM/development-guide/step-4).

After the application is released, you can use the mobile /PC to access the application. You need to log in and associate your (Feishu <->Flashduty ) account for your first visit. You can use it without logging in later.

1. Mobile: On the mobile side, access the application through Feishu > Workbench > search for the application name > open the application to use the web application.
2. PC: On the desktop (PC) side, access the application through Feishu > Workbench > search for the application name > open the application to use the web application.

## 5. Frequently Asked Questions
---

1. **Messages cannot be delivered to individuals**, and the operation record indicates `Unassociated Application`?

- Go to Feishu > Workbench > search for the application name > open the application, complete a login, and associate the (Feishu <-> Flashduty) account so that the system can obtain the user identity for message delivery

2. **Message card buttons are not clickable or result in errors**?

- Ensure that the account has been associated. Go to Feishu > Workbench > search for the application name > open the application, complete a login, and associate the (Feishu <-> Flashduty) account. If you have already logged in, try clicking the menu in the upper right corner, switch accounts, and log in again to bind the account
- Ensure that you have purchased an adequate number of licenses. The usage status of licenses can be viewed in the console > Expense Center

2. **The Feishu group chat list is empty in the distribution strategy**?

- Go to Feishu, select a group chat session, and add the created Flashduty robot as shown in the figure below:
- Return to the distribution strategy configuration page, refresh, and then re-select the group chat list

<img alt="drawing" width="800" src="https://fcdoc.github.io/img/tWCiY7hewPCCai_aENHshvt2Beaa3zMSxH8N6ZiLzAw.avif" />
<img src="https://fcdoc.github.io/img/UWIKy3ycnjzP0bMylXS_6NG-4G2-SSfq54kIjC-hruQ.avif" alt="drawing" width="800"/>
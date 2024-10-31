---
brief: You can customize the account settings and configure personal notification methods
---

# Personal Preference Settings

## Account Center
- Access the Account Center: Hover over the user icon in the top right corner and select Account Settings.
- Display personalized account settings and options to configure personal contact information, account password, APP Key, and notification methods.
- You can configure the following items in your account settings:
- Basic Information: Such as nickname, email, password, etc.
- APP Key: Create or delete an APP key.
- Notification Method: Configure according to personal preferences.

![](https://fcdoc.github.io/img/zh/flashduty/conf/preference/1.avif)

## Account Information
- Account identities are divided into two types: main account and member account.
- Account nickname supports both Chinese and English, primarily used for display purposes.
- Verification code is required when changing the email or mobile phone number.
- Regions currently supported by mobile phone numbers include Mainland China, the United States, Canada, Indonesia, Germany, Malaysia, Australia, Singapore, Thailand, Russia, South Korea, Saudi Arabia, Vietnam, and Japan.

## APP key
- APP key is crucial credential information for API requests.
- Each account can create up to 5 APP keys. Deleting a key releases the quota; please distribute and use them sensibly.
- The APP key value is only displayed upon successful creation; please keep it secure.

> [!WARN]
> - Each APP key possesses full API operation permissions. Please ensure the security of the created App key to prevent leakage.
> - When deleting an APP key, ensure no business is using it. Once deleted, any business that previously used the key will become ineffective.

## Notification Methods
- Different notification methods can be set for various alert levels.
- Notifications will be sent according to the individual's configuration only **if the incident is directly assigned to a person, or assigned to a person via a dispatch strategy with private chat enabled and personal preferences adhered to**.
- When configuring IM applications like DingTalk, WeChat, or Feishu, you must first associate the application to receive notifications.

## FAQs

|+| I set my preferred notification method, but why wasn't the notification triggered?

    The way Flashduty assigns personnel and sends notifications is solely reliant on the settings of the dispatch strategy. This implies that if no dispatch strategy is set, no notifications will be sent when an incident is triggered.

    Moreover, the single chat notification channel of the assignment strategy supports two settings: "Follow personal preferences" and "Follow unified settings." Notifications are personalized based on your settings only under the "Follow personal preferences" option. If you choose "Follow unified settings," everyone will receive notifications according to this setting, rather than their individual preferences.

    Go to Collaboration Space Details => Assignment Policy to review your specific settings.
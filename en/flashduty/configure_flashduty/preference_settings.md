---
brief: You can customize the account settings and configure personal notification methods
---

# Personal Preference Settings

---

## Account Center
---
- Access the Account Center: Hover over the user icon in the top right corner and select Account Settings.
- Display personalized account settings and options to configure personal contact information, account password, APP Key, and notification methods.
- You can configure the following items in your account settings:
- Basic Information: Such as nickname, email, password, etc.
- APP Key: Create or delete an APP key.
- Notification Method: Configure according to personal preferences.

![](https://fcdoc.github.io/img/CqPJGldQsfI5kyyYGAFno50wbTJB4VV0Wz4Hb8IqXpc.avif)

## Account Information
---
- Account identities are divided into two types: main account and member account.
- Account nickname supports both Chinese and English, primarily used for display purposes.
- Verification code is required when changing the email or mobile phone number.
- Regions currently supported by mobile phone numbers include Mainland China, the United States, Canada, Indonesia, Germany, Malaysia, Australia, Singapore, Thailand, Russia, South Korea, Saudi Arabia, Vietnam, and Japan.

## APP key
---
- APP key is crucial credential information for API requests.
- Each account can create up to 5 APP keys. Deleting a key releases the quota; please distribute and use them sensibly.
- The APP key value is only displayed upon successful creation; please keep it secure.

::: caution

- Each APP key possesses full API operation permissions. Please ensure the security of the created App key to prevent leakage.
- When deleting an APP key, ensure no business is using it. Once deleted, any business that previously used the key will become ineffective.

:::

## Notification Methods
---
- Different notification methods can be set for different alert levels.
- Notifications will be sent according to personal configurations only **when the fault is directly assigned to an individual, or assigned to an individual via a dispatch policy with single chat enabled and personal preferences set**.
- When configuring IM applications like DingTalk, WeChat, or Feishu, you must first associate the application to receive notifications.


## FAQs

<details><summary>I have set my personal preference notification method, why is the notification not triggered?</summary> Flashduty How to dispatch people and notify them only depends on the settings of the dispatch policy. This means that if you do not set a dispatch policy, there will be no notification when a failure occurs.<p> Secondly, the dispatch strategy single chat notification channel supports two settings, one is "follow personal preferences" and the other is "follow unified settings". Only in the "Follow personal preferences" setting, notifications will be personalized according to your settings. If you select "Follow unified settings", everyone will be notified according to this setting, rather than each person's preference.</p><p> Go to Collaboration Space Details = > Policy to view your specific settings.</p></details>
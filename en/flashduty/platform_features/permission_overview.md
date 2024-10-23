---
brief: Understand the difference between feature permissions and data permissions
---

# Permissions, Roles

---

Flashduty employs two types of permissions: functional permissions and data permissions, which are utilized in conjunction across different functional scenarios.

:::caution
You must possess both functional and data permissions to manipulate certain data objects.
:::

## Function Permissions
---
:::tip
Function permissions, also known as operational permissions, determine which system features or operations a user can access.
:::

Flashduty **manages functional permissions based on (RBAC) roles**. The system comes with several predefined roles (and you can also create custom roles):

- **Account.Admin**: Account administrator, with full operational rights except for modifying entity information, capable of assisting with the daily management of the entity account.
- **Tech.Admin**: Technical administrator, with access control, operational auditing, and all functional permissions not listed in the table below.
- **Fin.Admin**: Financial administrator, with the authority to place orders in the fee center and all functional permissions not listed in the table below.

The following table lists the functional permissions that can currently be controlled:

| Permission Point | Account.Admin | Teah.Admin | Fin.Admin |
| ------------ | :--------: | :--------:  | :--------: |
| **API Key Management**    | ✔️       |            |            |
| **Operation Audit Read**     | ✔️ | ✔️ |  |
| **Monitoring System Event Management**    | ✔️ |  |  |
| **Custom Field Management**    | ✔️ | ✔️ |  |
| **Access Control**<br>- Member Management<br>- Role Management<br>- Single Sign-On Management     | ✔️ | ✔️ |  |
| **Subscription Management**<br>- Subscription Management<br>- Balance Insufficient Reminder<br>- Change Expiration Policy for Version<br>- Enable Monitoring Management Function    | ✔️ |  | ✔️ |
| **All Other Features** | ✔️ | ✔️ | ✔️ |


:::caution
Note that **all other functions** not listed in the table *(such as managing collaboration spaces)* are permissions that all users have by default (even if a user is not assigned a role) and do not require manual control.
:::

## Data Permissions
---
:::tip
Data permissions, also known as access permissions, control the scope of data that a user can access or view.
:::

Flashduty **controls data permissions based on teams** and applies to the following scenarios:

- **Team Management**: Creators, main accounts, and team members can modify team information and manage team members.
- **Collaboration Space**: Creators, main accounts, and team members responsible for the collaboration space can modify the space's basic information, noise reduction settings, and assignment policies.
- **Duty Management**: Creators, main accounts, and team members responsible for duty can modify the basic information and rotation rules of the duty.
- **Template Management**: Creators, main accounts, and team members responsible for templates can modify the basic information and channel template configurations.
- **Service Calendar**: Creators, main accounts, and team members responsible for the service calendar can modify the calendar's basic information and holiday settings.

If you lack data permissions for a corresponding resource, the system will provide the following prompt:


![](https://fcdoc.github.io/img/dCWMN_bb4xQtkzwoFjba1jqNWm_4J0RjzhIubwbGtCw.avif)

## FAQs
---

<details><summary>I am already an account administrator, why can’t I modify the collaboration space settings?</summary> Because the collaboration space applies data permissions, you must be the creator, the main account, and one of the responsible team members before you can modify the information of the corresponding collaboration space.<p> If the space does not have a responsible team, you can ask the space creator or owner to set up a team for the collaboration space and invite you to join. Then you will have management rights for the space.</p></details>

<details><summary>Why can a member with no role handle failures?</summary> Because sometimes you will encounter a failure that requires the cooperation of multiple teams to deal with it. Therefore, Flashduty has no authority control over handling alarms. All personnel on the platform can view all alarms under the account and handle them.<p> However, we do not rule out the possibility that we will implement access control for handling faults in the future.</p></details>
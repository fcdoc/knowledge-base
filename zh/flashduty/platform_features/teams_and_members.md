---
brief: 团队的操作和成员的管理
---

# 团队和成员

---

## 团队介绍
---
团队是成员的集合，也可以理解为是一个组，可以将不同的职责或项目的成员归纳到一个团队里，用于管理**协作空间、分派通知、值班安排以及服务日历**等场景。

## 团队管理
---

### 团队查询

- 默认展示全部团队，可以选择只有‘我’的团队。
- 支持按团队名称模糊搜索，不支持按成员搜索。

### 创建与编辑

- 团队数量限制： 目前无限制。
- 团队中可添加用户数量： 目前无限制。
- 同一个成员可以属于多个团队。
- 可以对已创建的团队的名称、描述、成员可以进行修改。
- 修改团队成员时，请确保该成员确实属于该团队。

### 删除团队

> [!WARN]
> 删除前请先确认是否有协作空间、分派策略等其他地方与该团队有关联。
> 删除后其他有关联的路径将即刻失效且不可恢复，请谨慎操作。

## 成员管理
---

### 邀请方式

- 控制台仅支持邮件邀请，用户昵称默认为邮箱前缀，可在激活后进入账户设置页面修改
- 您可以通过 [Open API](https://developer.flashcat.cloud/api-110655699) 进行邀请，支持手机号邀请
- 系统会向被邀请的同事发送短信或邮件，每天邀请数量上限为 200 人，单次邀请至多 10 人
- 除了以上方式，您也可以联系组织管理员配置单点登录，新成员登录自动创建账号
- 向对方发生邀请后，对方登录即可激活账号，未激活之前账号无法接收告警相关通知

### 邀请成员

- 邀请成员时，可以直接赋予该成员一个角色；[了解权限设计](https://docs.flashcat.cloud/zh/flashduty/permission-overview)。
- 邮箱模式邀请时，被邀请成员会收到相应的通知邮件并可以在邮件中直接跳转登陆验证。
- 短信模式邀请时，被邀请成员会收到相应的短信提醒。
- 被邀请成员可通过邀请时的验证类型进行登录，如邮箱或手机号。

### 变更角色

- 账户管理员可以变更成员的角色。
- 成员自己可以向下变更自己的角色，不能向上变更。

### 删除成员
> [!WARN]
> 成员一经删除，不可恢复，请谨慎操作。
> 成员被删除后，该成员的数据并不会被删除。

## 常见问题
---
<details>
<summary>邮件邀请成员未收到验证邮件？</summary>
请确认邮箱地址填写是否正确、邮箱垃圾收件箱是否有收到以及邮箱未设置拦截策略，如果都正常，可以尝试让邀请人重新下发邀请，或联系官方技术支持人员。
</details>


<details>
<summary>短信邀请成员未收到验证短信？</summary>
请确认手机号填写是否正确以及手机未设置拦截策略，如果都正常，可以尝试让邀请人重新下发邀请，或联系官方技术支持人员。
</details>

<details>
<summary>同一成员是否可以属于多个主体租户？</summary>
可以，比如成员A属于多个主体，那么成员A在登录时会让其选择要登录的主体。
</details>

<details>
<summary>同一账户主体下的成员手机号或邮箱是否可以重复？</summary>
不可以重复，手机号或邮箱需要保证唯一。
</details>

<details>
<summary>管理员为什么不能修改其他成员邮箱或手机号？</summary>
手机号或邮箱是故障通知和登录控制台的重要渠道，为了防止在本人不知晓的情况下被修改这些信息，从而导致不可预期的事故发生，所以只能本人修改且修改时要验证。
</details>
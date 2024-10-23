---
brief: Tutorial: Configuring Single Sign-On in Authing
---

# Authing Single Sign-On Configuration and SSO Login Setup

---


Quick Overview
---
[Authing](https://www.authing.cn/) is a provider offering identity recognition and access control management. Through the Authing platform, you can log in to the FlashDuty management console using OIDC, SAML 2.0, or CAS protocols

## Preparation
---
### 1. Login or Register with Authing
- Newly registered users need to first create a user pool; follow the prompts to do so
### 2. Create an Application
- Select a Standard Web Application
- Enter the Application Name
- Enter the Authentication Address (the address to redirect to during SSO login)

![](https://fcdoc.github.io/img/rFaOo-DGswfKSPSbWGS-FebSKSdFDAaJo3_ZHWgK_wQ.avif)

### 3. Record Relevant Information

![](https://fcdoc.github.io/img/fGGU2F0PnKeRglPMvHaQN3TN_CfapC7bCv3_Vy8BfOU.avif)

|Field|Description|
|---|---|
|App ID|FlashDuty Corresponding Client ID|
|APP Secret|FlashDuty Corresponding Client Secret|
|Issuer|FlashDuty Corresponding Issuer|
|Authentication Address|Redirect Address for SSO Login|



## Begin Configuring the OIDC Protocol
---
### 1. Open the [FlashDuty](console.flashcat.cloud) Console and Enable SSO Configuration

![](https://fcdoc.github.io/img/KZ0bU4AgfrxBFrbiDy_aMlMw0OAovw8d5iX6eDbvV4s.avif)

### 2. Copy the Relevant Information to the Corresponding Fields

#### 2.1 Copy the Authing Application's Relevant Information to the Corresponding Fields
![](https://fcdoc.github.io/img/EnWuL87KZb8WkGRFWWeCbuL71AKXlskG4mXl5pa5lIo.avif)

#### 2.2 Copy the Redirect URL Domain to Authing's Login Callback URL

![](https://fcdoc.github.io/img/AeIek4wYqa6GcRPqBYxP7FumgpZzgc1LD_x0ZqYbf6s.avif)

### 3. Modify Authing Configuration

#### 3.1 As shown in the diagram, change the id_token Signature Algorithm to RS256

![](https://fcdoc.github.io/img/wcUYTZJtdrz7pJK07m203p9XGGmKdgmHGB1t5MGH8s0.avif)

#### 3.2 Configure Login Control

![](https://fcdoc.github.io/img/Q99TWiFqHE9MZVkQS7Bq3SO0hoOPIWpNBff8OvZtCxY.avif)

#### 3.3 Change Permissions

![](https://fcdoc.github.io/img/xz9eG4P2Cx6LhdzB5gqUU0FHtO7wahe-nEhelpSCRW0.avif)

### 4. Create a User and Test Login

#### 4.1 Create a User in Authing

:::tip
FlashDuty only supports user email association, so create users using email addresses
:::


![](https://fcdoc.github.io/img/wJC3EQjcBkksln8c1Yetxw-EqkMQpM7O-3nGITx7604.avif)

#### 4.2 Test Login Using the SSO Address

![](https://fcdoc.github.io/img/z9i-MqlbSY5iUstNJ8ApL8MPmY9otvMtB1aUxVMSSaY.avif)

:::tip
**Access console.flashcat.cloud via SSO Login**
:::

#### 4.3 The SSO Address Redirects to the Login Page

![](https://fcdoc.github.io/img/te7WxbegivYwwq0vTcN4i_v8Z8eO5TctotvNNbMQhbE.avif)

:::tip
Use the user created in Authing to log in to the FlashDuty console
:::


## Begin Configuring the SAML 2.0 Protocol
---

:::tip
You can create a new application or modify an existing one. Here, we demonstrate by modifying an application
:::

### 1. Protocol Configuration

#### 1.1 Select SAML 2.0

![](https://fcdoc.github.io/img/FLJsSEpdqdy0U4HsEClrmG0ynti-TiKoxv7eyEsiNs4.avif)

#### 1.2 Change FlashDuty's SSO Protocol to SAML and Copy the ACS Address

![](https://fcdoc.github.io/img/QrzVo2DKOIUF4ueiMMN5d1-svypFEEiB774hYJ57SiI.avif)

#### 1.3 After Copying the ACS Address to the Authing Application, Click Save and Change the Protocol Type

![](https://fcdoc.github.io/img/WEk3joVymAUwHiKpW8_6FEBoitqmF5TDKH_h4sCGIKw.avif)

### 2. Configure in FlashDuty

#### 2.1 Download the Metadata, Click the Link, and Save Locally

![](https://fcdoc.github.io/img/heB07DtLDMuL9U9fpAKCl7VXrRrWY4uNNgDT_Xiwfj4.avif)

#### 2.2 Upload to FlashDuty's SSO Configuration and Save

![](https://fcdoc.github.io/img/5p4rgQ127lvqz9vVtvR1gNjjTys9uMmDvax0iJzn8BI.avif)

#### 2.3 Test Login (Refer to the OIDC Protocol Login)
![](https://fcdoc.github.io/img/te7WxbegivYwwq0vTcN4i_v8Z8eO5TctotvNNbMQhbE.avif)

:::tip
The above are the complete configurations for both methods. The configurations on the two platforms overlap, so please be cautious not to overlook any critical information. If you encounter any issues during the configuration process, you can contact FlashDuty technical support for assistance
:::


## Begin Configuring the CAS Protocol
---
### 1. Open the [FlashDuty](console.flashcat.cloud) Console and Enable SSO Configuration

![](https://fcdoc.github.io/img/KZ0bU4AgfrxBFrbiDy_aMlMw0OAovw8d5iX6eDbvV4s.avif)

### 2. Copy the Relevant Information to the Corresponding Fields

#### 2.1 Copy the Authing Application's Relevant Information to the Corresponding Fields
![](https://fcdoc.github.io/img/_zRk5lRlLaIJ2pR5Gn3G_AJRG1l1a5Ge9zlaZXWdArQ.avif)

#### 2.2 Copy the Redirect URL to Authing's Login Callback URL

![](https://fcdoc.github.io/img/y33ADY93aySH--oBiwzD_DzD6lRm8J_E-UkVrWXxliQ.avif)

### 3. Modify Authing Configuration

#### 3.1 Configure as Shown

![](https://fcdoc.github.io/img/_e5BujT71dx4Lh5uiaNcvgIxEL493d5n2rZXWfnEB78.avif)

#### 3.2 Configure Login Control

![](https://fcdoc.github.io/img/Q99TWiFqHE9MZVkQS7Bq3SO0hoOPIWpNBff8OvZtCxY.avif)

#### 3.3 Change Permissions

![](https://fcdoc.github.io/img/xz9eG4P2Cx6LhdzB5gqUU0FHtO7wahe-nEhelpSCRW0.avif)

### 4. Create a User and Test Login

#### 4.1 Create a User in Authing

:::tip
FlashDuty only supports user email association, so create users using email addresses
:::


![](https://fcdoc.github.io/img/wJC3EQjcBkksln8c1Yetxw-EqkMQpM7O-3nGITx7604.avif)

#### 4.2 Test Login Using the SSO Address

![](https://fcdoc.github.io/img/dII3AxQNII7gMXCoB0qo_PNjiVrH1km-IBFJTjlGKxY.avif)


#### 4.3 The SSO Address Redirects to the Login Page

![](https://fcdoc.github.io/img/te7WxbegivYwwq0vTcN4i_v8Z8eO5TctotvNNbMQhbE.avif)

:::tip
Use the user created in Authing to log in to the FlashDuty console
:::
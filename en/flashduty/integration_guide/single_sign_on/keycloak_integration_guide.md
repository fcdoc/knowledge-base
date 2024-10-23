---
brief: Configuring Single Sign-On Tutorial in Keycloak
---

# Keycloak Single Sign-On Configuration and SSO Login Setup

---

## Quick Overview
---

Keycloak is an open-source identity and access management solution that offers a comprehensive suite of tools and features to assist developers in swiftly implementing secure user authentication and authorization mechanisms, while also streamlining the identity and access management process for applications

:::tip

This article does not cover the deployment or explanation of Keycloak-related content. For more information, please refer to [the official documentation](https://www.keycloak.org/)

:::

## Based on the SAML2.0 Protocol
---
### 1. Log in to the FlashDuty Console
#### 1.1 Obtain the ACS Address from FlashDuty (to be used in step 2)
#### 1.2 Path: Access Control => Single Sign-On => Settings => SAML2.0 Protocol => Flashcat Service Provider Information => Assertion Consumer Service URL

![](https://fcdoc.github.io/img/pkIrovp8kA32UAW82e8aqEsjkfDKFn6xy-n3V8li-tE.avif)

### 2. Log in to the Keycloak Console and Create a New Client
#### 2.1 Path: Clients => Create Client
#### 2.2 Client Type: Select SAML Protocol
#### 2.3 Client ID: Enter flashcat.cloud (fixed value, cannot be changed)
#### 2.4 Valid Redirect URIs: Enter the ACS address obtained from FlashDuty

![](https://fcdoc.github.io/img/MfLl4ovdUShiYNm12SAH0u29lERlAacWYOM9YPEj3gE.avif)
![](https://fcdoc.github.io/img/1qZPWJilLeqTWb1TFnVAiQf3Pe7yerpVtPyMpOUAueA.avif)

### 3. Configure Client-Related Information

#### 3.1 Change Name ID Format to Email Type

![](https://fcdoc.github.io/img/ZEvRR_z-YOH66aOTsmV6Zz3Izeh5PTaW7tAixV2ZCJY.avif)

#### 3.2 Set Client Signature Required to Off

![](https://fcdoc.github.io/img/PYpH626xaO7ZfOx6O9_UcGu0gZGRSJU2E61bNhM2fug.avif)


#### 3.3 Create Three Field Types: email/phone/username
:::tip
Before creating, you need to delete the user associated with the previous OpenID Connect protocol and set the new one as Default after completion
:::
![](https://fcdoc.github.io/img/ZePSBlsiaCFbpDSp0YLNTx176uqLjnfnCxquFITbSpQ.avif)
![](https://fcdoc.github.io/img/oB7-tH-qpVSj-NNNkXBW_aFkWOhdqhnkvbopr83k98w.avif)

#### 3.4 Add the Created Users to the Client
![](https://fcdoc.github.io/img/OWCPp0soyAyMh-eZBaokxk-cs9_xgPruEL9VfxvAEF0.avif)
![](https://fcdoc.github.io/img/mkZNfR9v63jjkT9vZ480v2-wHCRYCg8OPGILwJBrQH4.avif)


#### 3.5 Configure Email/Phone/Username Mappers (Using Email as an Example; Configure Others Following These Steps)
![](https://fcdoc.github.io/img/pBg2KT_RubAPb4vIIEfNbKYMJCb-ome2Kw4xhSSUXEI.avif)
![](https://fcdoc.github.io/img/SSSiSST_PmkcbEKioDY6PcOvtAhuDEOTZ9lFlSvV95w.avif)
![](https://fcdoc.github.io/img/XDIIw8olppBjfOzge_U4bJ528AwuuLYx1Go8qnUY_Ts.avif)

### 4. Download the XML File
:::tip

The downloaded file is a compressed package. After extracting it locally, you will find two XML files, but only the idp-metadata.xml file is needed

:::
#### 4.1 Download to Local in Client > Action
![](https://fcdoc.github.io/img/iNbRXI4HmjjefWj5OIWXuAxA9yjncL7NTmnQHUw_UB0.avif)

#### 4.2 Upload the XML File to FlashDuty's Single Sign-On Configuration
![](https://fcdoc.github.io/img/idsjJegDi2gpoyDZmawJGYL-iccbjRzXo_gzM4JwDro.avif)


### 5. Create a User in Keycloak and Test Login

#### 5.1 Create a User (Make Sure to Bind an Email Address)
![](https://fcdoc.github.io/img/_2tbJ0_OLLyERNxooaRGWXL0JnsX9W6cEisxR0cEnQ8.avif)

#### 5.2 Test Login
- Access console.flashcat.cloud, select SSO Login, and fill in the login domain prefix as specified in the single sign-on configuration

![](https://fcdoc.github.io/img/gDmsph7lG5N0JV3i5NvyCWDBgbpKe3OMKgP9IOskT70.avif)

## Based on the OIDC Protocol
---
### 1. Log in to the FlashDuty Platform
- Obtain the Redirect URL from FlashDuty (to be used in step 2)
- Path: **Access Control => Single Sign-On => Settings => OIDC Protocol => Flashcat Service Provider Information => Redirect URL**
![](https://fcdoc.github.io/img/-89ER30ZP-j4UDDbMraGeT4R351z2UsSUiMQD3yLSTY.avif)

### 2. Log in to the Keycloak Console and Create a New Client

- Client Type: Select OIDC Protocol
- Client ID: No Special Requirements
- Client Authentication: Keep Enabled
- Valid Redirect URIs: Enter the Redirect URL Address Obtained in Step 1

![](https://fcdoc.github.io/img/7wIOsG6oJ8zfGw0QSqiLwrGsSWeRFS9dgxhp0UTL2jY.avif)
![](https://fcdoc.github.io/img/X_en7d1IG7mMqbCR7WNBsflGLodwhSuFcHGNTdHQrfo.avif)
![](https://fcdoc.github.io/img/dR55AMDCD2lBGunpaMHPPJfZuTykNpyHTgj8sF682Mw.avif)

### 3. Obtain Client-Related Information

- Client ID: The ID Filled in When Creating the Client
- Client Secret: Visible in the **Client Details > Credentials** Tab
- Issuer: Found in **Realm Settings > Endpoints > OpenID Endpoint Configuration**

![](https://fcdoc.github.io/img/NP_LOrJitxQoWR8v3qRRc_m9Vi2RWsR8LJw-3OlNOP4.avif)
![](https://fcdoc.github.io/img/_iEUT3fJeOYyvMLTJ7_LvSSowT9xZ5SkLW2kcxq1CUM.avif)

### 4. FlashDuty Single Sign-On Configuration Format

![](https://fcdoc.github.io/img/NGsXfo0hUCLw7RiK_M0iiwxNOx4CaBoZBHGzXOkVWLw.avif)

:::tip
After completing the OIDC configuration, refer to the "Configuring Single Sign-On" section for login testing

:::
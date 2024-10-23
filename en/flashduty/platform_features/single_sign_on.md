---
brief: Single sign-on allows you to easily integrate into a variety of different applications and platforms, allowing you to log in once and access multiple associated applications and services
---

# Configure Single Sign-On

---

FlashDuty currently offers single sign-on (SSO) support for SAML2.0, OIDC, CAS, and LDAP (available only in the private version), making it effortless to integrate with various applications and platforms. These functionalities enable rapid sharing of identity information across platforms. Users need to authenticate only once on a single platform to access multiple related applications and services, eliminating the need for individual authentication for each app. This not only enhances work efficiency and user experience but also streamlines the login process and fortifies security.

## Configure SAML Protocol
---
Configuration path: **Access Control => Single Sign-On => Enable => Settings => Select SAML2.0 Protocol Type**

|Field|Description|
|----|----|
|Protocol Type|Select SAML2.0|
|Metadata Document|XML document obtained from the identity provider|
|Field Mapping|FlashDuty extracts user email, username, and mobile information from the identity provider through field mapping.|
|Login Domain|A crucial identifier, unique globally|
|Create Account on Login|Enabled by default. **If disabled, members must be invited to join before they can log in.**|
|Flashcat Service Provider Information|**Service Provider Metadata:**<br>**Assertion Consumer Service URL:** The assertion address used for SSO when called by the identity provider|

## Configure OIDC Protocol
---
Configuration path: **Access Control => Single Sign-On => Enable => Settings => Select OIDC Protocol Type**

|Field|Description|
|----|----|
|Protocol Type|Select OIDC Protocol|
|Issuer|Retrieve Issuer from the identity provider, a case-sensitive URL without query parameters|
|Client ID|Client ID obtained from the identity provider|
|Client Secret|Client Secret obtained from the identity service provider|
|Field Mapping|FlashDuty extracts user email, username, and mobile information from the identity provider through field mapping.|
|Login Domain|A crucial identifier, unique globally|
|Create Account on Login|Enabled by default. **If disabled, members must be invited to join before they can log in.**|
|Flashcat Service Provider Information|**Redirect URL:** The callback URL for the identity provider to redirect to Kuaimao Nebula.<br>**Supported Signature Algorithms:** RS256, RS384, RS512, ES256, ES384, ES512, PS256, PS384, PS512 (HS256 not supported).<br>**Requested Scope:** openid, email, phone |

## Configure CAS Protocol
---
Configuration path: **Access Control => Single Sign-On => Enable => Settings => Select CAS Protocol Type**

|Field|Description|
|----|----|
|Protocol Type|Select CAS Protocol|
|CAS Address|CAS service address obtained from the identity provider|
|CAS Login Path|CAS Login Path|
|Field Mapping|FlashDuty extracts user email, username, and mobile information from the identity provider through field mapping.|
|Login Domain|A crucial identifier, unique globally|
|Create Account on Login|Enabled by default. **If disabled, members must be invited to join before they can log in.**|
|Flashcat Service Provider Information|**Redirect URL:** The callback URL for the identity provider to redirect to Kuaimao Nebula


## Configure LDAP Protocol
---
:::tip

LDAP Single sign-on, only `私有化版本` supported

:::

Configuration path: **Access Control => Single Sign-On => Enable => Settings => Select LDAP Protocol Type**

|Field|Description|
|----|----|
|Protocol Type|Select LDAP Protocol|
|LDAP Link|LDAP service address, e.g., ldap://10.10.10.10:389 |
|BIND DN|Username for connecting to LDAP, used for testing connection results and searching for users or user groups, e.g., cn=admin,dc=flashduty,dc=com |
|BIND DN Password|Password for connecting to LDAP, stored encrypted in the database.|
|TLS|Skip Verify on TLS Login|
|StartTLS|Enable StartTLS|
|User DN|Define the directory to start searching for users, e.g., ou=people,dc=flashduty,dc=com|
|Authentication Filtering|This condition, combined with Bind DN and the corresponding password, is used for user search to retrieve the user's DN information and perform Ldap authentication. Custom filter expressions are supported in the basic form: (&&(mail=%s)). Note: Opening and closing brackets are required.|
|Field Mapping|FlashDuty extracts user email, username, and mobile information from the identity provider through field mapping, with email as a required mapped field|
|Login Domain|A crucial identifier, unique globally|
|Create Account on Login|Enabled by default. **If disabled, members must be invited to join before they can log in.**|

:::tip

Field mapping must be consistent with the identity provider's configuration to avoid exceptions. Specific values should be filled according to the description and can be referenced in the [OpenLDAP Integration Guide](https://docs.flashcat.cloud/zh/flashduty/openldap-integration-guide). If further assistance is needed, contact FlashDuty support.

:::

## Best Practices

Configure SSO Single Sign-On via [Authing Configuration](https://docs.flashcat.cloud/zh/flashduty/introduction) for FlashDuty.
Configure SSO Single Sign-On via [Keycloak Configuration](https://docs.flashcat.cloud/zh/flashduty/introduction) for FlashDuty.
Configure SSO Single Sign-On via [Ldap Configuration](https://docs.flashcat.cloud/zh/flashduty/introduction) for FlashDuty.

## FAQs
---

<details><summary>What is SSO Single Sign-On?</summary>Single sign-on (SSO) is a solution for integrating enterprise systems that unifies user identity authentication, allowing users to access all mutually trusted enterprise application systems with a single login.</details>

<details><summary>What are the features of the SAML2.0 protocol?</summary>The SAML 2.0 protocol is based on XML and uses a secure, standardized declaration method to achieve cross-domain single sign-on and authentication. It supports multiple data exchange bindings, ensuring interoperability and flexibility.</details>

<details><summary>What are the features of the OIDC protocol?</summary>The OIDC protocol, based on OAuth 2.0, provides a standardized and secure identity verification process. It uses JSON Web Tokens to transmit user information, enabling cross-platform single sign-on and identity management.</details>

<details><summary>What are the features of the CAS protocol?</summary>The CAS protocol is a single sign-on (SSO) protocol for web applications. It allows users to use a single authentication process across multiple services, using service tickets (Service Ticket) and authentication tickets (Authentication Ticket) to authenticate services.</details>

<details><summary>What are the features of the LDAP protocol?</summary>The LDAP protocol, developed from the X.500 standard, organizes data in a tree structure, facilitating hierarchical management and rapid data retrieval. It provides a flexible query language (LDAP Search Filter) that allows users to filter and search data based on complex conditions.</details>

<details><summary>Does it support multiple protocol access?</summary>Currently, it does not support multiple protocol access; you can only choose one protocol to integrate.</details>
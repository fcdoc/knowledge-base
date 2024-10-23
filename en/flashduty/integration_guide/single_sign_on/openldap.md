---
brief: Tutorial on Setting Up LDAP with Docker Compose
---

# Guide to Integrating OpenLDAP

---

## Quick Overview
---

LDAP (Lightweight Directory Access Protocol) is a protocol based on the X.500 standard and is used to access and maintain distributed directory services. LDAP enables users and applications to query, browse, and search information stored in the directory, such as user identity information, network resources, etc. LDAP usually runs on the TCP/IP protocol stack, specifically using TCP ports 389 (for unencrypted communication) and 636 (for encrypted communication, using LDAPS).

Core Features of LDAP Include:

Tree Structure: LDAP data is organized in a tree structure known as the DIT (Directory Information Tree), which facilitates hierarchical searching and browsing.

Entries and attributes: Each entry (Entry) in LDAP contains multiple attributes (Attribute). Attributes have types and values. For example, "cn" represents the common name (Common Name), and "mail" represents the email address.

OpenLDAP is an open-source implementation of the Lightweight Directory Access Protocol (LDAP). Due to its open-source nature and flexibility, OpenLDAP has become the preferred LDAP implementation for many enterprises and organizations.


:::tip

This article assumes that the environment already supports Docker and Docker Compose. If not, please install them first.

:::


## Docker Compose Configuration File
---
```
version: '1'

networks:
go-ldap-admin:
driver: bridge

services:
openldap:
image: osixia/openldap:1.5.0
container_name: go-ldap-admin-openldap
hostname: go-ldap-admin-openldap
restart: always
environment:
TZ: Asia/Shanghai
LDAP_ORGANISATION: "flashduty.com"
LDAP_DOMAIN: "flashduty.com"
LDAP_ADMIN_PASSWORD: "password"
volumes:
- ./openldap/ldap/database:/var/lib/ldap
- ./openldap/ldap/config:/etc/ldap/slapd.d
ports:
- 389:389
networks:
- go-ldap-admin

phpldapadmin:
image: osixia/phpldapadmin:0.9.0
container_name: go-ldap-admin-phpldapadmin
hostname: go-ldap-admin-phpldapadmin
restart: always
environment:
TZ: Asia/Shanghai
PHPLDAPADMIN_HTTPS: "false"
PHPLDAPADMIN_LDAP_HOSTS: go-ldap-admin-openldap
ports:
- 8088:80
volumes:
- ./openldap/phpadmin:/var/www/phpldapadmin
depends_on:
- openldap
links:
- openldap:go-ldap-admin-openldap
networks:
- go-ldap-admin

```

:::tip

Replace "password" with the desired password

:::

## Service Startup
---
Save the above configuration file as docker-compose.yml. In the directory containing the configuration file, open a terminal or command prompt and run the following command to start the service:
```
docker-compose up
```

If you wish to run the service in the background, you can add the -d flag:
```
docker-compose up -d
```

View Service Status:
Use the following command to check the service status:
```
docker-compose ps
```

Stop the Service:
To stop the service, use the following command:
```
docker-compose down
```

## Login to OpenLDAP:
---
Access http://ip:8088/ in your browser and log in using the username cn=admin,dc=flashduty,dc=com and the password xxx.

## OpenLDAP Configuration
---
### Add Groups and Users

![](https://fcdoc.github.io/img/1rC8UssQX0Djb1bLj3EWmNjZPG1BX-DLWxY_Q8CSWmA.avif)


:::tip

In the `User Path` (for example, under ou=people, cn=falsh duty) -> `Add new attribute` -> Select `Email`, add the Email attribute for the user, if it does not already exist.

:::

## FlashDuty Integration
With the above OpenLDAP configuration, the FlashDuty integration details are as shown in the figure below:
![](https://fcdoc.github.io/img/lEGCTBal4Z6hl7Vawh6NpyUPvtqeLfHG1c55qXBZQX8.avif)


:::tip

For the meaning and description of the above fields, please refer to [Configuring Single Sign-On](https://docs.flashcat.cloud/zh/flashduty/single-sign-on)

:::
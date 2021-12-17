---
description: >-
  This page describes how to configure SQL Server credentials for use by Census
  and why those permissions are needed.
---

# MySQL

## Required Permissions <a href="#required-permissions" id="required-permissions"></a>

{% hint style="info" %}
These instructions are well tested to connect Census to MySQL. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your database and publishes it to the corresponding objects in your destination systems.

We recommend you create a dedicated `CENSUS` user account with a strong, unique password. Census uses this account to connect to your SQL Server database. In order for the Census connection to work correctly, the `CENSUS` account must have these permissions:

* Read-only access to any tables and views in any schemata that you would like Census to publish to your service destinations.

MySQL permissions are complex and there are many ways to configure access for Census. The script below has been tested with recent MySQL versions and is known to work correctly:

```
-- Create census user the ability to sign in with a password
CREATE USER CENSUS IDENTIFIED BY '<strong, unique password>';

-- GRANT read-only access to which ever schemas you'd like to give access to
GRANT SELECT ON <your schema>.* TO CENSUS;
```

## 💡 Notes <a href="#notes" id="notes"></a>

* If you have multiple schemata that you would like Census to read from, repeat the steps for "\<your schema>" for each of them
* All sync behavior will be **Read Only**, meaning that every sync will be a full sync because we do not currently support tracking sync state in MySQL

## 🚦Allowed IP Addresses <a href="#allowed-ip-addresses" id="allowed-ip-addresses"></a>

Census will always connect to your data warehouse from of these static IP addresses located within AWS:

* 34.216.163.241
* 54.212.243.205

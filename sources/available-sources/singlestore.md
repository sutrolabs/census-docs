---
description: >-
  This page describes how to configure SingleStore credentials for use by Census
  and why those permissions are needed.
---

# SingleStore

## Required Permissions <a href="#required-permissions" id="required-permissions"></a>

{% hint style="info" %}
These instructions are well tested to connect Census to SingleStore. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your database and publishes it to the corresponding objects in your destination systems.

We recommend you create a dedicated `CENSUS` user account with a strong, unique password. Census uses this account to connect to your SingleStore database. In order for the Census connection to work correctly, the `CENSUS` account must have these permissions:

* Read-only access to any tables and views in any schemata that you would like Census to publish to your destinations.

SingleStore permissions are complex and there are many ways to configure access for Census. The script below has been tested with recent SingleStore versions and is known to work correctly:

```
-- Create census user the ability to sign in with a password
CREATE USER CENSUS IDENTIFIED BY '<strong, unique password>';

-- GRANT read-only access to which ever schemas you'd like to give access to
GRANT SELECT ON <your schema>.* TO CENSUS;
```

## Notes

* Census supports SingleStoreDB Cloud and SingleStoreDB v7.1+
* If you have multiple schemata that you would like Census to read from, repeat the steps for "\<your schema>" for each of them

## Advanced Network Configuration

Census can successfully connect to SingleStore instances that are using advanced networking controls including region constraints and IP address allow lists. For more information, see our [regions-and-ip-addresses.md](../basics/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.

## Need help connecting to SingleStore?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

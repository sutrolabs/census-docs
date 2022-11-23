---
description: >-
  This page describes how to configure Azure Synapse credentials for use by
  Census and why those permissions are needed.
---

# Azure Synapse

## Required Permissions

{% hint style="info" %}
These instructions are well tested to connect Census to Azure Synapse. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.&#x20;
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your database and publishes it to the corresponding objects in destination tools.&#x20;

We recommend you create a dedicated `CENSUS` user account with a strong, unique password. Census uses this account to connect to your Azure Synapse database. In order for the Census connection to work correctly, the `CENSUS` account must have these permissions:

* Read-only access to any tables and views in any schemata that you would like Census to publish to your service destinations.

Azure Synapse permissions are complex and there are many ways to configure access for Census. The script below has been tested with recent Azure Synapse versions and is known to work correctly:

```
USE <your database>;
-- Create census user the ability to sign in with a password
CREATE LOGIN CENSUS WITH PASSWORD = '<strong, unique password>';

-- Give the census user the ability to login
CREATE USER CENSUS FOR LOGIN CENSUS;

-- Give the census user the ability to connect to database
GRANT CONNECT TO CENSUS;

-- Give the census user the ability to read all tables
EXEC sp_addrolemember 'db_datareader', CENSUS;

-- Grant census user ability to read schema and data
GRANT SELECT, VIEW DEFINITION ON SCHEMA::<your schema> TO CENSUS;
```

## 💡 Notes

* If you have multiple schemata that you would like Census to read from, repeat the steps for "\<your schema>" for each of them
* All sync behavior will be **Read Only**, meaning that every sync will be a full sync because we do not currently support tracking sync state in Azure Synapse
* We based our connection protocol on SQL Server [SQL JDBC driver](https://docs.microsoft.com/en-us/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server?view=sql-server-ver15)



## 🚦Allowed IP Addresses

Please allowlist [Census's IP Addresses](../basics/security-and-privacy/census-ip-addresses.md) in your firewall. By default, Census will connect to your data source from these static US-based IP addresses:

* 34.216.163.241
* 54.212.243.205

To ensure Census can connect to your Synapse data warehouse, use the Windows Azure Management Portal or run **sp\_set\_firewall\_rule** on the primary database to create a firewall rule for these two IP addresses.&#x20;

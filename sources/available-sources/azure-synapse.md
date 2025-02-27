---
description: >-
  This page describes how to configure Azure Synapse credentials for use by
  Census and why those permissions are needed.
---

# Azure Synapse

## Required Permissions

{% hint style="info" %}
These instructions are well tested to connect Census to Azure Synapse. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your database and publishes it to the corresponding objects in destination tools.

We recommend you create a dedicated `CENSUS` user account with a strong, unique password. Census uses this account to connect to your Azure Synapse database. In order for the Census connection to work correctly, the `CENSUS` account must have these permissions:

* Read-only access to any tables and views in any schemata that you would like Census to publish to your destinations.

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

## Notes

* If you have multiple schemata that you would like Census to read from, repeat the steps for "\<your schema>" for each of them
* We based our connection protocol on SQL Server [SQL JDBC driver](https://docs.microsoft.com/en-us/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server?view=sql-server-ver15)

## Advanced Network Configuration

Census can successfully connect to Azure Synapse instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../../misc/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.

Specifically, to ensure Census can connect to your Synapse data warehouse, use the Windows Azure Management Portal or run **sp\_set\_firewall\_rule** on the primary database to create a firewall rule to allow access to Census's IP addresses.

## Need help connecting to Azure Synapse?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

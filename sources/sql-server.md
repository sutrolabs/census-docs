---
description: >-
  This page describes how to configure SQL Server credentials for use by Census
  and why those permissions are needed.
---

# SQL Server

## 🔑 Permissions

{% hint style="info" %}
These instructions are well tested to connect Census to SQL Server. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your database and publishes it to the corresponding objects in destination tools.

We recommend you create a dedicated `CENSUS` user account with a strong, unique password. Census uses this account to connect to your SQL Server database. In order for the Census connection to work correctly, the `CENSUS` account needs a number of permissions

### Required Permissions

These permissions are required for both [Basic and Advanced sync engines](overview.md#sync-engines). They give Census read-only access to any tables and views in any schemata that you would like Census to publish to your service destinations.&#x20;

SQL Server permissions are complex and there are many ways to configure access for Census. The script below has been tested with recent SQL Server versions and is known to work correctly:

```
-- Create census user the ability to sign in with a password
CREATE USER CENSUS WITH PASSWORD = '<strong, unique password>';

-- Give the census user the ability to connect to database
GRANT CONNECT TO CENSUS;

-- Give the census user the ability to read table within the database
-- Note: census user just will have the ability to gain explicit permissions
-- in the following command
EXEC sp_addrolemember 'db_datareader', CENSUS;

-- Grant census user ability to read data from within a schema.
-- Run this for each schema you intend Census to access.
-- Note: this can also be granted to specific tables as well
GRANT SELECT, VIEW DEFINITION ON SCHEMA::<schema> TO CENSUS;
```

{% hint style="info" %}
Important: all SQL Server Commands will run within the Database that is specified when running the script
{% endhint %}

### Advanced Sync Engine Permissions

To enable Advanced Sync engine, Census requires additional permissions to enable state tracking within your warehouse.

```
-- Create a private bookkeeping schema where Census can store sync state
CREATE SCHEMA CENSUS AUTHORIZATION CENSUS;

-- Give the census user full access to the bookkeeping schema
GRANT ALTER, DELETE, EXECUTE, INSERT, REFERENCES, SELECT,
          UPDATE, VIEW DEFINITION ON SCHEMA::CENSUS TO CENSUS;

-- Give the census user the ability to create tables within the database
-- Note: census user just will have the ability to write within the explicit
-- permissions within the Census schema created in the previous command
GRANT CREATE TABLE TO CENSUS;
```

## Advanced Network Configuration

Census can successfully connect to SQL Server instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../basics/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.&#x20;

## Need help connecting to SQL Server?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

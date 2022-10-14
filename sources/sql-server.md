---
description: >-
  This page describes how to configure SQL Server credentials for use by Census
  and why those permissions are needed.
---

# SQL Server

## Required Permissions

{% hint style="info" %}
These instructions are well tested to connect Census to SQL Server. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.&#x20;
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your database and publishes it to the corresponding objects in destination tools.&#x20;

We recommend you create a dedicated `CENSUS` user account with a strong, unique password. Census uses this account to connect to your SQL Server database. In order for the Census connection to work correctly, the `CENSUS` account must have these permissions:

* Read-only access to any tables and views in any schemata that you would like Census to publish to your service destinations.

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

-- Grant census user ability to read data from within a schema
-- Note: this can also be granted to specific tables as well
GRANT SELECT, VIEW DEFINITION ON SCHEMA::<schema> TO CENSUS;
```

{% hint style="info" %}
Important: all SQL Server Commands will run within the Database that is specified when running the script
{% endhint %}

## 💡 Notes

* If you have multiple schemata that you would like Census to read from, repeat the steps for "\<your schema>" for each of them
* We based our connection protocol on SQL Server [SQL JDBC driver](https://docs.microsoft.com/en-us/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server?view=sql-server-ver15)
* Sync behavior will be **Read Only**, meaning that every sync will be a full sync because we do not currently support tracking sync state in SQL Server. If you configured SQL Server after 10/13/2022 and communicated with a Census representative following the documentation below.

## :writing\_hand: Write Support for SQL Server

The following commands are run to enable Write Access for SQL Server.

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

As of 10/13/2022, after successfully running these commands, please reach out to your Census technical representative or through support, and we can help finalize configuring this functionality for you.

## 🚦Allowed IP Addresses

Please whitelist [Census's IP Addresses](../basics/security-and-privacy/census-ip-addresses.md) in your firewall. By default, Census will connect to your data source from these static US-based IP addresses:

* 34.216.163.241
* 54.212.243.205

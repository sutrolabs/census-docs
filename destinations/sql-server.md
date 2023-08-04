---
description: This page describes how to sync data to your Microsoft SQL Server Instance
---

# SQL Server

* Navigate to the **Destinations** page in Census and click **New Destination**.
* Select **Microsoft SQL Server** from the menu.
* Enter the requested database credentials:
  1. **Hostname**
  2. **Port**
  3. **Database Name**
  4. **Username**
  5. **Password**
  6. **Number of Client Connections (1-8):** the maximum number of concurrent connections Census will establish with your Snowflake destination
  7. **If Using SSH**
     1. **SSH Hostname**
     2. **SSH Port**
     3. **SSH Username**



<figure><img src="../.gitbook/assets/Screenshot 2023-07-19 at 4.35.38 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2023-07-19 at 4.35.54 PM.png" alt=""><figcaption></figcaption></figure>

## Required Permissions

{% hint style="info" %}
These instructions are well tested to connect Census to SQL Server. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your database and publishes it to the corresponding objects in destination tools.

We recommend you create a dedicated `CENSUS` user account with a strong, unique password. Census uses this account to connect to your SQL Server database. In order for the Census connection to work correctly, the `CENSUS` account must have these permissions:

* Read-only access to any tables and views in any schemata that you would like Census to publish to your destinations.

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



## 🔀 Supported Objects and Behaviors

<table data-header-hidden><thead><tr><th width="155" align="right"></th><th width="147" align="center"></th><th width="243"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Identifiers</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Table</td><td align="center">✅</td><td>Primary keys or columns with uniqueness constraints</td><td>Update or Create, Update Only</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more sync behaviors for Snowflake.

## 🚑 Need help connecting to Snowflake?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

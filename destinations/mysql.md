---
description: This page describes how to sync data to your MySQL database.
---

# MySQL

## 🏃‍♀️ Getting Started

This guide will walk you through connecting to MySQL as a destination.&#x20;

{% hint style="info" %}
If you are trying to use MySQL as a data source (to query data from MySQL and sync to elsewhere), that process is documented separately here: [MySQL Data Source](../sources/mysql.md)
{% endhint %}

1. Visit the [Destinations page](https://app.getcensus.com/destinations) and click **+ New Destination**.
2. Select **Microsoft SQL Server** from the menu.
3. Enter the requested database credentials:

<table><thead><tr><th width="203">Credential</th><th>Description</th></tr></thead><tbody><tr><td>Hostname</td><td>Host name or IP address of database</td></tr><tr><td>Port</td><td>Port of database (3306 by default for MySQL)</td></tr><tr><td>Database Name</td><td>Name of database within MySQL to connect to</td></tr><tr><td>Username</td><td>Username Census will use to connect</td></tr><tr><td>Password</td><td>Password Census will use to connect</td></tr><tr><td>Number of Client Connections</td><td>Value between 1 and 8 (default is 1). This is the maximum number of concurrent connections Census will use to connect to database. The default should be fine in most cases, but increasing this value can increase throughput on very large syncs.</td></tr><tr><td>Use SSH Tunnel</td><td>Default: Off - Toggle on to indicate that Census should connect via an SSH Tunnel. For more information, see <a data-mention href="../basics/security-and-privacy/regions-and-ip-addresses.md">regions-and-ip-addresses.md</a></td></tr><tr><td>SSH Hostname</td><td>Hostname of the Census accessible SSH Tunnel bastion. </td></tr><tr><td>SSH Port</td><td>Port of SSH Tunnel bastion.</td></tr><tr><td>SSH Username</td><td>Username Census will use to connect to bastion.</td></tr></tbody></table>

## 🔑 Permissions

To use MySQL as a destination, Census requires permission to write to the desired destination tables, as well as read metadata about the table and database structures.&#x20;

```
-- Note that creating a user may be redundant if you're already configured
-- MySQL as a source.

-- Create census user the ability to sign in with a password
CREATE USER CENSUS IDENTIFIED BY '<strong, unique password>';

-- GRANT access to which ever schemas you'd like to give access to
-- Note: this can also be granted to specific tables as well
GRANT INSERT, UPDATE, SELECT ON <your schema>.* TO CENSUS;
```

## 🔀 Supported Objects and Behaviors

<table data-header-hidden><thead><tr><th align="right"></th><th width="152" align="center"></th><th width="250"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Identifiers</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Table</td><td align="center">✅</td><td>Primary keys or columns with uniqueness constraints</td><td>Update or Create, Update Only</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more sync behaviors for MySQL.

## 🚦Advanced Network Configuration

Census can successfully connect to SQL Server instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../basics/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.&#x20;

## 🚑 Need help connecting to MySQL?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

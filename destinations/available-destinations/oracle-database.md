---
description: This page describes how to sync data into your Oracle Database instance.
---

# Oracle Database

## Getting Started

This guide will walk you through connecting to Oracle Database as a destination.

1. Visit the [Destinations page](https://app.getcensus.com/destinations) and click **+ New Destination**.
2. Select **Oracle Database** from the menu.
3. Enter the requested database credentials:

<table><thead><tr><th width="203">Credential</th><th>Description</th></tr></thead><tbody><tr><td>Hostname</td><td>Host name or IP address of database</td></tr><tr><td>Port</td><td>Port of database (1521 by default for Oracle Database)<br><br>If port 2484 is specified, connection will be made using TLS. Your root certificate must be from a publicly-trusted CA.</td></tr><tr><td>Database Name</td><td>Name of database within Oracle Database to connect to</td></tr><tr><td>Username</td><td>Username Census will use to connect</td></tr><tr><td>Password</td><td>Password Census will use to connect</td></tr><tr><td>Number of Client Connections</td><td>Value between 1 and 8 (default is 1). This is the maximum number of concurrent connections Census will use to connect to database. The default should be fine in most cases, but increasing this value can increase throughput on very large syncs.</td></tr><tr><td>Use SSH Tunnel</td><td>Default: Off - Toggle on to indicate that Census should connect via an SSH Tunnel. For more information, see <a data-mention href="../../misc/security-and-privacy/regions-and-ip-addresses.md">regions-and-ip-addresses.md</a></td></tr><tr><td>SSH Hostname</td><td>Hostname of the Census accessible SSH Tunnel bastion.</td></tr><tr><td>SSH Port</td><td>Port of SSH Tunnel bastion.</td></tr><tr><td>SSH Username</td><td>Username Census will use to connect to bastion.</td></tr></tbody></table>

## 🔑 Permissions

To use Oracle Database as a destination, Census requires permission to write to the desired destination tables, as well as read metadata about the table and database structures.

```
-- Create Census user the ability to sign in with a password
CREATE USER CENSUS IDENTIFIED BY '<strong, unique password>';

-- Give the Census user the ability to connect to the database and
-- sync data to it:
GRANT
    CONNECT,
    SELECT ANY TABLE,
    INSERT ANY TABLE,
    UPDATE ANY TABLE,
    DELETE ANY TABLE
TO CENSUS;

-- It may be possible to restrict the privileges granted to the Census
-- user to specific operations and database objects depending on your
-- use-case.
```

## Supported Objects and Behaviors

<table data-header-hidden><thead><tr><th width="155" align="right"></th><th width="147" align="center"></th><th width="243"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Sync Keys</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Table</td><td align="center">✅</td><td>Primary keys or columns with uniqueness constraints</td><td>Update or Create, Update Only, Mirror</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more sync behaviors for Oracle Database.

## Advanced Network Configuration

Census can successfully connect to Oracle Database instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../../misc/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.

## Need help connecting to Oracle Database?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

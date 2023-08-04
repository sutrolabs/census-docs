---
description: This page walks through how to connect Census with your PostgreSQL database.
---

# PostgreSQL

## 🏃‍♀️ Getting Started

This guide will walk you through connecting to PostgreSQL as a destination.&#x20;

{% hint style="info" %}
If you are trying to use PostgresSQL as a data source (to query data from Postgres and sync to elsewhere), that process is documented separately here: [Postgres Data Source](../sources/postgres-1.md)
{% endhint %}

1. Visit the [Destinations page](https://app.getcensus.com/destinations) and click **+ New Destination**.
2. Select **PostgreSQL** from the menu.
3. Enter the requested database credentials:

<table><thead><tr><th width="203">Credential</th><th>Description</th></tr></thead><tbody><tr><td>Hostname</td><td>Host name or IP address of database</td></tr><tr><td>Port</td><td>Port of database (5432 by default for Postgres)</td></tr><tr><td>Database Name</td><td>Name of database within Postgres to connect to</td></tr><tr><td>Username</td><td>Username Census will use to connect</td></tr><tr><td>Password</td><td>Password Census will use to connect</td></tr><tr><td>Number of Client Connections</td><td>Value between 1 and 8 (default is 1). This is the maximum number of concurrent connections Census will use to connect to database. The default should be fine in most cases, but increasing this value can increase throughput on very large syncs.</td></tr><tr><td>Use SSH Tunnel</td><td>Default: Off - Toggle on to indicate that Census should connect via an SSH Tunnel. For more information, see <a data-mention href="../basics/security-and-privacy/regions-and-ip-addresses.md">regions-and-ip-addresses.md</a></td></tr><tr><td>SSH Hostname</td><td>Hostname of the Census accessible SSH Tunnel bastion. </td></tr><tr><td>SSH Port</td><td>Port of SSH Tunnel bastion.</td></tr><tr><td>SSH Username</td><td>Username Census will use to connect to bastion.</td></tr></tbody></table>

## 🔑 Permissions

To use Postgres as a destination, Census requires permission to write to the desired destination tables, as well as read metadata about the table and database structures.&#x20;

```
-- Note that creating a user may be redundant if you're already configured
-- Postgres as a source.

-- Give the census user the ability to sign in with a password
CREATE USER CENSUS WITH PASSWORD '<strong, unique password>';

-- Let the census user see this schema
GRANT USAGE ON SCHEMA "<your schema>" TO CENSUS;

-- Let the census user read all existing tables in this schema
-- Note: this can also be granted to specific tables as well
GRANT SELECT, INSERT, UPDATE ON ALL TABLES IN SCHEMA "<your schema>" TO CENSUS;
```

## 🗄️ Supported Objects and Behaviors <a href="#supported-objects" id="supported-objects"></a>

We support syncing data to Tables in PostgreSQL, but they must have a uniqueness constraint on a column. ​

<table data-header-hidden><thead><tr><th width="157" align="center"></th><th width="133" align="center"></th><th></th><th></th></tr></thead><tbody><tr><td align="center"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><a data-footnote-ref href="#user-content-fn-1"><strong>Identifiers</strong></a></td><td><strong>Behavior</strong></td></tr><tr><td align="center">Table</td><td align="center">✅</td><td>Primary Keys or Columns with Uniqueness Constraints</td><td>Update or Create, Update Only, Append, Mirror</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for PostgreSQL.

## 🚦Advanced Network Configuration

Census can successfully connect to PostgreSQL instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../basics/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.&#x20;

## ❗️Common Troubleshooting Issues

You may be trying to sync to a table that does not have a uniqueness constraint. If possible, you need to add one to be able to sync to it. The syntax to do so is [here](https://www.postgresql.org/docs/current/ddl-alter.html#DDL-ALTER-ADDING-A-CONSTRAINT).

## 🚑 Need help connecting to PostgreSQL?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

[^1]: 

---
description: >-
  This page walks through how to connect Census with your Google AlloyDB
  database.
---

# Google AlloyDB

## 🏃‍♀️ Getting Started

This guide shows you how to use Census to connect your AlloyDB database to your data warehouse and create your first sync.

{% hint style="info" %}
In order for a third party application (like Census) to query your AlloyDB, Google Cloud requires that you [set up an Auth proxy as detailed in their documentation](https://cloud.google.com/alloydb/docs/auth-proxy/overview). If you have any questions at all setting up this Auth proxy, please reach out to [support@getcensus.com](mailto:support@getcensus.com).
{% endhint %}

1. Visit the [Destinations page](https://app.getcensus.com/destinations) and click **+ New Destination**.
2. Select **AlloyDB** from the menu.
3. Enter the requested database credentials:

<table><thead><tr><th width="203">Credential</th><th>Description</th></tr></thead><tbody><tr><td>Hostname</td><td>Host name or IP address of database</td></tr><tr><td>Port</td><td>Port of database </td></tr><tr><td>Database Name</td><td>Name of database to connect to</td></tr><tr><td>Username</td><td>Username Census will use to connect</td></tr><tr><td>Password</td><td>Password Census will use to connect</td></tr><tr><td>Number of Client Connections</td><td>Value between 1 and 8 (default is 1). This is the maximum number of concurrent connections Census will use to connect to database. The default should be fine in most cases, but increasing this value can increase throughput on very large syncs.</td></tr><tr><td>Use SSH Tunnel</td><td>Default: Off - Toggle on to indicate that Census should connect via an SSH Tunnel. For more information, see <a data-mention href="../basics/security-and-privacy/regions-and-ip-addresses.md">regions-and-ip-addresses.md</a></td></tr><tr><td>SSH Hostname</td><td>Hostname of the Census accessible SSH Tunnel bastion. </td></tr><tr><td>SSH Port</td><td>Port of SSH Tunnel bastion.</td></tr><tr><td>SSH Username</td><td>Username Census will use to connect to bastion.</td></tr></tbody></table>

## 🔑 Permissions

To use AlloyDB as a destination, Census requires permission to write to the desired destination tables, as well as read metadata about the table and database structures.&#x20;

```
-- Note that creating a user may be redundant if you're already configured
-- AlloyDB as a source.

-- Give the census user the ability to sign in with a password
CREATE USER CENSUS WITH PASSWORD '<strong, unique password>';

-- Let the census user see this schema
GRANT USAGE ON SCHEMA "<your schema>" TO CENSUS;

-- Let the census user read all existing tables in this schema
-- Note: this can also be granted to specific tables as well
GRANT SELECT, INSERT, UPDATE ON ALL TABLES IN SCHEMA "<your schema>" TO CENSUS;
```

## 🗄️ Supported Objects and Behaviors <a href="#supported-objects" id="supported-objects"></a>

We support syncing data to Tables in AlloyDB, but they must have a uniqueness constraint on a column. ​

| **Object Name** | **Supported?** | **Sync Keys**          | **Behaviors**                              |
| --------------: | :------------: | ---------------------- |--------------------------------------------|
|         Table |        ✅       | Primary Keys or Columns with Uniqueness Constraints | Update or Create, Update Only, Add, Mirror |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for AlloyDB.

## 🚦Advanced Network Configuration

Census can successfully connect to AlloyDB instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../basics/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.&#x20;

## ❗️Common troubleshooting issues

You may be trying to sync to a table that does not have a uniqueness constraint. If possible, you need to add one to be able to sync to it. The syntax to do so is [here](https://www.postgresql.org/docs/current/ddl-alter.html#DDL-ALTER-ADDING-A-CONSTRAINT).

## 🚑 Need help connecting to Google AlloyDB?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

[^1]: 

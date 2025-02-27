---
description: This page walks through how to connect Census with your PostgreSQL database.
---

# PostgreSQL

## Getting Started

This guide will walk you through connecting to PostgreSQL as a destination.

{% hint style="info" %}
If you are trying to use PostgresSQL as a data source (to query data from Postgres and sync to elsewhere), that process is documented separately here: [Postgres Data Source](../sources/available-sources/postgres.md)
{% endhint %}

1. Visit the [Destinations page](https://app.getcensus.com/destinations) and click **+ New Destination**.
2. Select **PostgreSQL** from the menu.
3. Enter the requested database credentials:

<table><thead><tr><th width="203">Credential</th><th>Description</th></tr></thead><tbody><tr><td>Hostname</td><td>Host name or IP address of database</td></tr><tr><td>Port</td><td>Port of database (5432 by default for Postgres)</td></tr><tr><td>Database Name</td><td>Name of database within Postgres to connect to</td></tr><tr><td>Username</td><td>Username Census will use to connect</td></tr><tr><td>Password</td><td>Password Census will use to connect</td></tr><tr><td>Number of Client Connections</td><td>Value between 1 and 8 (default is 1). This is the maximum number of concurrent connections Census will use to connect to database. The default should be fine in most cases, but increasing this value can increase throughput on very large syncs.</td></tr><tr><td>Use SSH Tunnel</td><td>Default: Off - Toggle on to indicate that Census should connect via an SSH Tunnel. For more information, see <a data-mention href="../misc/security-and-privacy/regions-and-ip-addresses.md">regions-and-ip-addresses.md</a></td></tr><tr><td>SSH Hostname</td><td>Hostname of the Census accessible SSH Tunnel bastion.</td></tr><tr><td>SSH Port</td><td>Port of SSH Tunnel bastion.</td></tr><tr><td>SSH Username</td><td>Username Census will use to connect to bastion.</td></tr></tbody></table>

## 🔑 Permissions

To use Postgres as a destination, Census requires permission to write to the desired destination tables, as well as read metadata about the table and database structures.

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

### Custom Field Permissions

Census allows you to create custom fields in your destination Postgres as a by-product of your sync (see [#creating-new-fields-on-your-destination-object](../syncs/core-concept/#creating-new-fields-on-your-destination-object "mention")).&#x20;

To enable this in Postgres, Census needs to have the required permissions to add columns to your Postgres table.&#x20;

{% hint style="info" %}
The following instructions give you details on how to enable this with a new role, but you may want to reuse a similar existing role instead.
{% endhint %}

Run these commands to enable custom fields (in addition to those above).

```
-- Step 1: Create a role for managing custom field operations, including the ability to alter tables
CREATE ROLE census_table_manager;

-- Step 2: Allow the census_table_manager role to access the schema
GRANT USAGE ON SCHEMA "<your schema>" TO census_table_manager;

-- Step 3: Transfer ownership of the relevant table(s) to the census_table_manager role
-- This allows the role to manage table structures, including adding custom fields.
-- (Repeat this step for each table that will be managed)
ALTER TABLE <your_table> OWNER TO census_table_manager;

-- Step 4: Grant the census_table_manager role to the census user
GRANT census_table_manager TO CENSUS;

-- Step 5: Ensure the census user always uses the census_table_manager role by default
ALTER USER CENSUS SET ROLE census_table_manager;
```

## ️ Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

We support syncing data to Tables in PostgreSQL, but they must have a uniqueness constraint on a column. ​

| **Object Name** | **Supported?** | **Sync Keys**                                       | **Behaviors**                              |
| --------------: | :------------: | --------------------------------------------------- | ------------------------------------------ |
|           Table |        ✅       | Primary Keys or Columns with Uniqueness Constraints | Update or Create, Update Only, Add, Mirror |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/core-concept/#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Postgres objects and/or behaviors

## Advanced Network Configuration

Census can successfully connect to PostgreSQL instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../misc/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.

## ❗️Common Troubleshooting Issues

You may be trying to sync to a table that does not have a uniqueness constraint. If possible, you need to add one to be able to sync to it. The syntax to do so is [here](https://www.postgresql.org/docs/current/ddl-alter.html#DDL-ALTER-ADDING-A-CONSTRAINT).

## Need help connecting to PostgreSQL?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

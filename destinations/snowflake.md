---
description: This page describes how to sync data to your Snowflake data warehouse.
---

# Snowflake

## Getting Started <a href="#getting-started" id="getting-started"></a>

This guide will walk you through connecting to Snowflake as a destination.

{% hint style="info" %}
If you are trying to use Snowflake as a data source (to query data from Snowflake and sync to elsewhere), that process is documented separately here: [Snowflake Data Source](../sources/available-sources/snowflake.md)
{% endhint %}

1. Visit the [Destinations page](https://app.getcensus.com/destinations) and click **+ New Destination**.
2. Select **Snowflake** from the menu.
3. Enter the requested database credentials:

<table><thead><tr><th width="203">Credential</th><th>Description</th></tr></thead><tbody><tr><td>Account</td><td>Should be in the form <code>iq18923.us-east-1</code></td></tr><tr><td>User</td><td>User Census will use to connect</td></tr><tr><td>Use Key-pair Auth?</td><td>Yes (Recommended) / No</td></tr><tr><td>Password</td><td>(Deprecated) User / Password authentication on Snowflake <a href="https://www.snowflake.com/en/blog/blocking-single-factor-password-authentification/">will be blocked November 2025</a>. If you intend to use this authentication mechanism, see the section below.</td></tr><tr><td>Warehouse</td><td>The Snowflake compute warehouse Census will use</td></tr><tr><td>Database</td><td>The database within the Snowflake account Census will connect to</td></tr><tr><td>Schema</td><td>(Optional) This can be enforced or left empty. If empty, you'll have the option to select this when creating a sync.</td></tr><tr><td>Number of Client Connections</td><td>Value between 1 and 8 (default is 1). This is the maximum number of concurrent connections Census will use to connect to database. The default should be fine in most cases, but increasing this value can increase throughput on very large syncs.</td></tr><tr><td>Use SSH Tunnel</td><td>Default: Off - Toggle on to indicate that Census should connect via an SSH Tunnel. For more information, see <a data-mention href="../misc/security-and-privacy/regions-and-ip-addresses.md">regions-and-ip-addresses.md</a></td></tr><tr><td>SSH Hostname</td><td>Hostname of the Census accessible SSH Tunnel bastion.</td></tr><tr><td>SSH Port</td><td>Port of SSH Tunnel bastion.</td></tr><tr><td>SSH Username</td><td>Username Census will use to connect to bastion.</td></tr></tbody></table>

### Using User/Password Authentication (between now and Nov 2025)

[Snowflake has announced](https://www.snowflake.com/en/blog/blocking-single-factor-password-authentification/) that they will block User/Password authentication w/o MFA starting April 1, 2025 and completing November 2025. Requiring MFA makes this authentication form impractical for automated use cases like Census. If you are currently using User/Password, you have a few options:

1. Switch to using Key-pair authentication (recommended).
2. You can temporarily opt an account of this constraint by indicating they are a service account. Note that this will only allow continued access until November 2025.

```sql
ALTER USER CENSUS SET TYPE = LEGACY_SERVICE;
```

## 🔑 Permissions

To use Snowflake as a destination, Census requires permission to write to the desired destination tables, as well as read metadata about the table and database structures.

```
-- Note that creating a user may be redundant if you're already configured
-- Snowflake as a source.

-- Create a role for the census user
CREATE ROLE CENSUS_ROLE;

-- Ensure the sysadmin role inherits any privileges the census role is granted. Note that this does not grant sysadmin privileges to the census role
GRANT ROLE CENSUS_ROLE TO ROLE SYSADMIN;

-- Create a warehouse for the census user, optimizing for cost over performance
CREATE WAREHOUSE CENSUS_WAREHOUSE WITH WAREHOUSE_SIZE = XSMALL AUTO_SUSPEND = 60 AUTO_RESUME = TRUE INITIALLY_SUSPENDED = FALSE;

-- Allow the census user to run queries in the warehouse
GRANT USAGE ON WAREHOUSE CENSUS_WAREHOUSE TO ROLE CENSUS_ROLE;

-- Allow the census user to start and stop the warehouse and abort running queries in the warehouse
GRANT OPERATE ON WAREHOUSE CENSUS_WAREHOUSE TO ROLE CENSUS_ROLE;

-- Allow the census user to see historical query statistics on queries in its warehouse
GRANT MONITOR ON WAREHOUSE CENSUS_WAREHOUSE TO ROLE CENSUS_ROLE;

-- Create the census user
-- Do not set DEFAULT_WORKSPACE, this will impact which tables are visible to Census
CREATE USER CENSUS WITH DEFAULT_ROLE = CENSUS_ROLE DEFAULT_WAREHOUSE = CENSUS_WAREHOUSE PASSWORD = '<strong, unique password>';

-- Grant the census role to the census user
GRANT ROLE CENSUS_ROLE TO USER CENSUS;

-- Let the census user see this database
GRANT USAGE ON DATABASE "<your database>" TO ROLE CENSUS_ROLE;

-- Let the census user see this schema
GRANT USAGE ON SCHEMA "<your database>"."<your schema>" TO ROLE CENSUS_ROLE;

-- Grant census user ability to write data to tables within a schema
-- Note: this can also be granted to specific tables as well
GRANT INSERT, UPDATE, SELECT ON ALL TABLES IN SCHEMA "<your database>"."<your schema>" TO ROLE CENSUS_ROLE;
```

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys**                                       | **Behaviors**                              |
| --------------: | :------------: | --------------------------------------------------- | ------------------------------------------ |
|           Table |        ✅       | Primary keys or columns with uniqueness constraints | Mirror, Update or Create, Update Only, Add |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Snowflake objects and/or behaviors.

## Advanced Network Configuration

Census can successfully connect to Snowflake instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../misc/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.

## Need help connecting to Snowflake?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

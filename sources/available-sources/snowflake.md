---
description: >-
  This page describes how to configure Snowflake credentials for use by Census
  and why those permissions are needed.
---

# Snowflake

## Required Permissions

{% hint style="success" %}
These instructions are well tested to connect Census to Snowflake. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your data warehouse and publishes it to the corresponding objects in destinations such as Salesforce. To limit the load on your database as well as external APIs, Census computes a “diff” to determine changes between each update. In order to compute these diffs, Census creates and writes to a number of tables in the `CENSUS` schema. In order for the Census connection to work correctly, the account you provide to Census must have these permissions:

* Full access to the `CENSUS` database and the `CENSUS` schema in that database. Skip this step if working in read-only mode.
* Read-only access to any tables and views in any schemata from which you want Census to publish
* The `CENSUS` database and schema are reserved for Census's bookkeeping operations. **Do not** place your source data here, as this database is **inaccessible** inside Census syncs.

Snowflake permissions are complex and there are many ways to configure access for Census. The script below is known to work correctly and follows [Snowflake's best practices](https://docs.snowflake.com/en/user-guide/security-access-control-configure.html#creating-read-only-roles) for creating read-only roles in a role hierarchy:

<pre class="language-sql"><code class="lang-sql">-- Create a role for the census user
CREATE ROLE CENSUS_ROLE;

-- Ensure the sysadmin role inherits any privileges the census role is granted. Note that this does not grant sysadmin privileges to the census role
GRANT ROLE CENSUS_ROLE TO ROLE SYSADMIN;

-- Create a warehouse for the census role, optimizing for cost over performance
CREATE WAREHOUSE CENSUS_WAREHOUSE WITH WAREHOUSE_SIZE = XSMALL AUTO_SUSPEND = 60 AUTO_RESUME = TRUE INITIALLY_SUSPENDED = FALSE;
GRANT USAGE ON WAREHOUSE CENSUS_WAREHOUSE TO ROLE CENSUS_ROLE;
GRANT OPERATE ON WAREHOUSE CENSUS_WAREHOUSE TO ROLE CENSUS_ROLE;
GRANT MONITOR ON WAREHOUSE CENSUS_WAREHOUSE TO ROLE CENSUS_ROLE;

-- Create the census user
-- Do not set DEFAULT_WORKSPACE, this will impact which tables are visible to Census
CREATE USER CENSUS WITH DEFAULT_ROLE = CENSUS_ROLE DEFAULT_WAREHOUSE = CENSUS_WAREHOUSE PASSWORD = '&#x3C;strong, unique password>';
GRANT ROLE CENSUS_ROLE TO USER CENSUS;

-- Let the census user read the data you want to sync
-- This database and schema must have a different name than CENSUS
GRANT USAGE ON DATABASE "&#x3C;your database>" TO ROLE CENSUS_ROLE;
GRANT USAGE ON SCHEMA "&#x3C;your database>"."&#x3C;your schema>" TO ROLE CENSUS_ROLE;
GRANT SELECT ON ALL TABLES IN SCHEMA "&#x3C;your database>"."&#x3C;your schema>" TO ROLE CENSUS_ROLE;
GRANT SELECT ON FUTURE TABLES IN SCHEMA "&#x3C;your database>"."&#x3C;your schema>" TO ROLE CENSUS_ROLE;
GRANT SELECT ON ALL VIEWS IN SCHEMA "&#x3C;your database>"."&#x3C;your schema>" TO ROLE CENSUS_ROLE;
GRANT SELECT ON FUTURE VIEWS IN SCHEMA "&#x3C;your database>"."&#x3C;your schema>" TO ROLE CENSUS_ROLE;
GRANT USAGE ON ALL FUNCTIONS IN SCHEMA "&#x3C;your database>"."&#x3C;your schema>" TO ROLE CENSUS_ROLE;
GRANT USAGE ON FUTURE FUNCTIONS IN SCHEMA "&#x3C;your database>"."&#x3C;your schema>" TO ROLE CENSUS_ROLE;

-- Required for Advanced Sync Engine, not required for Basic Sync Engine:
--  Create a private bookkeeping database where Census can store sync state,
--  perform faster unloads, and keep Warehouse Writeback logs

CREATE DATABASE "CENSUS";
GRANT ALL PRIVILEGES ON DATABASE "CENSUS" TO ROLE CENSUS_ROLE;
-- If you want to explicitly grant the required permissions instead of using GRANT ALL you can use the following command
<strong>--GRANT USAGE, CREATE TABLE, CREATE VIEW,MODIFY, MONITOR ON DATABASE "CENSUS"."CENSUS" TO ROLE CENSUS_ROLE
</strong>
CREATE SCHEMA "CENSUS"."CENSUS";
GRANT ALL PRIVILEGES ON SCHEMA "CENSUS"."CENSUS" TO ROLE CENSUS_ROLE;
-- If you want to explicitly grant the required permissions instead of using GRANT ALL you can use the following command
<strong>--GRANT CREATE TABLE, CREATE VIEW, MODIFY, MONITOR, CREATE STAGE  ON SCHEMA "CENSUS"."CENSUS" TO ROLE CENSUS_ROLE
</strong>
GRANT CREATE STAGE ON SCHEMA "CENSUS"."CENSUS" TO ROLE CENSUS_ROLE;
</code></pre>

## :nut\_and\_bolt:Configuring a new Snowflake connection

1. Visit the **Sources** section on Census, and press **New Source**, selecting **Snowflake** from the list.
2. Census will ask you to provide the **following:**
   *   Snowflake Account Name

       This is the URL prefix you use to connect or log into Snowflake. It may include a service region or cloud provider:

       ```
       https://<account_name>.snowflake-computing.com/
       ```

       See the [Snowflake documentation](https://docs.snowflake.com/en/user-guide/jdbc-configure.html#connection-parameters) for more information about the supported options.
   * Query Execution Warehouse - this should match the warehouse you've created in the above instructions - for example`CENSUS_WAREHOUSE`
   * User - the user you use to log into Snowflake
   * Database Name (optional) - default database to log into
   * Schema Name (optional) - default schema to log into
   * Authentication - choose one of the following
     * password - recommended.
     * keypair - After saving the connection, Census will generate a public/private keypair and provide instructions for configuring your Snowflake user account to use it.
3. Once you provide the required information, click Connect to finish the connection to Snowflake.
4. After the connection is saved, go ahead and press the **Test** button. This will validate that you've completed the above steps correctly. Once you've got a checkmark for all four steps, you're good to go!

## 💸 Managing Snowflake Warehouse Costs

The script above creates a new virtual data warehouse (execution environment) for Census. This allows you to monitor and tune Census queries for the best balance of performance and speed.

The script above creates the smallest available virtual warehouse ("X-Small") and configures it to aggressively auto-suspend if not in use, which makes the best use of your Snowflake account credits. However, some Census jobs (especially involving lots of data or complex models) will benefit from a larger warehouse. You can use Snowflake's [ALTER WAREHOUSE](https://docs.snowflake.com/en/sql-reference/sql/alter-warehouse.html) command to adjust the size of the CENSUS warehouse and tune it for your workload.\
\
Alternatively, if cost concerns are an issue, you can also share a warehouse with other batch processing systems (for example Segment, Fivetran, dbt, etc).\
\
You may also want to [adjust the schedules](../basics/core-concept/#scheduling-a-sync) of your Census syncs. Using Hourly and Daily syncs that are scheduled at the same time, rather than Continuous or every 15 minutes will give the largest continuous idle periods and save on account credits.

## 🔗 Connecting to Snowflake on AWS VPS or via PrivateLink

Connecting to a Snowflake instance running on AWS VPS or via PrivateLink requires a modified connection configuration. Please contact your Census account manager to have this configured for you.

## Allowed IP Addresses

If you're using Snowflake's Allowed IPs network policy, you'll need to add these Census IP addresses to your list. You can find Census's set of IP address for your region in [Regions & IP Addresses](../basics/security-and-privacy/regions-and-ip-addresses.md#ip-addresses). Visit the [Snowflake Help Center](https://docs.snowflake.net/manuals/user-guide/network-policies.html) for more details on how to specify these IPs as part of your network policy.

## ⚡ Change tracking for Live Syncs

If you are trying to use [Live Syncs](../basics/core-concept/live-syncs.md) you may need to modify the settings on the source table(s) as follows:

```sql
ALTER TABLE "<table_name>" SET CHANGE_TRACKING = TRUE;
```

## Need help connecting to Snowflake?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

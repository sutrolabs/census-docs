---
description: >-
  This page describes how to configure Snowflake credentials for use by Census
  and why those permissions are needed.
---

# Snowflake

## 🔐 Required Permissions

{% hint style="success" %}
These instructions are well tested to connect Census to Snowflake. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your data warehouse and publishes it to the corresponding objects in destinations such as Salesforce. To limit the load on your database as well as external APIs, Census computes a “diff” to determine changes between each update. In order to compute these diffs, Census creates and writes to a number of tables in the `CENSUS` schema. In order for the Census connection to work correctly, the account you provide to Census must have these permissions:

* Full access to the `CENSUS` database and the `CENSUS` schema in that database. Skip this step if working in read-only mode.
* Read-only access to any tables and views in any schemata from which you want Census to publish

Snowflake permissions are complex and there are many ways to configure access for Census. The script below is known to work correctly and follows [Snowflake's best practices](https://docs.snowflake.com/en/user-guide/security-access-control-configure.html#creating-read-only-roles) for creating read-only roles in a role hierarchy:

```
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

-- Create a private bookkeeping database where Census can store sync state
-- Skip this step if working in read-only mode
CREATE DATABASE "CENSUS";

-- Give the census user full access to the bookkeeping database
-- Skip this step if working in read-only mode
GRANT ALL PRIVILEGES ON DATABASE "CENSUS" TO ROLE CENSUS_ROLE;

-- Create a private bookkeeping schema where Census can store sync state
-- Skip this step if working in read-only mode
CREATE SCHEMA "CENSUS"."CENSUS";

-- Give the census user full access to the bookkeeping schema
-- Skip this step if working in read-only mode
GRANT ALL PRIVILEGES ON SCHEMA "CENSUS"."CENSUS" TO ROLE CENSUS_ROLE;

-- Give the census user the ability to create stages for unloading data
-- Skip this step if working in read-only mode
GRANT CREATE STAGE ON SCHEMA "CENSUS"."CENSUS" TO ROLE CENSUS_ROLE;

-- Let the census user see this database
GRANT USAGE ON DATABASE "<your database>" TO ROLE CENSUS_ROLE;

-- Let the census user see this schema
GRANT USAGE ON SCHEMA "<your database>"."<your schema>" TO ROLE CENSUS_ROLE;

-- Let the census user read all existing tables in this schema
GRANT SELECT ON ALL TABLES IN SCHEMA "<your database>"."<your schema>" TO ROLE CENSUS_ROLE;

-- Let the census user read any new tables added to this schema
GRANT SELECT ON FUTURE TABLES IN SCHEMA "<your database>"."<your schema>" TO ROLE CENSUS_ROLE;

-- Let the census user read all existing views in this schema
GRANT SELECT ON ALL VIEWS IN SCHEMA "<your database>"."<your schema>" TO ROLE CENSUS_ROLE;

-- Let the census user read any new views added to this schema
GRANT SELECT ON FUTURE VIEWS IN SCHEMA "<your database>"."<your schema>" TO ROLE CENSUS_ROLE;

-- Let the census user execute any existing functions in this schema
GRANT USAGE ON ALL FUNCTIONS IN SCHEMA "<your database>"."<your schema>" TO ROLE CENSUS_ROLE;

-- Let the census user execute any new functions added to this schema
GRANT USAGE ON FUTURE FUNCTIONS IN SCHEMA "<your database>"."<your schema>" TO ROLE CENSUS_ROLE;
```

## :nut\_and\_bolt:Configuring a new Snowflake connection

1. Visit the **Sources** section on Census, and press **New Source**, selecting **Snowflake** from the list.
2. Census will ask you to provide the **following:**
   *   Snowflake Account Name&#x20;

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

## 🚦 Allowed IP Addresses

If you're using Snowflake's Allowed IPs network policy, you'll need to add these Census IP addresses to your list. You can find Census's set of IP address for your region in [Regions & IP Addresses](../basics/security-and-privacy/regions-and-ip-addresses.md#ip-addresses). Visit the [Snowflake Help Center](https://docs.snowflake.net/manuals/user-guide/network-policies.html) for more details on how to specify these IPs as part of your network policy.

## 🚑 Need help connecting to Snowflake?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

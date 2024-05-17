---
description: >-
  This page describes how to configure Google Cloud SQL for PostgreSQL
  credentials for use by Census and why those permissions are needed.
---

# Google Cloud SQL for PostgreSQL

## 🔐 Required Permissions

{% hint style="info" %}
These instructions are well-tested to connect Census to Google Cloud SQL for PostgreSQL. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your database and publishes it to the corresponding objects in external systems such as Salesforce. To limit the load on your database as well as to other apps' APIs, Census computes a “diff” to determine changes between each update. In order to compute these diffs, Census creates and writes to a set of tables to a private bookkeeping schema (2 or 3 tables for each sync job configured).

We recommend you create a dedicated `CENSUS` user account with a strong, unique password. Census uses this account to connect to your PostgreSQL database. In order for the Census connection to work correctly, the `CENSUS` account must have these permissions:

* Skip this step if working in read-only mode. The ability to create the `CENSUS` schema and full admin access to all tables within that schema (including creating tables, deleting tables, and reading and writing to all tables).
* Read-only access to any tables and views in any schemata that you would like Census to publish to your service destinations.
* If you are using Census to load service data into your warehouse, read-write access to the schema where Census should load data (note that this is not included in the sample script below).

PostgreSQL permissions are complex and there are many ways to configure access for Census. The script below has been tested with recent PostgreSQL versions and is known to work correctly:

```
-- Give the census user the ability to sign in with a password
CREATE USER CENSUS WITH PASSWORD '<strong, unique password>';

-- Create a private bookkeeping schema where Census can store sync state
-- Skip this step if working in read-only mode
CREATE SCHEMA CENSUS;

-- Give the census user full access to the bookkeeping schema
-- Skip this step if working in read-only mode
GRANT ALL ON SCHEMA CENSUS TO CENSUS;

-- Ensure the census user has access to any objects that may have already existed in the bookkeeping schema
-- Skip this step if working in read-only mode
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA CENSUS TO CENSUS;

-- Let the census user see this schema
GRANT USAGE ON SCHEMA "<your schema>" TO CENSUS;

-- Let the census user read all existing tables in this schema
GRANT SELECT ON ALL TABLES IN SCHEMA "<your schema>" TO CENSUS;

-- Let the census user read any new tables added to this schema
ALTER DEFAULT PRIVILEGES IN SCHEMA "<your schema>" GRANT SELECT ON TABLES TO CENSUS;

-- Let the census user execute any existing functions in this schema
GRANT EXECUTE ON ALL FUNCTIONS IN SCHEMA "<your schema>" TO CENSUS;

-- Let the census user execute any new functions added to this schema
ALTER DEFAULT PRIVILEGES IN SCHEMA "<your schema>" GRANT EXECUTE ON FUNCTIONS TO CENSUS;
```

## 💡Notes

{% hint style="danger" %}
We **strongly recommend against** connecting Census to a production Google Cloud SQL for PostgreSQL instance. Census queries are often very analytical in nature and do not always play nicely with production environments. Unfortunately, PostgreSQL doesn't give you much ability to control performance impacts across users so to avoid issues, please use Census with databases set up for analytic workloads only!
{% endhint %}

* If you have multiple schemata that you would like Census to read from, repeat the steps for "\<your schema>" for each of them
* In older versions of PostgreSQL, if there are views in your schema that reference tables in other schemata, you will also need to give Census read access to those other schemata. In later versions of PostgreSQL this extra read access is not required.
* If you are using Census models to execute stored procedures (this is rare and not recommended for most users) you may also need to give Census access to those procedures

## 🚦Advanced Network Configuration

Census can successfully connect to Google Cloud SQL instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../misc/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.&#x20;

## 🚑 Need help connecting to Google Cloud SQL for Postgres?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

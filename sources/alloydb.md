---
description: >-
  This page describes how to configure AlloyDB credentials for use by Census and
  why those permissions are needed.
---

# Google AlloyDB

## 🔐 Required Permissions

{% hint style="info" %}
In order for a third party application (like Census) to query your AlloyDB, Google Cloud requires that you [set up an Auth proxy as detailed in their documentation](https://cloud.google.com/alloydb/docs/auth-proxy/overview). If you have any questions at all setting up this Auth proxy, please reach out to [support@getcensus.com](mailto:support@getcensus.com).
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your database and publishes it to the corresponding objects in external systems such as Salesforce. To limit the load on your database as well as to other apps' APIs, Census computes a “diff” to determine changes between each update. In order to compute these diffs, Census creates and writes to a set of tables to a private bookkeeping schema (2 or 3 tables for each sync job configured).

We recommend you create a dedicated `CENSUS` user account with a strong, unique password. Census uses this account to connect to your AlloyDB database. In order for the Census connection to work correctly, the `CENSUS` account must have these permissions:

* The ability to create the `CENSUS` schema and full admin access to all tables within that schema (including creating tables, deleting tables, and reading and writing to all tables).
* Read-only access to any tables and views in any schemata that you would like Census to publish to your service destinations.
* If you are using Census to load service data into your warehouse, read-write access to the schema where Census should load data (note that this is not included in the sample script below).

AlloyDB permissions are complex and there are many ways to configure access for Census. The script below has been tested with AlloyDB and is known to work correctly:

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

## 💡 Notes

{% hint style="danger" %}
We **strongly recommend against** connecting Census to a production AlloyDB database. Census queries are often very analytical in nature and do not always play nicely with production environments.
{% endhint %}

* If you have multiple schemata that you would like Census to read from, repeat the steps for "\<your schema>" for each of them
* If you are using Census models to execute stored procedures (this is rare and not recommended for most users) you may also need to give Census access to those procedures

## 🚦Advanced Network Configuration

Census can successfully connect to AlloyDB instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../basics/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.&#x20;

We recommend configuring your AlloyDB instance to use TLS v1.2 or later for all connections.

## 🚑 Need help connecting to AlloyDB?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

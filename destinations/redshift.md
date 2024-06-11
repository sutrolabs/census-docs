---
description: This page describes how to sync data to your Redshift data warehouse.
---

# Amazon Redshift

## 🏃‍♀️ Getting Started

This guide will walk you through connecting to AWS Redshift as a destination.

{% hint style="info" %}
If you are trying to use Redshift as a data source (to query data from Redshift and sync to elsewhere), that process is documented separately here: [Redshift Data Source](../sources/redshift.md)
{% endhint %}

1. Visit the [Destinations page](https://app.getcensus.com/destinations) and click **+ New Destination**.
2. Select **Redshift** from the menu.
3. Enter the requested database credentials:

<table><thead><tr><th width="203">Credential</th><th>Description</th></tr></thead><tbody><tr><td>Hostname</td><td>Host name or IP address of database</td></tr><tr><td>Port</td><td>Port of database (5439 by default for Redshift)</td></tr><tr><td>Database Name</td><td>Name of database within Redshift to connect to</td></tr><tr><td>Username</td><td>Username Census will use to connect</td></tr><tr><td>Password</td><td>Password Census will use to connect</td></tr><tr><td>Number of Client Connections</td><td>Value between 1 and 8 (default is 1). This is the maximum number of concurrent connections Census will use to connect to database. The default should be fine in most cases, but increasing this value can increase throughput on very large syncs.</td></tr></tbody></table>

## 🔑 Permissions

To use Redshift as a destination, Census requires permission to write to the desired destination tables, as well as read metadata about the table and database structures.

```
-- Note that creating a user may be redundant if you're already configured
-- Redshift as a source.

-- Give the census user the ability to sign in with a password
CREATE USER CENSUS WITH PASSWORD '<strong, unique password>';

-- Let the census user see this schema
GRANT USAGE ON SCHEMA "<your schema>" TO CENSUS;

-- Let the census user read all existing tables in this schema
-- Note: this can also be granted to specific tables as well
GRANT SELECT, INSERT, UPDATE ON ALL TABLES IN SCHEMA "<your schema>" TO CENSUS;
```

## 🔀 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys**                                       | **Behaviors**                      |
| --------------: | :------------: | --------------------------------------------------- | ---------------------------------- |
|           Table |        ✅       | Primary Keys or Columns with Uniqueness Constraints | Update or Create, Update Only, Add |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Redshift objects and/or behaviors.

## 🚦Advanced Network Configuration

Census can successfully connect to Redshift instances that are using advanced networking controls including region constraints and IP address allow lists. For more information, see our [regions-and-ip-addresses.md](../basics/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.

## 🚑 Need help connecting to Redshift?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

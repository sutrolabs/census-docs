---
description: This page describes how to configure Greenplum as a source for Census.
---

# Greenplum

## Sync Engines and Permissions

Census reads data from tables and views in Greenplum and syncs it to your desired objects in any supported [destination](broken-reference). To limit the load on your database as well as destination apps' APIs, Census maintains state tracking tables that enable it to only sync data that has been modified sync the last sync (incremental syncs). When configuring your Greenplum connection, you'll choose a [Sync Engine](overview.md#sync-engines) that determines how state tracking is handled.

The _Basic Sync Engine_ maintains state tracking tables on Census-owned infrastructure and is therefore simpler to configure and requires read access only.

The _Advanced Sync Engine_ delivers enhanced performance by maintaining state tracking tables in a dedicated schema within your own Greenplum instance. Using this feature [requires additional configuration.](greenplum.md#advanced-sync-engine)

<figure><img src="../.gitbook/assets/Screenshot 2023-08-04 at 3.59.40 PM (1).png" alt=""><figcaption><p>Greenplum Connection Setup</p></figcaption></figure>

For either choice, we recommend you create a dedicated database user with a strong, unique password for Census to use to connect to your database.

#### Create a Census User

```sql
-- Create CENSUS user and set password
CREATE USER CENSUS WITH PASSWORD '<strong unique password>';
```

### Basic Sync Engine

#### Grant Read Access to Your Data

The following commands grant read access to your data schema.

{% hint style="info" %}
Replace`<your schema>` with the name of your schema. Run once for each schema that contains data you wish to sync using Census.
{% endhint %}

```sql
-- Let the census user read all existing tables in this schema
GRANT SELECT ON ALL TABLES IN SCHEMA "<your schema>" TO CENSUS;

-- Let the census user read any new tables added to this schema
ALTER DEFAULT PRIVILEGES IN SCHEMA "<your schema>" GRANT SELECT ON TABLES TO CENSUS;

-- Let the census user execute any existing functions in this schema
GRANT EXECUTE ON ALL FUNCTIONS IN SCHEMA "<your schema>" TO CENSUS;

-- Let the census user execute any new functions added to this schema
ALTER DEFAULT PRIVILEGES IN SCHEMA "<your schema>" GRANT EXECUTE ON FUNCTIONS TO CENSUS;
```

### Advanced Sync Engine

The following steps are only required if using the _Advanced Sync Engine._

You must complete the steps [Create a Census User](greenplum.md#create-a-census-user) and [Grant Read Access to Your Data](greenplum.md#basic-sync-engine) before proceeding with the steps in this section.

#### Create Census Schema and Grant Permissions

If you wish to utilize the Advanced Sync Engine, run the following commands to create the necessary schema and permission grants.

```sql
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

## Advanced Network Configuration

Census can successfully connect to Greenplum instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../basics/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.

We recommend configuring your Greenplum instance to use TLS v1.2 or later for all connections.

## Need help connecting to Greenplum?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

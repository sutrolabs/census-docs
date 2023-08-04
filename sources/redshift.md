---
description: >-
  This page describes how to configure Redshift credentials for use by Census
  and why those permissions are needed.
---

# Redshift

## 🔐 Required Permissions

{% hint style="danger" %}
These instructions are well tested to connect Census to Redshift. If you're running into connection issues or missing tables or views, please confirm you've run all of these instructions.
{% endhint %}

Census reads data from one or more tables (possibly across different schemata) in your database and publishes it to the corresponding objects in external systems such as Salesforce. To limit the load on your database as well as to other apps' APIs, Census computes a “diff” to determine changes between each update. In order to compute these diffs, Census creates and writes to a set of tables to a private bookkeeping schema (2 or 3 tables for each sync job configured).

We recommend you create a dedicated `CENSUS` user account with a strong, unique password. Census uses this account to connect to your Redshift warehouse. In order for the Census connection to work correctly, the `CENSUS` account must have these permissions:

* Skip this step if working in read-only mode. The ability to create the `CENSUS` schema and full admin access to all tables within that schema (including creating tables, deleting tables, and reading and writing to all tables).
* Read-only access to any tables and views in any schemata that you would like Census to publish to your service destinations.

Redshift permissions are complex and there are many ways to configure access for Census. The script below has been tested with Redshift and is known to work correctly:

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

{% hint style="warning" %}
**Using dbt? Make sure Census retains access after each dbt run!**
{% endhint %}

dbt (data build tool) often requires permissions to be re-granted on objects after it rebuilds models. Census customers frequently extend permissions management on their dbt models in two ways:

1. **Fine-grained permissions** – By adding [post-hooks](https://docs.getdbt.com/reference/resource-configs/pre-hook-post-hook#grant-privileges-on-a-directory-of-models) in a dbt project, Census customers immediately grant access to the Census database user after each desired model builds.
2. **Access to all dbt tables and views (Recommended)** – Census customers change the default permissions of the database user for their production dbt runs so that any tables and views created by that users are accessible to the Census database user. In this case, we extend the `ALTER DEFAULT PRIVILEGES` to specifically indicate the defaults of the dbt production run user.

```
ALTER DEFAULT PRIVILEGES FOR USER "<your dbt run user> IN SCHEMA "<your dbt target schema>" GRANT SELECT ON TABLES TO CENSUS;
```

Because this is altering the default behavior of another user, this command must be run by a Redshift superuser.

## 💡 Notes

* If you have multiple schemata that you would like Census to read from, repeat the steps for "\<your schema>" for each of them
* In Redshift if there are views in your schema that reference tables in other schemata, you will also need to give Census read access to those other schemata.
* If you are using Census models to execute stored procedures (this is rare and not recommended for most users) you may also need to give Census access to those procedures

## 🚦Advanced Network Configuration

Census can successfully connect to AlloyDB instances that are using advanced networking controls including region constraints, IP address allow lists, or SSH Tunneling. For more information, see our [regions-and-ip-addresses.md](../basics/security-and-privacy/regions-and-ip-addresses.md "mention") documentation.&#x20;

### Deploying Redshift within an AWS VPC

Advanced methods of Redshift deployment include deploying Redshift within an AWS VPC or private subnet and limiting direct database access to a separate proxy (typically the SSH Tunnel method described above).

Census uses the `UNLOAD` command to bulk extract data efficiently (you can read more about our architecture in [How Census Works](https://docs.getcensus.com/basics/security-and-privacy#how-it-works)). By default, Redshift-in-VPC deployments do not allow Redshift to talk to S3. So when using this method, you'll need to separately grant permission to Redshift to communicate directly with S3 by adding an S3 VPC Endpoint.\
\
This is definitely an obscure feature of AWS but this article does a good job of [explaining S3 VPC endpoints](https://tomgregory.com/when-to-use-an-aws-s3-vpc-endpoint/), why they're needed and how to set one up.

## 🚑 Need help connecting to Redshift?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

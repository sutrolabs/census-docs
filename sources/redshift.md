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

* The ability to create the `CENSUS` schema and full admin access to all tables within that schema (including creating tables, deleting tables, and reading and writing to all tables).
* Read-only access to any tables and views in any schemata that you would like Census to publish to your service destinations.

Redshift permissions are complex and there are many ways to configure access for Census. The script below has been tested with Redshift and is known to work correctly:

```
-- Give the census user the ability to sign in with a password
CREATE USER CENSUS WITH PASSWORD '<strong, unique password>';

-- Create a private bookkeeping schema where Census can store sync state
CREATE SCHEMA CENSUS;

-- Give the census user full access to the bookkeeping schema
GRANT ALL ON SCHEMA CENSUS TO CENSUS;

-- Ensure the census user has access to any objects that may have already existed in the bookkeeping schema
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

1. &#x20;**Fine-grained permissions** – By adding [post-hooks](https://docs.getdbt.com/reference/resource-configs/pre-hook-post-hook#grant-privileges-on-a-directory-of-models) in a dbt project, Census customers immediately grant access to the Census database user after each desired model builds.
2. **Access to all dbt tables and views (Recommended)** – Census customers change the default permissions of the database user for their production dbt runs so that any tables and views created by that users are accessible to the Census database user. In this case, we extend the `ALTER DEFAULT PRIVILEGES` to specifically indicate the defaults of the dbt production run user.&#x20;

```
ALTER DEFAULT PRIVILEGES FOR USER "<your dbt run user> IN SCHEMA "<your dbt target schema>" GRANT SELECT ON TABLES TO CENSUS;
```

Because this is altering the default behavior of another user, this command must be run by a Redshift superuser.

## 💡 Notes

* If you have multiple schemata that you would like Census to read from, repeat the steps for "\<your schema>" for each of them
* In Redshift if there are views in your schema that reference tables in other schemata, you will also need to give Census read access to those other schemata.&#x20;
* If you are using Census models to execute stored procedures (this is rare and not recommended for most users) you may also need to give Census access to those procedures

## 🔑 Encryption

All connections from the Census Data Warehouse Service to your database, as well as connections from your Redshift database to S3, are protected by TLS encryption - Census will refuse to connect to a warehouse that does not support TLS. All Census data stored in S3 is encrypted with AWS Server-Side Encryption (SSE).&#x20;

## 🚦 Allowed IP Addresses

Redshift by default prevents any external IP address from accessing your data warehouse so you will need to add these IP addresses to your security groups. You can find Census's set of IP address for your region in [Regions & IP Addresses](../basics/security-and-privacy/regions-and-ip-addresses.md#ip-addresses). For more information, visit [AWS Redshift Help Center](https://docs.aws.amazon.com/redshift/latest/mgmt/working-with-security-groups.html).

## 🚇 Connecting via SSH tunnel

Census optionally allows connecting to Redshift that are only accessible on private/internal networks via SSH tunneling. To do so, you'll need to provide an SSH host server that is visible on the public internet and can connect to the private warehouse, and you'll also need to be able to perform some basic admin actions on that server.

1. Create a new user account for Census on the SSH host. (This account is separate from the database user account and can have a different username.)
2. On the Census connections page, create a new connection to Redshift enter the warehouse connection details, and then check the 'Use SSH Tunnel' option as shown below.  Fill in the host and port of the SSH host machine along with the name of the user created in the previous step.

![](../.gitbook/assets/redshift\_pg\_1.png)

3\. Once the connection is created, Census will generate a keypair for SSH authentication which can be accessed from the connections page.&#x20;

To install the keypair, copy the public key in Census to you clipboard and add it to the SSH authorized keys file on the SSH host for the user created in the first step.  If, for example, this user is named `census`, the file should be located at`/home/census/.ssh/authorized_keys`. You may need to create this file if it doesn't exist.

Note that the keypair is unique for each Census Warehouse connection. Even if you're reusing the same credentials, you'll need to add the new public keys.

![](../.gitbook/assets/redshift\_pg\_2.png)

4\. If the SSH host restricts IP ranges that can connect to it, add the Census IPs to the allowlist.

With these steps complete, you should be able to complete a connection test, indicating that your tunneled connection is ready to be used in syncs.

## 🌌 Deploying Redshift within an AWS VPC

Advanced methods of Redshift deployment include deploying Redshift within an AWS VPC or private subnet and limiting direct database access to a separate proxy (typically the SSH Tunnel method described above).&#x20;

Census uses the `UNLOAD` command to bulk extract data efficiently (you can read more about our architecture in [How Census Works](https://docs.getcensus.com/basics/security-and-privacy#how-it-works)). By default, Redshift-in-VPC deployments do not allow Redshift to talk to S3. So when using this method, you'll need to separately grant permission to Redshift to communicate directly with S3 by adding an S3 VPC Endpoint.\
\
This is definitely an obscure feature of AWS but this article does a good job of [explaining S3 VPC endpoints](https://tomgregory.com/when-to-use-an-aws-s3-vpc-endpoint/), why they're needed and how to set one up.

## 🚑 Need help connecting to Redshift?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

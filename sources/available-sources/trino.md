---
description: This page describes how to use Trino or Starburst as a source in Census.
---

# Trino

## Getting Started <a href="#getting-started" id="getting-started"></a>

Census can use Trino (and any supported Trino catalog) as a source. Census has been tested with the open-source Trino as well as Starburst Galaxy and Starburst Enterprise.

* Open Census and navigate to the **Sources** page.
* Click **New Source** and select Trino from the list.
* Configure your Trino connection:
  * Enter your Trino host name
  * Enter your Trino user name
  * Enter your Trino password
  * (Optional) If your Trino instance does not run on port 443, enter the port here. Census requires a TLS connection to Trino.
* You’re all set! Head over to the **Syncs** page to activate your data.

#### **How to find your Hostname in Starburst:**&#x20;

Census utilizes JDBC in order to connect to Trino/Starburst. In order to get the correct hostname to input into your Census connection you will want to follow the instructions [linked here in Starburst's documentation](https://docs.starburst.io/clients/gather-connection-information.html#jdbc-connections) to get your JDBC url for your desired cluster.

Once you have the JDBC url you'll only need to input the subdomain into the Census hostname field.&#x20;

**Example JDBC url:** \
`jdbc:trino://census-example-cluster.trino.galaxy.starburst.io:443?user=mytestuser@getcensus.com/accountadmin`\
&#x20;\
**Hostname value to input into Census**\
`census-example-cluster.trino.galaxy.starburst.io`

## :gear: Using the Advanced Sync Engine

Trino supports both of Census' [Sync Engines](../overview.md#sync-engines): Basic and Advanced. In order to use the Advanced Sync Engine with Trino, all of the following must be true:

* Your Trino cluster must have a catalog named `CENSUS` containing a schema named `CENSUS`
* The connector you use for the `CENSUS` catalog must support:
  * `CREATE TABLE` and `DROP TABLE`
  * Table writes, including row-level `INSERT`, `DELETE`, and `UPDATE` operations. Tables that support these operations are sometimes called "transactional" tables in Trino connector documentation, although Census does not require true ACID transactions for the Advanced Sync Engine.
  * The `CREATE OR REPLACE TABLE` statement, which was added to Trino in October 2023 and is available in some Starburst releases (check the release notes for your Starburst Enterprise version or for Starburst Galaxy).
* The account (service account or user) that Census uses to connect to your Trino cluster must have full permissions for the `CENSUS.CENSUS` schema.

We have successfully tested Census' Advanced Sync Engine with the following configurations - it's possible that other configurations are supported, and we encourage you to use the Census connection tester to obtain diagnostics if needed:

* `CENSUS` catalog using the MySQL, Postgres, and Snowflake connectors in read-write mode
* `CENSUS` catalog using the Iceberg connector with S3 object storage and the AWS Glue catalog
* `CENSUS` catalog using the [Starburst Delta Lake](https://docs.starburst.io/latest/connector/delta-lake.html) connector, on both the AWS Glue catalog and the Starburst Galaxy catalog

Census is unable to provide any additional Trino table options (such as location) to the `WITH` clause when creating or managing tables in the `CENSUS` catalog, so please ensure your catalog and schema are configured with any needed default table options.

## Notes

As of December 2023, Warehouse Writeback is not yet supported but is coming soon - please reach out to your Census account executive for details.

## Need help connecting to Trino?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

---
description: >-
  Learn about using data sources to connect to the core data that matters for
  your business.
---

# Overview

Source data for all Census Syncs come from your Data Warehouse. Historically, a
data warehouse was the end of the line, where data went to collect dust. But
modern cloud data warehouses enable a huge variety of data sources and data
size, as well as the flexibility to define how data should be aggregated,
joined, and organized specifically for your business. It's this flexibility and
scalability that make it the perfect data hub for your operations.

At Census, we refer to Data Sources as exactly that - the data warehouse or database that is used as the single source of truth within your organization.

The following pages cover the various data sources that you can connect to with Census.&#x20;

* [Amazon Athena](aws-athena.md)
* [Amazon S3](s3.md)
* [Azure Synapse](azure-synapse.md)
* [Databricks](https://docs.getcensus.com/sources/databricks)
* [Elasticsearch](https://docs.getcensus.com/sources/elasticsearch)
* [Google AlloyDB](alloydb.md)
* [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
* [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
* [MySQL](https://docs.getcensus.com/sources/mysql)
* [Postgres](https://docs.getcensus.com/sources/postgres)
* [Redshift](https://docs.getcensus.com/sources/redshift)
* [Rockset](https://docs.getcensus.com/sources/rockset)
* [Snowflake](https://docs.getcensus.com/sources/snowflake)
* [SQL Server](https://docs.getcensus.com/sources/sql-server)

[Contact us](mailto:support@getcensus.com) if you want Census to support more data sources.

## 🚦Allowed IP Addresses

Most sources require allowlisting IP Addresses so that Census's systems can unload data from the source. [BigQuery](google-bigquery.md) and [Databricks](databricks.md) are notable exceptions, so do check the source-specific docs if you have any questions.

If your source is protected by a firewall, please add Census's IP addresses to the allowlist. You can find Census's set of IP address for your region in [Regions & IP Addresses](../basics/security-and-privacy/regions-and-ip-addresses.md#ip-addresses).

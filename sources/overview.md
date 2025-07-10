---
description: Use data sources to connect to the data that matters most for your business.
---

# Overview

Census connects to a variety of data sources to power your syncs and data activation workflows. These sources include:

* **Data Warehouses & Databases**: Snowflake, BigQuery, Redshift, PostgreSQL, and more
* **SaaS Platforms**: Salesforce, HubSpot, and other business applications
* **Streaming Sources**: Kafka, Confluent Cloud, Google Pub/Sub
* **File Uploads**: CSV files for ad-hoc or one-time data needs

This flexibility allows you to use Census as a Universal Data Platform, unifying data from multiple sources and activating it across your business tools.

The menu to the left lists all of the data sources that Census currently supports. If you don't see your data source listed, please [let us know](mailto:support@getcensus.com)!

## Source Types

### Data Warehouses & Databases

Data warehouses and databases serve as powerful central repositories for your business data. Census connects directly to these sources to leverage your existing data models and transformations.

### SaaS Platforms

SaaS platforms like Salesforce and HubSpot contain valuable business data. Census can create [SaaS Datasets](../datasets/overview/saas-datasets.md) directly from these sources, making it easy to work with your CRM data alongside your warehouse data.

### Streaming Sources

For real-time use cases, Census connects to streaming sources like Kafka and Confluent Cloud. These connections power [Streaming Datasets](../datasets/overview/streaming-datasets.md) that enable low-latency data activation.

### File Uploads

For ad-hoc or one-time data needs, Census supports [CSV Datasets](../datasets/overview/csv-datasets.md) that can be uploaded directly through the UI.

## Data Warehouse-Specific Features

The following sections apply specifically to data warehouse and database connections (Snowflake, BigQuery, Redshift, PostgreSQL, etc.). SaaS, streaming, and file upload sources have different connection methods and considerations, which are detailed in their respective documentation pages.

### ️ Sync Engines for Data Warehouses

When connecting a data warehouse source, Census offers two methods of connecting and keeping track of what's been synced (a.k.a. "state tracking"). We call these Sync Engines. When connecting a data warehouse for the first time, we'll ask you to select either Basic or Advanced Sync Engine.

<figure><img src="../.gitbook/assets/sync-engines.png" alt=""><figcaption><p>Select your preferred Sync Engine when connecting a data warehouse.</p></figcaption></figure>

While **your experience of the Census product will be identical either way**, there are some important differences between these two options:

|                             | Basic Sync Engine                            | Advanced Sync Engine               |
| --------------------------- | -------------------------------------------- | ---------------------------------- |
| **State tracking location** | Census infrastructure                        | Your data warehouse                |
| **Sync performance**        | Slower                                       | Faster                             |
| **Ease of setup**           | Very easy                                    | Slightly more involved             |
| **Warehouse permissions**   | Read-only access                             | Read/write access                  |
| **Ability to switch**       | Ability to upgrade to advanced (coming soon) | Not possible to downgrade to basic |

If you have any questions about which Sync Engine is right for you, please [reach out to our support team](mailto:support@getcensus.com).

### Allowed IP Addresses for Data Warehouses

Most data warehouse sources require allowlisting IP Addresses so that Census's systems can access data from the source. [BigQuery](available-sources/google-bigquery.md) and [Databricks](available-sources/databricks.md) are notable exceptions, so do check the source-specific docs if you have any questions.

If your data warehouse is protected by a firewall, please add Census's IP addresses to the allowlist. You can find Census's set of IP address for your region in [Regions & IP Addresses](../misc/security-and-privacy/regions-and-ip-addresses.md#ip-addresses).

{% hint style="info" %}
For SaaS sources like Salesforce and HubSpot, IP allowlisting is typically not required as Census connects through their APIs using OAuth authentication.
{% endhint %}

### Data Warehouse Usage

Census performs automated processes and queries on your data warehouse, even when a sync isn't running. This activity may appear in your internal reporting but is essential to ensure Census operates efficiently and effectively on your behalf. Census generally has a very minor impact on data warehouse usage.

These processes and queries include and are not limited to:

* Reading metadata from the warehouse
* Regular health check queries
* Clicking into a Dataset
* Clicking into a Segment
* Adding or removing a filter in a Segment
* Segment size refresh
* Previewing a Dataset

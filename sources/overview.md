---
description: Use data sources to connect to the data that matters most for your business.
---

# Overview

Source data for all Census Syncs come from your data warehouse. Historically, a data warehouse was the end of the line, where data went to collect dust. But modern cloud data warehouses enable a huge variety of data sources and data size, as well as the flexibility to define how data should be aggregated, joined, and organized specifically for your business. It's this flexibility and scalability that make it the perfect data hub for your operations.

At Census, we refer to Data Sources as exactly that—the data warehouse or database that is used as the single source of truth within your organization.

The menu to the left lists all of the data sources that Census currently supports. If you don't see your data source listed, please [let us know](mailto:support@getcensus.com)!

## ️ Sync Engines

Census offers two methods of connecting to your data source and keeping track of what's been synced (a.k.a. "state tracking"). We call these Sync Engines. When connecting a data source for the first time, we'll ask you to select either Basic or Advanced Sync Engine.

<figure><img src="../.gitbook/assets/sync-engines.png" alt=""><figcaption><p>Select your preferred Sync Engine when connecting a data source.</p></figcaption></figure>

While **your experience of the Census product will be identical either way**, there are some important differences between these two options:

|                             | Basic Sync Engine                            | Advanced Sync Engine               |
| --------------------------- | -------------------------------------------- | ---------------------------------- |
| **State tracking location** | Census infrastructure                        | Your data warehouse                |
| **Sync performance**        | Slower                                       | Faster                             |
| **Ease of setup**           | Very easy                                    | Slightly more involved             |
| **Warehouse permissions**   | Read-only access                             | Read/write access                  |
| **Ability to switch**       | Ability to upgrade to advanced (coming soon) | Not possible to downgrade to basic |

{% hint style="info" %}
Some data sources (e.g. Google Sheets and Elasticsearch) only support Basic Sync Engine since writing state back to them is either challenging or impossible.
{% endhint %}

If you have any questions about which Sync Engine is right for you, please [reach out to our support team](mailto:support@getcensus.com).

## Allowed IP Addresses

Most sources require allowlisting IP Addresses so that Census's systems can unload data from the source. [BigQuery](google-bigquery.md) and [Databricks](databricks.md) are notable exceptions, so do check the source-specific docs if you have any questions.

If your source is protected by a firewall, please add Census's IP addresses to the allowlist. You can find Census's set of IP address for your region in [Regions & IP Addresses](../basics/security-and-privacy/regions-and-ip-addresses.md#ip-addresses).

## Data Warehouse Usage

Census performs automated processes and queries on your data warehouse, even when a sync isn't running. This activity may appear in your internal reporting but is essential to ensure Census operates efficiently and effectively on your behalf. Census generally has a very minor impact on data warehouse usage.

These processes and queries include and are not limited to:

* Reading Metadata from the warehouse
* Regular health check queries
* Clicking into a Dataset
* Clicking into a Segment
* Adding or removing a filter in a Segment
* Segment size refresh
* Previewing a Dataset

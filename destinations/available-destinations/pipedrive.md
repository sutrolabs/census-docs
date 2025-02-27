---
description: This page describes how to use Census with Pipedrive.
---

# Pipedrive

## Getting Started

In this guide, we will show you how to connect Pipedrive to Census and create your first sync.

{% embed url="https://youtu.be/s3pCULG8Zkg" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Pipedrive account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Azure Synapse](../sources/available-sources/azure-synapse.md)
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Elasticsearch](https://docs.getcensus.com/sources/elasticsearch)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [MySQL](https://docs.getcensus.com/sources/mysql)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)
  * [SQL Server](https://docs.getcensus.com/sources/sql-server)

{% hint style="info" %}
This part of our documentation is still under construction! If you have any questions, please don't hesitate to [contact us](mailto:support@getcensus.com).
{% endhint %}

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | Identifiers                   | **Behaviors**    |
| --------------: | :------------: | ----------------------------- | ---------------- |
|    Organization |        ✅       | Object ID, name               | Update or Create |
|          Person |        ✅       | Object ID, name, email, phone | Update or Create |
|            Lead |        ✅       | Object ID, name, email, phone | Update or Create |
|            Deal |        ✅       | Object ID, title              | Update or Create |
|            Note |        ✅       | Unique ID                     | Add              |
|        Activity |        ✅       | Unique ID                     | Send             |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/core-concept/#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Pipedrive objects and/or behaviors

## Need help connecting to Pipedrive?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

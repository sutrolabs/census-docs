---
description: This page describes how to use Census with Shopify.
---

# Shopify

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Shopify to Census.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Shopify account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Azure Synapse](../sources/azure-synapse.md)
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Elasticsearch](https://docs.getcensus.com/sources/elasticsearch)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [MySQL](https://docs.getcensus.com/sources/mysql)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)
  * [SQL Server](https://docs.getcensus.com/sources/sql-server)

### :electric\_plug:Connecting Shopify

There is some setup that is needed to do on the Census side to setup Shopify, while this process is under construction :construction\_site:, please [contact us](mailto:support@getcensus.com) via email or start a conversation with us via the [in-app](https://app.getcensus.com) chat with the topic: "Shopify Setup". In your communication please provide your Shopify Store URL so we can get started on your set up!

## 🗄 Supported Objects

Census currently supports syncing to the following Shopify objects ([Contact us](mailto:support@getcensus.com) if you're looking for more!):

| **Object Name** |       **Supported?**      | **Identifiers** |
| --------------: | :-----------------------: | --------------- |
|        Customer |             ✅             | Email           |
| Inventory Level |             ✅             |                 |
|           Order |             ✅             | Source ID       |
|         Product |             ✅             | Tag ID, Handle  |
|   Product Image | <p>✅<br>(via Product)</p> |                 |
| Product Variant |             ✅             | SKU             |

Census also supports Shopify's Custom Metafields on Customer and Product as well.

#### Updating Product Images

Census supports setting product images by passing a [structured-data.md](../basics/data-models-and-entities/defining-source-data/structured-data.md "mention") Array to the `images` field on the Product. The images array needs to be a set of one more objects that contain URLs to each image you want to upload. It should look something like the following:

```
[
  { 
    "position": 1, 
    "src": "https://via.placeholder.com/300.png?text=iPod%20Nano,%208GB", 
    "width": 640, 
    "height": 480 
  }
]
```

Only the `src` field is required. `position`, `width`, and `height` are optional.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|    **Behaviors** | **Supported?** |                **Objects**                |
| ---------------: | :------------: | :---------------------------------------: |
| Update or Create |        ✅       | Customer, Inventory Level, Order, Product |
|      Update Only |        ✅       |                   Order                   |
|           Mirror |        ✅       |              Product Variant              |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Shopify.

## 🚑 Need help connecting to Shopify?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

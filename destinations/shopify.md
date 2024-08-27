---
description: This page describes how to use Census with Shopify.
---

# Shopify

## Getting Started

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
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)
  * [SQL Server](https://docs.getcensus.com/sources/sql-server)

### :electric\_plug:Connecting Shopify

{% hint style="info" %}
Note: Census will only query Shopify based on the syncs/objects that you configure
{% endhint %}

1.  Census connects via OAuth, so you need a Shopify user that can login to the instance with the following permission scopes:

    | write\_products                               | read\_products                               |
    | --------------------------------------------- | -------------------------------------------- |
    | write\_customers                              | read\_customers                              |
    | write\_orders                                 | read\_orders                                 |
    | write\_inventory                              | read\_inventory                              |
    | write\_fulfillments                           | read\_fulfillments                           |
    | write\_assigned\_fulfillment\_orders          | read\_assigned\_fulfillment\_orders          |
    | write\_merchant\_managed\_fulfillment\_orders | read\_merchant\_managed\_fulfillment\_orders |
    | write\_third\_party\_fulfillment\_orders      | read\_third\_party\_fulfillment\_orders      |
2. There is some setup that is needed to do on the Census side to setup Shopify, while this process is under construction :construction\_site:, please [contact us](mailto:support@getcensus.com) via email or start a conversation with us via the [in-app](https://app.getcensus.com) chat with the topic: "Shopify Setup". In your communication please provide your Shopify Store URL so we can get started on your set up!

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Census currently supports syncing to the following Shopify objects and Sync Behaviors ([Contact us](mailto:support@getcensus.com) if you're looking for more!):

| **Object Name** | **Supported?** | **Sync Keys**         | **Behaviors**                 |
| --------------: | :------------: | --------------------- | ----------------------------- |
|        Customer |        ✅       | Email                 | Update or Create              |
|     Fulfillment |        ✅       | Any unique identifier | Add                           |
| Inventory Level |        ✅       | N/A                   | Update or Create              |
|           Order |        ✅       | Source ID             | Update or Create, Update Only |
|         Product |        ✅       | Tag ID, Handle        | Update or Create              |
| Product Variant |        ✅       | SKU                   | Mirror                        |

Census also supports Shopify's Custom Metafields on Customer and Product as well.

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Shopify objects and/or behaviors.

#### Updating Product Images

Census supports setting product images by passing an [Array](../basics/data-defining/defining-source-data/structured-data.md) to the `images` field on the Product. The images array needs to be a set of one more objects that contain URLs to each image you want to upload. It should look something like the following:

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

## Need help connecting to Shopify?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

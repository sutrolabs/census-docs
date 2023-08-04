---
description: This page describes how to use Census with Segment.
---

# Segment

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Segment to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Segment account ready.
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

## Segment Sync Setup

### 1. Create or get a Segment Write key

{% hint style="info" %}
Segment Documentation on Write Keys are [here](https://segment.com/docs/connections/find-writekey/).
{% endhint %}

* Create a new HTTP API Source in the Connections page of Segment (found under "Server")
* Name your connection and optionally label it (We recommend "Census" for ease of debugging)
* Copy your write key from the saved connection
* Navigate to the [Destinations Page](https://app.getcensus.com/destinations) of Census, click on the "New Destination" button and select Segment, and past the created token in the designated field

![](<../.gitbook/assets/Screen Shot 2021-11-12 at 11.16.21 AM.png>)

* Census will convert this right here and now you're all set with the Segment Connection!

![Don't worry if the credential here is different!](<../.gitbook/assets/Screen Shot 2021-11-12 at 11.16.53 AM.png>)

Note: Census's permissions will be the same as this Segment token.

### 2. Connect your data warehouse

If you don't already have a data warehouse connected, follow one of our short guides depending on your data warehouse service:

* [Databricks](https://docs.getcensus.com/sources/databricks)
* [Elasticsearch](../sources/elasticsearch.md)
* [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
* [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
* [Postgres](https://docs.getcensus.com/sources/postgres)
* [Redshift](https://docs.getcensus.com/sources/redshift)
* [Rockset](https://docs.getcensus.com/sources/rockset)
* [Snowflake](https://docs.getcensus.com/sources/snowflake)

You should now have a connection to Segment and to your data warehouse! Let's start syncing user data.

### 3. Create your first Model <a href="#3-create-your-first-model" id="3-create-your-first-model"></a>

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models).​‌

Here you will have to write SQL queries to select the data you want to join to a Segment User. Here are some ideas of data you should select‌.

* User with product usage properties
* User with the organization they are associated to
* User with the classification coming from a User Classification model

### 4. Create your first Sync <a href="#4-create-your-first-sync" id="4-create-your-first-sync"></a>

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button‌.

In the " **What data do you want to sync?"** section‌

* For the **Connection**, select the data warehouse you connected in step 2
* For the **Source,** select the model you created in step 3

Next up is the **"Where do you want to sync data to?"** section‌

* Pick the name of Segment service from step 1 as **the Connection**, right now the object we can sync to is [limited to **User**](segment.md#supported-objects)

For the " **How should changes to the source be synced?"** section‌

* **Update or Create** will be preselected as it is [supported](segment.md#supported-sync-behaviors)
* Pick the right mapping key, we can sync based on userId from the Segment Identify call or to the device: AnonymousId

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section‌.

* Here simply map the fields from your model to the Segment User Properties you want to sync to. You can specify specific properties or "Sync All Properties" such that new columns in the source table will be created on the Segment User object according to the normalization rule you apply :magic\_wand:

The end result should look something like this​:

![](<../.gitbook/assets/Screen Shot 2021-11-12 at 11.37.07 AM.png>)

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync‌.

That's it! In 4 steps, you've connected Segment and started syncing user properties data from your warehouse 🎉

## 🗄 Supported Objects

Segment support is pretty straight forward! [Let us know](mailto:support@getcensus.com) if you want Census to support more objects for Segment.

| **Object Name** | **Supported?** |
| :-------------: | :------------: |
|       User      |        ✅       |
|  Track (Event)  |        ✅       |

#### Syncing track events

Like most [events.md](../basics/data-models-and-entities/defining-source-data/events.md "mention"), Segment Track Events have the standard set of fields. Though the `event` type field is the only required field, you should typically set at least all the standard event fields.

* `event` (required) - This is the event type field
* `anonymousId` or `userId` (one of these required) - This indicates which user caused or triggered the event
* `timestamp` - The time the event occurred. If not provided, Segment will use their server time when the event was received by them (which can be quite different from when it happened, particularly if you're using Census to backfill events).
* `properties` - Acts as a Properties bundle. See[#using-the-properties-bundle](../basics/data-models-and-entities/defining-source-data/events.md#using-the-properties-bundle "mention") for more information.
* `context` and `integrations` - Optional event context and controls. See [structured-data.md](../basics/data-models-and-entities/defining-source-data/structured-data.md "mention") for more information on how to create objects to map to these fields.

For more information on the meaning of different Segment fields, take a look at their [documentation](https://segment.com/docs/connections/spec/track/).

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** |  **Objects**  |
| -------------------: | :------------: | :-----------: |
| **Update or Create** |        ✅       |      User     |
|           **Append** |        ✅       | Track (Event) |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Segment.

## 🚑 Need help connecting to Segment?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

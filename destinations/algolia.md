---
description: This page describes how to use Census with Algolia.
---

# Algolia

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Algolia to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Algolia account ready.
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

### 1. Collect your Algolia Credentials

Census needs the following information to create an Algolia connection:

* **Application ID**
* **Admin API Key**

To find these credentials in Algolia confirm you are in the correct app you want to connect with Census then navigate to the **Settings** page then click on the **API Keys** tab under **Teams & Access.**

### 2. Connect Algolia in Census

* In Census, navigate to [Connections](https://app.getcensus.com/connections)
* Click the **Add Service** button
* Select Algolia in the dropdown list
* Enter your credentials and click **Connect**

![](<../.gitbook/assets/Screen Shot 2022-04-01 at 2.42.38 PM.png>)

### 3. Create your Model

Navigate to the [Models](https://app.getcensus.com/models)

Here you can write SQL queries or select dbt models that contain the data you want to see in Algolia. Here are some ideas of data you should select:

* Users that can be added as "friends"
* Products that are searchable in an E-commerce app
* Locations that you have for a destination stay

Once you have created your model, click save.&#x20;

![](<../.gitbook/assets/Screen Shot 2022-01-27 at 3.31.32 PM (1).png>)

### 4. Create your first Sync

Now head to the [Syncs page](https://app.getcensus.com/syncs) and click the Add Sync button, which will take you to a step-by-step wizard for building a data mapping.

In the "**What data do you want to sync?**" section

* For the Connection, select the data warehouse you'd like to use
* For the Source, select your one of your models or connect directly to a table within your data warehouse

![](<../.gitbook/assets/Screen Shot 2022-04-01 at 2.55.41 PM.png>)

Next up is the "**Where do you want to sync data to?**" section

* Pick Algolia as the Connection
* Pick the Algolia Index you want to sync to as the Object

![](<../.gitbook/assets/Screen Shot 2022-04-01 at 2.56.24 PM.png>)

For the "**How should changes to the source be synced?**" section&#x20;

* Select **Update Or Create**
* Pick the appropriate mapping key, it should be a field where there is a unique value for each record

![](<../.gitbook/assets/Screen Shot 2022-04-01 at 2.57.28 PM.png>)

Finally, select the fields you want to update in the mapper in the "**Which Fields should be updated?**" section

* For each field in your Algolia instance, you can choose a column from your model.

![](<../.gitbook/assets/Screen Shot 2022-04-01 at 2.59.16 PM.png>)

Click the Next button to see a preview of what will happen when you start the sync. You can check the "Run Sync Now" checkbox to kick off an initial sync and pick a schedule afterwards.

### 5. Confirm the data is in Algolia

Now go back to Algolia and go view an object in an Index that should have been updated. If everything went well, you should see your data in Algolia.

That's it, in 5 steps, you connected Census to Algolia and made data from your warehouse searchable by users using Algolia 🎉

If you have any questions or if you have any issues getting started, please contact us via the in-app live chat in the bottom right corner or send us an email at support@getcensus.com

## 🗄️ Supported Objects

Algolia stores data within collections called Indices. Your Indices in Algolia can be used as objects to sync to from Census.&#x20;

| **Object Name** | **Supported?** | **Identifiers** |
| --------------: | :------------: | :-------------: |
|           Index |        ✅       |    Object ID    |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Algolia.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects** |
| -------------------: | :------------: | :----------: |
| **Update or Create** |        ✅       |     Index    |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Algolia.

## 🚑 Need help connecting to Algolia?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

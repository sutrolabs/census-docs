---
description: Learn how to use Census with Sailthru
---

# Sailthru

## 🏃‍♂️ Getting started

This guide shows you how to use Census to connect your Sailthru Account to your data warehouse and create your first sync.

### **Prerequisites**

Before you begin, you'll need the following:

* Census account: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* Sailthru account: so that you can copy the API key.
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

### Step 1: Connect Sailthru

1. Log into Census and navigate to [Destinations](https://app.getcensus.com/destinations).
2. Click **New Destination**.
3. Select Sailthru from the dropdown list.
4. Follow the Sailthru authentication flow, see below screenshots where to find your credentials.

![Click on the Lock](<../.gitbook/assets/API and Postbacks Sailthru.png>) ![Copy and paste from here into Census](<../.gitbook/assets/API Key and Secret.png>)

![Paste into the Corresponding fields and hit "Connect"](<../.gitbook/assets/Census Sailthru Configuration.png>)

Your end state should look something like this: 👇

![You are tested and ready to go](<../.gitbook/assets/Sailthru Tested.png>)

### Step 2: Connect your data source

The steps for connecting your data source will depend on your technology. See the following guides:

* [Databricks](../sources/databricks.md)
* [Elasticsearch](../sources/elasticsearch.md)
* [Google BigQuery](../sources/google-bigquery.md)
* [Google Sheets](google-sheets.md)
* [MySQL](../sources/mysql.md)
* [Postgres](../sources/postgres.md)
* [Redshift](../sources/redshift.md)
* [Rockset](../sources/rockset.md)
* [Snowflake](../sources/snowflake.md)
* [SQL Server](../sources/sql-server.md)

### Step 3: Create your model

When defining models, you'll write SQL queries to select the data you want to see in Sailthru. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the **Models** page.
2. Enter a name for your model. You'll use this to select the model later.
3. Enter your SQL query. If you want to test the query, use the **Preview** button.
4. Click **Save Model**.

{% hint style="info" %}
You can also use [dbt](../basics/data-models-and-entities/models/native-dbt-integration.md), [Looker](../basics/data-models-and-entities/models/looker.md), or [Segments](broken-reference/) as other source models. And you can also use a Warehouse Table/View.
{% endhint %}

### Step 4: Create your first sync

The sync will move data from your warehouse to Sailthru. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose Sailthru as the **Connection** and an **Object** from the Sailthru [Supported Objects](sailthru.md#supported-objects).
4. Under **How should changes to the source be synced?**, choose among our [Supported Sync Behaviors](sailthru.md#supported-sync-behaviors).
5. Under **How are source and destination records matched?**, select a mapping key. See [Supported Objects](sailthru.md#supported-objects) for details for options.
6. Under **Which properties should be updated?**, select the fields you want to update by mapping a field in Sailthru to a column in your model.
7. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
8. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
9. Click **Create Sync**.

When configuring your sync, the page should look something like this: 👇

### Step 5: Confirm the synced data in Sailthru

Once your sync is complete, it's time to check your data. Open Sailthru and check that the records updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to Sailthru! [🥳️](https://emojikeyboard.org/copy/Partying\_Face\_Emoji\_%F0%9F%A5%B3%EF%B8%8F?utm\_source=extlink)

And if anything went wrong, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## 🗄 Supported objects

| **Object Name** | **Supported?** | **Sync Keys** |
| --------------: | :------------: | --------------- |
|            User |        ✅       | Email           |
|            List |       🔜       |                 |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional objects for Sailthru.

## 🔄 Supported sync behaviors

|     **Behavior** | **Supported?** | **Objects** |
| ---------------: | :------------: | :---------: |
| Update or Create |        ✅       |     User    |
|      Update Only |       `✅`      |     User    |

{% hint style="info" %}
Learn about all of our sync behaviors in [Core Concepts](../basics/core-concept/#sync-behaviors).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Sailthru.

## 🚑 Need help connecting to Sailthru?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

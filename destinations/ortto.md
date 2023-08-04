---
description: This page describes how to use Census with Ortto.
---

# Ortto

## 🏃‍♀️ Getting started

This guide shows you how to use Census to connect your Ortto account to your data warehouse and create your first sync.

### Prerequisites

Before you begin, you'll need the following:

* **Census account**: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* **Ortto account**
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

### Step 1: Connect Ortto

1. Log into Census and Navigate to [Destinations](https://app.getcensus.com/destinations).
2. Click **New Destination**.
3. Select **Ortto** from the dropdown list.
4. Ortto uses API keys to authorize access to the API, so you will need to provide an **API Key** to Census.
   1. You can create an API key in Ortto specifically for Census. On the left-hand menu click **More** > **Data Sources.** On the Data Sources page click the **New Data Source** button then select **Custom API (advanced).** Give the source a name of your choosing and click **Create.** The API Key will be shown on the following page. Make sure to save it somewhere secure.
   2. Copy the API key and paste it into the **API Key** field in the Ortto setup in Census.
   3. Ortto has custom rate limiting based on what plan you're on. You can check out the limits for your specific plan [here](https://help.ortto.com/developer/latest/developer-guide/rate-limits.html). Enter the limit for the 60s interval of your plan in the **Rate limit per 60s** field. If no limit is specified we will default to the Pro plan (600 requests/min).

### Step 2: Connect your data warehouse

The steps for connecting your data warehouse will depend on your technology. See the following guides:

* [Databricks](https://docs.getcensus.com/sources/databricks)
* [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
* [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
* [Postgres](https://docs.getcensus.com/sources/postgres)
* [Redshift](https://docs.getcensus.com/sources/redshift)
* [Rockset](https://docs.getcensus.com/sources/rockset)
* [Snowflake](https://docs.getcensus.com/sources/snowflake)

### Step 3: Create your model

When defining models, you'll write SQL queries to select the data you want to see in Ortto. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the [**Models**](https://app.getcensus.com/models) page.
2. Enter a name for your model. You'll use this to select the model later.
3. Enter your SQL query. If you want to test the query, use the **Preview** button.
4. Click **Save Model**.

![Basic SQL query for a new model](<../.gitbook/assets/image (22) (1).png>)

### Step 4: Create your first sync <a href="#step-4-create-your-first-sync" id="step-4-create-your-first-sync"></a>

The sync will move data from your warehouse to Ortto. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose Ortto as the **Connection** and an **Object** in Ortto. (See [Supported Objects](ortto.md#supported-objects).)
4. Under **How should changes to the source be synced?**, choose **Update or Create**. (See [Supported Sync Behavior](ortto.md#supported-sync-behaviors).)
5. Under **How are source and destination records matched?**, select a mapping key. (See [Supported Objects](ortto.md#supported-objects) for details.)
6. Under **Which properties should be updated?**, select the fields you want to update by mapping a field in Ortto to a column in your model.
7. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
8. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
9. Click **Create Sync**.

When configuring your sync, the page should look something like this: 👇

![Sync setup for Ortto](<../.gitbook/assets/Ortto Create Sync Screenshot.png>)

### Step 5: Confirm the synced data in Ortto

Once your sync is complete, it's time to check your data. Open Ortto and check that the records updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to Ortto! 🎉

And if anything went wrong, [contact the Census support team](mailto:support@getcensus.com) to get some help.

## 🏎 Sync Speed

Sync speeds can be affected by API rate limiting from the destination app. Ortto has a number of different rate limiting criteria for their API depending on IP, Ortto tier, responses, and payloads. (See [Ortto API Documentation](https://help.ortto.com/developer/latest/developer-guide/rate-limits.html) for details.)

In most cases, you won't run into any issue with sync speed based on rate limiting unless:

* You're running an initial sync action that will update many records in Ortto.
* You have another integration or service that's making API calls to Ortto and using the same API key.

## 🗄 Supported objects

| **Object Name** | **Supported?** | **Sync Keys**    |
| --------------: | :------------: | ------------------ |
|    Organization |        ✅       | Name, Website      |
|          Person |        ✅       | Email, External ID |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional objects for Ortto.

## 🔄 Supported Sync Behaviors

{% hint style="warning" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** |      **Objects**     |
| -------------------: | :------------: | :------------------: |
| **Update or Create** |        ✅       | Organization, Person |
|      **Update Only** |        ✅       |        Person        |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for Ortto.

## 🚑 Need help connecting to Ortto?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

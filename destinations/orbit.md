---
description: This page describes how to use Census with Orbit.
---

# Orbit

## Getting started

This guide shows you how to use Census to connect your Orbit account to your data warehouse and create your first sync.

### Prerequisites

Before you begin, you'll need the following:

* **Census account**: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* **Orbit account**
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

### Step 1: Connect Orbit

1. Log into Census and navigate to [Destinations](https://app.getcensus.com/destinations).
2. Click **New Destination**.
3. Select **Orbit** from the dropdown list.
4. Orbit uses API tokens to authorize access to the API, so you will need to provide an **API Key** and **Workspace Slug** to Census.
   1. You can find your API token on the [Account Settings](https://app.orbit.love/user/settings/edit) page, in the API Tokens section. Copy the API token and paste it into the **API Key** field in the Orbit setup in Census.
   2. The workspace slug can be fetched from the URL. In the url provided below, **census** is the workspace slug. https://app.orbit.love/census. Copy the workspace slug and paste it into the **Workspace Slug** field in the Orbit setup in Census.

### Step 2: Connect your data warehouse

The steps for connecting your data warehouse will depend on your technology. See the following guides:

* [Databricks](https://docs.getcensus.com/sources/databricks)
* [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
* [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
* [Postgres](https://docs.getcensus.com/sources/postgres)
* [Redshift](https://docs.getcensus.com/sources/redshift)
* [Snowflake](https://docs.getcensus.com/sources/snowflake)

### Step 3: Create your model

When defining models, you'll write SQL queries to select the data you want to see in Orbit. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the [**Models**](https://app.getcensus.com/models) page.
2. Enter a name for your model. You'll use this to select the model later.
3. Enter your SQL query. If you want to test the query, use the **Preview** button.
4. Click **Save Model**.

![Basic SQL query for a new model](<../.gitbook/assets/image (22) (1).png>)

### Step 4: Create your first sync <a href="#step-4-create-your-first-sync" id="step-4-create-your-first-sync"></a>

The sync will move data from your warehouse to Orbit. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose Orbit as the **Connection** and an **Object** in Orbit. (See [Supported Objects](outreach.md#supported-objects).)
4. Under **How should changes to the source be synced?**, choose **Update or Create**. (See [Supported Sync Behaviors](outreach.md#supported-sync-behaviors).)
5. Under **How are source and destination records matched?**, select a mapping key. (See [Supported Objects](outreach.md#supported-objects) for details.)
6. Under **Which properties should be updated?**, select the fields you want to update by mapping a field in Orbit to a column in your model.
7. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
8. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
9. Click **Create Sync**.

When configuring your sync, the page should look something like this: 👇

![Sync setup for Orbit](<../.gitbook/assets/Screen Shot 2022-04-05 at 11.24.56 AM.png>)

### Step 5: Confirm the synced data in Orbit

Once your sync is complete, it's time to check your data. Open Orbit and check that the records updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to Orbit! 🎉

And if anything went wrong, contact the support team to get some help.

## 🐎 Sync Speed

Sync speeds can be affected by API rate limiting from the destination app. Orbit allows an API call rate of up to 120 calls per minute, per IP. (See [Orbit API Documentation](https://docs.orbit.love/reference/rate-limiting) for details.)

In most cases, you won't run into any issue with sync speed based on rate limiting unless:

* You're running an initial sync action that will update many records in Orbit.
* You have another integration or service that's making API calls to Orbit and using the same API Token.

## 📚 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|  **Object Name** | **Supported?** | **Sync Keys**                | **Behaviors**    |
| ---------------: | :------------: | ---------------------------- | ---------------- |
|           Member |        ✅       | Name, Email, Github, Twitter | Update or Create |
| Content Activity |        ✅       | N/A                          | Send             |
|  Custom Activity |        ✅       | Activity Key                 | Send             |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

Contact the support team if you want Census to support more Orbit objects and/or behaviors

## Need help connecting to Orbit?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

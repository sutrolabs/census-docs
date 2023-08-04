---
description: This page describes how to use Census with Twitter Ads.
---

# Twitter

## 🏃‍♂️ Getting started

This guide shows you how to use Census to connect your Twitter Ads account to your data warehouse and create your first sync.

### **Prerequisites**

Before you begin, you'll need the following:

* Census account: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* Twitter Ads account
* Credentials for your data warehouse: For details, see the guide for your [specific data source technology](twitter.md#step-2-connect-your-data-warehouse).

### Step 1: Connect Twitter Ads Account

1. Log into Census and navigate to [Connections](https://app.getcensus.com/connections).
2. Click **Add Service**.
3. Select **Twitter** from the dropdown list.
4. Follow the Twitter authentication flow.

Your end state should look something like this: 👇

![Connections page after setting up connection to Twitter Ads](../.gitbook/assets/202206\_Twitter\_Connection.png)

### Step 2: Connect your data warehouse

The steps for connecting your data warehouse will depend on your technology. See the following guides:

* [Databricks](../sources/databricks.md)
* [Google BigQuery](../sources/google-bigquery.md)
* [Google Sheets](google-sheets.md)
* [Postgres](../sources/postgres.md)
* [Redshift](../sources/redshift.md)
* [Snowflake](../sources/snowflake.md)

After setting up your warehouse, your Connections page should look something like this: 👇

![Connections page after setting up a data source](../.gitbook/assets/202110\_Connections\_Generic.png)

### Step 3: Create your model

When defining models, you'll write SQL queries to select the data you want to see in Twitter Ads. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the **Models** page.
2. Enter a name for your model. You'll use this to select the model later.
3. Enter your SQL query. If you want to test the query, use the **Preview** button.
4. Click **Save Model**.

![Basic SQL query for a new model](../.gitbook/assets/202201\_Model\_Page.png)

### Step 4: Create your first sync

The sync will move data from your warehouse to Twitter Ads. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose **Twitter** as the **Connection** and an **Object** in Twitter Ads. Based on the selected object, your sync options will vary. See [Supported Objects](twitter.md#supported-objects)
4. (When syncing conversion events) Under **How do you want to update the destination?**, choose **Append**. See [Supported sync behaviors](twitter.md#supported-sync-behaviors).
5. (When syncing conversion events) Under **How are source records identified?**, select a column from the model that serves as a unique ID for each record. If needed, turn on the **Use timestamp column** setting and select a property from the model. This setting allows the sync to skip records that have not changed (according to the timestamp) since the last sync.
6. (When syncing audiences) Under **How should we identify audience members?**, specify how Census should match audience members in Twitter Ads to records in the model.
7. (When syncing audiences) Under **Audience Sync**, select an existing Twitter Ads audience or create a new audience list in Twitter Ads. If the audience list includes members that don't have matching records in your model, Census will remove those members from the list.
8. Under **Which properties should be updated?**, select the fields you want to update by mapping a field in Twitter Ads to a column in your model.
9. (When syncing conversion events) Under **Should existing data be synced?**, choose whether to sync existing records (**Backfill All Records**) or only sync new records going forward (**Skip Current Records**).
10. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
11. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
12. Click **Create Sync**.

When configuring your sync, the page should look something like this: 👇

![Setting up a Twitter Ads sync with a new audience list](../.gitbook/assets/202206\_Twitter\_Sync\_Details.png)

### Step 5: Confirm the synced data in Twitter Ads

Once your sync is complete, it's time to check your data. Open Twitter Ads and check that the records updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to Twitter Ads! [🥳️](https://emojikeyboard.org/copy/Partying\_Face\_Emoji\_%F0%9F%A5%B3%EF%B8%8F?utm\_source=extlink)

And if anything went wrong, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## 🏎 Sync speed & limits

Rate limits affect how many records you can sync in a specific period of itme. Twitter Ads API has a rate limit of 1,500 calls per minute. Calls to sync audience data and conversion event data share the same rate limit.

### Conversion Events: Use timestamp setting

When syncing data to conversion events, the **Use timestamp column to identify new data** setting can help limit the number of API calls. With this setting, Census will check if the record has changed since the last sync occurred and skip syncing for the record if there have been no changes.

To use this setting, you'll also need to include a column in your database/data source that tracks the latest sync for each record.

## 🗄 Supported objects

|  **Object Name** | **Supported?** | **Sync Keys**                                                        |
| ---------------: | :------------: | ---------------------------------------------------------------------- |
|         Audience |        ✅       | Email, Handle, Device ID                                               |
| Conversion Event |        ✅       | App ID, Conversion Time, Conversion Type, Hashed Device ID, OS Typees} |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional objects for Twitter Ads.

## 🔄 Supported sync behaviors

| **Behavior** | **Supported?** |    **Objects**   |
| -----------: | :------------: | :--------------: |
|       Append |        ✅       | Conversion Event |
|       Mirror |        ✅       |     Audience     |

{% hint style="info" %}
Learn about all of our sync behaviors in [Core Concepts](../basics/core-concept/#sync-behaviors).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Twitter Ads.

## 🚑 Need help connecting to Twitter Ads?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

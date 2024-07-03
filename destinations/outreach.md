---
description: This page describes how to use Census with Outreach.
---

# Outreach

## Getting started

This guide shows you how to use Census to connect your Outreach account to your data warehouse and create your first sync.

### Prerequisites

Before you begin, you'll need the following:

* **Census account**: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* **Outreach account**: We recommend using a dedicated service account with Admin user profile privileges. (See [Required Permissions](outreach.md#required-permissions).)
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

### Step 1: Connect Outreach

1. Log into Census and navigate to [Destinations](https://app.getcensus.com/destinations).
2. Click **New Destination**.
3. Select **Outreach** from the dropdown list.
4. Follow the Outreach authentication flow, which will ask you to log in with your Outreach username and password.

Your end state should look something like this. 👇

![Destinations page with Outreach](../.gitbook/assets/202109\_Service\_Connection\_Outreach.png)

### Step 2: Connect your data warehouse

The steps for connecting your data warehouse will depend on your technology. See the following guides:

* [Databricks](https://docs.getcensus.com/sources/databricks)
* [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
* [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
* [Postgres](https://docs.getcensus.com/sources/postgres)
* [Redshift](https://docs.getcensus.com/sources/redshift)
* [Rockset](https://docs.getcensus.com/sources/rockset)
* [Snowflake](https://docs.getcensus.com/sources/snowflake)

After connecting your warehouse, your **Destinations** page will look something like this: 👇

![Destinations page with data warehouse and Outreach](<../.gitbook/assets/202109\_Connections\_Outreach (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)

### Step 3: Create your model

When defining models, you'll write SQL queries to select the data you want to see in Outreach. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the [**Models**](https://app.getcensus.com/models) page.
2. Enter a name for your model. You'll use this to select the model later.
3. Enter your SQL query. If you want to test the query, use the **Preview** button.
4. Click **Save Model**.

![Basic SQL query for a new model](../.gitbook/assets/202109\_Outreach\_Basic\_Model.png)

### Step 4: Create your first sync <a href="#step-4-create-your-first-sync" id="step-4-create-your-first-sync"></a>

The sync will move data from your warehouse to Outreach. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose Outreach as the **Connection** and an **Object** in Outreach. (See [Supported Objects](outreach.md#supported-objects).)
4. Under **How should changes to the source be synced?**, choose **Update or Create**. (See [Supported Sync Behaviors](outreach.md#supported-sync-behaviors).)
5. Under **How are source and destination records matched?**, select a mapping key. (See [Supported Objects](outreach.md#supported-objects) for details.)
6. Under **Which properties should be updated?**, select the fields you want to update by mapping a field in Outreach to a column in your model.
7. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
8. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
9. Click **Create Sync**.

When configuring your sync, the page should look something like this: 👇

![Sync setup for Outreach](<../.gitbook/assets/202109\_sync\_details (1).png>)

#### Custom Fields in Outreach

Although the sync can update custom fields in Outreach, these fields will show up as _Custom#_ rather than using the custom field name. You may need to visit the custom field configuration in Outreach settings to check the field number.

![Sync setup displays custom fields without the custom field name](../.gitbook/assets/202110\_Custom\_Fields\_Outreach.png)

### Step 5: Confirm the synced data in Outreach

Once your sync is complete, it's time to check your data. Open Outreach and check that the records updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to Outreach! 🎉

And if anything went wrong, [contact the Census support team](mailto:support@getcensus.com) to get some help.

## Sync speed

Sync speeds can be affected by API rate limiting from the destination app. Outreach allows an API call rate of up to 10,000 calls per hour, per user. (See [Outreach API Documentation](https://api.outreach.io/api/v2/docs) for details.)

In most cases, you won't run into any issue with sync speed based on rate limiting unless:

* You're running an initial sync action that will update many records in Outreach.
* You have another integration or service that's making API calls to Outreach and using the same user account.

## Supported objects

| **Object Name** | **Supported?** | **Sync Keys**                       |
| --------------: | :------------: | ----------------------------------- |
|         Account |        ✅       | any Text field                      |
|        Prospect |        ✅       | Email (recommended), any Text field |
|            User |        ✅       | Email (recommended), any Text field |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional objects for Outreach.

## Supported sync behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

|     **Behavior** | **Supported?** | **Objects** |
| ---------------: | :------------: | ----------- |
| Update or Create |        ✅       | All         |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Outreach.

## Email Identifier Formatting:

If you are using email as an identifier to sync to Prospects or Users Outreach requires the data to be formatted as an array.&#x20;

You'll need to format your email identifiers in your source data to follow the format `["email@example.com"]`

Please also note that your source column should still be typed as a text based column as Census only pulls in text or numeric source columns as available options for sync identifiers.

## 🔑 Required permissions

We recommend authenticating your Outreach connection with an Outreach user that has the standard Admin governance profile.

If using another profile, the profile must include permissions to view, create, and edit all records for the synced objects. See [Outreach Support](https://support.outreach.io/hc/en-us/articles/219027188-Creating-and-Assigning-Governance-Profiles) for details on user governance settings.

## Need help connecting to Outreach?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

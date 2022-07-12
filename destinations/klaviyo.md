---
description: This page describes how to use Census with Klaviyo.
---

# Klaviyo

## 🏃‍♀️ Getting Started

This guide shows you how to use Census to connect your Klaviyo account to your data warehouse and create your first sync.

{% embed url="https://youtu.be/U8q7E2SZJkI" %}

### Prerequisites

Before you begin, you'll need the following:

* Census account: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* Klaviyo account
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

### Step 1: Connect Klaviyo

1. Log into Census and navigate to [**Connections**](https://app.getcensus.com/connections).
2. Click **Add Service**.
3. Select Klaviyo from the dropdown list.
4. Paste in your Klaviyo API Key. (See [Klaviyo's Help Center](https://help.klaviyo.com/hc/en-us/articles/115005062267-How-to-Manage-Your-Account-s-API-Keys) for details on finding or generating API keys.)

Your end state should look something like this: 👇

![Connections page with Klaviyo](<../.gitbook/assets/202201\_Klaviyo\_Connection (1).png>)

### Step 2: Connect your data warehouse

The steps for connecting your data warehouse will depend on your technology. See the following guides:

* [Databricks](../sources/databricks.md)
* [Google BigQuery](../sources/google-bigquery.md)
* [Google Sheets](../sources/google-sheets.md)
* [Postgres](../sources/postgres-1.md)
* [Redshift](../sources/redshift.md#allowed-ip-addresses)
* [Snowflake](../sources/snowflake.md)

After setting up your warehouse, your Connections page should look something like this: 👇

![Connections page with Klaviyo and source warehouse](../.gitbook/assets/202201\_Klaviyo\_Connection\_2.png)

### Step 3: Create your model

When defining models, you'll write SQL queries to select the data you want to see in Klaviyo. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.&#x20;

1. From inside your Census account, navigate to the **Models** page.&#x20;
2. Click **Add Model**.
3. Enter a name for your model. You'll use this to select the model later.&#x20;
4. Enter your SQL query. If you want to test the query, use the **Preview** button.&#x20;
5. Click **Save Model**.

![Basic SQL query for a new model](../.gitbook/assets/202201\_Model\_Page.png)

### Step 4: Create your first sync

The sync will move data from your warehouse to Klaviyo. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.&#x20;
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose Klaviyo as the **Connection** and "Profile" as the **Object**. (See [Supported objects](klaviyo.md#supported-objects).)
4. Under **How should changes to the source be synced?**, choose **Update or Create**. (See [Supported sync behaviors](klaviyo.md#supported-sync-behaviors).)
5. Under **How are source and destination records matched?**, select an **Identifier** for the model and for Klaviyo. We recommend using an internal ID when possible. (See [Supported objects](klaviyo.md#supported-objects).)
6. Under **Which properties should be updated?**, choose to update **Specific Properties** or **Sync All Properties**.&#x20;
7. Set up the mapping for the [List property](klaviyo.md#syncing-the-list-property) and any other properties you want to update by mapping a column in your model to a property in Klaviyo.
8. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
9. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
10. Click **Create Sync.**

When configuring your sync, the page should look something like this: 👇

![Sync setup for Klaviyo](../.gitbook/assets/202201\_Klaviyo\_Sync.png)

### Step 5: Confirm the synced data in Klaviyo

Once your sync is complete, it's time to check your data. Open Klaviyo and check that the profiles updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to Klaviyo! [🥳️](https://emojikeyboard.org/copy/Partying\_Face\_Emoji\_%F0%9F%A5%B3%EF%B8%8F?utm\_source=extlink)

And if anything went wrong, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## 💡 Things to know about the Klaviyo connector

### Syncing the List property

All profiles in Klaviyo belong to at least one list. All syncs must include the **List** property to ensure that profiles in Klaviyo are valid.&#x20;

We recommend creating a list specifically for syncing. For example, you could use a Klaviyo list called "Census Uploads" that simply includes every profile created or updated by a Census sync. Note that updating through Census sync will only add profiles to additional lists; it cannot remove a profile from a list.

![Syncing the Klaviyo list property](../.gitbook/assets/202201\_Klaviyo\_List\_Property.png)

To update the **List** property, you'll need to provide the list **ID** or **Name** values as a JSON array of strings, for example:

```
["List A", "List B", "List C"]
```

```
["RYkk48", "Xmpet6", "DyreR0"]
```

## 🗄 Supported objects

| **Object Name** | **Supported** | **Identifiers**                                |
| --------------: | :-----------: | ---------------------------------------------- |
|         Profile |       ✅       | External ID (recommended), Email, Phone Number |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional objects for Klaviyo.

## 🔄 Supported sync behaviors

|     **Behavior** | **Supported** | **Objects** |
| ---------------: | :-----------: | :---------: |
| Update or Create |       ✅       |     All     |

{% hint style="info" %}
Learn about all of our sync behaviors in [Core Concepts](https://app.gitbook.com/s/-MV3poo0VqVau1o8I79\_/basics/core-concept#sync-behaviors).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Klaviyo.



## 🚑 Need help connecting to Klaviyo?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

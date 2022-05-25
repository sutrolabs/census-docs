---
description: This page describes how to use Census with Pendo.
---

# Pendo

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Pendo to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Pendo account ready, with create access for Pendo Integration keys.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
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

### 1. Create a Pendo Integration key

Pendo lets you create a number of Integration keys. You should create a new API key for Census rather than reusing an existing one.

Within Pendo's left navigation bar, click the **Settings** ⚙️icon and select **Integrations** from the popup menu. Then, inside the **Integration Keys** tab, click **+ Add Integration Key**.

Provide a name you'll recognize ("Census" is a good choice) and check the **Allow Write Access**. Save your new key.

![](../.gitbook/assets/screely-1624583157927.png)

Finally, copy the long code you see under **Key**. We'll use that in a minute.

![](../.gitbook/assets/screely-1624583167649.png)

### 2. Create the Census Connection

Now let's create your new Census connection to Pendo.

1. In the **Settings** tab, Create a new Pendo Service Connection in Census.\
   &#x20;<img src="../.gitbook/assets/screely-1624583177140.png" alt="" data-size="original">&#x20;
2. You can provide whatever name you like.
3.  Copy and paste your new Pendo Integration key.\


    ![](../.gitbook/assets/screely-1624583188453.png)

And you're all set and ready to get syncing! 🎉

## 🗄 Supported Objects

Census currently supports syncing to the following Pendo objects.

| **Object Name** | **Supported?** | Identifiers |
| --------------: | :------------: | ----------- |
|         Account |        ✅       | Account ID  |
|         Visitor |        ✅       | Visitor ID  |
|           Event |       🔜       |             |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Pendo.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** |   **Objects?**  |
| -------------------: | :------------: | :-------------: |
|      **Update Only** |        ✅       | Account/Visitor |
| **Update or Create** |        ✅       | Account/Visitor |

{% hint style="warning" %}
For Pendo, "Update or Create" syncs will take longer than "Update Only" syncs. This is because - for newly created accounts and visitors - Pendo processes the previous hour’s data at the top of the hour. In addition, it may take up to 15 minutes for the data to fully appear in the UI. \
\
Census will wait until \~15 minutes after the top of the hour to then update the newly created visitor or account with additional properties that are part of the sync.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for Pendo.

## 🚑 Need help connecting to Pendo?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

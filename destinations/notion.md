---
description: >-
  This page describes how to use Census with Notion, the all-in-one workspace
  for your notes, tasks, wikis, and databases.
---

# Notion

## 🏃‍♀️ Getting Started

This guide shows you how to use Census to connect your Notion account to your data warehouse and create your first sync.

{% embed url="https://www.youtube.com/watch?v=xPlQip0_q6Y" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Notion account ready.
* Have the proper credentials to access your data source. See our docs for each supported data source for further information:
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

### Step 1: Connect Notion

* Once you're in Census, navigate to [Connections](https://app.getcensus.com/connections)
* Click the **Add Service** button
* Select **Notion** in the list

You'll be redirected to a page to log in to Notion to authorize access to your account. Once you sign in, you'll see a page like the image below, confirming you want to authorize Census.

You can grant access to the entire workspace or specific pages only, including private pages.

![](<../.gitbook/assets/image (8) (2).png>)

When configuring your sync, the page should look something like this 👇

![](<../.gitbook/assets/Notion sync setup (1920 × 2300 px).png>)

## 🗄️ Supported Objects <a href="#supported-objects" id="supported-objects"></a>

We support syncing data to Tables in Notion. ​

| **Object Name** | **Supported?** | **Identifiers** |
| :-------------: | :-----------: | :-------------: |
|      Table      |       ✅       |      Title      |

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects** |
| -------------------: | :------------: | :----------: |
|           **Update** |        ✅       |      All     |
| **Update or Create** |        ✅       |      All     |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Notion.

## ❗️Common troubleshooting issues

You may have to provide explicit permission (rather than relying on inherited permission from a parent page) for it to show up in the list of tables you can sync to.&#x20;

* Explicitly sharing means hitting "Share" on the top right of a page and adding the Census integration to the list, or selecting it directly in the OAuth flow. Children of shared parent pages will be shared, but not "explicitly," so going through and adding them manually during either OAuth or through the UI will help. For context, in the images below, the first is a page that is explicitly shared and the second is one that is shared based on a parent being shared.

![Screen Shot 2022-03-08 at 5.39.03 PM.png](https://uploads.linear.app/eb66e31d-15eb-4269-9860-aebf164343bb/4ec654ee-633b-4355-af2a-68ca6ebc80d4/c716ec16-5ac1-41e4-80a0-854d1ed55135)![Screen Shot 2022-03-08 at 5.41.34 PM.png](https://uploads.linear.app/eb66e31d-15eb-4269-9860-aebf164343bb/6d2b915a-48fd-4523-96be-efb82995ed48/c2bcb696-531e-4d06-9a9e-62ae9b585967)

## 🚑 Need help connecting to Notion?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


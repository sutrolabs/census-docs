---
description: This page describes how to use Census with Tik Tok Ads.
---

# TikTok

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Tik Tok Ads to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Tik Tok Ads account ready.
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

### Connect TikTok

* Once you are in Census, Navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select **TikTok** in the list
* You will not need to enter credentials in Census. Just click **Connect** and you will be redirected to sign in to your TikTok for Business Account

![](<../.gitbook/assets/Screen Shot 2022-02-11 at 4.17.57 PM.png>)

* Sign In to your TikTok for Business account and authorize the necessary permission for Census. Click **Confirm** to authorize.

![Authorize the Census Connection](<../.gitbook/assets/Screen Shot 2022-02-11 at 4.22.17 PM.png>)

* Back in the Census user interface select the TikTok Advertiser account to connect

![Select the intended account](<../.gitbook/assets/Screen Shot 2022-02-11 at 4.29.16 PM.png>)

* The TikTok connection will be present and authorized on the Connections page and ready for a sync.

## 🗄 Supported Objects

| **Object Name** | **Supported?** |      **Sync Keys**      |
| --------------: | :------------: | :-----------------------: |
| Custom Audience |        ✅       | Email, IDFA/GAID, Phone\* |

\*Note: All identifiers can be provided as either the original value or a hashed value&#x20;

![](<../.gitbook/assets/Screen Shot 2022-02-15 at 12.03.01 PM.png>)

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for TikTok.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** |   **Objects**   |
| -------------------: | :------------: | :-------------: |
| **Update or Create** |        ✅       | Custom Audience |
|           **Mirror** |        ✅       | Custom Audience |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for TikTok.

## 🚑 Need help connecting to TikTok Ads?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

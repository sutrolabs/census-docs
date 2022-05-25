---
description: This page describes how to use Census with Chargebee
---

# Chargebee

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect Chargebee to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Chargebee account ready.
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

### **1. Collect Your Credentials from Chargebee**

Census needs only your Chargebee **API token** and **sub domain** to connect you to your Chargebee instance.

* The API token can be found in your Chargebee **Settings** under **Configure Chargebee**
* The **sub domain** will be in your instance's URL and follow the structure _subdomain.chargebee_

![Collect the API token and sub domain from Chargebee](<../.gitbook/assets/Screen Shot 2022-02-16 at 3.27.30 PM.png>)

### 2. Connect Chargebee

* Once you are in Census, navigate to [Connections](https://app.getcensus.com/connections)
* Click the **Add Service** button
* Select Chargebee in the list
* Enter your Chargebee credentials and click **Connect**

![](<../.gitbook/assets/Screen Shot 2022-02-16 at 3.00.06 PM.png>)

## 🗄️ Supported Objects <a href="#supported-objects" id="supported-objects"></a>

Census currently supports syncing to the following Chargebee objects.

| **Object Name** | **Supported?** | **Identifiers** |
| :-------------: | :------------: | :-------------: |
|     Customer    |        ✅       |    ID, Email    |
|   Subscription  |        ✅       |   ID, Plan ID   |

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|   **Behaviors** | **Supported?** |      **Objects?**      |
| --------------: | :------------: | :--------------------: |
| **Update Only** |        ✅       | Customer, Subscription |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Chargebee.

If run into a dead end, start a conversation with us via the [in-app](https://app.getcensus.com/) chat.

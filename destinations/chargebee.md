---
description: This page describes how to use Census with Chargebee
---

# Chargebee

## Getting Started

‌In this guide, we will show you how to connect Chargebee to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Chargebee account ready.
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

### **1. Collect Your Credentials from Chargebee**

Census needs only your Chargebee **API token** and **sub domain** to connect you to your Chargebee instance.

* The API token can be found in your Chargebee **Settings** under **Configure Chargebee**
* The **sub domain** will be in your instance's URL and follow the structure _subdomain.chargebee_

![Collect the API token and sub domain from Chargebee](<../.gitbook/assets/Screen Shot 2022-02-16 at 3.27.30 PM.png>)

### 2. Connect Chargebee

* Once you are in Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select Chargebee in the list
* Enter your Chargebee credentials and click **Connect**

![](<../.gitbook/assets/Screen Shot 2022-02-16 at 3.00.06 PM.png>)

## Custom Fields in Chargebee <a href="#supported-objects" id="supported-objects"></a>

Custom fields defined in Chargebee can be added to the sync mapping by manually entering the custom field API Name in the destination field mapping.

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption><p>Chargebee Custom Field</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption><p>Sync Mapping</p></figcaption></figure>

## ️ Supported Objects <a href="#supported-objects" id="supported-objects"></a>

Census currently supports syncing to the following Chargebee objects.

| **Object Name** | **Supported?** | **Sync Keys** |
| :-------------: | :------------: | :-----------: |
|     Customer    |        ✅       |   ID, Email   |
|   Subscription  |        ✅       |  ID, Plan ID  |

## Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

|   **Behaviors** | **Supported?** |       **Objects**      |
| --------------: | :------------: | :--------------------: |
| **Update Only** |        ✅       | Customer, Subscription |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Chargebee.

If run into a dead end, start a conversation with us via the [in-app](https://app.getcensus.com/) chat.

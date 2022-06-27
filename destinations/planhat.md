---
description: >-
  This describes how you can connect Census to the Customer Success tool:
  Planhat.
---

# Planhat

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Planhat to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Planhat account ready.
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

### 1. Generate a Planhat API Key

In your Planhat account:

1. Navigate to **Settings > Service Accounts**
2. Create an **API Key**
3. Hold onto this API Key for the next section, you'll need it!

{% hint style="warning" %}
In Planhat, once a token is created, it will appear once and last forever. Make sure to copy and store it securely once generated. It should be over 340 characters long.
{% endhint %}

### 2. Connect Planhat to Census

* Head back to Census and navigate to [Connections](https://app.getcensus.com/connections).
* Click the Add Service button.
* Select Planhat in the dropdown list.
* Paste your Planhat account's **API Key**. Save your connection and if everything is set up correctly, you should see a successful connection test verifying the connection.
* Paste the region in the region box. If your Planhat app url is `app-us3.planhat.com`, paste **us3**.

## 🗄 Supported Objects

Census currently supports syncing to the following Planhat objects.

| **Object Name** | **Supported?** | **Identifiers**        |
| --------------: | :------------: | ---------------------- |
|         Company |        ✅       | Source ID, External ID |
|        End User |        ✅       | Source ID              |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Planhat. Custom fields for both objects are supported.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** |    **Objects?**   |
| -------------------: | :------------: | :---------------: |
| **Update or Create** |        ✅       | Company, End User |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Planhat.

## 🚑 Need help connecting to Planhat?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

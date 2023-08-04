---
description: This page describes how to use Census with Snapchat Ads.
---

# Snapchat

## ​🏃‍♀️ Getting Started

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Snapchat Ads account ready.
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

### Connect Snapchat Ads

1. In Census, navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Snapchat** from the menu.
3. Follow the OAuth flow to connect to your Snapchat account.

![Enter your Snapchat credentials to complete the OAuth flow.](<../.gitbook/assets/Screen Shot 2022-04-25 at 4.23.34 PM.png>)

## 🗄 Supported Objects

| Object Name      |      Supported?      | Identifiers                |
| ---------------- | :------------------: | -------------------------- |
| Conversion Event | :white\_check\_mark: | External ID                |
| Customer List    | :white\_check\_mark: | Mobile Ad ID, Email, Phone |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Snapchat objects.

## 🔄 Supported Sync Behaviors

|     Behaviors    |      Supported?      |      Objects     |
| :--------------: | :------------------: | :--------------: |
| Update or Create | :white\_check\_mark: |   Customer List  |
|      Append      | :white\_check\_mark: | Conversion Event |
|      Mirror      | :white\_check\_mark: |   Customer List  |

[Contact us](mailto:support@getcensus.com) if you want Census to support more sync behaviors.

## 🚑 Need help connecting to Snapchat?

Contact us via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com/) chat.

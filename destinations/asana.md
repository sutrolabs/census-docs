---
description: This page describes how to use Census with Asana
---

# Asana

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect Asana to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Asana account ready.
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

### 1. Connect Asana

* Once you are in Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the New Destination button
* Select Asana in the list

You will be redirected to a page to log in to Asana to authorize access to your account. Once you sign in, you'll see a page like the image below, confirming you want to authorize Census.

![](<../.gitbook/assets/Screen Shot 2022-02-12 at 12.17.40 AM.png>)

## 🗄️ Supported Objects <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Asana's primary object is a Task, which we support in Census.​

|  **Object Name** | **Supported?** | **Sync Keys**  | **Behaviors**         |
|-----------------:| :------------: | ---------------- |-----------------------|
| Task | ✅ | External ID | Add, Update or Create |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Asana.

If run into a dead end, start a conversation with us via the [in-app](https://app.getcensus.com/) chat.

---
description: This page describes how to use Census with Microsoft Advertising(or Bing Ads).
---

# Microsoft Advertising

## ​🏃‍♀️ Getting Started

In this guide, we will show you how to connect Microsoft Ads to Census.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Microsoft Ads account ready.
  * To create Customer Match syncs, your Microsoft Ads Account will need access to the Customer Match feature. See [Microsoft's Customer Match policy](https://about.ads.microsoft.com/en-us/solutions/audience-targeting/customer-match) for more details.
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

### 1. Connect Microsoft Ads

* Once you are in Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select Microsoft Advertising in the dropdown list.

![](<../.gitbook/assets/Screen Shot 2022-03-11 at 9.50.12 AM.png>)

Follow Microsoft OAuth flow to connect to your Microsoft Advertising account.

![](<../.gitbook/assets/Screen Shot 2022-03-11 at 9.54.12 AM.png>)

![](<../.gitbook/assets/Screen Shot 2022-03-11 at 9.56.02 AM.png>)

Finally, select the Microsoft Advertising account you'd like to sync to

![](<../.gitbook/assets/Screen Shot 2022-03-11 at 10.01.08 AM.png>)

### 2. Connect your Data Warehouse

Please follow one of our short guides depending on your data warehouse technology

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)
* [Databricks](../sources/databricks.md)

After setting up your warehouse, your Census sync should look like this:

![](<../.gitbook/assets/Screen Shot 2022-03-11 at 10.08.23 AM.png>)

## 🗄 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|    **Object Name** | **Supported?** |    **Identifiers**    | **Behaviors** |
| -----------------: | -------------- | :-------------------: | ------------- |
|    Custom Audience | ✅              |         Email         | Mirror        |
| Offline Conversion | ✅              | Any unique identifier | Send          |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](broken-reference) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Microsoft Ads objects and/or behaviors

## 🚑 Need help connecting to Microsoft Ads?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

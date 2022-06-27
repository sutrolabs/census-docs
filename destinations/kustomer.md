---
description: This page describes how to use Census with Kustomer
---

# Kustomer

## 🏃‍♀️ Getting Started <a href="#getting-started" id="getting-started"></a>

In this guide, we will show you how to connect Kustomer to Census and create your first sync.

**Prerequisites**

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Planhat account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Azure Synapse](../sources/azure-synapse.md)
  * ​[Databricks](https://docs.getcensus.com/sources/databricks)​
  * ​[Elasticsearch](https://docs.getcensus.com/sources/elasticsearch)​
  * ​[Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)​
  * ​[Google Sheets](https://docs.getcensus.com/sources/google-sheets)​
  * ​[MySQL](https://docs.getcensus.com/sources/mysql)​
  * ​[Postgres](https://docs.getcensus.com/sources/postgres)​
  * ​[Redshift](https://docs.getcensus.com/sources/redshift)​
  * ​[Rockset](https://docs.getcensus.com/sources/rockset)​
  * ​[Snowflake](https://docs.getcensus.com/sources/snowflake)​
  * ​[SQL Server](https://docs.getcensus.com/sources/sql-server)​

### 1. Generate a Kustomer API Key <a href="#1.-generate-a-planhat-api-key" id="1.-generate-a-planhat-api-key"></a>

In your Kustomer account:

1. Navigate to **Settings > Security > API Key**
2. Create an **API Key** with the following permissions:
   1. `org.admin.klass.read`
   2. `org.user.kobject.read`
   3. `org.admin.metadata.read`
   4. `org.admin.search.read`
   5. `org.user.customer.write`
   6. `org.user.kobject.write`
3. Hold onto this API Key for the next section, you'll need it!

In Kustomer, once a token is created, it will be created with those scopes and it is immutable. If there is a permission change, you will need to create a completely separate API key. Make sure to copy and store it securely once generated.

More on Kustomer's API permission scopes [here](https://help.kustomer.com/permissions-for-common-api-requests-HkltTBZbN).

### 2. Connect Kustomer to Census <a href="#2.-connect-planhat-to-census" id="2.-connect-planhat-to-census"></a>

* Head back to Census and navigate to [Connections](https://app.getcensus.com/connections).
* Click the Add Service button.
* Select Kustomer in the dropdown list.
* Paste your Kustomer account's **API Key**. Save your connection and if everything is set up correctly, you should see a successful connection test verifying the connection.

## 🗄 Supported Objects

| **Object Name** | **Supported?** | **Identifiers** |
| --------------: | :------------: | --------------- |
|        Customer |        ✅       | External Id     |
|         Company |        ✅       | External Id     |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Kustomer.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|    **Behaviors** | **Supported?** | **Objects?** |
| ---------------: | :------------: | :----------: |
| Update or Create |        ✅       |      All     |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Kustomer.

## 🚑 Need help connecting to Kustomer? <a href="#need-help-connecting-to-planhat" id="need-help-connecting-to-planhat"></a>

​[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com/) chat.


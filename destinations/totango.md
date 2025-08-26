---
description: This page describes how to use Census with Totango.
---

# Totango

## Getting Started

In this guide, we will show you how to connect Totango to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Totango account ready.
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

### 1. Collect your Totango Credentials

Census requires your Totango API key and Service ID to send data. Before we can connect Census to Totango, we need to first collect the two credentials. An additional parameter, Server Region, is optional

#### **API Key**

1. Click on your **User Profile** in Totango (it will be in the top right with your initials)
2. Click on the **Integrations** tab in the pop up tab
3. Copy the key out of the **API Token Key** box

#### **Service Id:**

1. Click on your **User Profile** in Totango (it will be in the top right with your initials)
2. At the bottom of the dropdown copy the Service Id which will be formatted in three parts SP-\<Service Id>-\<Instance>. For example: SP-25001-01
3. Copy the Service Id portion only into the Census connection (e.g. 25001 rather than the full SP-25001-01)

For additional information on finding Totango credentials you can find instructions in the [Totango documentation](https://support.totango.com/hc/en-us/articles/203036939-Personal-Access-Token-and-Service-ID).

### 2. Connect Totango

* Once you are in Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select **Totango** in the list
* Paste your API Key into the **API Token** field
* Paste your **Service Id** in the Service Id field
* Optionally name your new connection and add a **Server Region** then click **Connect**

![Totango Connection Example](<../.gitbook/assets/Screen Shot 2022-10-12 at 5.31.08 PM.png>)

## Supported Objects

| **Object Name** | **Supported?** | Identifiers |
| --------------: | :------------: | ----------- |
|         Account |        ✅       | Account ID  |
|            User |        ✅       | User ID     |

## Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects** |
| -------------------: | :------------: | :---------: |
| **Update or Create** |        ✅       |     All     |

Contact us if you want Census to support more Sync Behaviors for Totango

## Need help connecting to Totango?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

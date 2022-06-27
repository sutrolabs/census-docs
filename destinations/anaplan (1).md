---
description: >-
  This page describes how to use Census to sync data from your warehouse to
  Anaplan.
---

# Anaplan

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Anaplan to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Anaplan account ready, with the Administrator role the username and password on hand.
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

### 1. Navigate to your Anaplan Model

From the URL, you will find the WorkspaceId and the ModelId. These will be needed to configure the connection from Census.

![Copy the WorkspaceId and the ModelId](<../.gitbook/assets/Anaplan URL.png>)

{% hint style="warning" %}
The Model Id needs to be the model to which you want to sync, both the Workspace ID and the Model ID should be 32 characters long
{% endhint %}

### 2. Configure the Anaplan Connection

Navigate to the connections tab in Census. Select Anaplan which will prompt you for your username and password.&#x20;

![Add a descriptive label and copy your credentials](<../.gitbook/assets/Anaplan Census.png>)

After adding your credentials, paste your Anaplan Workspace and Model ID into Census.

![Hit the "Connect" button](<../.gitbook/assets/Anaplan Census 2.png>)

### 3. Test the Connection

![You will be prompted after ](<../.gitbook/assets/Test Anaplan Connection.png>)

You have successfully configured and tested the connection, so you can now sync data into your financial models from your data source! :tada:

## 🗄️ Supported Objects

|        **Object** | **Supported?** |
| ----------------: | :------------: |
| **Import Action** |        ✅       |

{% hint style="info" %}
Import Actions must have the Source Type of File in order for Census to be able to sync to it. Look [here](https://help.anaplan.com/f19cdb3d-385a-4a27-aaa8-7422b240e8bc-Get-started-with-imports) for more details on how to configure this on the Anaplan side
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Anaplan.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

| **Behaviors** | **Supported?** | **Objects?** |
| ------------: | :------------: | :----------: |
|    **Mirror** |        ✅       |      All     |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for Anaplan.

## 🚑 Need help connecting to Anaplan?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


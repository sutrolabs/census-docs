---
description: This page describes how to use Census with Gainsight.
---

# Gainsight

## 🏃‍♀️ Getting started

This guide shows you how to use Census to connect your Gainsight account to your data warehouse and create your first sync.

### Prerequisites

Before you begin, you'll need the following:

* **Census account**: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* **Gainsight account**: You need your Gainsight domain as well as an API Access Key for the Gainsight API
* **Credentials for your data warehouse**: For details, see the guide for your specific technology.
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Elasticsearch](../sources/elasticsearch.md)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [MySQL](../sources/mysql.md)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)
  * [SQL Server](../sources/sql-server.md)

### Step 1: Generate Access Token :key:

Within Gainsight, click on the Sidebar > Administration > Integrations > Connectors 2.0

![](<../.gitbook/assets/Screen Shot 2021-11-19 at 8.27.40 PM.png>)

Click this and click on the Create Connection button in the top right, then select the Gainsight API

{% hint style="info" %}
Do not select the GS Bulk API, select the Gainsight API
{% endhint %}

![](<../.gitbook/assets/Screen Shot 2021-11-19 at 8.28.18 PM.png>)

Copy the Access Key after hitting Edit Connection

![](<../.gitbook/assets/Gainsight Credentials.png>)

Great, now navigate back to the [Connections](https://app.getcensus.com/connections) page in Census

### Step 2: Connect Gainsight as a Service Connection

Click Add Service and select Gainsight. Then paste your Access Key for the Gainsight API. Also, paste in the domain for your Gainsight account

![](<../.gitbook/assets/Gainsight Credentials Census.png>)

Click Save Connection and ensure that Gainsight passes the connectivity test

![](<../.gitbook/assets/Successful GS Test.png>)

With a :white\_check\_mark:, we are good to move on to the data!

### Step 3: Create a Model

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models).​‌

Here you will have to write SQL queries to select the data you want to see in Gainsight. Here are some ideas of data you should select‌.

* New user sign-ups
* Product usage data for customers
* CSAT scores
* Contract values

{% hint style="info" %}
Make sure you have an [identifier for Gainsight](gainsight.md#supported-objects) in your data source
{% endhint %}

Once you have created your model, click **Save**.‌

### Step 4: Create your first Sync <a href="#4-create-your-first-sync" id="4-create-your-first-sync"></a>

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button‌.

In the " **What data do you want to sync?"** section‌

* For the **Source,** select the model you created in step 3
* Or you can select a Table or View from your Warehouse

Next up is the **"Where do you want to sync data to?"** section‌

* Pick Gainsight from step 2 as **the Connection**
* For Object, pick the table you want to sync data to

For the " **How should changes to the source be synced?"** section‌

* Select your preferred behavior. **Update only** is a great place to start if the object already exists in Gainsight. **Update or Create** is great for sending data from the warehouse into Gainsight that might not already be there (like all users from your warehouse to the Gainsight Person object).

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section‌.

The end result should look something like this:

![](<../.gitbook/assets/Screen Shot 2021-11-19 at 8.59.30 PM.png>)

Confirm the mappings and click Next in the bottom right corner. On the next page, click the run a sync now checkbox and click on Create Sync

![](<../.gitbook/assets/Screen Shot 2021-11-19 at 9.02.14 PM.png>)

That's it, in 4 steps you have connected your Data Source to Gainsight! :tada:

## 🗄 Supported Objects

|     **Object Name** | **Supported?** | **Identifiers**                                                                     |
| ------------------: | :------------: | ----------------------------------------------------------------------------------- |
|              Person |        ✅       | Email                                                                               |
|             Company |        ✅       | Name                                                                                |
|      Company Person |        ✅       | UniqueId for Census. Company Name and Person Email are required                     |
| Relationship Person |        ✅       | UniqueId for Census. Company Name, Person Email, and Relationship Name are required |
|     Custom Object\* |        ✅       | Available Update Keys that are not a lookup                                         |

\*The Custom Object must be configured like below for Census to be able to edit it. You can access this on your Administration > Customer Data > Data Management path on the lefthand sidebar.

![](<../.gitbook/assets/Screen Shot 2022-02-01 at 6.47.18 PM.png>)

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Gainsight.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** |        **Objects?**       |
| -------------------: | :------------: | :-----------------------: |
| **Update or Create** |        ✅       |            All            |
|      **Update Only** |        ✅       | Company, Custom Objects\* |

## 🚑 Need help connecting to Gainsight?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

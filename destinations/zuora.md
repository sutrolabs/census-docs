---
description: This page describes how to use Census with Zuora.
---

# Zuora

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect Zuora to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
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

### **1.** Collect your Zuora API Credentials

Census will need needs the following pieces of information to connect to your Zuora instance:

* Client ID
* Client Secret
* Rest API Endpoint

### 2. **Add the Destination**

Now that we have the credentials from Zuora, we can now set up Zuora as a Destination in Census.

1. In the **Destinations** tab of Census, go to your Destinations and click the **New Destination** button to create a new Zuora connection.
2. You can provide whatever name you like.
3. Provide your credentials collected from Zuora in Step 1.
4. Click **Connect**

![](<../.gitbook/assets/Screen Shot 2022-02-02 at 9.58.20 AM.png>)

### 3. Create your Model

Navigate to the [Model section of our Dashboard](https://app.getcensus.com/models)

Here you can write a SQL query to select the data you want to see in Zuora. You can also use tables or views already in your data warehouse or models from data transformation tools like dbt or Looker. Here are some ideas of data you could select

* The Lifetime Value of a customer
* The end date of a user's trial
* The date a user became active in your product
* The number of key activities a user did in your app in the last 7/30 days

Once you have created your model, click **Save Model**.

![](<../.gitbook/assets/Screen Shot 2022-01-27 at 3.31.32 PM (1).png>)

### 4. Create your first Sync

Head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button

In the "What data do you want to sync?" section:

* For the Connection, select the data warehouse you've already connected (See Prerequisites).
* For the Source, select the model you created in step 3.

![Choose your connection and source (your model from step 3)](<../.gitbook/assets/Screen Shot 2022-02-02 at 10.10.12 AM.png>)

Next up is the "Where do you want to sync data to?" section.

* Pick the Zuora connection you created in step 3.
* For Object, select Account or Subscription.

![Select which object you want to sync to](<../.gitbook/assets/Screen Shot 2022-02-02 at 10.11.33 AM.png>)

For the "How do you want to update the destination?" section.

* Select Update Only

![](<../.gitbook/assets/Screen Shot 2022-02-02 at 10.13.09 AM.png>)

For the "How are source and destination records matched?" section.

* Pick the mapping key:
  * For syncs to the Account object select either **Account ID** or **Account Number**
  * For syncs to the Subscription object select either **Subscription ID** or **Subscription Number**
* Select the field from your model you want mapped to the identifier.

![](<../.gitbook/assets/Screen Shot 2022-02-02 at 10.20.58 AM.png>)

Finally, select the fields you want to update in the Mapper in the "Which Fields should be updated?" section. Here simply map the field from your Zuora instance to the column from your model.

![](<../.gitbook/assets/Screen Shot 2022-02-02 at 10.27.12 AM.png>)

Click the **Next** button to see the final preview, which will have a recap of what will happen when you start the sync.

## 🗄️ Supported Objects

| **Object Name** | **Supported?** | **Sync Keys**                        |
| --------------- | :------------: | ------------------------------------ |
| Account         |        ✅       | Account ID, Account Number           |
| Subscription    |        ✅       | Subscription ID, Subscription Number |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Objects for this destination

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

| **Behaviors** | **Supported?** |      **Objects**      |
| ------------: | :------------: | :-------------------: |
|   Update Only |        ✅       | Account, Subscription |

‌ [Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for this destination

## 🚑 Need help connecting to Zuora?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

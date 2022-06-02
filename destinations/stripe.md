---
description: This page describes how to use Census with Stripe.
---

# Stripe

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Stripe to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Stripe account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
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

### 1. Connect Stripe

* Once you are in Census, Navigate to [Connections](https://app.getcensus.com/connections)
* Click the Add Service button
* Select Stripe in the dropdown list
* Add your API key

![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5fbc4462cff47e00160bcde2/file-tKjZxmKj6C.png)

In Stripe, go to [Developers > API Keys](https://dashboard.stripe.com/apikeys) and create an API key that has Write permissions into Customers (and Read permission to Balances for testing our connection).

![](<../.gitbook/assets/Screen Shot 2021-10-28 at 5.03.59 PM (1).png>)

### 2. Connect your Data Warehouse

Please follow one of our short guides depending on your data warehouse technology

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)

### 3. Create your first Model

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models)

Here you will have to write SQL queries to select the data you want to see in Stripe. Here are some ideas of data you should select

* The type of customer
* The attribution of the customer
* Order form data to generate an invoice

Once you have created your model, click save.&#x20;

![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5f6563834cedfd00173b9a49/file-zg53SxxpoO.png)

### 4. Create your first Sync

No head to the [Sync page](https://app.getcensus.com/syncs) and click the Add Sync button

In the " What data do you want to sync?" section

* For the Connection, select the data warehouse you connected in step 2
* For the Source,  select the model you created in step 3

Next up is the "Where do you want to sync data to?" section

* Pick Stripe as the Connection
* For Object, pick **Customer**

For the " How should changes to the source be synced?" section&#x20;

* Select Update or Create
* Pick the right mapping key, it can be Email or any other external id for Customer

Finally, select the fields you want to update in the Mapper in the "Which Fields should be updated?" section

* Here simply map the field from your Stripe instance to the column from your model.

The end result should look something like this

![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5fbc4804cff47e0017d34b6d/file-drmWJMVTz9.png)

Click the Next button to see the final preview which will have a recap of what will happen when you start the sync

### 5. Confirm the data is in Stripe

Now go back to your Stripe and go view a Customer Profile that should have been updated. If everything well well, you should see your data in Stripe

![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5fbc4ae846e0fb0017fcee63/file-mYnHg4FN41.png)

That's it, in 5 steps, you connect Census to Stripe and started syncing customer & product data from your warehouse to Stripe 🎉

If you have any question or if you have any issues getting started, please contact us via the in-app live chat in the bottom right corner or send us an email at support@getcensus.com

## 🗄 Supported Objects

Census currently supports syncing to the following Stripe objects:

| **Object Name** | **Supported?** | Identifiers |
| --------------: | :------------: | ----------- |
|        Customer |        ✅       | Email       |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Stripe.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects?** |
| -------------------: | :------------: | :----------: |
| **Update or Create** |        ✅       |      All     |
|      **Update Only** |        ✅       |      All     |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Stripe.

## 🚑 Need help connecting to Stripe?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

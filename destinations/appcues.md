---
description: This page describes how to use Census with Appcues.
---

# Appcues

## Getting Started

‌In this guide, we will show you how to connect Appcues to Census and create your first sync.

#### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com) now.
* Have your Appcues account ready.
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

#### 1. Connect Appcues

* Once you are in Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select **Appcues** in the dropdown list
* Copy your Appcues **Account ID**, and your **API key & secret**, which can be created and managed in your [API Keys page on studio.appcues.com](https://studio.appcues.com/settings/keys). For more details on where these values are located, check out [Appcues' official documentation](https://docs.appcues.com/article/745-appcues-public-api). It's important to ensure that your API Key has proper permissions. If not, you may run into issues accessing certain endpoints.

#### 2. Create your first Model

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models)

Here you can write SQL queries to select the data you want to see in Appcues. Here are some ideas of data you can select

* The Lifetime Value of a customer and add it to a user
* The end date of a users' trials
* The date users became active in your product
* The number of key activities a user did in your app in the last 7/30 days

Once you have created your model, click save.

Note: you can also sync an existing table or view from your source directly.

#### 3. Create your first Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button

In the " **What data do you want to sync?"** section

* For the **Connection**, select your data warehouse
* For the **Source,** select the model you created in step 2

Next up is the **"Where do you want to sync data to?"** section

* Pick Appcues as **the Connection**
* For Object, pick the one you want to sync data to.

After selecting the update mechanism and the matching identifiers, you can select the fields you want to update in the mapper under the **"Which properties should be updated?"** section

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync

#### 4. Confirm the data is in Appcues

Now go back to Appcues and go view a User record that should have been updated or created. If everything went well, you should see your data in Appcues

That's it! In 4 steps, you've connected Appcues and started syncing customer & product data from your warehouse 🎉

### Supported Objects

Census currently supports syncing to the following Appcues objects.

| **Object Name** | **Supported?** | Identifiers |
| --------------: | :------------: | ----------- |
|            User |        ✅       | User ID     |

### Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects** |
| -------------------: | :------------: | :---------: |
| **Update or Create** |        ✅       |     User    |

### Need help connecting to Appcues?

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects or more sync behaviors for Appcues or just to start a conversation!

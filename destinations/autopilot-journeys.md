---
description: This page describes how to use Census with Autopilot Journeys.
---

# Autopilot

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect Autopilot Journeys to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com) now.
* Have your Autopilot Journeys account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

### 1. Get Autopilot API Key

1. Within Autopilot Journeys, visit **Settings** then **Autopilot API** page.
2. Copy the API key and provide to Census. If you have not yet generated an API key click on **Generate**.

![](<../.gitbook/assets/Screen Shot 2022-01-14 at 3.16.10 PM.png>)

### 2. Connect Autopilot Journeys

* Once you are in Census, Navigate to [Connections](https://app.getcensus.com/connections)
* Click the **Add Service** button
* Select Autopilot Journeys in the dropdown list

![Select Autopilot](<../.gitbook/assets/Screen Shot 2022-02-10 at 2.19.13 PM.png>)

* Enter a name of your choosing that makes sense for your own reference
* When prompted for your API Credentials, enter your Autopilot API Key

![](<../.gitbook/assets/Screen Shot 2022-02-10 at 2.22.04 PM.png>)

### 3. Connect to your Data Warehouse

Please follow one of our short guides depending on your data warehouse technology

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)   &#x20;
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)

### 4. Create your first Model

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models)

Here you can write a SQL query to select the data you want to see in Heap.io, or you can use a model from a dbt project or a Looker Look. Here are some ideas of data you could select

* The Lifetime Value of a customer and add it to a contact or companies
* The end of their trial
* The date they became active in your product
* The number of key activities a user did in your app in the last 7/30 days

Once you have created your model, click save.

### 5. Create your first Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button

In the " **What data do you want to sync?"** section

* For the **Connection**, select the data warehouse you connected in step 2
* For the **Source,** select the model you created in step 3&#x20;

Next up is the **"Where do you want to sync data to?"** section

* Pick Autopilot as **the Connection**&#x20;
* For Object, pick the one you want to sync data to; currently only Contact is available.

For the " **How should changes to the source be synced?"** section

* Select **Update or Create**
* Pick the right mapping key, it will be Email for Contacts.

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section

* Here simply map the field from your Autopilot instance to the column from your model.

The end result should look something like&#x20;

![](<../.gitbook/assets/Screen Shot 2022-02-10 at 3.00.06 PM.png>)

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync

### 6. Confirm the data is in Autopilot

Now go back to your Autopilot and go view the record type (Contact) that should have been updated. If everything went well, you should see your data in Autopilot.

![](<../.gitbook/assets/Screen Shot 2022-02-10 at 3.05.59 PM.png>)

That's it! In 6 steps, you connected Census to Autopilot and started syncing customer & account data from your warehouse to Autopilot 🎉

## 🗄 Supported Objects

| **Object Name** | **Supported?** | **Identifiers** |
| --------------- | :------------: | --------------- |
| Contact         |        ✅       | Email           |

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects?** |
| -------------------: | :------------: | :----------: |
| **Update or Create** |        ✅       |      All     |

##

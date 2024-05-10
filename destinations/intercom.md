---
description: This page describes how to use Census with Intercom.
---

# Intercom

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Intercom to Census and create your first sync.

{% embed url="https://www.youtube.com/watch?v=RCKO3w-qw9g" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Intercom account ready.
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

### 1. Connect Intercom

* Once you are in Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select **Intercom** in the dropdown list

![](../.gitbook/assets/screely-1618112961265.png)

You will be directed to a screen describing the permissions Census needs. Note that if your account has access to multiple Intercom workspaces, you'll also have the option to select the specific workspace. As well you can specify the data host region of your Intercom instance.

![View the permissions needed, select the correct Intercom workspace, and specify the data host region](<../.gitbook/assets/Screen Shot 2022-09-14 at 3.04.00 PM.png>)

Once the connection is created, make sure that the region Census uses is the same as your `Data host region` in Intercom. To do this select `edit` on your connection and then manually select your region from the dropdown.

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-21 at 9.52.13 AM.png" alt=""><figcaption></figcaption></figure>

### 2. Connect your Data Warehouse

Please follow one of our short guides depending on your data warehouse technology

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)

After setting up your warehouse, your Census Destinations page should look like this

![](../.gitbook/assets/screely-1618112995751.png)

### 3. Create your first Model

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models)

Here you will have to write SQL queries to select the data you want to see in Intercom. Here are some ideas of data you should select

* The Lifetime Value of a customer and add it to a contact or companies
* The end of their trial
* The date they became active in your product
* The number of key activities a user did in your app in the last 7/30 days

Once you have created your model, click save.

### 4. Create your first Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button

In the " **What data do you want to sync?"** section

* For the **Connection**, select the data warehouse you connected in step 2
* For the **Source,** select the model you created in step 3

Next up is the **"Where do you want to sync data to?"** section

* Pick Intercom as **the Connection**
* For Object, pick the one you want to sync data to.

For the " **How should changes to the source be synced?"** section

* Select your preferred behavior. **Update only** is a great place to start!
* Pick the right mapping key, it could be Email for Contacts, Company ID for Companies but we recommend you use your own database id if possible

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section

* Here simply map the field from your Intercom instance to the column from your model.

The end result should look something like this

![](../.gitbook/assets/screely-1618113035239.png)

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync

### 5. Confirm the data is in Intercom

Now go back to your Intercom and go view a record type (Contact or Company) that should have been updated. If everything went well, you should see your data in Intercom

![](../.gitbook/assets/screely-1618113503713.png)

That's it! In 5 steps, you've connected Intercom and started syncing customer & product data from your warehouse 🎉

## 🗄 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Census currently supports syncing to the following Intercom objects.

|        **Object Name** | **Supported?** | Identifiers                     | **Behaviors**                         |
| ---------------------: | :------------: | ------------------------------- |---------------------------------------|
|                Company |        ✅       | Company ID                      | Update or Create, Delete              |
| Contact (Lead or User) |        ✅       | Email, Intercom ID, External ID | Update or Create, Update Only, Delete |
|                   Lead |        ✅       | Email, Intercom ID, External ID | Update or Create, Update Only, Delete |
|                   User |        ✅       | Email, Intercom ID, External ID | Update or Create, Update Only, Delete |
|                  Event |        ✅       | Event ID                        | Send                                  |

{% hint style="info" %}
If you're finding Companies missing in Intercom after a sync, make sure the company also has users associated with them. By default, Intercom hides companies with no associated users.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Intercom objects and/or behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

### :x: Deleting Objects

When deleting objects in Intercom, Census's default mode is to archive those objects (except in the case of Companies, which don't allow archiving). Intercom will permanently delete those objects 30 days after they've been archived. In some instances, you may opt to have Census permanently delete objects. This could lead to irreversible data loss and is not recommended unless you are confident you don't need those records.

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Intercom.

## 🚑 Need help connecting to Intercom?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

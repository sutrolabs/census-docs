---
description: This page describes how to use Census with Delighted.
---

# Delighted

## 🏃‍♀️ Getting Started

In this guide, we'll show you how to connect Delighted to Census and create your first sync.&#x20;

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Delighted account ready,
*   Have the proper credentials to access your data source. See our docs for each supported data source for further information:

    * [Databricks](https://docs.getcensus.com/sources/databricks)
    * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
    * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
    * [Postgres](https://docs.getcensus.com/sources/postgres)
    * [Redshift](https://docs.getcensus.com/sources/redshift)
    * [Rockset](https://docs.getcensus.com/sources/rockset)
    * [Snowflake](https://docs.getcensus.com/sources/snowflake)



### 1. Create a Delighted connection

* In Census, navigate to [Connections](https://app.getcensus.com/connections)
* Click the **Add Service** button
* Search for **Delighted** in the search bar

![](<../.gitbook/assets/Screen Shot 2022-03-31 at 6.13.13 PM.png>)

Next, you'll need your API Token from Delighted in order to connect. Your authentication flow should look like this:\


![](<../.gitbook/assets/Screen Shot 2022-03-31 at 6.22.48 PM.png>)



![](<../.gitbook/assets/Screen Shot 2022-03-31 at 6.23.57 PM.png>)

### 2. Create your first Model

Now navigate to the [models page](https://app.getcensus.com/models) in your Census account.

Here you will have to write SQL queries to select the data you want to send to your Delighted account. Your model can be a complex query selecting details about customers and generating metrics, or as simple as a `SELECT * FROM ...`, it's up to you. Once you have created your model, click **Save Model**.&#x20;

![](<../.gitbook/assets/Screen Shot 2022-03-31 at 6.35.16 PM.png>)

### 3. Create your first Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Create a Sync** button.

From there, select your object. Here's an example of how that should look:\


![](<../.gitbook/assets/Screen Shot 2022-03-31 at 7.15.52 PM.png>)

Next, select your behavior, identifier and mapped fields.

![](<../.gitbook/assets/Screen Shot 2022-03-31 at 7.16.05 PM.png>)

![](<../.gitbook/assets/Screen Shot 2022-03-31 at 7.16.31 PM.png>)

Decide whether to sync existing data or not and then click the **Next** button:

![](<../.gitbook/assets/Screen Shot 2022-03-31 at 7.16.48 PM.png>)



Click the Next button to see a preview of what will happen when you start the sync. You can check the "Run Sync Now" checkbox to kick off an initial sync and pick a schedule afterward.

### 4. Confirm the data is in Delighted

You should be able to view your data in Delighted now.



## 🗄 Supported Objects

Delighted supports two objects: Autopilot and Survey&#x20;

| Object Name |      Supported?      |
| ----------: | :------------------: |
|   Autopilot | :white\_check\_mark: |
|      Survey | :white\_check\_mark: |
|             |                      |



## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|                       Behaviors |      Supported?      |  Objects? |
| ------------------------------: | :------------------: | :-------: |
|                          Append | :white\_check\_mark: |   Survey  |
| Update Only, Upsert, and Mirror | :white\_check\_mark: | Autopilot |



## 🚑 Need help connecting to Delighted?

Contact us via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com/) chat.

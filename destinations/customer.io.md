---
description: This page describes how to use Census with Customer.io.
---

# Customer.io

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Customer.io to Census and create your first sync.

{% embed url="https://www.youtube.com/watch?v=sRYnagj_gIE" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Customer.io account ready.
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

### 1. Collecting Customer.io API Credentials

To connect Census to your Customer.io, you'll need to provide Census with a few credentials so that we can talk to it directly.

### **2. Go to your API Credentials page**

In the top right, click on your name, and select **Account Settings**

![](../.gitbook/assets/cio\_step1.png)

Then select **API Credentials**

![](../.gitbook/assets/cio\_step2.png)

### **3. Create a new set of Tracking API & App API credentials for Census**

Click the **Create New API Credentials** button in the top right.![](../.gitbook/assets/cio\_step3.png)

It's important to note that there are two types of API keys here: Track API Keys and App API Keys. Track API Keys are used to send behavioral tracking activity. App API Keys are used for triggering messages and broadcasts, as well as retrieving data from your workspace. For a more in-depth explanation, check out Customer.io's [docs here](https://customer.io/docs/managing-credentials/#track-api-keys-vs-app-api-keys). \\

![Tracking API Keys](<../.gitbook/assets/Screen Shot 2022-04-08 at 5.39.29 PM.png>)

\\

![App API Keys](<../.gitbook/assets/Screen Shot 2022-04-08 at 5.39.15 PM.png>)

Then, give the new credentials a name. It can be whatever you like, but give it something memorable so you know this key is used by Census. If you're using Customer.io's workspaces feature, you'll want to specify which workspace to use. If you want to connect Census to multiple workspaces, you'll need to create credentials for each one.

When you hit save, you'll return to the list of credentials. Make a note of the **Site ID** and **API Key**. You'll need to provide them to Census.

![](../.gitbook/assets/cio\_step4.png)

![](../.gitbook/assets/cio\_step5.png)

### **4. Create a new Customer.io connection in Census**

* Visit the **Connections** tab in Census
* Then select **Customer.io** from the **Add Service** menu

![](../.gitbook/assets/cio\_step6.png)

![](<../.gitbook/assets/Screen Shot 2022-04-08 at 5.50.05 PM.png>)

Finally, provide the Site ID and both API Keys you just created on Customer.io. You can name the connection something memorable. This is particularly useful if you're going to create multiple connections, one for each Customer.io workspace. In that case, include the Customer.io workspace name here.

Customer.io will now appear as a new destination for Census syncs. 🎉

## 🏎 Sync Speed

Customer.io is a destination with a fast API that can burst all the way to 600 api calls per second but usually we set a conservative **150 calls per second.**

| **Service** | Public API rate limit | **Records sync / Minute** |
| ----------- | --------------------- | ------------------------- |
| Customer.io | 150 / sec             | 7,000                     |

## 🗄️ Supported Objects

We currently support all objects of [Customer.io's core API.](https://customer.io/docs/api/#section/Overview)

| **Object Name** | **Supported?** | **Create Fields?** |
| --------------: | :------------: | :----------------: |
|          Person |        ✅       |          ✅         |
|          Device |        ✅       |          ✅         |
|           Event |        ✅       |          ✅         |
|      Collection |        ✅       |          ✅         |
|  Manual Segment |        ✅       |          ✅         |

{% hint style="warning" %}
Make sure you know what identifiers are used in your Customer.io Workspace!
{% endhint %}

Customer.io strongly prefers the ID field to be used as the identifier for a Person record and recommends using your internal ID when possible. If you plan to use the email field, make sure your workspace has enabled [Using email as an identifier](https://customer.io/docs/workspaces/#migrate-workspace). You can read more about [Customer.io's identifier guidelines here](https://customer.io/docs/data-mapping-guide#describing-users-with-customer-attributes).

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** |              **Objects**              |
| -------------------: | :------------: | :-----------------------------------: |
| **Update or Create** |        ✅       | Person, Event, Device, Manual Segment |
|      **Update Only** |        ✅       |                 Person                |
|           **Append** |        ✅       |                 Event                 |
|           **Mirror** |        ✅       |       Collection, Manual Segment      |

🔋[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for this destination

## 💡 Things to know about Customer.io

There are a few unique features available when syncing to a Customer.io instance.

* **Events** are unique (literally!). Census will only send new database rows to Customer.io and so Events only support the **Append Only** behavior for syncs. In order to make sure an event is only ever published once, each row in your events source needs a globally unique ID.
* All objects support arbitrary custom fields.
  * If you are creating a sync for the first time:
    * Go to the `Which properties should be updated?` section and click **Add Mapping** at the bottom, and then click **Create new field**. Then, type in the name of the custom field as it appears in your Customer.io instance and hit **Save**. After that, you can select the field from your source that you want to send into that the Customer.io custom field.
  * If you are editing an existing sync's mapping:
    * Go to the sync's Configuration tab and in the `Mapped Fields` section, click **Edit**, click **Add Mapping** at the bottom, and then click **Create new field**. Then, type in the name of the custom field as it appears in your Customer.io instance and hit **Save**. After that, you can select the field from your source that you want to send into that the Customer.io custom field.

## 🚑 Need help connecting to Customer.io?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

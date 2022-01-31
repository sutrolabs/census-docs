---
description: This page describes how to use Census with Heap.io
---

# Heap.io

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect Heap.io to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com) now.
* Have your Heap.io account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

### **1. Get Your App ID from Heap.io**

Census needs only one piece of information to connect you to your Heap.io instance:

* Your Heap.io app ID. This can be found in the **Account** settings section under **Privacy & Security**, and it will be in the **Use the API** tab.

![](<../.gitbook/assets/Screen Shot 2022-01-27 at 3.08.05 PM.png>)

### 2. **Create the Census Connection**

Now that we have the app ID from Heap.io, we can now set up Heap.io as a Destination in Census.

1. In the **Connections** tab of Census, create a new Heap.io Service Connection.
2. You can provide whatever name you like.
3. Provide the app ID from Heap.io.
4. Save.

![Heap.io set up form in Census](<../.gitbook/assets/Screen Shot 2022-01-27 at 2.30.41 PM.png>)

### 3. Create your Model

Navigate to the [Model section of our Dashboard](https://app.getcensus.com/models)

Here you will can write a SQL query to select the data you want to see in Heap.io, or you can use a model from a dbt project or a Looker Look. Here are some ideas of data you could select

* The Lifetime Value of a customer
* The end date of a user's trial
* The date a user became active in your product
* The number of key activities a user did in your app in the last 7/30 days

Once you have created your model, click save.&#x20;

![](<../.gitbook/assets/Screen Shot 2022-01-27 at 3.31.32 PM.png>)

### 4. Create your first Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the Add Sync button

In the "What data do you want to sync?" section.

* For the Connection, select the data warehouse you've already connected (See Prerequisites).
* For the Source, select the model you created in step 3.

![Choose your connection an source (your model from step 3)](<../.gitbook/assets/Screen Shot 2022-01-27 at 3.46.33 PM.png>)

Next up is the "Where do you want to sync data to?" section.

* Pick the Heap.io connection you created in step 3.
* For Object, Select Account or User.

![Select which object you want to sync to](<../.gitbook/assets/Screen Shot 2022-01-27 at 3.49.02 PM.png>)

For the "How should changes to the source be synced?" section.&#x20;

* Select Update Or Create

![](<../.gitbook/assets/Screen Shot 2022-01-27 at 3.50.51 PM.png>)

For the "How are source and destination records matched?" section.&#x20;

* Pick the mapping key; for syncs to the User object the identifier is Identity and for the Account object the identifier is Account Id
* Select the field from your model you want mapped to the identifier.&#x20;

![](<../.gitbook/assets/Screen Shot 2022-01-27 at 4.06.50 PM.png>)

Finally, select the fields you want to update in the Mapper in the "Which Fields should be updated?" section. Here simply map the field from your Heap.io instance to the column from your model.

![](<../.gitbook/assets/Screen Shot 2022-01-27 at 4.15.03 PM.png>)

Click the Next button to see the final preview, which will have a recap of what will happen when you start the sync.

## 🗄️ Supported Objects

| **Object Name** | **Supported?** | **Identifiers** |
| --------------- | :------------: | --------------- |
| Account         |        ✅       | Account ID      |
| User            |        ✅       | Identity        |

🎒 [Contact us](mailto:support@getcensus.com) if you want Census to support more Objects for this destination

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

|    **Behaviors** | **Supported?** |  **Objects?** |
| ---------------: | :------------: | :-----------: |
| Update or Create |        ✅       | Account, User |

‌ 🔋 [Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for this destination



## 🚑 Need help connecting to Heap.io?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
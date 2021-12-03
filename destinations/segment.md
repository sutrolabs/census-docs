---
description: This page describes how to use Census with Segment.
---

# Segment

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Segment to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com) now.
* Have your Segment account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Elasticsearch](../sources/elasticsearch.md)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

## Segment Sync Setup

### 1. Create or get a Segment API key

* From within Segment, navigate to Settings > Workspace Settings > Access Management > Tokens. Or click [here](https://app.segment.com/\[YOUR-PROJECT-ID-GOES-HERE]/settings/access-management/tokens) and change the URL to add your Project Id.

![](<../.gitbook/assets/Screen Shot 2021-11-10 at 5.06.58 PM.png>)

* Click the Create Token Button and grant access as an Admin to the sources to which you want to sync.

![](<../.gitbook/assets/Screen Shot 2021-11-10 at 5.16.04 PM.png>)

* Copy the Created Token.

![](<../.gitbook/assets/Screen Shot 2021-11-12 at 11.15.31 AM.png>)

* Navigate to the [Connections Page](https://app.getcensus.com/connections) of Census, click on the "Add Service" button and select Segment, and past the created token in the designated field

![](<../.gitbook/assets/Screen Shot 2021-11-12 at 11.16.21 AM.png>)

* Census will convert this right here and now you're all set with the Segment Connection!

![Don't worry if the credential here is different!](<../.gitbook/assets/Screen Shot 2021-11-12 at 11.16.53 AM.png>)

Note: Census's permissions will be the same as this Segment token.



### 2. Connect your data warehouse

If you don't already have a data warehouse connected, follow one of our short guides depending on your data warehouse service:

* [Databricks](https://docs.getcensus.com/sources/databricks)
* [Elasticsearch](../sources/elasticsearch.md)
* [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
* [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
* [Postgres](https://docs.getcensus.com/sources/postgres)
* [Redshift](https://docs.getcensus.com/sources/redshift)
* [Rockset](https://docs.getcensus.com/sources/rockset)
* [Snowflake](https://docs.getcensus.com/sources/snowflake)

You should now have a connection to Segment and to your data warehouse! Let's start syncing user data.&#x20;

### 3. Create your first Model <a href="#3-create-your-first-model" id="3-create-your-first-model"></a>

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models).​‌

Here you will have to write SQL queries to select the data you want to join to a Segment User. Here are some ideas of data you should select‌.

* User with product usage properties
* User with the organization they are associated to
* User with the classification coming from a User Classification model

### 4. Create your first Sync <a href="#4-create-your-first-sync" id="4-create-your-first-sync"></a>

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button‌.

In the " **What data do you want to sync?"** section‌

* For the **Connection**, select the data warehouse you connected in step 2
* For the **Source,** select the model you created in step 3

Next up is the **"Where do you want to sync data to?"** section‌

* Pick the name of Segment service from step 1 as **the Connection**, right now the object we can sync to is [limited to **User**](segment.md#supported-objects)****

For the " **How should changes to the source be synced?"** section‌

* **Update or Create** will be preselected as it is [supported](segment.md#supported-sync-behaviors)
* Pick the right mapping key, we can sync based on userId from the Segment Identify call or to the device: AnonymousId

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section‌.

* Here simply map the fields from your model to the Segment User Properties you want to sync to. You can specify specific properties or "Sync All Properties" such that new columns in the source table will be created on the Segment User object according to the normalization rule you apply :magic\_wand:

The end result should look something like this​:

![](<../.gitbook/assets/Screen Shot 2021-11-12 at 11.37.07 AM.png>)

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync‌.

That's it! In 4 steps, you've connected Segment and started syncing user properties data from your warehouse 🎉

## 🗄 Supported Objects

Segment support is pretty straight forward!

| **Object Name** | **Supported?** |
| :-------------: | :------------: |
|       User      |        ✅       |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Segment.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects?** |
| -------------------: | :------------: | :----------: |
| **Update or Create** |        ✅       |      All     |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Segment.

## 🚑 Need help connecting to Segment?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

---
description: This page describes how to use Census with Braze.
---

# Braze

### Note on Braze API Costs

Census' sync engine sends updated or changed data by row, meaning that this includes all values of the sync, even if they have not changed. This works well with the majority of services but does cause additional usage for Braze. Please be aware that large data sets, particularly with  full syncs, can rapidly increase your Braze API usage.&#x20;

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Braze to Census and create your first sync.

{% embed url="https://youtu.be/qwa2BEuxEBs" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com) now.
* Have your Braze account ready, with create access for Braze API keys.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

### 1. Create a Braze API key

Braze lets you create a number of API keys, each with their own set of permissions. You'll almost certainly want to create a new API key for Census rather than reusing an existing one.

Within Braze's left navigation bar, scroll down to the very bottom. Under **App Settings** and click **Developer Console**.

Then, inside the **API Settings** tab, under **Rest API Keys**, click **+ Create New API Key**.

![](../.gitbook/assets/screely-1619749695118.png)

Provide a name you'll recognize ("Census" is a good choice) and select the following permissions:

* All User Data permissions, except for `users.delete`&#x20;
* `segments.list`
* This permission set may change as we add support for more Braze objects so you may want to grant more permissions now or plan to update these permissions in the future.&#x20;

Scroll down and click **Save API Key**.

Finally, copy the long code you see under **Identifier**. We'll use that in a minute.

![](../.gitbook/assets/screely-1619749895841.png)

### 2. Select your Braze API Endpoint

Braze requires that we use a slightly different URL to access your account depending on where it's been set up. See the [full list of all Braze API Endpoints](https://www.braze.com/docs/api/basics/#endpoints). In general, you just need the number from the URL you see in your browser when you're signed into Braze.\
\
For example, if your Braze URL is https://dashboard-**03**.braze.com/, then your API Endpoint should be https://rest.iad-**03**.braze.com.

### 3. Create the Census Connection

Great! Now let's pull it all together.&#x20;

1. In the **Settings** tab, Create a new Braze Service Connection in Census.\
   &#x20;![](../.gitbook/assets/screely-1619749986549.png)&#x20;
2. You can provide whatever name you like.
3. Provide the appropriate Braze Endpoint URL.
4.  Copy and paste your new Braze API key.\


    ![](../.gitbook/assets/screely-1619749992320.png)

And you're all set and ready to get syncing! 🎉

## 🗄 Supported Objects

Census currently supports syncing to the following Braze objects.

| **Object Name** | **Supported?** | Identifiers      |
| --------------: | :------------: | ---------------- |
|            User |        ✅       | External User ID |
|           Event |        ✅       | Event ID         |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Braze.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** |                       **Supported?**                      | **Objects?** |
| -------------------: | :-------------------------------------------------------: | :----------: |
| **Update or Create** | [✅](https://docs.getcensus.com/basics/alerts#sync-alerts) |     User     |
|           **Mirror** |                             ✅                             |     User     |
|           **Append** |                             ✅                             |     Event    |

Braze's Mirror behavior optionally supports a choice of two actions when a records is removed from the source. This can be configured when setting up the sync initially:

* **Delete record** - This is the typical behavior for most mirror syncs. When a record is removed from the source, the corresponding record will be deleted from Braze.&#x20;
* **Null out fields** - This is a new behavior for mirror syncs in Braze. In this case, when a record is removed from the source, the currently mapped fields of the synced will be removed from the destination record (by setting them to Null).

[Contact us](mailto:support@getcensus.com) if you want Census to support more sync behaviors for Braze.

## 🚑 Need help connecting to Braze?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

---
description: This page describes how to use Census with Microsoft Dynamics.
---

# Microsoft Dynamics

## Getting Started

This guide shows you how to use Census to connect your Microsoft Dynamics account to your data warehouse and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Microsoft Dynamics account ready.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Azure Synapse](../sources/azure-synapse.md)
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Elasticsearch](https://docs.getcensus.com/sources/elasticsearch)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [MySQL](https://docs.getcensus.com/sources/mysql)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)
  * [SQL Server](https://docs.getcensus.com/sources/sql-server)

### Step 1: Connect Microsoft Dynamics

{% hint style="info" %}
For Production Dynamics instances, the user to authenticate Census needs to have "Service Writer" permissions. For the [Default environment](https://docs.microsoft.com/en-us/power-platform/admin/environments-overview#the-default-environment), the user must be an Admin. Read more about this [here](https://docs.microsoft.com/en-us/power-platform/admin/database-security).
{% endhint %}

1. Log into Census and navigate to [Destinations](https://app.getcensus.com/destinations).
2. Click **New Destination** and select **Microsoft Dynamics** from the menu.
3. Follow the Microsoft Dynamics OAuth authentication flow, which will ask you to log in with your Microsoft Dynamics username and password.

Once complete, you'll see your new connection in the **Destinations** list. 👇

![](<../.gitbook/assets/Screen Shot 2022-06-23 at 10.54.40 AM.png>)

### Step 2: Create your model

When defining models, you'll write SQL queries to select the data you want to see in Microsoft Dynamics. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the **Models** page.
2. Click **Add Model**.
3. Enter a name for your model. You'll use this to select the model later.
4. Enter your SQL query. If you want to test the query, use the **Preview** button.
5. Click **Save Model**.

![Basic SQL query for a new model](../.gitbook/assets/202201\_Model\_Page.png)

### Step 3: Create your first sync

The sync will move data from your warehouse to Microsoft Dynamics. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose Microsoft Dynamics as the **Connection** and the object (aka entity in Microsoft Dynamics) that you want to sync to (see [Supported objects](microsoft-dynamics.md#supported-objects) for more detail).
4. Under **How should changes to the source be synced?**, choose **Update or Create** (see [Supported sync behaviors](microsoft-dynamics.md#supported-sync-behaviors) for options)
5. Under **How are source and destination records matched?**, select an **Identifier** for the model and for the Microsoft Dynamics object. Valid identifiers are single-columns keys for entities that you can set up in your Microsoft Dynamics instance (see [Supported objects](microsoft-dynamics.md#supported-objects) for more detail).
6. Under **Which properties should be updated?**, select which fields you would like to update.
7. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
8. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
9. Click **Create Sync.**

When configuring your sync, the page should look something like this: 👇

![Source, destination and sync operation selectors](<../.gitbook/assets/Screen Shot 2022-06-23 at 11.05.27 AM.png>)

![Sync identifier and mappings selectors](<../.gitbook/assets/Screen Shot 2022-06-23 at 11.06.35 AM.png>)

### Step 5: Confirm the synced data is in Microsoft Dynamics

Once your sync is complete, it's time to check your data. Open Microsoft Dynamics and check that the entity that you sent data to has updated entries.

If everything went well, that's it! You've started syncing data from your warehouse to Microsoft Dynamics! [🥳️](https://emojikeyboard.org/copy/Partying\_Face\_Emoji\_%F0%9F%A5%B3%EF%B8%8F?utm\_source=extlink)

And if anything went wrong, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## Supported objects

| **Object Name** | **Supported?** | **Sync Keys**                         |
| --------------: | :------------: | ------------------------------------- |
|     Entity name |        ✅       | All single-column keys for the entity |

All Microsoft Dynamic [entities](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/introduction-entities?view=op-9-1) are supported as objects to sync to in Census. Here is some documentation on defining keys for entities in Microsoft Dynamics:

* [Define keys in Microsoft Dynamics](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/define-alternate-keys-reference-records?view=op-9-1)
* [Define keys in Power Apps](https://docs.microsoft.com/en-us/power-apps/maker/data-platform/define-alternate-keys-portal) (Power Apps is the platform that Dynamics is built atop)

### Lookups to other records

Lookups from one Dynamics Entity to another in the same 365 workspace can be configured, and this happens via the single-column keys for the entity as such:

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption><p>The lookup by key needs to single-column keys</p></figcaption></figure>

{% hint style="info" %}
When you have a null lookup, or a reference from which you want to disassociate a record, you need to sync over null.

For a string example of a column in Snowflake:

`IFF(lookup_ref = '', NULL, lookup_ref) as lookup_ref`
{% endhint %}

## Supported sync behaviors

|     **Behavior** | **Supported?** | **Objects** |
| ---------------: | :------------: | :---------: |
| Update or Create |        ✅       |     All     |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Microsoft Dynamics.

## Need help connecting to Microsoft Dynamics?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

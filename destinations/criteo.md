# Criteo

## 🏃‍♀️ Getting Started

This guide shows you how to use Census to connect your Criteo account to your data warehouse and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Criteo account ready.
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

### Step 1: Connect Criteo

{% hint style="warning" %}
Criteo can only be authorized once to any Census instance. In order to create a second connection, you'll need to deauthorize Census first inside the Criteo UI.\
\
This can be done by a Criteo Admin from the page consent.criteo.com
{% endhint %}

1. Log into Census and navigate to [Connections](https://app.getcensus.com/connections).
2. Click **Add Service**.
3. Select **Criteo** from the menu
4. Follow the Criteo OAuth authentication flow, which will ask you to log in with your Criteo username and password.
5. Once logged in, select the Portfolio's you want Census to have access to and Approve
6. Finally once back in Census you'll select the Audience

Once complete, you'll see your new connection in the **Service Connections** list. 👇

![Connections page with Criteo](<../.gitbook/assets/Screen Shot 2022-02-23 at 5.51.59 PM.png>)

### Step 2: Create your model

When defining models, you'll write SQL queries to select the data you want to see in Criteo. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the **Models** page.
2. Click **Add Model**.
3. Enter a name for your model. You'll use this to select the model later.
4. Enter your SQL query. If you want to test the query, use the **Preview** button.
5. Click **Save Model**.

![Basic SQL query for a new model](../.gitbook/assets/202201\_Model\_Page.png)

### Step 3: Create your first sync

The sync will move data from your warehouse to Criteo. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose Criteo as the **Connection** and "Audience" as the **Object**. (See [Supported objects](criteo.md#supported-objects) for options.)
4. Under **How should we identify audience members?**, select an **Identifier** for the model and for Criteo. We recommend using an internal ID when possible. (See [Supported objects](criteo.md#supported-objects).)
5. Under **Audience Sync**, choose the **Audience ID Name** that you want to sync to, or choose to Create New List. Also choose what to do when a record is removed from the source.
6. Set up the Audience property mappings that you want to update by mapping a column in your model to a property in Criteo.
7. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
8. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
9. Click **Create Sync.**

When configuring your sync, the page should look something like this: 👇

<figure><img src="../.gitbook/assets/screely-1670609548345.png" alt=""><figcaption></figcaption></figure>

### Step 5: Confirm the synced data is in Criteo

Once your sync is complete, it's time to check your data. Open Criteo and check that the Audience updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to Criteo! [🥳️](https://emojikeyboard.org/copy/Partying\_Face\_Emoji\_%F0%9F%A5%B3%EF%B8%8F?utm\_source=extlink)

And if anything went wrong, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## 🗄 Supported objects

| **Object Name** | **Supported?** | **Identifiers**                                            |
| --------------: | :------------: | ---------------------------------------------------------- |
|        Audience |        ✅       | GUM Cookie ID, Mobile Ad ID, Email, LiveRamp Identity Link |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional objects for Criteo.

## 🔄 Supported sync behaviors

|     **Behavior** | **Supported?** | **Objects** |
| ---------------: | :------------: | :---------: |
| Update or Create |        ✅       |   Audience  |
|           Mirror |        ✅       |   Audience  |

{% hint style="info" %}
Learn about all of our sync behaviors in [Core Concepts](../basics/core-concept/#sync-behaviors).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Criteo.

## 🚑 Need help connecting to Criteo?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

---
description: This page describes how to use Census with Zendesk.
---

# Zendesk

## Getting started

In this guide, we will show you how to connect Zendesk to Census and create your first sync.

### Prerequisites

* Census account: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* Zendesk account
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Azure Synapse](../sources/available-sources/azure-synapse.md)
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Elasticsearch](https://docs.getcensus.com/sources/elasticsearch)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [MySQL](https://docs.getcensus.com/sources/mysql)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)
  * [SQL Server](https://docs.getcensus.com/sources/sql-server)

### Step 1: Connect Zendesk

1. Log into Census and navigate to the [**Destinations**](https://app.getcensus.com/destinations) page.
2. Click **New Destination**.
3. Select **Zendesk** from the dropdown list.
4. Follow the Zendesk authentication flow and login with the desired account. The Zendesk connection within Census will have the permissions of the connected user account.

Your end state should look something like this: 👇

![Destinations page with Zendesk](../.gitbook/assets/202110_Service_Connection_Zendesk.png)

### Step 2: Connect your data warehouse

The steps for connecting your data warehouse will depend on your technology. See the following guides:

* [Databricks](../sources/available-sources/databricks.md)
* [Google BigQuery](../sources/available-sources/google-bigquery.md)
* [Google Sheets](google-sheets.md)
* [Postgres](../sources/available-sources/postgres.md)
* [Redshift](../sources/available-sources/redshift.md)
* [Snowflake](../sources/available-sources/snowflake.md)

After setting up your warehouse, your **Destinations** page should look something like this: 👇

![Destinations page with data warehouse](../.gitbook/assets/202110_Connections_Generic.png)

### Step 3: Create your model

When defining models, you'll write SQL queries to select the data you want to see in Zendesk. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the **Models** page.
2. Enter a name for your model. You'll use this to select the model later.
3. Enter your SQL query. If you want to test the query, use the **Preview** button.
4. Click **Save Model**.

![Basic SQL query for a new model](../.gitbook/assets/202109_Outreach_Basic_Model.png)

### Step 4: Create your first sync

The sync will move data from your warehouse to Zendesk. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose **Zendesk** as the **Connection** and an **Object** in Zendesk. (See [Supported objects](zendesk.md#supported-objects).)
4. Under **How should changes to the source be synced?**, choose **Update or Create**. (See [Supported sync behaviors](zendesk.md#supported-sync-behaviors).)
5. Under **How are source and destination records matched?**, select a mapping key. We recommend mapping an internal ID property in your database to the **External ID** field in Zendesk. (See [Supported objects](zendesk.md#supported-objects).)
6.  Under **Which properties should be updated?**, select the fields you want to update by mapping a field in Zendesk to a column in your model. Choose a mapping setting:

    * **Set** overrides the existing value in Zendesk if the field is already populated.
    * **Only If Empty** does not set the value if the field is already populated.
    * For any properties that accept lists of values such as the Organization or Tags property, instead you'll see **Replace**. Replace mappings override any existing values or relationships for the property.

    Note that there are some gotchas with updating Zendesk data. Check out [Things to know about the Zendesk destination](zendesk.md#things-to-know-about-the-zendesk-destination).
7. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
8. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
9. Click **Create Sync**.

When configuring your sync, the page should look something like this: 👇

![Sync setup for Zendesk](../.gitbook/assets/202110_Zendesk_Sync.png)

### Step 5: Confirm the synced data in Zendesk

Once your sync is complete, it's time to check your data. Open Zendesk and check that the records updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to Zendesk! 🥳️

And if anything went wrong, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## Things to know about the Zendesk destination

The way that Zendesk updates certain properties is complex.

### Additional permissions required for syncs to the User object

Census utilizes Zendesk's Bulk User Import api endpoints to most efficiently sync your user data to Zendesk.

Bulk user imports are not enabled by default in Zendesk accounts. The account owner must contact [Zendesk Customer Support](https://support.zendesk.com/hc/en-us/articles/4408843597850) to enable the imports.

If data imports are not enabled a 403 Forbidden error is returned.

### Setting Organizations on the End User object

In Zendesk, users (records in the **End User** object) can belong to multiple **Organizations**. When syncing the **End User** object, you can provide either a single **External ID** value or a list of values.

{% hint style="info" %}
Support for multiple organization relationships is an optional setting in Zendesk. See the [Zendesk documentation](https://support.zendesk.com/hc/en-us/articles/204281436-Enabling-multiple-organizations-for-users) for details.
{% endhint %}

To link a user to multiple organizations, you'll need to format the list of **External ID** values as a JSON array of strings, for example:

```
["Team A", "Team B", "Team C"]
```

When syncing the **Organizations** property, Census will overwrite any existing relationships with the provided value. To maintain existing relationships, make sure that the corresponding External ID values are included in the array.

### Setting the Tags property

{% hint style="info" %}
Because of the way tags work in Zendesk, we don't recommend them for syncs. When possible, use dropdown and checkbox properties instead.
{% endhint %}

In Zendesk, the **Ticket**, **End User**, and **Organization** objects all include a **Tags** property. Tickets automatically pick up tags from related users and organizations. When configuring custom dropdown and checkbox fields in Zendesk, you can also configure those fields to add specific tags.

If you need to update the Tags property directly, keep these details in mind:

* Tag names cannot contain spaces. Zendesk will treat spaces as separators between tags.
* You can update the **Tags** property with multiple values by providing a JSON array, a space-separated list, or comma-separated list.
* Syncing the **Tags** property will replace any existing tags on the records. To maintain existing tags, you'll need to make sure they appear in the list of tags you provide from your data source.

### Updating a dropdown property

To update a dropdown property, the Zendesk API requires that you provide the API name of the dropdown option rather than the user-visible label.

By default, the API name is the user-visible label, but converted to lowercase and snake\_case, for example, **Paid User** becomes **paid\_user**. To update a dropdown property in this example, you'd provide the value **paid\_user**.

If the Zendesk API names have not been modified, you can transform the label values using the following SQL:

```
lower(replace(column_name, ' ', '_'))
```

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Census currently supports syncing to the following Zendesk objects:

| **Object Name** | **Supported?** | **Sync Keys**                    | **Behavior**                          |
| --------------: | :------------: | -------------------------------- | ------------------------------------- |
|        End User |        ✅       | External ID (recommended), Email | Update or Create, Update Only, Delete |
|    Organization |        ✅       | External ID (recommended), Name  | Update or Create, Update Only, Delete |
|          Ticket |        ✅       | External ID                      | Update or Create, Update Only, Delete |
|  Custom Objects |        ✅       | External ID                      | Update or Create, Update Only         |
|  Ticket Comment |        ✅       | Comment ID                       | Add                                   |

Please note that Zendesk requires the `Name` property for the End User object. Feel free to check out Zendesk's documentation [here](https://developer.zendesk.com/api-reference/ticketing/users/users/#json-format).

{% hint style="warning" %}
**Warning**

**Delete** syncs can result in data loss! Census recommends you backup this data if you're concerned about accidentally deleting the wrong records.
{% endhint %}

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Zendesk objects and/or behaviors.

## Need help connecting to Zendesk?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

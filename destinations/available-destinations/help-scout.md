---
description: This page describes how to use Census with Help Scout
---

# Help Scout

## Getting Started

In this guide, we will show you how to connect Help Scout to Census.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Help Scout account ready. If you need one, create a [free trial with Help Scout](https://www.helpscout.com/?utm_source=partner\&utm_campaign=partner-integration-marketplace-listing\&utm_content=census) now.
* Have your data source properly configured within Census. See our docs for each supported data source for further information:
  * [Azure Synapse](../sources/available-sources/azure-synapse.md)
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Elasticsearch](../sources/available-sources/elasticsearch.md)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [MySQL](../sources/available-sources/mysql.md)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)
  * [SQL Server](../sources/available-sources/sql-server.md)

### Step 1: Connect Help Scout

* Once you are in Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button and find Help Scout from the dropdown list

![](<../.gitbook/assets/Screen Shot 2022-06-25 at 8.34.07 AM.png>)

* You'll be taken to a Help Scout OAuth screen

![](<../.gitbook/assets/Screen Shot 2022-06-24 at 5.31.14 PM.png>)

* Next you'll be taken back to Census where you'll find a new Help Scout connection!

![](<../.gitbook/assets/Screen Shot 2022-06-25 at 8.36.52 AM.png>)

### Step 2: Create a Model

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models).​‌

Here you can write a SQL query to select the data you want to see in Help Scout, or you can use a model from a dbt project or a Looker Look. You can also use tables or views already in your data warehouse. Here are some ideas of data you could select

* The Lifetime Value of a customer
* The end date of a user's trial
* The date a user became active in your product
* The number of key activities a user did in your app in the last 7/30 days

![](<../.gitbook/assets/Screen Shot 2022-01-27 at 3.31.32 PM.png>)

### Step 3: Create your Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the Add Sync button

In the "**What data do you want to sync?**" section.

* For the Connection, select the data warehouse you've already connected (See Prerequisites).
* For the Source, select the model you created in step 3.

![Choose your connection an source (your model from step 3)](<../.gitbook/assets/Screen Shot 2022-06-25 at 8.46.50 AM.png>)

Next up is the "**Where do you want to sync data to?**" section.

* Pick the Help Scout connection you created.
* Select the Customer object

![Select which object you want to sync to](<../.gitbook/assets/Screen Shot 2022-06-25 at 8.47.31 AM.png>)

For the "**How should changes to the source be synced?**" section.

* Select either **Update or Create** or **Update Only**

![](<../.gitbook/assets/Screen Shot 2022-03-31 at 11.46.19 AM.png>)

For the "**How are source and destination records matched?**" section.

* Pick the mapping key. For syncs to the Customer object the identifier is Primary Email.
* Select the field from your model you want as the identifier.

![](<../.gitbook/assets/Screen Shot 2022-06-25 at 8.50.21 AM.png>)

Finally, select the fields you want to update in the Mapper in the "**Which Properties should be updated?**" section. Here simply map the field from your Help Scout instance to the column from your model.

![](<../.gitbook/assets/Screen Shot 2022-06-25 at 8.50.52 AM.png>)

Click the **Next** button to see the final preview, which will have a recap of what will happen when you start the sync and then click **Create Sync**!

## Supported Objects

| **Object Name** | **Supported?** | **Sync Keys** |
| --------------: | :------------: | ------------- |
|        Customer |        ✅       | Primary Email |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Help Scout.

## Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/core-concept/#sync-behaviors) documentation.
{% endhint %}

|    **Behaviors** | **Supported?** | **Objects** |
| ---------------: | :------------: | :---------: |
| Update or Create |        ✅       |     All     |
|      Update Only |        ✅       |     All     |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Help Scout.

### Syncing to the Customer Object:

**Address:** When updating address fields on a Customer record please note that if one of the below is present in your sync then all have to be included in the sync configuration. This is because all four fields are required by Help Scout to update the address ([Help Scout documentation here](https://developer.helpscout.com/mailbox-api/endpoints/customers/address/create/#request-fields)).

* `City`, `State`, `Postal Code`, `Country`

## Need help connecting to Help Scout?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

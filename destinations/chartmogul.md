---
description: >-
  This page describes how to use Census to sync data from your warehouse to
  ChartMogul.
---

# ChartMogul

## Getting Started

In this guide, we will show you how to connect ChartMogul to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your ChartMogul account ready.
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

### 1. Generate a ChartMogul API Key

In your ChartMogul account:

1. Navigate to **Profile > View Profile**
2. Scroll down to **API Keys**
3. Click **New API Keys**
4. Hold onto this API Key for the next section, you'll need it!

For more details on finding your ChartMogul API keys, you may [follow ChartMogul's documentation here.](https://dev.chartmogul.com/docs/authentication)

### 2. Connect ChartMogul to Census

* Head back to Census and navigate to [Destinations](https://app.getcensus.com/destinations).
* Click the New Destination button.
* Select ChartMogul in the dropdown list
* Paste your ChartMogul account's **API Key**. Save your connection and if everything is set up correctly, you should see a successful connection test verifying the connection.

### 3. Connect your Data Warehouse

Please follow one of our short guides depending on your data warehouse technology.

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)

### 4. Create your first model

Next we'll define the data you'll send to ChartMogul. Navigate to the [Models](https://app.getcensus.com/models) page.

Here you have the ability to write SQL queries to select the data you want to see in ChartMogul. (If you already have you data available in a table or view, you can skip this step and connect your sync directly to that).

Once you have created your model, click **Save**.

### 5. Create your first Sync

For our sample sync, we're going to update a ChartMogul **Customer** record.

Head to the [Sync page](https://app.getcensus.com/syncs) and click the Add Sync button

In the "What data do you want to sync?" section

* For the Connection, select the data warehouse you connected in step 2
* For the Source, select the model you created in step 3

Next up is the "Where do you want to sync data to?" section.

* Pick ChartMogul as the Connection
* For Object, we will be using Customer

For the "How should changes to the source be synced?" section.

* Select Update Only

Now we'll start mapping fields. ChartMogul requires two fields to be mapped: the customer's External ID and their Data Source ID. You can find the Data Source ID by navigating to [this page](https://t.sidekickopen01.com/s3t/c/5/f18dQhb0S7kF8cFC2RW1K7Z1759hl3kW7\_k2841CX6NGW35QNwB7tCtH0Vs7zDQ8qd1Kwf197v5Y04?te=W3R5hFj4cm2zwW3zfPSj3F7xMPW4fKXXf4hHZdBW43T4MG1LwsHHW3yLX3g3zhrVDW49NLhq3zhrqJF4cNcV-W1v31\&si=8000000017473620\&pi=3d1e4afe-99d8-4b66-b041-de8a431bfb88) within ChartMogul and clicking the gear icon next to the Data Source.

After the required fields, you can add any further fields you like.

Click the Next button to see the final preview, which will have a recap of what will happen when you start the sync.

### 6. Confirm the data is in ChartMogul

Now go back to ChartMogul, and check that the customer has been updated as expected.

That's it! In 6 steps, you've connected Census and started syncing product data from your warehouse to ChartMogul 🎉

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Census currently supports syncing to the following ChartMogul objects.

| **Object Name** | **Supported?** |                   **Sync Keys**                  |       **Behaviors**      |
| --------------: | :------------: | :----------------------------------------------: | :----------------------: |
|        Customer |        ✅       | Data Source ID + External ID (both are required) | Update or Create, Update |
|         Invoice |        ✅       |                    External ID                   |            Add           |
|     Transaction |        ✅       |                    External ID                   |            Add           |

{% hint style="info" %}
Syncs to the ChartMogul **Customer** object require both the Data Source ID and the External ID to ensure the customer is updated or created as expected. This is necessary because External IDs can be duplicated across Data Sources. You can find the Data Source ID by navigating to [this page](https://t.sidekickopen01.com/s3t/c/5/f18dQhb0S7kF8cFC2RW1K7Z1759hl3kW7\_k2841CX6NGW35QNwB7tCtH0Vs7zDQ8qd1Kwf197v5Y04?te=W3R5hFj4cm2zwW3zfPSj3F7xMPW4fKXXf4hHZdBW43T4MG1LwsHHW3yLX3g3zhrVDW49NLhq3zhrqJF4cNcV-W1v31\&si=8000000017473620\&pi=3d1e4afe-99d8-4b66-b041-de8a431bfb88) in ChartMogul and clicking the gear icon next to the desired Data Source.
{% endhint %}

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Chart Mogul objects and/or behaviors

## :question:FAQ

#### How do I include line items alongside my invoices?

Line items must be modelled as a JSON array on the Invoice record itself. This is necessary because Line Items do not have their own endpoint and must be supplied inline on Invoice creation. For an example of how this type of JSON array might look, see the "line\_items" [field here within ChartMogul's documentation](https://dev.chartmogul.com/reference/import-customers-invoices).

## Need help connecting to ChartMogul?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

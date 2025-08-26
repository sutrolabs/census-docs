---
description: This page describes how to use Census with Sendrid.
---

# SendGrid

## Getting Started

‌In this guide, we will show you how to connect SendGrid to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your SendGrid account ready.
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

### 1. Gather SendGrid API Credentials

To connect Census to SendGrid, you'll need to collect one piece of information:

* API Token

From the home page of your SendGrid account click on **Settings** in the left hand navigation bar then select **API Keys.** From the **API Keys** page you can create a new key or use an existing one.

![Create a New API Key in Sendgrid](<../.gitbook/assets/Screen Shot 2022-05-24 at 5.38.48 PM.png>)

{% hint style="info" %}
Please note that SendGrid will only allow you to view your API key once when initially created.
{% endhint %}

### 3. Adding Credentials to Census

With the SendGrid API key, return to Census and visit the **Destinations** tab. Click on the **New Destination** button and select **SendGrid** from the menu. Copy and paste the API Key into the dialog and hit save. You should be clear to create a new sync!

![](<../.gitbook/assets/Screen Shot 2022-05-24 at 5.44.57 PM.png>)

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Census currently supports syncing to the following SendGrid objects.

| **Object Name** | **Supported?** | Identifiers           | **Behaviors**                 |
| --------------: | :------------: | --------------------- | ----------------------------- |
|         Contact |        ✅       | Email                 | Update or Create, Update Only |
|            List |        ✅       | Email                 | Update or Create              |
| Email Templates |        ✅       | Any unique identifier | Send                          |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

Contact the support team if you want Census to support more Sendgrid objects and/or behaviors.

## Syncing to Subject Field

To sync to the email subject line, first update the email subject in the Sendgrid dynamic template to be `{{{subject}}}`. Then, when creating a sync in Census, add a custom destination field called `subject` in the sync mapper and map it to the corresponding source field containing the subject line data.

## Need help connecting to SendGrid?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

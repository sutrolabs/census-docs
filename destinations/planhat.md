---
description: >-
  This describes how you can connect Census to the Customer Success tool:
  Planhat.
---

# Planhat

## Getting Started

In this guide, we will show you how to connect Planhat to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Planhat account ready.
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

### 1. Generate a Planhat API Key

In your Planhat account:

1. Navigate to **Settings > Service Accounts**
2. Create an **API Key**
3. Hold onto this API Key for the next section, you'll need it!

{% hint style="warning" %}
In Planhat, once a token is created, it will appear once and last forever. Make sure to copy and store it securely once generated. It should be over 340 characters long.
{% endhint %}

### 2. Connect Planhat to Census

* Head back to Census and navigate to [Destinations](https://app.getcensus.com/destinations).
* Click the New Destination button.
* Select Planhat in the dropdown list.
* Paste your Planhat account's **API Key**. Save your connection and if everything is set up correctly, you should see a successful connection test verifying the connection.
* Paste the region in the region box. If your Planhat app url is `app-us3.planhat.com`, paste **us3**. If your Planhat api endpoint is simply`api.planhat.com`, the value of **default** should be used here.

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Census currently supports syncing to the following Planhat objects.

<table data-header-hidden><thead><tr><th width="177.08984375" align="right"></th><th align="center"></th><th></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Sync Keys</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Activity</td><td align="center">✅</td><td>Any unique ID</td><td>Send</td></tr><tr><td align="right">Asset</td><td align="center">✅</td><td>Source ID, External ID</td><td>Update or Create, Update Only</td></tr><tr><td align="right">Churn</td><td align="center">✅</td><td>Source ID</td><td>Update or Create</td></tr><tr><td align="right">Company</td><td align="center">✅</td><td>Source ID, External ID</td><td>Update or Create, Update Only</td></tr><tr><td align="right">End User</td><td align="center">✅</td><td>Source ID</td><td>Update or Create</td></tr><tr><td align="right">Invoices</td><td align="center">✅</td><td>External ID, Source ID</td><td>Update or Create</td></tr><tr><td align="right">License</td><td align="center">✅</td><td>Source ID, External ID</td><td>Update or Create</td></tr><tr><td align="right">Metric</td><td align="center">✅</td><td>External ID</td><td>Send</td></tr><tr><td align="right">NPS</td><td align="center">✅</td><td>Source ID</td><td>Update or Create</td></tr><tr><td align="right">Opportunity</td><td align="center">✅</td><td>Source ID, External ID</td><td>Update or Create, Update Only</td></tr><tr><td align="right">Sale</td><td align="center">✅</td><td>Source ID, External ID</td><td>Update or Create, Update Only</td></tr></tbody></table>

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Planhat objects and/or behaviors

## Need help connecting to Planhat?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

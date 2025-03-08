---
description: This page describes how to use Census with Enterpret.
---

# Enterpret

{% hint style="info" %}
Entepret is a Partner-Built Destination. See our [PBD announcement](https://www.getcensus.com/blog/announcing-partner-built-destinations) and [docs](https://developers.getcensus.com/custom-destinations/partner-destinations) for more info.
{% endhint %}

## Enterpret

### Getting Started

In this guide, we will show you how to connect Enterpret to Census and create your first sync.

#### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Enterpret
* account ready, with admin access to create API-only users and API credentials.
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

#### 1. Generate an API Token within Enterpret

Before setting up the Enterpret connection within Census, you'll first need to generate an API key within Enterpret.

Further instructions on how to configure your API key within Enterpret [available here!](https://helpcenter.enterpret.com/en/articles/8317703-census-integration) For instructions more specifically on syncing to Users and Accounts select there is additional documentation [available here](https://helpcenter.enterpret.com/en/articles/8611269-syncing-users-and-accounts).

#### 3. Adding API Key to Census

With your API key, return to Census and visit the **Destinations** tab. Click on the **New Destination** button and select **Enterpret** from the menu. Copy and paste the value into the dialog and hit save. You should be clear to create a new sync!

<figure><img src="../.gitbook/assets/Screenshot 2024-02-05 at 12.10.36 PM.png" alt=""><figcaption></figcaption></figure>

### Supported Objects

Census currently supports syncing to the following Enterpret objects.

<table data-header-hidden><thead><tr><th width="236.33333333333331" align="right"></th><th width="214" align="center"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Sync Keys</strong></td></tr><tr><td align="right">Account</td><td align="center">✅</td><td>Id</td></tr><tr><td align="right">Review Records</td><td align="center">✅</td><td>Id</td></tr><tr><td align="right">Survey Response Records</td><td align="center">✅</td><td>Id</td></tr><tr><td align="right">User</td><td align="center">✅</td><td>Id</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Enterpret.

### Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

<table data-header-hidden><thead><tr><th width="182.33333333333331" align="right"></th><th width="156.42460567823346" align="center"></th><th align="center"></th></tr></thead><tbody><tr><td align="right"><strong>Behaviors</strong></td><td align="center"><strong>Supported?</strong></td><td align="center"><strong>Objects</strong></td></tr><tr><td align="right"><strong>Create Only</strong></td><td align="center">✅</td><td align="center">Account, Review Records, Survey Response Records, User</td></tr><tr><td align="right"><strong>Update Only</strong></td><td align="center">✅</td><td align="center">Account, User</td></tr><tr><td align="right"><strong>Update or Create</strong></td><td align="center">✅</td><td align="center">Account, User</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Enterpret.

### Need help connecting to Enterpret?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

---
description: This page describes how to use Census with Google Ads.
---

# Google Ads

## 🏃‍♀️ Getting Started

{% hint style="success" %}
Just a heads up: We use the new [Google Ads API](https://developers.google.com/google-ads/api/docs/start) as opposed to the older AdWords API.
{% endhint %}

In this guide, we will show you how to connect Google Ads to Census.

{% embed url="https://youtu.be/COk7s0axxVw" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Google Ads account ready.
  * To create Customer Match syncs, your Google Ads Account will need access to the Customer Match feature. See [Google's Customer Match policy](https://support.google.com/adspolicy/answer/6299717?hl=en) for more details.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Azure Synapse](../../sources/azure-synapse.md)
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

### 1. Connect Google Ads

* Once you are in Census, Navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select Google Ads in the dropdown list.

![](../../.gitbook/assets/screely-1619113580005.png)

Follow Google OAuth flow to connect your Google Ads account.&#x20;

![](../../.gitbook/assets/screely-1619118724964.png)

Finally, select the Google Ads account you'd like to sync to

![](../../.gitbook/assets/screely-1619118759931.png)

### 2. Connect your Data Warehouse

Please follow one of our short guides depending on your data warehouse technology

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)
* [Databricks](../../sources/databricks.md)

After setting up your warehouse, your Census Connections Page should look like this:

![](../../.gitbook/assets/screely-1619121030102.png)

## 🗄 Supported Objects

| Service                                                                                                         | **Object Name** | **Supported?** | Identifiers                                        |
| --------------------------------------------------------------------------------------------------------------- | --------------: | :------------: | -------------------------------------------------- |
| [Customer Match Lists (Audiences)](https://docs.getcensus.com/destinations/google-ads/customer-match-audiences) |        Customer |        ✅       | <p>User ID, Mobile ID, Email, <br>Phone Number</p> |
| [Offline Conversions](https://docs.getcensus.com/destinations/google-ads/offline-conversions)                   |     Click, Call |        ✅       | Click ID, Caller ID                                |

[Contact us](mailto:support@getcensus.com) if you're looking for additional Google Ads objects.

## :question:Did my sync work? It says completed but it isn't showing the updated timestamp I expect.

The standard place where bulk files uploading update status doesn't actually update when using Census. Instead, you've gotta hover on a specific card.&#x20;

Steps to get there:

1. Open your google ads account
2. Navigate to Tools & Settings > Audience Manager
3. Hover over the name of your desired audience in the list.
4. Expand the section labeled `Customers based on email, phone, and/or mailing address uploads`
5. Within that, you'll see a `Last upload` label.

![](<../../.gitbook/assets/Screen Shot 2021-11-16 at 10.34.57 AM.png>)

If that date isn't the same time as the most recent sync completed, please reach out via our in-app chat and we will investigate it with you.

## 🚑 Need help connecting to Google Ads?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

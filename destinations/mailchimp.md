---
description: This page describes how to use Census with Mailchimp.
---

# Mailchimp

## 🏃‍♀️⠀Getting Started

In this guide, we will show you how to connect Mailchimp to Census and create your first sync.

{% embed url="https://youtu.be/tu3hr3BV6Sg" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com) now.
* Have your Mailchimp account ready.
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

### 1. Connect Census to Mailchimp <a href="#id-1-connect-census-to-braze" id="id-1-connect-census-to-braze"></a>

In the **Destinations** page in Census, Click the **New Destination** button under the **Destinations** section, and select Mailchimp.

You will be redirected to a page to log in to Mailchimp to authorize your account to Census. Once you enter your credentials and click the **Log In** button, you'll see a page like the image below, confirming you want to authorize Census.

![](<../.gitbook/assets/Screen Shot 2021-04-13 at 10.08.02 AM.png>)

Once you've authorized Census, you'll be redirected back to the Destinations page in Census and you should see your Mailchimp connection there.

If you want to see your connections in Mailchimp in the future, simply navigate to the **Profile** page, and scroll down to the **Connections and notifications** section.

## 💡⠀Mailchimp Field Quirks

{% hint style="info" %}
Please note that the mandatory status field only accepts the following values **in lower case**: `"subscribed"`, `"unsubscribed"`, `"cleaned"`, or `"pending"`.
{% endhint %}

With Mailchimp, the API endpoint needs a Status field value, so if you find yourself seeing this error:

![Oh no!](<../.gitbook/assets/Screen Shot 2022-07-21 at 5.30.25 PM.png>)

_But_ you don't want to overwrite existing Statuses in Mailchimp, you just need to provide a mapping to the field labelled, "**Status For New Subscriber**".

Then your test sync, or completed syncs will be good to go, like this one:

![SUCCESS!](<../.gitbook/assets/Screen Shot 2022-07-21 at 5.42.49 PM.png>)

{% hint style="danger" %}
If you do want to update the Status field, you can include that instead. However, we **highly** recommend understanding your organization's implications of potentially re-subscribing a member that has previously unsubscribed.
{% endhint %}

For more details, take a look at Mailchimp's [API documentation](https://mailchimp.com/developer/marketing/api/list-members/update-list-member/).

## 🗄⠀Supported Objects

|       **Object Name** | **Supported?** | Identifiers                                                    |
| --------------------: | :------------: | -------------------------------------------------------------- |
| List/Audience Members |        ✅       | <p>Email Address,<br>Prehashed Email Address (update-only)</p> |

#### Prehashed Email Identifiers

To prehash your emails, first lowercase the email address and then apply an MD5 hash, both which can be done directly in SQL. For example, here's the SQL you'd use in Snowflake (syntax for other data warehouses vary slightly)

`SELECT MD5(LOWER('Example@company.co'))`

#### Status and Unsubscribing List Members

The Mailchimp `status` field supports one of four values: `subscribed`, `unsubscribed`, `cleaned`, or `pending`. To unsubscribe a member from a particular list, simply set the status field to `unsubscribed`.

#### Tags

Mailchimp `tags` field can be set by providing an array of string values as structured data. [Read more about syncing Structured Data](../basics/data-defining/defining-source-data/structured-data.md) using Census.

## 🔄⠀Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects** |
| -------------------: | :------------: | :---------: |
| **Update or Create** |        ✅       |     All     |
|      **Update Only** |        ✅       |     All     |

## 🚑⠀Need help connecting to Mailchimp?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

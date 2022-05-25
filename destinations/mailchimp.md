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

### 1. Connect Census to Mailchimp <a href="#1-connect-census-to-braze" id="1-connect-census-to-braze"></a>

In the **Connections** page in Census, click the **Add Service** button under the **Service Connections** section, and select Mailchimp.

You will be redirected to a page to log in to Mailchimp to authorize your account to Census. Once you enter your credentials and click the **Log In** button, you'll see a page like the image below, confirming you want to authorize Census.

![](../.gitbook/assets/screen-shot-2021-04-13-at-10.08.02-am.png)

Once you've authorized Census, you'll be redirected back to the Connections page in Census and you should see your Mailchimp connection there.

If you want to see your connections in Mailchimp in the future, simply navigate to the **Profile** page, and scroll down to the **Connections and notifications** section.

## 💡⠀Mailchimp Field Quirks

There are two mandatory fields for the Mailchimp connection: **email** and **status**.

Please note that the mandatory status field only accepts the following values: `"subscribed"`, `"unsubscribed"`, `"cleaned"`, or `"pending"`.

In addition, pre-hashed emails can be used as the record identifier for syncs with the Update behavior. The hash must be the MD5 hash of the lowercase version of the list member's email.

For more details, take a look at Mailchimp's [API documentation](https://mailchimp.com/developer/marketing/api/list-members/update-list-member/).

## 🗄⠀Supported Objects

|       **Object Name** | **Supported?** | Identifiers                                                     |
| --------------------: | :------------: | --------------------------------------------------------------- |
| List/Audience Members |        ✅       | <p>Email Address, <br>Prehashed Email Address (update-only)</p> |

#### Prehashed Email Identifiers

To prehash your emails, first lowercase the email address and then apply an MD5 hash, both which can be done directly in SQL. For example, here's the SQL you'd use in Snowflake (syntax for other data warehouses vary slightly)

`SELECT MD5(LOWER('Example@company.co'))`

#### Status and Unsubscribing List Members

The Mailchimp `status` field supports one of four values: `subscribed`, `unsubscribed`, `cleaned`, or `pending`. To unsubscribe a member from a particular list, simply set the status field to `unsubscribed`.

#### Tags

Mailchimp `tags` field can be set by providing an array of string values as structured data. [Read more about syncing Structured Data](../basics/defining-source-data/structured-data.md) using Census.

## 🔄⠀Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects?** |
| -------------------: | :------------: | :----------: |
| **Update or Create** |        ✅       |      All     |
|      **Update Only** |        ✅       |      All     |

## 🚑⠀Need help connecting to Mailchimp?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

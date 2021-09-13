---
description: This page describes how to use Census with Slack.
---

# Slack

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect your Slack workspace to Census and create your first sync.

### Prerequisites

* [Create a Free Trial Census Account](https://app.getcensus.com/)
* Have your Slack account ready
* Have the proper credentials to access to your data source. See our docs for each support data source here:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

### 1. Connect Census to Slack <a id="1-connect-census-to-braze"></a>

In the **Connections** page in Census, click the **Add Service** button under the **Service Connections** section, and select Slack.

If you are not already logged in to Slack, you will be redirected to a page to log in to Slack to authorize your account to use Census. Once you are logged in, you'll see a page like the image below, confirming you want to authorize Census.

![](../.gitbook/assets/screen-shot-2021-09-13-at-9.39.16-am.png)

Once you've authorized Census, you'll be redirected back to the Connections page in Census and you should see your Slack connection there.

### 2. Connect your Data Warehouse

Please follow one of our short guides depending on your data warehouse technology:

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)

### 3. Create your first Model

Now navigate to the [Model section of our Dashboard](https://app.getcensus.com/models)

Here you will have to write SQL queries to select the data you want to see in Slack. Here are some ideas of data you should select

* The type of customer
* The attribution of the customer
* Order form data to generate an invoice

Once you have created your model, click save. 

![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5f6563834cedfd00173b9a49/file-zg53SxxpoO.png)

### 4. Create your first Sync

No head to the [Sync page](https://app.getcensus.com/syncs) and click the Add Sync button

In the " What data do you want to sync?" section

* For the Connection, select the data warehouse you connected in step 2
* For the Source,  select the model you created in step 3

Next up is the "Where do you want to sync data to?" section

* Pick Stripe as the Connection
* For Object, pick **Customer**

For the " How should changes to the source be synced?" section 

* Select Update or Create
* Pick the right mapping key, it can be Email or any other external id for Customer

Finally, select the fields you want to update in the Mapper in the "Which Fields should be updated?" section

* Here simply map the field from your Stripe instance to the column from your model.

The end result should look something like this

![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5fbc4804cff47e0017d34b6d/file-drmWJMVTz9.png)

Click the Next button to see the final preview which will have a recap of what will happen when you start the sync

### 5. Confirm the data is in Stripe

Now go back to your Stripe and go view a Customer Profile that should have been updated. If everything well well, you should see your data in Stripe

![](https://d33v4339jhl8k0.cloudfront.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5fbc4ae846e0fb0017fcee63/file-mYnHg4FN41.png)

That's it, in 5 steps, you connect Census to Stripe and started syncing customer & product data from your warehouse to Stripe 🎉

If you have any question or if you have any issues getting started, please contact us via the in-app live chat in the bottom right corner or send us an email at support@getcensus.com

## 💡 Slack Field Quirks

There are two mandatory fields for the Mailchimp connection: **email** and **status**.

Please note that the mandatory status field only accepts the following values: `"subscribed"`, `"unsubscribed"`, `"cleaned"`, or `"pending"`.

For more details, take a look at Mailchimp's [API documentation](https://mailchimp.com/developer/marketing/api/list-members/update-list-member/).

## 🗄️ Supported Objects

| Object Name | Supported? | Identifiers |
| :--- | :---: | :--- |
| \[channel name\] | ✅ | \[field name\] |

In your Slack workspace, Census can send data to **all** public channels and any private channels that Census has been explicitly invited to \(e.g. `/invite @census`\).

## 🔄 Supported Sync Behaviors

| **Behaviors** | **Supported?** | **Objects?** |
| ---: | :---: | :---: |
| **Append** | ✅ | \[channel name\] |

In your Slack workspace, Census will only write new records to a specific channel when new records appear in your data warehouse.

## 🚑 Need help connecting to Slack?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


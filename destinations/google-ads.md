---
description: This page describes how to use Census with Google Ads.
---

# Google Ads

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Google Ads to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Google Ads account ready.
  * To create Customer Match syncs, your Google Ads Account will need access to the Customer Match feature. See [Google's Customer Match policy](https://support.google.com/adspolicy/answer/6299717?hl=en) for more details.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

### 1. Connect Google Ads

* Once you are in Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select Google Ads in the dropdown list.

![](../.gitbook/assets/screely-1619113580005.png)

Follow Google OAuth flow to connect your Google Ads account. 

![](../.gitbook/assets/screely-1619118724964.png)

Finally, select the Google Ads account you'd like to sync to

![](../.gitbook/assets/screely-1619118759931.png)

### 2. Connect your Data Warehouse

Please follow one of our short guides depending on your data warehouse technology

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)
* [Databricks](../sources/databricks.md)

After setting up your warehouse, your Census Connections Page should look like this:

![](../.gitbook/assets/screely-1619121030102.png)

## 🧑‍🤝‍🧑 Audiences

### 1. Create your Google Ads Customer Match Model <a id="3-create-your-first-model"></a>

Navigate to the [Models](https://app.getcensus.com/models) page.​

Here you can write SQL queries or select dbt models that contain the data you want to send to Google Ads.

Right now, we're going to send data to an existing Customer Match list, which requires a specific set of properties. We'll create a model that has:

* The email of the Customer
* A list of the target Customer Match lists
* Any other properties about the Customer that can assist in the match.

Once you have created your model, click save.

### 2. Create your first Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button

In the " **What data do you want to sync?"** section

* For the **Connection**, select the data warehouse you connected in the Prerequisites Step 2
* For the **Source,** select the model you created in step 1 of this section

Next up is the **"Where do you want to sync data to?"** section

* Pick **Google Ads** as the Connection
* For Object, pick **Customer**

For the " **How should changes to the source be synced?"** section 

* **Update or Create** will be selected by default
* Pick the right mapping key, in this case, we'll use **Email**

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section. Here simply map the field from your model to the properties of the Customer Match List. 

The end result should look something like this

![](../.gitbook/assets/screely-1619138106154.png)

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync.

### 3. Confirm the data is in your Customer Match List

Now go back to your Google Ads account and view the list. If everything went well, you should see that the list has been updated with your data. Because this is an Audience Matching mechanism, Google will not tell you the exact number of matches it found, but should tell you that it was updated. 

![](../.gitbook/assets/screely-1619138538677.png)

That's it! In 3 steps, you connected your data warehouse to Google Ads and built live Customer Match audiences Google Ads 🎉

## 🏪 Offline Click and Call Conversions

### 1. Create or find your custom conversion event

Google Ads has extensive documentation on [creating offline conversion events](https://support.google.com/google-ads/answer/7012522?hl=en-GB). The main steps are:

1. Create a new conversion action.
2. Select the data source for this conversion action as **Import**.
3. Select **Other data sources or CRMs**.
4. Select **Track conversions from clicks** or **Track conversions from calls**.
5. Enter a name for the conversion action that you're creating. Hold onto this name exactly as entered -- spelling and capitalization will be important when syncing these conversions via Census!
6. Choose your [counting option](https://support.google.com/google-ads/answer/3438531?hl=en-GB) for the conversion action, either **One conversion** or **Every conversion**. Many offline conversions occur only once \(e.g. "Reached onboarding milestone X"\). In this case, select the counting option **One conversion** to protect yourself from accidentally syncing duplicate conversions.
7. Complete the set-up for this conversion event, selecting your desired conversion window \(we recommend using the maximum 90-days\) and ads attribution model.

{% hint style="danger" %}
Important: After creating a new conversion action, wait 6 hours before syncing conversions for that conversion action. If you sync conversions during the first 6 hours, it can take two days for those conversions to appear on your reports.
{% endhint %}

### 2. Create your Census Model for the Conversion Action

Navigate to the [Models](https://app.getcensus.com/models) page.​

Here you can write SQL queries that contain the conversion action you want to send to Google Ads.

Google Ads Offline Click and Call Conversions require a specific set of properties. We'll want a model that has the following three required fields:

* The **Google Click ID** \(also often known as the `gclid`\)
* The **Conversion Name**, spelled exactly as it is found in Google Ads
* The **Conversion Timestamp**, with timezone specified

Optional properties include:

* Conversion Value, in [microunits](https://developers.google.com/adwords/api/docs/appendix/codes-formats#currency-codes) for the currency
* Currency Code, the[ ISO 4217 3-character currency code](https://developers.google.com/adwords/api/docs/appendix/codes-formats#currency-codes)
* External Attribution Credit and Model, calculated outside Google Ads

Once you have created your model, click save.

### 3. Create your Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button

In the "**What data do you want to sync?"** section

* For the **Connection**, select the data warehouse you connected in the Prerequisites Step 2
* For the **Source,** select the model you created in step 2 of this section

Next up is the **"Where do you want to sync data to?"** section

* Pick **Google Ads** as the Connection
* For Object, pick **Click Conversion** or **Call Conversion**

For the "**How should changes to the source be synced?"** section 

* **Append** will be selected by default
* Pick the right mapping key, the **Google Click ID** in your model

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section. Here simply map the fields from your model to the properties of the Click or Call Conversion. 

The end result should look something like this:

![](../.gitbook/assets/screely-1631098088943%20%281%29.png)

Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync.

### 4. Confirm the conversions are now in Google Ads

It may take around 3 hours for synced offline conversions to show up in your Google Ads account. When they do, they'll appear in reporting on these conversion actions. To learn more about reporting on these conversions, you may wish to visit [this Google Ads help article](https://support.google.com/google-ads/answer/6270625).

## 🗄 Supported Objects

| Service | **Object Name** | **Supported?** | Identifiers |
| :--- | ---: | :---: | :--- |
| Customer Match | Customer | ✅ | User ID, Mobile ID, Email,  Phone Number |
| Offline Conversions | Click, Call | ✅ | Click ID, Caller ID |

[Contact us](mailto:support@getcensus.com) if you're looking for additional Google Ads objects.



### **Google Customer Match behavior**

Google Customer Match, as its name implies, is a matching service rather than the usual direct upload. In order to protect user data, we do not upload the data you provide directly. Instead, records are "matched" against Google's existing user base. To do this, both sides perform a "hash" -- or consistent, but irreversible conversion -- of data so users can be compared without revealing the actual personally identifiable information. Census automatically takes care of this hashing step for you. 

We recommend you do not use Google's Customer Match expiration setting. Census-synced records are subject to the same expiration and will not be re-uploaded unless they are changed in your source data. 

## 🔄 Supported Sync Behaviors

| **Behaviors** | **Supported?** | **Objects** |
| ---: | :---: | :---: |
| **Update or Create** | ✅ | All |
| **Mirror** | ✅ | Audiences |

[Contact us](mailto:support@getcensus.com) if you're looking for additional Sync Behaviors!

Note: If you're reusing an existing Customer Match Lists, Census will not remove any users already added to those lists through other means. 

{% hint style="info" %}
Learn more about our sync behaviors on our [Core Concept page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

## 🚑 Need help connecting to Google Ads?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


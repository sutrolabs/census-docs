---
description: This page describes how to use Census with Google Cloud Storage.
---

# Google Cloud Storage

## Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com) now.
* Have your Google Cloud Storage Account in the [Browser tab](https://console.cloud.google.com/storage/browser/) on the bucket that you want to sync to.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Elasticsearch](../sources/elasticsearch.md)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

### Step 1: Create a Google Cloud Storage Connection

Our Google Cloud connector behaves a little differently than other Census connectors. Instead of going through an OAuth connection flow, we provide you a Google Identity address to which you grant Storage Object permissions.

* In Census, navigate to [Connections](https://app.getcensus.com/connections)
* Click the Add Service button, and select Google Cloud Storage
* Paste the name of the GCS bucket, name the connection, and click the Save Connection button

![](<../.gitbook/assets/Screen Shot 2021-11-03 at 1.46.43 PM.png>)

* Your new Google Cloud Storage connection will include a GCP service account for that specific Census connection. Click the copy button (![](../.gitbook/assets/copy-solid.svg)) to save it to your clipboard.

### Step 2: Grant Access to GCS

* Now head to the Google Cloud Storage bucket that you want to sync to, and click into that bucket's details.
* Click the Permissions tab on the Bucket, then click "Add Permissions".

![](<../.gitbook/assets/Screen Shot 2021-11-03 at 2.02.14 PM.png>)

* Paste the credentials in the New Principals portion and select "Storage Object Admin."&#x20;

![](<../.gitbook/assets/GCS Add.png>)

{% hint style="info" %}
You **will** be able to send a successful sync if the file path variables are unique per sync run by only granting this service account "Storage Object Creator", but the Test Connection in the next step will fail.
{% endhint %}

* Click save to save the permission.&#x20;
* Then navigate back to the [Connections](https://app.getcensus.com/connections) page and click "Test" on the service.

![You are good to go!](<../.gitbook/assets/Cloud Successful Connection.png>)

### Step 3: Create your first sync

The sync will move data from your warehouse to your GCS bucket. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your **source:** either a Model from the Census Models tab or a database table.
3.  Under **Where do you want to sync data to?**, choose the name you assigned in Step 1 (we used GCS) as the **Connection**. Enter the **File Path** for the CSV file where data will sync. The path can accept variables that will populate when the sync runs. See [File Path Variables](google-cloud-storage.md#file-path-variables). Confirm the file path in the **Template Preview** field.&#x20;

    __:bulb: _If the service account only has "Storage Object Creator" permissions, this file path needs to be unique per sync run_
4. Under **How should changes to the source be synced?**, **Mirror** will be automatically selected. This is the only supported sync behavior for GCS.&#x20;
5. Under **Which properties should be updated?**, choose whether to sync only **Selected Properties** or **Sync All Properties**. Syncing all properties will automatically add new properties to the sync if the model or database table changes.
6. To test your sync without actually syncing data, click **Run Test** and verify the results.
7. Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync. If you're happy, check the Sync Now checkbox and save the sync.
8. Confirm the data arrives in the GCS bucket!

If you need any help configuring GCS, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## File path variables

When defining the **File Path** for an GCS sync, you can use variables that will be set when the sync runs. This allows you to create and sync to new CSV files in the GCS bucket that reflect the date and time of the sync.

| **Variable** | **Description**              | **Example Values** |
| ------------ | ---------------------------- | ------------------ |
| `%Y`         | 4-digit year                 | 1997               |
| `%y`         | 2-digit year                 | 97                 |
| `%m`         | month with zero padding      | 07, 12             |
| `%-m`        | month without zero padding   | 7, 12              |
| `%d`         | day with zero padding        | 03, 23             |
| `%-d`        | day without zero padding     | 3, 23              |
| `%H`         | 24 hour with zero padding    | 08, 18             |
| `%k`         | 24 hour without zero padding | 8, 18              |
| `%I`         | 12 hour with zero padding    | 08, 12             |
| `%l`         | 12 hour without zero padding | 8, 12              |
| `%M`         | minute with zero padding     | 04, 56             |
| `%S`         | second with zero padding     | 06, 54             |

## 🔄 Supported sync behaviors

| **Behavior** | **Supported** | **Objects** |
| -----------: | :-----------: | :---------: |
|       Mirror |       ✅       |     All     |

{% hint style="info" %}
Learn about all of our sync behaviors in [Core Concepts](https://app.gitbook.com/s/-MV3poo0VqVau1o8I79\_/basics/core-concept#sync-behaviors).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Google Cloud Storage.

## 💡 Things to know

* Currently, the connector only supports syncing for files up to 5GB.
* Data arrives in one file to the designated bucket and file path.
* Files are written as a CSV with headers.

[Contact us](mailto:support@getcensus.com) if your use cases don't work with these limitations. We plan on addressing at least a few of these in the future!

## 🚑 Need help connecting to Google Cloud Storage?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

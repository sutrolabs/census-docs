---
description: This page describes how to use Census with Google Cloud Storage.
---

# Google Cloud Storage

## Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Google Cloud Storage Account in the [Browser tab](https://console.cloud.google.com/storage/browser/) on the bucket that you want to sync to.
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

### Step 1: Create a Google Cloud Storage Connection

Our Google Cloud destination behaves a little differently than other Census destinations. Instead of going through an OAuth connection flow, we provide you a Google Identity address to which you grant Storage Object permissions.

* In Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the New Destination button, and select Google Cloud Storage
* Paste the name of the GCS bucket, name the connection, and click the Save Connection button

![](<../.gitbook/assets/Screen Shot 2021-11-03 at 1.46.43 PM.png>)

* Your new Google Cloud Storage connection will include a GCP service account for that specific Census connection. Click the copy button (<img src="../.gitbook/assets/copy-solid.svg" alt="" data-size="line">) to save it to your clipboard.

### Step 2: Grant Access to GCS

* Now head to the Google Cloud Storage bucket that you want to sync to, and click into that bucket's details.
* Click the Permissions tab on the Bucket, then click "Add Permissions".

![](<../.gitbook/assets/Screen Shot 2021-11-03 at 2.02.14 PM.png>)

* Paste the credentials in the New Principals portion and select "Storage Object Admin."

![](<../.gitbook/assets/GCS Add.png>)

{% hint style="info" %}
You **will** be able to send a successful sync if the file path variables are unique per sync run by only granting this service account "Storage Object Creator", but the Test Connection in the next step will fail.
{% endhint %}

* Click save to save the permission.
* Then navigate back to the [Destinations](https://app.getcensus.com/destinations) page and click "Test" on the service.

![You are good to go!](<../.gitbook/assets/Cloud Successful Connection.png>)

### Step 3: Create your first sync

The sync will move data from your warehouse to your GCS bucket. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your **source:** either a Model from the Census Models tab or a database table.
3.  Under **Where do you want to sync data to?**, choose the name you assigned in Step 1 (we used GCS) as the **Connection**. Enter the **File Path** for the file where data will sync. The path can accept variables that will populate when the sync runs. See [File Path Variables](google-cloud-storage.md#file-path-variables). Confirm the file path in the **Template Preview** field.

    \_\_:bulb: _If the service account only has "Storage Object Creator" permissions, this file path needs to be unique per sync run_
4. Under **How should changes to the source be synced?**, **Replace** will be automatically selected. This is the only supported sync behavior for GCS.
5. Under **Which properties should be updated?**, choose whether to sync only **Selected Properties** or **Sync All Properties**. Syncing all properties will automatically add new properties to the sync if the model or database table changes.
6. To test your sync without actually syncing data, click **Run Test** and verify the results.
7. Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync. If you're happy, check the Sync Now checkbox and save the sync.
8. Confirm the data arrives in the GCS bucket!

If you need any help configuring GCS, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## Supported Sync Behaviors

| **Behavior** | **Supported?** | **Objects** |
| -----------: | :------------: | :---------: |
|      Replace |        ✅       |     All     |

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](broken-reference).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Google Cloud Storage.

## File Path

When setting up a sync to GCS, you can provide a file path for the file name Census will create/replace. The file path can include folders. Data arrives in one file to the designated bucket and file path.

### Variables

When defining the **File Path**, you can use variables that will be set when the sync runs. This allows you to create and sync to new files that reflect the date and time of the sync.

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

## Advanced Configuration

In addition to the file path, you can configure how the data is encoded as it is written. Primarily this is a question of file format:

* CSV - The standard comma separated values file. You can optionally specify an alternative delimeter such as `|`\*, and you can enable/disable the header row.
* TSV - The tab separated values file. You can enable/disable the header row.
* JSON - A single JSON arraay of objects
* NDJSON - New line-delimited list of JSON objects
* Parquet - A columnar storage format that is more efficient for certain types of data.
* If your configured delimiter is present in data values, Census will automatically add double quotes around the value.\
  &#xNAN;_&#x45;xample: `Hello, world` is written as as `"Hello, world"` if the chosen delimiter is a comma._

In addition to file format, you can also provide a PGP Public Key to encrypt the data before it is written to the file. This is useful for ensuring that the data is secure in transit and at rest.

## Other Things to Know

* Currently, the destination only supports syncing for files up to 5GB.

[Contact us](mailto:support@getcensus.com) if your use cases don't work with these limitations. We plan on addressing at least a few of these in the future!

## Need help connecting to Google Cloud Storage?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

---
description: This page describes how to use Census with SFTP.
---

# SFTP

## Getting started

This guide shows you how to use Census to connect your SFTP server to your data warehouse and create your first sync.

### **Prerequisites**

Before you begin, you'll need the following:

* **Census account**: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* **SFTP server**: You'll need the host address, username, and password or private key.
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

### Step 1: Connect SFTP

1. Log into Census and navigate to [**Destinations**](https://app.getcensus.com/destinations).
2. Click **New Destination**.
3. Select **SFTP** from the dropdown list.
4. Enter a **Name** for your destination. This is only for your reference – it can be anything that makes sense to you.
5. Enter authentication details for your SFTP server. **Host** and **Username** are always required. If your server requires a password instead of an SSH key, enter the **Password**. If your server uses SSH keys, you can leave the **Password** blank.
6. Click **Save Connection**.
7. If you're using **SSH keys** to authenticate your server, download the **SFTP Public Key** from this screen and upload it to your server. Then, click **Test** to verify that the connection works.

* If you aren't using a password for your server, Census provides an RSA token with an OpenSSH-formatted public key.

Your end state should look something like this: 👇

![Destinations page with SFTP server set up](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.14.04 PM.png>)

### Step 2: Connect your data warehouse

The steps for connecting your data warehouse will depend on your technology. See the following guides:

* [Databricks](../sources/available-sources/databricks.md)
* [Google BigQuery](../sources/available-sources/google-bigquery.md)
* [Google Sheets](google-sheets.md)
* [Postgres](../sources/available-sources/postgres.md)
* [Redshift](../sources/available-sources/redshift.md)
* [Snowflake](../sources/available-sources/snowflake.md)

After setting up your warehouse, your **Destinations** page should look something like this: 👇

![Destinations page with data warehouse and SFTP server](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.11.44 PM.png>)

### Step 3: Create your model

When defining models, you'll write SQL queries to select the data you want to sync. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the [**Models**](https://app.getcensus.com/models) page.
2. Enter a name for your model. You'll use this to select the model later.
3. Enter your SQL query. If you want to test the query, use the **Preview** button.
4. Click **Save Model**.

![Basic SQL query for a new model](../.gitbook/assets/202109_Outreach_Basic_Model.png)

### Step 4: Create your first sync

The sync will move data from your warehouse to a new or existing CSV file on your SFTP server. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose the name you assigned in Step 1 (we used **SFTP**) as the **Connection**. Enter the **File Path** for the CSV file where data will sync. The path can accept variables that will populate when the sync runs. See [File Path Variables](sftp.md#file-path-variables). Confirm the file path in the **Template Preview** field.
4. Under **How should changes to the source be synced?**, **Replace** will be automatically selected. This is the only supported sync behavior for SFTP.
5. Under **Which properties should be updated?**, choose whether to sync only **Selected Properties** or **Sync All Properties**. Syncing all properties will add new properties to the sync if the model changes.
6. To test your sync without actually syncing data, click **Run Test** and verify the results.
7. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
8. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
9. Click **Create Sync**.

When configuring your sync, the page should look something like this: 👇

![Setting up a sync to an SFTP server](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.18.52 PM.png>)

### Step 5: Confirm the synced data

Once your sync is complete, it's time to check your data. Go to the specified path on your SFTP server and check that the file updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to your SFTP server! [🥳️](https://emojikeyboard.org/copy/Partying_Face_Emoji_%F0%9F%A5%B3%EF%B8%8F?utm_source=extlink)

And if anything went wrong, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## Supported Sync Behaviors

|    **Behaviors** | **Supported?** | **Objects** |
| ---------------: | :------------: | :---------: |
| Update or Create |        ✅       |     All     |
|          Replace |        ✅       |     All     |

### Update or Create Syncs

Update or Create syncs upload your whole dataset on the first run and only new changes on subsequent runs. Each sync run saves to a different file. The first run saves with "full" at the end of the file name. For example, `filename_12_12_23_full.csv` if it runs on 12/12/2023. Later syncs save with a timestamp at the end, like `filename_12_12_23_1702426195.csv`, so you can see how your data changes over time.

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../syncs/core-concept/#the-different-sync-behaviors).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for SFTP server connections.

## File Path

When setting up a sync to SFTP, you can provide a file path for the file name Census will create/replace. The file path can include folders. Data arrives in one file to the designated server and file path.

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

## Need help connecting your server?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

---
description: This page describes how to use Census with SFTP.
---

# SFTP

## 🏃‍♀️ Getting started

This guide shows you how to use Census to connect your SFTP server to your data warehouse and create your first sync.

### **Prerequisites**

Before you begin, you'll need the following:

* **Census account**: If you don't have this already, [start with a free trial](https://app.getcensus.com).
* **SFTP server**: You'll need the host address, username, and password or private key.
* **Credentials for your data warehouse**: For details, see the guide for your [specific data source technology](sftp.md#step-2-connect-your-data-warehouse).

### Step 1: Connect SFTP

1. Log into Census and navigate to [**Connections**](https://app.getcensus.com/connections).
2. Click **Add Service**.
3. Select **SFTP** from the dropdown list.
4. Enter a **Name** for your destination. This is only for your reference – it can be anything that makes sense to you.
5. Enter authentication details for your SFTP server. **Host** and **Username** are always required. If your server requires a password instead of an SSH key, enter the **Password**. If your server uses SSH keys, you can leave the **Password** blank.&#x20;
6. Click **Save Connection**.
7. If you're using **SSH keys** to authenticate your server, download the **SFTP Public Key** from this screen and upload it to your server. Then, click **Test** to verify that the connection works.

Your end state should look something like this: 👇

![Connections page with SFTP server set up](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.14.04 PM.png>)

### Step 2: Connect your data warehouse

The steps for connecting your data warehouse will depend on your technology. See the following guides:

* [Databricks](../sources/databricks.md)
* [Google BigQuery](../sources/google-bigquery.md)
* [Google Sheets](google-sheets.md)
* [Postgres](../sources/postgres.md)
* [Redshift](../sources/redshift.md)
* [Rockset](../sources/rockset.md)
* [Snowflake](../sources/snowflake.md)

After setting up your warehouse, your **Connections** page should look something like this: 👇

![Connections page with data warehouse and SFTP server](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.11.44 PM.png>)

### Step 3: Create your model

When defining models, you'll write SQL queries to select the data you want to sync. This can be as simple as selecting everything in a specific database table or as complex as creating new calculated values.

1. From inside your Census account, navigate to the [**Models**](https://app.getcensus.com/models) page.
2. Enter a name for your model. You'll use this to select the model later.
3. Enter your SQL query. If you want to test the query, use the **Preview** button.
4. Click **Save Model**.

![Basic SQL query for a new model](<../.gitbook/assets/202109\_outreach\_basic\_model (1).png>)

### Step 4: Create your first sync

The sync will move data from your warehouse to a new or existing CSV file on your SFTP server. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your model as the **Source**.
3. Under **Where do you want to sync data to?**, choose the name you assigned in Step 1 (we used **SFTP**) as the **Connection**. Enter the **File Path** for the CSV file where data will sync. The path can accept variables that will populate when the sync runs. See [File Path Variables](sftp.md#file-path-variables). Confirm the file path in the **Template Preview** field.
4. Under **How should changes to the source be synced?**, **Mirror** will be automatically selected. This is the only supported sync behavior for SFTP.
5. Under **Which properties should be updated?**, choose whether to sync only **Selected Properties** or **Sync All Properties**. Syncing all properties will add new properties to the sync if the model changes.
6. To test your sync without actually syncing data, click **Run Test** and verify the results.
7. Click **Next**. This will open the **Confirm Details** page where you can see a recap of your setup.
8. If you want to start a sync immediately, set the **Run a sync now?** checkbox.
9. Click **Create Sync**.

When configuring your sync, the page should look something like this: 👇

![Setting up a sync to an SFTP server](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.18.52 PM.png>)

### Step 5: Confirm the synced data

Once your sync is complete, it's time to check your data. Go to the specified path on your SFTP server and check that the file updated correctly.

If everything went well, that's it! You've started syncing data from your warehouse to your SFTP server! [🥳️](https://emojikeyboard.org/copy/Partying\_Face\_Emoji\_%F0%9F%A5%B3%EF%B8%8F)

And if anything went wrong, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## File path variables

When defining the **File Path** for an S3 sync, you can use variables that will be set when the sync runs. This allows you to create and sync to new CSV files in the S3 bucket that reflect the date and time of the sync.

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

|    **Behaviors** | **Supported** | **Objects** |
| ---------------: | :-----------: | :---------: |
| Update or Create |       ✅       |     All     |
|           Mirror |       ✅       |     All     |

{% hint style="info" %}
Learn about all of our sync behaviors in [Core Concepts](https://app.gitbook.com/s/-MV3poo0VqVau1o8I79\_/basics/core-concept#sync-behaviors).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for SFTP server connections.

## 💡 Things to know

* If you aren't using a password for your server, Census provides an RSA token with an OpenSSH-formatted public key.
* Data arrives in one file written to the designated SFTP file path.
* Files are written as a CSV with headers.

## 🚑 Need help connecting your server?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

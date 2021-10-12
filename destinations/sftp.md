---
description: This page describes how to use Census with SFTP.
---

# SFTP

## 🏃‍♀️ Getting Started

‌ In this guide, we will show you how to connect SFTP servers to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com) now.
* Have an SFTP server ready for use, along with access to its host address, username, and password if it doesn't use a private key.
* Have the proper credentials to access to your data source. See our docs for each supported data source for further information:
  * [Databricks](https://docs.getcensus.com/sources/databricks)
  * [Google BigQuery](https://docs.getcensus.com/sources/google-bigquery)
  * [Google Sheets](https://docs.getcensus.com/sources/google-sheets)
  * [Postgres](https://docs.getcensus.com/sources/postgres)
  * [Redshift](https://docs.getcensus.com/sources/redshift)
  * [Rockset](https://docs.getcensus.com/sources/rockset)
  * [Snowflake](https://docs.getcensus.com/sources/snowflake)

### 1. Create an SFTP Destination in Census

* Once you are in Census, Navigate to [Connections](https://app.getcensus.com/connections)
* Click the **Add Service **button
* Select **SFTP** in the dropdown list
* Name your Destination (for example, `SFTP`) and enter the host and username for your SFTP server. If your server requires a password instead of an ssh key, enter the password here. If a password is not provided, we will give you a public key to upload to your user on your SFTP server. For SFTP connections with no password, this error will be shown until the provided public key is uploaded:

![](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.11.03 PM.png>)

* Once the public key has been uploaded, you can click the **Test** button again to see if we can connect to the SFTP server successfully. If so, you'll see this:

![](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.14.04 PM.png>)

{% hint style="success" %}
Your SFTP credentials will automatically be tested by ensuring we can set up a connection to the SFTP server.
{% endhint %}

### 2. Connect your Data Warehouse

Please follow one of our short guides depending on your data warehouse technology:

* [Redshift](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [Postgres](https://help.getcensus.com/article/10-configuring-redshift-postgresql-access)
* [BigQuery](https://help.getcensus.com/article/21-configuring-bigquery-access)
* [Snowflake](https://help.getcensus.com/article/8-configuring-snowflake-access)

After setting up your warehouse, your Census Connections Page should look like this:

![](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.11.44 PM.png>)

### 3. Create your first Sync

Now head to the [Sync page](https://app.getcensus.com/syncs) and click the **Add Sync** button

In the " **What data do you want to sync?" **section

* For the **Connection**, select the data warehouse you connected in step 2
* For the **Source,  **select a model or table in your warehouse

Next up is the **"Where do you want to sync data to?"** section

* Pick your SFTP destination (for us it is `SFTP`) as **the Connection.**
* A **File Path** text field populated with a placeholder file path will pop up below the connection:

![](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.17.23 PM.png>)

* Change the file path to reflect the name and place of the csv file you want to send data to.
* File paths accept variables that are set when the sync is run, and you can see the preview of your file path if you were to run the sync right now in the **Template Preview** section.
*   The full list of variables you can use to template your file path is:

    %Y => 4 number year like 1997

    %y => 2 number year like 97

    %m => zero padded month like 07

    %-m => month like 7

    %d => zero padded day like 03

    %-d => day like 3

    %H => zero padded 24 hour like 08 or 18

    %k => 24 hour like 8 or 18

    %I => zero padded 12 hour like 08 or 12

    %l => 12 hour like 8 or 12

    %M => zero padded minute like 04 or 56

    %S => zero padded second like 05 or 55

For the " **How should changes to the source be synced?"** section 

* **Mirror** should automatically be selected. 

Finally, select the fields you want to update in the Mapper in the **"Which Fields should be updated?"** section

* By default, all of your table columns will be added to the mapper. If you don't want that, simply remove the columns/fields you don't want to sync in the mapper.

The end result should look something like this:

![](<../.gitbook/assets/Screen Shot 2021-10-11 at 6.18.52 PM.png>)

Click the **Next **button to see the final preview which will have a recap of what will happen when you start the sync

### 4. Confirm the data was sent to your SFTP Server

Now go back to your destination or service, in our case we will go to our SFTP server and we should see a new file with the specified file path 🎉

That's it, in 4 steps, you used Census to sync data from your warehouse or source to your SFTP server 🎉

## 🔄 Supported Sync Behaviors

| **Behaviors** | **Supported?** | **Objects?** |
| ------------: | :------------: | :----------: |
|    **Mirror** |        ✅       |      All     |

‌ 🔋 [Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for this destination

## 💡 Things to know about the SFTP connector

* If a password is not provided to the SFTP connection, an RSA token with an openssh formatted public key is provided to upload to the SFTP server.
* Data arrives in one file to the designated file path.
* Files are written as a csv with headers.

[Contact us](mailto:support@getcensus.com) if your use cases don't work with these current limitations, we plan on addressing at least a few of these limitations in the future!

## 🚑 Need help connecting to SFTP?

‌ Contact us via [support@getcensus.com](mailto:support@getcensus.com) or start a conversion via the [in-app](https://app.getcensus.com) chat.

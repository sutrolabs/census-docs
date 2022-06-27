---
description: This page describes how to use Census with Salesforce Marketing Cloud.
---

# Salesforce Marketing Cloud

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Salesforce Marketing Cloud to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Salesforce Marketing Cloud account ready, with the Administrator role.

{% hint style="warning" %}
This process involves several steps - please set aside 15-30 minutes to complete it. Note that you may be on an older or newer version of Marketing Cloud which has slightly different screens than the ones pictured below. Marketing Cloud configuration can be complex, so if you have any questions please [contact us](mailto:support@getcensus.com) via support@getcensus.com and we'll help you tailor these instructions to your needs.
{% endhint %}

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

### 1. Create and Configure a Server-to-Server Installed Package

Sign in to Salesforce Marketing Cloud and enter "Setup"

Navigate to "Apps > Installed Packages". Click "New" to create a new package. Create an app called "Census" and provide an optional description, then click "Save"

![](../.gitbook/assets/sfmc\_step1.png)

![](../.gitbook/assets/sfmc\_step2.png)

Click "Add Component" and choose "API Integration"

![](../.gitbook/assets/sfmc\_step3.png)

Choose "Server-to-Server" as the OAuth Integration Type

![](../.gitbook/assets/sfmc\_step4.png)

In "Set Server-to-Server Properties", given the new component the following permissions by checking the appropriate boxes:

* Automation > **Automations: Read, Write, Execute**
* Contacts > **Audiences: Read, Write**
* Contacts > **List and Subscribers: Read, Write**
* Data > **Data Extensions: Read, Write**
* Data > **File Locations: Read, Write**

Click "Save" to continue. You should see a new Component in your package - verify that it has the correct permissions (in the Scope section) by comparing to the image below.

![](../.gitbook/assets/sfmc\_step5.png)

Copy the **Client Id**, **Client Secret**, and **Authentication Base URI** from this page - you will need to provide these values to Census in Step 3.

### 2. Create an SFTP Account in Salesforce Marketing Cloud

Census uses the ExactTarget Enhanced FTP server to upload large data files to your Salesforce Marketing Cloud instance and prepare them for import. In this step, you'll ensure there is a File Location for Census to upload the data, and create a new user account on your FTP server that Census can use to sign in.

**File Location**

In Salesforce Marketing Cloud Setup, navigate to "Data Management > File Locations". If you have an Enhanced FTP location with an external key of "ExactTarget Enhanced FTP", then no action is required. If you do not see this File Location, click "Create" to generate a new location with the following configurations:

* An "External Key" value of **ExactTarget Enhanced FTP**
* A "Location Type" of **Enhanced FTP Site Import Directory**

![](../.gitbook/assets/screely-1653426548785.png)

**FTP User**

Still in Salesforce Marketing Cloud Setup, navigate to "Data Management > FTP Accounts" and click "Add FTP User".

![](../.gitbook/assets/sfmc\_step6.png)

For the email address, type in "support@getcensus.com" and give the user a strong, random password. You do not need to write down or memorize this password - Census does not require it, and in step 4 we will replace it with an SSH key. Make sure to give the Census user "Full" access, and do not specify any IPs in the "Allowlist IPs" list. Click Next.

![](../.gitbook/assets/sfmc\_step7.png)

There's nothing to do yet on the next screen - we'll set up SSH Keys later. Click "Save" to create the user.

![](../.gitbook/assets/sfmc\_step8.png)

Salesforce Marketing Cloud will create the user, which may take a few seconds. Copy the **FTP Username** that was assigned to the user, which you'll need in Step 3.

### 3. Configure Census with Your Connection Information

Go to [Census Connections](https://app.getcensus.com/connections), click "Add Service" and choose "Salesforce Marketing Cloud".

![](../.gitbook/assets/sfmc\_step9.png)

In the dialog, fill out the data you gathered in steps 2 and 3:

* Name: A descriptive name of your choosing. If you have more than one Salesforce Marketing Cloud connection, you can use this field to help you keep track them
* Endpoint URL: Fill in the **Authentication Base URI** from Step 1
* Client ID and Client Secret: Fill in the **Client ID** and **Client Secret** from Step 1
* SFTP User: Fill in the **FTP Username** from Step 2

Click "Save Connection".

![](../.gitbook/assets/sfmc\_step10.png)

Census will show your new Salesforce Marketing Cloud connection in its connections list

### 4. Upload Census's SSH Public Key to Marketing Cloud

The final step is to configure Marketing Cloud to accept Census's SSH public key for FTP access, instead of using a password. Still in Census, click the button labeled "Click to Download" next to the "SFTP Public Key". This will download a file called "census.pub" to your computer - make a note of where it was saved.

Return to Salesforce Marketing Cloud Setup and navigate to "Data Management" > "Key Management". Click "Create".

![](../.gitbook/assets/sfmc\_step11.png)

* For "Key Type", choose "SSH"
* For "Name", type "Census Public Key"
* For "External Key", type "census-public-key"
* Check the "Public Key" checkbox
* Click "Browse" next to the "Key (required)" field and find the "census.pub" file you previously downloaded.
* Click "Save"

Now we'll associate the key with the Census user. Navigate to "Data Management" > "FTP Accounts". Choose the "support@getcensus.com" user and click the small arrow next to their name (you may need to scroll to the right. Choose "SSH Keys" from the drop-down menu.

![](../.gitbook/assets/sfmc\_step12.png)

![](../.gitbook/assets/sfmc\_step13.png)

Click in the "Search SSH Keys" box and find "Census Public Key" and select it. Change the "Authentication Options" to "SSH Key" and click "Save". In a few seconds, Salesforce Marketing Cloud will finish configuring the SSH key (you can click the refresh icon at the top right to see the activity log go from "Pending" to "Success".

![](../.gitbook/assets/sfmc\_step14.png)

### 5. Starting syncing

You're ready to start using Census to load data from your warehouse to Salesforce Marketing Cloud!

## 🏎 Sync Speed

| **Service**                | **Records sync / Minute** |
| -------------------------- | ------------------------- |
| Salesforce Marketing Cloud | \~20,000                  |

## 🗄️ Supported Objects

****

|           **Object Name** | **Supported?** |
| ------------------------: | :------------: |
| Any Custom Data Extension |        ✅       |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Objects for Salesforce Marketing Cloud.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** | **Objects?** |
| -------------------: | :------------: | :----------: |
| **Update or Create** |        ✅       |      All     |
|           **Mirror** |        ✅       |      All     |
|      **Update Only** |       🔜       |      All     |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for Salesforce Marketing Cloud.

## 🚑 Need help connecting to Salesforce Marketing Cloud?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

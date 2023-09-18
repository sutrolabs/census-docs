---
description: This page describes how to use Census with Salesforce Marketing Cloud.
---

# Salesforce Marketing Cloud

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Salesforce Marketing Cloud to Census and create your first sync.

{% hint style="warning" %}
This process involves several steps - please set aside 15-30 minutes to complete it. Note that you may be on an older or newer version of Marketing Cloud which has slightly different screens than the ones pictured below. Marketing Cloud configuration can be complex, so if you have any questions please [contact us](mailto:support@getcensus.com) via support@getcensus.com and we'll help you tailor these instructions to your needs.
{% endhint %}

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
* Journeys > **Journeys: Read, Write**

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

Go to [Census Destinations](https://app.getcensus.com/destinations), click **New Destination** and choose **Salesforce Marketing Cloud**.

<figure><img src="../.gitbook/assets/SFMC - Card.png" alt=""><figcaption></figcaption></figure>

In the dialog, fill out the data you gathered in steps 2 and 3:

* Name: A descriptive name of your choosing. If you have more than one Salesforce Marketing Cloud connection, you can use this field to help you keep track them
* Endpoint URL: Fill in the **Authentication Base URI** from Step 1
* Client ID and Client Secret: Fill in the **Client ID** and **Client Secret** from Step 1
* SFTP User: Fill in the **FTP Username** from Step 2
* (Optional) **Business Unit MID**: If you would like to create a connection for a business unit other than your primary SFMC account, you can provide a Business Unit MID. This can be found in the SFMC top navigation menu:

<figure><img src="../.gitbook/assets/CleanShot 2023-02-02 at 10.01.34@2x.png" alt=""><figcaption></figcaption></figure>

*   In order to enable Census support for business units, you will also need to turn on business unit app integration in your SFMC instance under `Setup` > `Apps` > `Installed Packages` > `Census` > `Access` > `Enable Integration` :

    <figure><img src="../.gitbook/assets/CleanShot 2023-01-03 at 11.12.41@2x.png" alt=""><figcaption></figcaption></figure>

Click **Save Connection**.

Census will show your new Salesforce Marketing Cloud connection in its connections list

### 4. Upload Census's SSH Public Key to Marketing Cloud

The final step is to configure Marketing Cloud to accept Census's SSH public key for FTP access, instead of using a password. Still in Census, click the button labeled "Click to Download" next to the "SFTP Public Key". This will download a file called "census.pub" to your computer - make a note of where it was saved.

Return to Salesforce Marketing Cloud Setup and navigate to "Data Management" > "Key Management". Click "Create".

![](<../.gitbook/assets/SFMC - Config.png>)

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

You're ready to start using Census to load data from your warehouse to Salesforce Marketing Cloud!

## 🔀 Supported Objects and Behaviors

<table data-header-hidden><thead><tr><th width="167" align="right"></th><th width="143" align="center"></th><th width="179"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Sync Keys</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Data Extension</td><td align="center">✅</td><td>Unique Identifier</td><td>Update or Create, Update Only, Mirror</td></tr><tr><td align="right">Contact</td><td align="center">✅</td><td>Contact Key</td><td>Update or Create</td></tr><tr><td align="right">API-Triggered Journey</td><td align="center">✅</td><td>Contact Key</td><td>Update or Create, Mirror</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more Marketing Cloud objects and/or behaviors.

## 🏗️ Working With Data Extensions

Data Extensions are a fundamental component of Salesforce Marketing Cloud and are used in various capacities, including email personalization, segmentation, and reporting. They're unique in that they combine the common marketing automation concepts of segmentation and custom/relational data together into a single mechanism.&#x20;

Census allows you to sync data to existing data extensions, create new ones, and add fields to existing ones as well.&#x20;

### Creating a data extension

You can select any existing data extension as a destination for a sync. You can also create a new data extension when setting up a Census sync.&#x20;

<figure><img src="../.gitbook/assets/SFMC - New DE.png" alt=""><figcaption></figcaption></figure>

1. Click New Object&#x20;
2. Provide a name for your data extension
3. Optionally, you can provide a different name for the identifier. By default, we'll use **ID**.

{% hint style="info" %}
You can also have Census create the data extension within a subfolder by providing it in the data extension name. The subfolder must already exist, Census won't automatically create it. The subfolder will be relative to any configured root folder (see below).
{% endhint %}

### Adding new properties

Whether you're working with a brand new data extension or an existing one, you can always add more properties to a data extension. Within the Mappings section, either the **Add Mapping** or **Generate Mappings** allow you to add new properties to the data extension that will be created next time the sync is run.&#x20;

### Setting a root folder

Some Salesforce Marketing Cloud installations have a very large number of data extensions. Census allows specify a specific folder to use as the root or base folder. Only data extensions within this folder or its subfolders will be shown in Census and new data extensions will be created in this folder.

<figure><img src="../.gitbook/assets/SFMC - Folder Path.png" alt=""><figcaption></figcaption></figure>

1. Visit the Destinations page and find your Salesforce Marketing Cloud connection.
2. Click **Edit**.
3. Set the Folder Path value to match your desired folder.
4. Click **Save Connection**.

## ⚙️ Advanced Configuration

By default, Census uses Salesforce Marketing Cloud's bulk upload mechanism which is powered by SFTP. This is the recommended mechanism for most syncs. However, for small data volumes, it may be preferred to send updates individually via Salesforce Marketing Cloud's SOAP API for faster processing. If your syncs must be processed with as low latency as possible and you have a relatively small number of changes, you can disable the standard SFTP method of syncing.

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

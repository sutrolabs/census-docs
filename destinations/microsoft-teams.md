---
description: This page describes how to use Census with Microsoft Teams.
---

# Microsoft Teams

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect Microsoft Teams to Census.

### 📋 Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Slack account ready.
* Have the proper credentials to access to your data source. See our [docs](broken-reference/) for each supported data source for further information.

## 1️⃣ Connect Census to Teams

In the [**Destinations**](https://app.getcensus.com/destinations) page in Census, Click the **New Destination** button in the top right, and select Microsoft Teams.

If you are not already logged in to Teams, you will be redirected to a page to log in to authorize your account to use Census. Once you've authorized Census, you'll be redirected back to the Destinations page in Census where you'll see your Teams connection.

## 2️⃣ Connect Census to your data source

See our [docs](broken-reference/) for each supported data source for further information.

## 3️⃣ Create your first Census model

Navigate to the **Models** page in Census and click the **Add Model** button.

Here you can a write SQL query to select the data you want to send to Teams.

Once you have created your model, give it a useful name, and click **Save Model**.

## 4️⃣ Create a Sync

Navigate to the [**Syncs**](https://app.getcensus.com/syncs) page in Census and click the **New Sync** button.

### 🎚 Setup your Source, Destination, and Sync Key

You'll need to start by specifying how to identify entries in your data warehouse that should trigger a Sync:

* For Source > **Connection**, select the data warehouse you connected in step 2.
* For Source > **Source**, select the model you created in step 3.
* For Destination > **Connection**, select Microsoft Teams
* For Destination > **Object**, Message should be auto-selected
* Next, pick the column that uniquely identifies each record in your data source. Census will use this to identify new records that need to be used to send messages to Microsoft.

<figure><img src="../.gitbook/assets/Screenshot 2023-06-21 at 3.00.06 PM.png" alt=""><figcaption></figcaption></figure>

### 💬 **Setup your Message**

* Select the Teams channel you'd like to send messages to.
* Finally, use the text editor to customize the message that you wish to send.
  * To embed values from the trigger columns or to mention users or channels from your Teams account, use the dropdown that will appear. If the list is long, try the search function.

<figure><img src="../.gitbook/assets/Screenshot 2023-06-21 at 3.01.08 PM.png" alt=""><figcaption></figcaption></figure>

### 🧪 Test your Teams message

* Click the Run Test button to see a single random record sent to your destination. For testing, you may want to temporarily change the destination message yourself.

<figure><img src="../.gitbook/assets/Screenshot 2023-06-21 at 3.14.57 PM.png" alt=""><figcaption></figcaption></figure>

### ☑️ Finishing touches

* Click the **Finish** button and you'll be taken to your new sync. You can now Schedule the sync to run on a schedule or run it manually yourself.

<figure><img src="../.gitbook/assets/CleanShot 2022-10-11 at 11.02.21@2x.png" alt=""><figcaption><p>Configure your new sync to run on a set schedule or run it manually.</p></figcaption></figure>

{% hint style="info" %}
Reminder: Census will send records to a Teams channel one at a time.
{% endhint %}

## 🗄️ Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

<table data-header-hidden><thead><tr><th></th><th align="center"></th><th width="173"></th><th align="center"></th></tr></thead><tbody><tr><td><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Identifiers</strong></td><td align="center"><strong>Behaviors</strong></td></tr><tr><td>Messsage</td><td align="center">✅</td><td>Custom message template.</td><td align="center">Send</td></tr></tbody></table>

{% hint style="info" %}
Census can send data to **all** public channels and any private channels that Census has been explicitly invited to (e.g. `/invite @census`).
{% endhint %}

{% hint style="info" %}
Census will only write new records to a specific channel when new records appear in your data warehouse.
{% endhint %}

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept/#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Microsoft Teams objects and/or behaviors

## 🚑 Need help connecting to Microsoft Teams?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

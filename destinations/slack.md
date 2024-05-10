---
description: >-
  Turn analytics signals and insights into Slack alerts to help GTM teams
  identify opportunities, personalize outreach, and prevent churn. All without
  writing a single line of code.
---

# Slack

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect Slack to Census.

### 📋 Prerequisites

* Have your Census account ready. If you need one, [start a free trial now](https://app.getcensus.com/) (or take a look at our [pricing for paid plans](https://www.getcensus.com/pricing)).
* Have your Slack account ready.
* Have the proper credentials to access to your data source. See our [docs](broken-reference/) for each supported data source for further information.

## 1️⃣ Connect Census to Slack

In the [**Destinations**](https://app.getcensus.com/destinations) page in Census, Click the **New Destination** button in the top right, and select Slack.

If you are not already logged in to Slack, you will be redirected to a page to log in to Slack to authorize your account to use Census. Once you are logged in, you'll see a page like the image below, confirming you want to authorize Census.

![](<../.gitbook/assets/Screen Shot 2021-09-13 at 9.39.16 AM.png>)

Once you've authorized Census, you'll be redirected back to the Destinations page in Census and you should see your Slack connection there.

## 2️⃣ Connect Census to your data source

See our [docs](broken-reference/) for each supported data source for further information.

## 3️⃣ Create your first Census model

Navigate to the **Models** page in Census and click the **Add Model** button.

Here you can a write SQL query to select the data you want to send to Slack.

Once you have created your model, give it a useful name, and click **Save Model**.

## 4️⃣ Create your Census Sync

Navigate to the [**Syncs**](https://app.getcensus.com/syncs) page in Census and click the **New Sync** button.

### 🎚 Setup your Source, Destination, and Sync Key

You'll need to start by specifying how to identify entries in your data warehouse that should trigger a Sync:

* For Source > **Connection**, select the data warehouse you connected in step 2.
* For Source > **Source**, select the model you created in step 3.
* For Destination > **Connection**, select Slack
* For Destination > **Object**, Message should be auto-selected
* Next, pick the column that uniquely identifies each record in your data source. Census will use this to identify new records that need to be used to send messages to Slack.

<figure><img src="../.gitbook/assets/Screenshot 2023-06-21 at 2.53.41 PM.png" alt=""><figcaption></figcaption></figure>

### 💬 **Setup your Message**

* Select the Slack channel you'd like to send messages to.
* Finally, use the text editor to customize the message that you wish to send.
  * To embed values from the trigger columns or to mention users or channels from your Slack account, use the dropdown that will appear. If the list is long, try the search function.

<figure><img src="../.gitbook/assets/Screenshot 2023-06-21 at 2.56.10 PM.png" alt=""><figcaption></figcaption></figure>

### 🧪 Test your Slack message

* Click the Run Test button to see a single random record sent to your destination. For testing, you may want to temporarily change the destination message yourself.

<figure><img src="../.gitbook/assets/Screenshot 2023-06-21 at 3.16.57 PM.png" alt=""><figcaption></figcaption></figure>

### ☑️ Finishing touches

* Click the **Finish** button and you'll be taken to your new notification. You can now Schedule the sync to run on a schedule or run it manually yourself.

<figure><img src="../.gitbook/assets/CleanShot 2022-10-11 at 11.02.21@2x.png" alt=""><figcaption><p>Configure your new Notification to run on a set schedule or run it manually.</p></figcaption></figure>

{% hint style="info" %}
Reminder: Census will send records to a Slack channel one at a time.
{% endhint %}

## Dynamic User Mentions

The Member ID can be used to mention specific channel members in a Slack message.&#x20;

Example: `<@member_id>`

## 🗄️ Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Identifiers**          | **Behaviors** |
|-----------------|:--------------:|--------------------------|---------------|
| Message         |       ✅        | Custom message template. | Send          |

{% hint style="info" %}
Census can send data to **all** public channels and any private channels that Census has been explicitly invited to (e.g. `/invite @census`).
{% endhint %}

{% hint style="info" %}
Census will only write new records to a specific channel when new records appear in your data warehouse.
{% endhint %}

## 🚑 Need help connecting to Slack?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

If you have questions about our privacy policy, you can check it out [here](https://www.getcensus.com/legal/privacy-policy).

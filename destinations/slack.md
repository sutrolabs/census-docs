---
description: This page describes how to use Census with Slack.
---

# Slack

## 🏃‍♀️ Getting Started

‌In this guide, we will show you how to connect Slack to Census and create your first Census Notification.

{% embed url="https://www.youtube.com/embed/Y8ygdX2lFEU" %}

### 📋 Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Slack account ready.
* Have the proper credentials to access to your data source. See our [docs](broken-reference) for each supported data source for further information.

## 1️⃣ Connect Census to Slack

In the [**Connections**](https://app.getcensus.com/connections) page in Census, click the **Add Service** button in the top right, and select Slack.

If you are not already logged in to Slack, you will be redirected to a page to log in to Slack to authorize your account to use Census. Once you are logged in, you'll see a page like the image below, confirming you want to authorize Census.

![](<../.gitbook/assets/Screen Shot 2021-09-13 at 9.39.16 AM.png>)

Once you've authorized Census, you'll be redirected back to the Connections page in Census and you should see your Slack connection there.

## 2️⃣ Connect Census to your data source

See our [docs](broken-reference) for each supported data source for further information.

## 3️⃣ Create your first Census model

Navigate to the **Models** page in Census and click the **Add Model** button.

Here you can a write SQL query to select the data you want to send to Slack.

Once you have created your model, give it a useful name, and click **Save Model**.

## 4️⃣ Create your first Census Notification

Navigate to the [**Notifications**](https://app.getcensus.com/notifications) page in Census and click the **Create a Notification** button.

### 🎚 Setup up your Trigger

You'll need to start by specifying how to identify entries in your data warehouse that should trigger a Notification:

* For **Connection**, select the data warehouse you connected in step 2.
* For **Source**, select the model you created in step 3.
* Next, pick the column that uniquely identifies each record in your data source. Census will use this to identify new records that need to be used to create Notifications to Slack.

<figure><img src="../.gitbook/assets/CleanShot 2022-10-11 at 10.03.37.png" alt=""><figcaption><p>Here is an example of a configured Notification trigger.</p></figcaption></figure>

### 💬 **Setup your Message**

* The notification destination should be selected by default but if you have more than one valid destination for Notifications configured (eg. two Slack accounts), ensure you have the right one selected.
* Then decide whether you want to send your Notification to a Slack channel or a direct message and select the destination from the list.&#x20;
* New Rows will be automatically selected for now as it is the only currently supported logic for Notifications.
* Finally, use the text editor to customize the message that you wish to send.&#x20;
  * To embed values from the trigger columns or to mention users or channels from your Slack account, use the dropdown that will appear. If the list is long, try the search function.

<figure><img src="../.gitbook/assets/CleanShot 2022-10-11 at 10.19.10.png" alt=""><figcaption><p>An example of a configured Notification message.</p></figcaption></figure>

### 🧪 Test your Slack message

* Click the Run Test button to see a single random record sent to your destination. For testing, you may want to temporarily change the destination message yourself.&#x20;

<figure><img src="../.gitbook/assets/CleanShot 2022-10-11 at 10.24.48@2x.png" alt=""><figcaption><p>Testing a new Notification.</p></figcaption></figure>

### ☑️ Finishing touches

* Click the **Finish** button and you'll be taken to your new notification. You can now Schedule the sync to run on a schedule or run it manually yourself.&#x20;
* Note that on the first run, Census will not send any Notifications but will do so on incremental runs when new rows are added to your source model.

<figure><img src="../.gitbook/assets/CleanShot 2022-10-11 at 11.02.21@2x (1).png" alt=""><figcaption><p>Configure your new Notification to run on a set schedule or run it manually.</p></figcaption></figure>

{% hint style="info" %}
Reminder: Census will send records to a Slack channel one at a time.
{% endhint %}

## 🗄️ Supported Objects

| Object Name | Supported? | Identifiers              |
| ----------- | :--------: | ------------------------ |
| Message     |      ✅     | Custom message template. |

{% hint style="info" %}
Census can send data to **all** public channels and any private channels that Census has been explicitly invited to (e.g. `/invite @census`).
{% endhint %}

## 🔄 Supported Sync Behaviors

| **Behaviors** | **Supported?** | **Objects** |
| ------------: | :------------: | :---------: |
|    **Append** |        ✅       |   channel   |

{% hint style="info" %}
Census will only write new records to a specific channel when new records appear in your data warehouse.
{% endhint %}

## 🚑 Need help connecting to Slack?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

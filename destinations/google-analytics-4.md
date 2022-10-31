---
description: This page describes how to use Census with Google Analytics 4
---

# Google Analytics 4

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Google Analytics 4 to Census and create your first sync.

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Google Analytics account ready, with an existing **Google Analytics 4 property**. For Universal Analytics, read our docs for the [Google Analytics connector](google-analytics.md)).&#x20;
  * You'll also need admin access to create API credentials.
* Have the proper credentials to access to your data source. See our [docs for each supported data source](../sources/overview.md) for further information.

### Step 1: Add a Data Stream to your Google Analytics 4 property

In order to add a Google Analytics 4 connection, you'll need to create what Google calls a Data Stream. A Data Stream represents events from either a website or a Firebase app. Google describes the process in more detail in [their docs](https://developers.google.com/analytics/devguides/collection/protocol/ga4/sending-events?client\_type=firebase#required\_parameters).

For a Web App:

* First create a new stream or choose an existing one in **Admin** > **Data Streams**. If creating a new one, specify Web type.



<figure><img src="../.gitbook/assets/screely-1667231371253.png" alt=""><figcaption></figcaption></figure>

* Then within the selected datastream, visit **Measurement Protocol** > **Create**
* Copy the **Secret Value** and the **Measurement ID**

<figure><img src="../.gitbook/assets/screely-1667231393306.png" alt=""><figcaption></figcaption></figure>

****

For Firebase (iOS/Android) applications:

* First create a new stream or choose an existing one in **Admin** > **Data Streams**. If creating a new one, specify iOS or Android types.
* Then within the selected datastream, visit **Measurement Protocol** > **Create**
* Copy the **Secret Value**&#x20;
* You'll also separately need the Firebase App ID. The identifier for a Firebase app is found in the Firebase console under: **Project Settings** > **General** > **Your Apps** > **App ID**

### Step 2: **Create the Census Connection**

* Navigate to the Census [**Connections**](https://app.getcensus.com/connections) page and click **Add Service**
* Select Google Analytics 4 from the drop down list (Not Google Analytics)
* Configure the three settings:
  * Add the Secret Value in the **API Secret** box of the connection.
  * Add the Measurement ID or Firebase App ID in **App ID**
  * Specify the Connection Type: Either **GTag** for websites or **Firebase** for iOS/Android apps.

<figure><img src="../.gitbook/assets/screely-1667231527175 (1).png" alt=""><figcaption></figcaption></figure>

### Step 3: Create your first sync

The sync will move event data from your warehouse to your Google Analytics 4 property.&#x20;

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your **source:** either a Model from the Census Models tab or a database table.
3. Under **Where do you want to sync data to?**, choose the Google Analytics 4 connection you created in Step 2 as the **Connection**.
   * Under **Object** select one of the data sets you created in Step 1.
4. Under **How should changes to the source be synced?**, **Append** will be automatically selected. This is the only supported sync behavior for Google Analytics.
5. Under **Which properties should be updated?** Add the fields from your data set you'd like to send to Google Analytics
6. Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync. If you're happy, check the Sync Now checkbox and save the sync.
7. Confirm the data arrives in Google Analytics!

If you need any help configuring Google Analytics, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## 🗄 Supported Objects

| **Object Name** | **Supported?** | **Identifiers** |
| --------------: | :------------: | :-------------: |
|           Event |        ✅       | Unique Event ID |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Google Analytics.

## 🔄 Supported sync behaviors

| **Behavior** | **Supported?** | **Objects** |
| -----------: | :------------: | :---------: |
|       Append |        ✅       |    Event    |

{% hint style="info" %}
Learn about all of our sync behaviors in [Core Concepts](../basics/core-concept/#sync-behaviors).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Google Analytics.

## 💡 Things to know

* For many Google Analytics reports, data imported this way will only shows up if the User ID has been used as a visitor to the property in the last **30 days**.
* Data takes up to **24 hours** to be fully indexed by google

[Contact us](mailto:support@getcensus.com) if your use cases don't work with these limitations. We'd love to hear how we can make this connection better in the future!

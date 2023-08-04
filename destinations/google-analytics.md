---
description: This page describes how to use Census with Google Analytics
---

# Google Analytics (UA)

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Google Analytics to Census and create your first sync. The Google Analytics connection uses the Universal Analytics API. For support for Google Analytics 4, take a look at the separate [Google Analytics 4 Connector docs](google-analytics-four.md).

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Google Analytics account ready, with admin access to create API-only users and API credentials.
* Have the proper credentials to access to your data source. See our [docs for each supported data source](../sources/overview.md) for further information.

### Step 1: Configure Your Google Analytics Account

Prior to adding Google Analytics as a Destination in Census you'll need to:

* Create a **Custom Dimension** scoped to the **User** ([Google Documentation](https://support.google.com/analytics/answer/2709829#zippy=%2Cin-this-article))
* Create the **Data Set** ([Google Documentation](https://support.google.com/analytics/answer/4524584?ref\_topic=6015090#zippy=%2Cin-this-article))

### **1A: Custom Dimension Set Up**

* Navigate to your Google Analytics account. Click into **Admin Settings**-->Custom **Definitions**-->**Custom Dimensions**

![Create a Custom Dimension](<../.gitbook/assets/Screen Shot 2022-05-31 at 1.18.04 PM.png>)

* Create a new custom dimension or view existing ones. If creating a new one click "**New Custom Dimension**" then provide a name and scope it to the **User**.

![](<../.gitbook/assets/Screen Shot 2022-05-31 at 1.23.06 PM.png>)

### **1B: Create the Data Set**

* Navigate to the **Data Import** tab within the **Settings** to \*\*\*\* view existing data sets or Create a new one.
* If creating a new Data Set start by setting the Data Set type to **User Data**

![](<../.gitbook/assets/Screen Shot 2022-05-31 at 3.20.36 PM.png>)

* Under **Data Set Details** provide a name and select the views that will use the data in the Data Set

![](<../.gitbook/assets/Screen Shot 2022-05-31 at 5.10.23 PM.png>)

* Finally, under **Data Set schema** Select a key from your dimensions and then select the data you'll import.

![](<../.gitbook/assets/Screen Shot 2022-05-31 at 5.18.34 PM.png>)

### Step 2: **Create the Census Connection**

* Navigate to the Census [**Destinations**](https://app.getcensus.com/destinations) page and click **New Destination**
* Select Google Analytics from the drop down list

![](<../.gitbook/assets/Screen Shot 2022-05-24 at 3.30.10 PM.png>)

* Follow the Google OAuth flow to connect your Google Analytics account and allow Census the appropriate permissions

![](<../.gitbook/assets/Screen Shot 2022-05-24 at 3.31.17 PM.png>)

* Once redirected back to Census select the Google Analytics account you want to sync to

![Select a Google Analytics account](<../.gitbook/assets/Screen Shot 2022-05-24 at 3.44.46 PM.png>)

### Step 3: Create your first sync

The sync will move data from your warehouse to your Google Analytics account. In this step, you'll define how that will work.

1. From inside your Census account, navigate to the [**Syncs**](https://app.getcensus.com/syncs) page and click **Add Sync**.
2. Under **What data do you want to sync?**, choose your data warehouse as the **Connection** and your **source:** either a Model from the Census Models tab or a database table.
3. Under **Where do you want to sync data to?**, choose the Google Analytics account you created in Step 2 as the **Connection**.
   * Under **Object** select one of the data sets you created in Step 1.
4. Under **How should changes to the source be synced?**, **Mirror** will be automatically selected. This is the only supported sync behavior for Google Analytics.
5. Under **Which properties should be updated?** Add the fields from your data set you'd like to send to Google Analytics
6. Click the **Next** button to see the final preview which will have a recap of what will happen when you start the sync. If you're happy, check the Sync Now checkbox and save the sync.
7. Confirm the data arrives in Google Analytics!

If you need any help configuring Google Analytics, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## 🗄 Supported Objects

{% hint style="info" %}
The available **Objects** for the Google Analytics destination are the data sets associated with your selected Google Analytics account.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Google Analytics.

## 🔄 Supported sync behaviors

| **Behavior** | **Supported?** | **Objects** |
| -----------: | :------------: | :---------: |
|       Mirror |        ✅       |     All     |

{% hint style="info" %}
Learn about all of our sync behaviors in [Core Concepts](../basics/core-concept/#sync-behaviors).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Google Analytics.

## 💡 Things to know

* Google Analytics has limits to how frequently properties are updated per day so you may want to avoid continuous syncs, especially if you’re importing data through other mechanisms
* For many Google Analytics reports, data imported this way will only shows up if the User ID has been used as a visitor to the property in the last **30 days**.
* Data takes up to **24 hours** to be fully indexed by google

[Contact us](mailto:support@getcensus.com) if your use cases don't work with these limitations. We'd love to hear how we can make this connection better in the future!

---
description: This page describes how to use Census with Marketo.
---

# Marketo

## 🏃‍♂️ Getting Started

### 1. Connecting Census to Marketo

This article describes how to connect Marketo as a Census data destination.

Before you start, you will need admin access to Marketo in order to create the API credentials. You may also want to create a new Marketo API-only user so that you can track changes made by your Census syncs.

### 2. Gathering Marketo Credentials

To connect Census to Marketo, you'll need to collect three pieces of information:

* Endpoint URL
* Client ID
* Client Secret

First, sign into Marketo and click the **Admin** button in the top menu bar. Once in Admin, expand the **Integrations** menu on the left and select the **Web Services** option. Scroll down to the **REST API** section. You'll the **Endpoint URL** excluding the `/rest` part

![](../.gitbook/assets/screely-1618889215086.png)

Then click on **LaunchPoint**. 

You can either reuse the existing default **REST Service** or create a new **Custom** type Service specifically for Census. Once created, click on **View Details**. You will need the **Client ID** and **Client Secret** here.

![](../.gitbook/assets/screely-1618889197214.png)

### 3. Adding Credentials to Census

With all three pieces of information, return to Census and visit the **Connections** tab. Click on the **Add Service** button and select **Marketo** from the menu. Copy and paste the values into the dialog and hit save. You should be good to create a new sync!

![](../.gitbook/assets/screely-1618889184718.png)

## 🗄 Supported Objects

Census currently supports syncing to the following Marketo objects.

| **Object Name** | **Supported?** | Identifiers |
| ---: | :---: | :--- |
| Lead | ✅ | Object ID, any Text/Number  |
| Named Account | ✅ | Object ID, any Text/Number |
| Custom Objects | ✅ | Object ID, any Text/Number |
| Static Lists | \(via Lead\) |  |
| Custom Activities | 🔜 |  |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Marketo.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

| **Behaviors** | **Supported?** | **Objects?** |
| ---: | :---: | :---: |
| **Update or Create** | ✅ | All |
| **Update Only** | ✅ | Lead, Named Account |
| **Mirror** | ✅ | Lead |

{% hint style="warning" %}
Please be aware that Update Only and Mirror make use of less efficient Marketo APIs and will result in more API usage for the same number of records. 
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Marketo.

## 🔑 Require Permissions

To access Custom Objects, the Census API user requires both the **Read-Write Custom Object** and **Read-Write Custom Object Type** permissions. 


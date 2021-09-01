---
description: This page describes how to use Census with Marketo.
---

# Marketo

## 🏃‍♂️ Getting Started

In this guide, we'll show you how to connect Census to Marketo.

### **Prerequisites**

To set up your first Marketo sync, you'll need three things:

* A Census Account – If you don't have one already, [create a Free Trial Census Account](https://app.getcensus.com/).
* A Marketo Account - Specifically, you'll need admin access in order to create an API-only user and API credentials.
* Access to your data warehouse. For details on how to create credentials, see our articles for [Redshift](../source-warehouse/redshift.md), [Snowflake](../source-warehouse/snowflake.md), [Google BigQuery](../source-warehouse/google-bigquery.md), [Databricks](../source-warehouse/databricks.md), and [Postgres](../source-warehouse/postgres.md).

### 1. Create a Marketo API User

Before setting up API credentials for Census, you'll first need a Marketo Role with API Access, as well as a user with that role. 

#### API Access Role

None of the default Marketo Roles have API access so if this is your first API integration, you'll first need to create an API access role. [Marketo's documentation walks through creating a new API Access role](https://developers.marketo.com/rest-api/custom-services/) as well as your first user.

Whether you're using an existing role or creating a new one, please make sure it has at least the following permissions: **Read-Write People** and **Read-Write Named Accounts**. To use Custom Objects, we'll also need **Read-Write Custom Object** and **Read-Write Custom Object Type**.

You can view/edit role permissions in **Admin, Users & Roles**, then clicking the **Roles** tab.

#### API Only User

We recommend you create a new Marketo API User so that you can track changes made by your Census syncs. Either way, the user must be marked **API Only** during creation.

### 2. Gather Marketo API Credentials

To connect Census to Marketo, you'll need to collect three pieces of information:

* Endpoint URL
* Client ID
* Client Secret

Back in **Admin**, expand the **Integrations** menu on the left and select the **Web Services** option. Scroll down to the **REST API** section. Copy and paste the **Endpoint URL** \(you can excluding the `/rest` part\).

![](../.gitbook/assets/screely-1618889215086.png)

Next we'll create a new LaunchPoint Service. Click on **LaunchPoint** and select **New** &gt; **New Service.**

Your new service should have the following properties:

* Display Name: Census
* Service: **Custom**
* Description: Census Data Integration
* API Only User: _\[The user you created in step 1\]_

Once created, you'll see your new service in the list of services. Click on **View Details**. You will need to copy the **Client ID** and **Client Secret** here.

![](../.gitbook/assets/screely-1618889197214.png)

### 3. Adding Credentials to Census

With all three pieces of information, return to Census and visit the **Connections** tab. Click on the **Add Service** button and select **Marketo** from the menu. Copy and paste the values into the dialog and hit save. You should be clear to create a new sync!

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

## 🚑 Need help connecting to Marketo?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


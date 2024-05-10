---
description: This page describes how to use Census with Vero Cloud.
---

# Vero Cloud

## 🏃‍♀️ Getting Started

#### Generate Vero Cloud auth token

1. Open Vero Cloud
2. Navigate to **Settings** > **Project Details**
3. Select **Add API Credentials**
4. Copy the **Auth Token** value to your clipboard

#### Add destination to Census

1. Open Census
2. Click **New Destination**
3. Select **Vero** **Cloud** from the menu
4. Paste your **Auth Token**
5. Click **Connect**

<figure><img src="../.gitbook/assets/Screen Shot 2022-12-30 at 2.36.13 PM.png" alt=""><figcaption><p>Add the auth token you generated in Vero Cloud.</p></figcaption></figure>

## 🗄 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys**       | **Behaviors**    |
| --------------: | :------------: | ------------------- |------------------|
|           Event |        ✅       | Event ID (optional) | Send             |
|            User |        ✅       | Email               | Update or Create |

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Vero Cloud objects and/or behaviors.

## 🚑 Need help connecting to Vero Cloud?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

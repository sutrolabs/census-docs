---
description: This page describes how to use Census with Crowd.dev.
---

# Crowd.dev

## 🏃‍♀️ Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Crowd.dev** from the menu.
3. When prompted, enter the following credentials:
   * **Tenant ID** and **Auth Token** can be found in the Crowd.dev app under **Settings** > **API Keys** ([here](https://app.crowd.dev/settings?activeTab=api-keys)).
   * **Base URL** depends on whether you're self-hosting Crowd.dev or using the hosted version. If you are using the hosted version, your Base URL is `https://app.crowd.dev`.

<figure><img src="../.gitbook/assets/crowd.png" alt=""><figcaption><p>Get your Tenant ID and Auth Token from the Crowd.dev app.</p></figcaption></figure>

## 🔀 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|      **Object Name** | **Supported?** | **Sync Keys**         | **Behaviors**    |
| -------------------: | :------------: | --------------------- | ---------------- |
|             Activity |        ✅       | Source ID             | Update or Create |
| Activity with Member |        ✅       | Source ID             | Update or Create |
|         Organization |        ✅       | Any unique identifier | Update Only, Add |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Crowd.dev objects and/or behaviors.

## 🚑 Need help connecting to Crowd.dev?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

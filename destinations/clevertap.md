---
description: This page describes how to use Census with CleverTap.
---

# CleverTap

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **CleverTap** from the menu.
3. Enter your **Account ID**, **Passcode**, and **Region**. You'll need to generate a passcode from the **Settings** > **Passcodes** screen in the CleverTap app (screenshot below). The account ID and region can be found in the URL: https://**us1**.dashboard.clevertap.com/**K97-K78-1234**/main.

<figure><img src="../.gitbook/assets/clevertap.png" alt=""><figcaption><p>Generate a passcode in the CleverTap app.</p></figcaption></figure>

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys**                                                   | **Behaviors**    |
| --------------: | :------------: | --------------------------------------------------------------- | ---------------- |
|           Event |        ✅       | N/A                                                             | Send             |
|         Profile |        ✅       | Facebook ID, Global Object ID, Google Plus ID, or User Identity | Update or Create |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more CleverTap objects and/or behaviors.

## Need help connecting to CleverTap?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

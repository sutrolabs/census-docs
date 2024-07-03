---
description: This page describes how to use Census with Userflow.
---

# Userflow

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Userflow** from the menu.
3. Enter your **API Key** (found in the Userflow app) and select your **Userflow Plan**.

<figure><img src="../.gitbook/assets/userflow-creds.png" alt="Userflow credentials"><figcaption><p>Enter your Userflow credentials to get started.</p></figcaption></figure>

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys** | **Behaviors**                         |
| --------------: | :------------: | ------------- | ------------------------------------- |
|           Event |        ✅       | Unique ID     | Send                                  |
|           Group |        ✅       | Group ID      | Update or Create                      |
|            User |        ✅       | User ID       | Update or Create, Update Only, Mirror |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Userflow objects and/or behaviors.

## Need help connecting to Userflow?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

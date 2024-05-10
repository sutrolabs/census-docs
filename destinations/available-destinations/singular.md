---
description: This page describes how to use Census with Singular.
---

# Singular

Singular can help you get a complete view of ROI with next-gen attribution,\
full-funnel marketing data, and best-in-class fraud prevention. Census can sync your event data to Singular via their server-to-server (S2S) integration.

## 🏃‍♀️ Getting Started

In order to connect Census to Singular, all that is required is your **SDK Key**. This can be found in your Singular dashboard; follow these steps:

1. Log in to Singular
2. On the sidebar, navigate to **Developer Tools > SDK Integration**
3. Choose the **SDK Keys** tab
4. Click **Show Keys**, and copy the **SDK Key**. You will not need the **SDK Secret**.
5. Back within Census, go to the [Destinations](https://app.getcensus.com/destinations) page in Census and click **New Destination**.
6. Select **Singular** from the menu.
7. Enter the **SDK Key** that you copied in step 4.

You should now be ready to sync your data to Singular.

## 🔀 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|                                                                                                                  **Object Name** | **Supported?** | **Sync Keys** | **Behaviors** |
| -------------------------------------------------------------------------------------------------------------------------------: | :------------: | ------------- |---------------|
| <p>Event<br><a href="../../basics/data-models-and-entities/defining-source-data/events/#defining-event-syncs">Event Sync</a></p> |        ✅       | Event ID      | Send          |
| <p>Session<br><a href="../../basics/data-models-and-entities/defining-source-data/events/#defining-event-syncs">Event Sync</a></p> |        ✅       | Event ID      | Send          |

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Singular objects and/or behaviors.

## 🚑 Need help connecting to Singular?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

---
description: Learn how to use Census to sync your Data Warehouse to ChurnZero.
---

# ChurnZero

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **ChurnZero** from the menu.
3. Enter your **domain**, and **App Key**. You can find all of these in the ChurnZero app under the **Admin > Application Keys > New App Key**.

<figure><img src="../.gitbook/assets/churnzero admin.png" alt=""><figcaption><p>Switch to Admin view</p></figcaption></figure>

<figure><img src="../.gitbook/assets/cz_app_keys.png" alt=""><figcaption><p>Select Application Keys</p></figcaption></figure>

## Custom Fields in ChurnZero

Custom fields defined in ChurnZero can be added to the sync mapping by manually entering the CZ API Name in the destination field mapping

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (2) (1) (1).png" alt=""><figcaption><p>ChurnZero Custom Field</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (2) (1) (1).png" alt=""><figcaption><p>Sync Mapping</p></figcaption></figure>

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys**         | **Behaviors**    |
| --------------: | :------------: | --------------------- | ---------------- |
|         Account |        ✅       | AccountExternalId     | Update or Create |
|         Contact |        ✅       | ContactExternalId     | Update or Create |
|           Event |        ✅       | Any unique identifier | Send             |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

Contact our support team if you want Census to support more ChurnZero objects and/or behaviors.

## Need help connecting to ChurnZero?

Contact our support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

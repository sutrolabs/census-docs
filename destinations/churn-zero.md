---
description: Learn how to use Census to sync your Data Warehouse to ChurnZero.
---

# ChurnZero

## 🏃‍♀️ Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **ChurnZero** from the menu.
3. Enter your **domain**, and **App Key**. You can find all of these in the ChurnZero app under the **Admin > Application Keys > New App Key**.

<figure><img src="../.gitbook/assets/churnzero admin.png" alt=""><figcaption><p>Switch to Admin view</p></figcaption></figure>

<figure><img src="../.gitbook/assets/cz_app_keys.png" alt=""><figcaption><p>Select Application Keys</p></figcaption></figure>

## Custom Fields in ChurnZero

Custom fields defined in ChurnZero can be added to the sync mapping by manually entering the CZ API Name in the destination field mapping

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>ChurnZero Custom Field</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Sync Mapping</p></figcaption></figure>

## 🔀 Supported Objects and Behaviors

| **Object Name** | **Supported?** | **Sync Keys**         | **Behaviors** |
| --------------: | :------------: | --------------------- | ------------- |
|         Account |        ✅       | AccountExternalId     | Upsert        |
|         Contact |        ✅       | ContactExternalId     | Upsert        |
|           Event |        ✅       | Any unique identifier | Append        |

[Contact us](mailto:support@getcensus.com) if you want Census to support more ChurnZero objects and/or behaviors.

## 🚑 Need help connecting to ChurnZero?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

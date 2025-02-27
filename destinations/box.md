---
description: This page describes how to use Census with Box.
---

# Box

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Box** from the menu.
3. Complete the OAuth flow to grant Census access to your Box instance.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p>Grant Census access to your Box account.</p></figcaption></figure>

## ️ File Path Variables

When defining the file path for a Box sync, you can use variables that will be set when the sync runs. This allows you to create and sync to new files in the Box folder that reflect the date and time of the sync.

| **Variable** | **Description**              | **Example Values** |
| ------------ | ---------------------------- | ------------------ |
| `%Y`         | 4-digit year                 | 1997               |
| `%y`         | 2-digit year                 | 97                 |
| `%m`         | month with zero padding      | 07, 12             |
| `%-m`        | month without zero padding   | 7, 12              |
| `%d`         | day with zero padding        | 03, 23             |
| `%-d`        | day without zero padding     | 3, 23              |
| `%H`         | 24 hour with zero padding    | 08, 18             |
| `%k`         | 24 hour without zero padding | 8, 18              |
| `%I`         | 12 hour with zero padding    | 08, 12             |
| `%l`         | 12 hour without zero padding | 8, 12              |
| `%M`         | minute with zero padding     | 04, 56             |
| `%S`         | second with zero padding     | 06, 54             |

## Supported Sync Behaviors

| **Behavior** | **Supported?** | **Objects** |
| -----------: | :------------: | ----------- |
|      Replace |        ✅       | All         |

{% hint style="info" %}
Our current Box integration only supports files up to 50MB in size. If you need support for larger files, please let us know!
{% endhint %}

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../syncs/core-concept/#the-different-sync-behaviors).
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more sync behaviors for Box.

## Need help connecting to Box?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

---
description: This page describes how to use Census with Google Cloud Storage.
---

# Google Cloud Storage

If you need any help configuring GCS, contact the [Census support team](mailto:support@getcensus.com) to get some help.

## File path variables

When defining the **File Path** for an GCS sync, you can use variables that will be set when the sync runs. This allows you to create and sync to new CSV files in the GCS bucket that reflect the date and time of the sync.

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

## 🔄 Supported sync behaviors

| **Behavior** | **Supported** | **Objects** |
| -----------: | :-----------: | :---------: |
|       Mirror |       ✅       |     All     |

{% hint style="info" %}
Learn about all of our sync behaviors in [Core Concepts](https://app.gitbook.com/s/-MV3poo0VqVau1o8I79\_/basics/core-concept#sync-behaviors).
{% endhint %}

[Let us know](mailto:support@getcensus.com) if you want Census to support additional sync behaviors for Google Cloud Storage.

## 💡 Things to know

* Currently, the connector only supports syncing for files up to 5GB.
* Data arrives in one file to the designated bucket and file path.
* Files are written as a CSV with headers.

[Contact us](mailto:support@getcensus.com) if your use cases don't work with these limitations. We plan on addressing at least a few of these in the future!

## 🚑 Need help connecting to Google Cloud Storage?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

---
description: This page describes how to use Census with Google Drive.
---

# Google Drive

Google Drive is Google's cloud file storage service. It allows users to store files in the cloud, synchronize files across devices, and share files. With Census, you can sync data from your data warehouse directly into Google Drive.

## Getting Started

In this guide, we will show you how to connect Google Drive to Census.

### 1. Create a Google Drive connection

Our Google Drive destination behaves a little differently than other Census destinations (but similar to Google Sheets). Instead of going through an OAuth connection flow, we provide you a Google Identity address you use to share the correct Google Shared Drive folder. This lets you be very specific about which Google Drive folders you give Census access to.

* In Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the New Destination button
* Select **Google Drive** in the menu

Your new Google Drive connection will include a Google Identity email. This is the email address you'll use to grant Census access to your target Google Shared Drive (or folder within it). Click the copy button (<img src="../.gitbook/assets/copy-solid.svg" alt="" data-size="line">) to save it to your clipboard, will use it in a minute.

### 2. Share your target Google Drive folder

Now head to the Google Shared Drive and navigate to the folder you'd like to sync to. If you don't have one in mind, you can create a new one.

To give Census access to the folder, press the Share button and then add paste the Google Identity email from Census into the share dialog and confirm.

That's it! You should now see your folder as an option when setting up a sync in Census.

## Supported Sync Behaviors

| **Object Name** | **Supported?** | **Behaviors** |
| :-------------: | :------------: | ------------- |
|       File      |        ✅       | Replace       |

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](/broken/pages/-MV8ovxVCiy1fEjc0SO-#the-different-sync-behaviors).
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Google Drive.

## File Path

When setting up a sync to Google Shared Drive, you can provide a file path for the file name Census will create/replace. The file path can include folders but note that the folders must already exist in Google Drive and must be unique.

### Variables

When defining the **File Path**, you can use variables that will be set when the sync runs. This allows you to create and sync to new files that reflect the date and time of the sync.

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

## Advanced Configuration

In addition to the file path, you can configure how the data is encoded as it is written. Primarily this is a question of file format:

* CSV - The standard comma separated values file. You can optionally specify an alternative delimeter such as `|`\*, and you can enable/disable the header row.
* TSV - The tab separated values file. You can enable/disable the header row.
* JSON - A single JSON arraay of objects
* NDJSON - New line-delimited list of JSON objects
* Parquet - A columnar storage format that is more efficient for certain types of data.
* If your configured delimiter is present in data values, Census will automatically add double quotes around the value.\
  &#xNAN;_&#x45;xample: `Hello, world` is written as as `"Hello, world"` if the chosen delimiter is a comma._

In addition to file format, you can also provide a PGP Public Key to encrypt the data before it is written to the file. This is useful for ensuring that the data is secure in transit and at rest.

## Need help connecting to Google Drive?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

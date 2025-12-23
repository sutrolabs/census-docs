---
description: This page describes how to use Census with Microsoft SharePoint.
---

# Microsoft SharePoint

Microsoft SharePoint is a cloud-based document management and storage service that's part of Microsoft 365. It allows organizations to store, organize, share, and access files from any device. With Census, you can sync data from your data warehouse directly into SharePoint document libraries.

## Getting Started

In this guide, we will show you how to connect Microsoft SharePoint to Census.

### Prerequisites

* A Microsoft 365 account with access to SharePoint
* Appropriate permissions to access the SharePoint sites and document libraries you want to sync to

### 1. Create a Microsoft SharePoint connection

* In Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select **Microsoft SharePoint** from the menu

### 2. Authorize Census

Census uses OAuth to connect to your Microsoft account. Click **Connect** to begin the authorization flow. You'll be redirected to Microsoft to sign in and grant Census the necessary permissions to access your SharePoint sites and document libraries.

### 3. Select your SharePoint site and document library

After authorizing, Census will display a list of SharePoint sites and document libraries you have access to. Select the site and document library where you want to sync your data.

That's it! You should now be able to create syncs to your selected SharePoint document library.

## Supported Sync Behaviors

| **Object Name** | **Supported?** | **Behaviors** |
| :-------------: | :------------: | ------------- |
|       File      |        ✅       | Replace       |

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](broken-reference/).
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync behaviors for Microsoft SharePoint.

## File Path

When setting up a sync to Microsoft SharePoint, you can provide a file path for the file name Census will create/replace. The file path can include folders, but note that the folders must already exist in your SharePoint document library.

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
| `%20`        | spaces in folder names       | Folder Name        |

## Advanced Configuration

In addition to the file path, you can configure how the data is encoded as it is written. Primarily this is a question of file format:

* CSV - The standard comma separated values file. You can optionally specify an alternative delimeter such as `|`\*, and you can enable/disable the header row.
* TSV - The tab separated values file. You can enable/disable the header row.
* JSON - A single JSON array of objects
* NDJSON - New line-delimited list of JSON objects
* Parquet - A columnar storage format that is more efficient for certain types of data.
* If your configured delimiter is present in data values, Census will automatically add double quotes around the value.\
  \&#xNAN;_Example: `Hello, world` is written as as `"Hello, world"` if the chosen delimiter is a comma._

In addition to file format, you can also provide a PGP Public Key to encrypt the data before it is written to the file. This is useful for ensuring that the data is secure in transit and at rest.

## Need help connecting to Microsoft SharePoint?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

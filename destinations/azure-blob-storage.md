---
description: This page describes how to sync data to Azure Blob Storage.
---

# Azure Blob Storage

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Azure Blob Storage** from the menu.
3. Enter the requested credentials.

<figure><img src="../.gitbook/assets/azure-blob-storage.png" alt=""><figcaption><p>Enter your Azure Blob Storage credentials in Census.</p></figcaption></figure>

## Supported Sync Behaviors

| **Behavior** | **Supported?** | **Objects** |
| -----------: | :------------: | ----------- |
|      Replace |        ✅       | All         |

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](/broken/pages/-MV8ovxVCiy1fEjc0SO-#the-different-sync-behaviors).
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more sync behaviors for Azure Blob Storage.

## File Path

When setting up a sync to Azure, you can provide a file path for the file name Census will create/replace. The file path can include folders. Data arrives in one file to the designated bucket and file path.

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

## Need help connecting to Azure Blob Storage?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

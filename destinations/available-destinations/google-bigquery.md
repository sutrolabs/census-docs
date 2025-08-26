---
description: This page describes how to configure Google BigQuery as a Census destination.
---

# Google BigQuery

## Getting Started

In this guide, we will show you how to connect Census to Google BigQuery as a destination.

{% hint style="info" %}
If you are configuring Google BigQuery as a source (to query data from BigQuery to sync elsewhere), that process is documented separately here: [Google BigQuery as a Source](../../sources/available-sources/google-bigquery.md)
{% endhint %}

1. Visit the [Destinations page](https://app.getcensus.com/destinations) and click **+ New Destination**.
2. Enter your Google Cloud Project ID.

## 🔑 Permissions and Service Accounts

In order to connect to your BigQuery projects, Census uses a service account. This service account can be provided by you or managed by Census (recommended).

#### Option A: Upload Service Account Key

If you would prefer to have Census to use a service account that you own (instead of our automatically-managed account) to connect to BigQuery, you may provide its service account key JSON file here.

#### Option B: Use Census-managed Service Account

Otherwise, one you save your connection, Census will create a dedicated Google Cloud Service Account for each BigQuery destination. After the previous step, this account was created. To load data into BigQuery, the account needs the appropriate permissions.

<figure><img src="../../.gitbook/assets/Screenshot 2023-07-21 at 8.55.40 AM.png" alt=""><figcaption></figcaption></figure>

Click the _Activate Cloud Shell_ (near top right) icon in Google Cloud and execute the following commands.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Replace `cs-sandbox-12345` with your Project ID.
* Replace `census-12345abcd1234512345abcdabcd@sutrolabs-giza-production.iam.gserviceaccount.com` with the service account provided in the Census UI.

```
gcloud projects add-iam-policy-binding cs-sandbox-123456 \
  --member serviceAccount:census-12345abcd1234512345abcdabcd@sutrolabs-giza-production.iam.gserviceaccount.com \
  --role roles/bigquery.dataOwner

  gcloud projects add-iam-policy-binding cs-sandbox-123456 \
  --member serviceAccount:census-12345abcd1234512345abcdabcd@sutrolabs-giza-production.iam.gserviceaccount.com \
  --role roles/bigquery.jobUser
```

{% hint style="info" %}
To optimize the time it takes to load your tables within the Census UI when creating and editing syncs, only grant the Census service account permissions to the datasets you want to use within your Census syncs. This will reduce the number of tables Census needs to load and display as well as limit the number of tables to which Census has access.
{% endhint %}

## ️ Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys**    | **Behaviors**                              |
| --------------: | :------------: | ---------------- | ------------------------------------------ |
|           Table |        ✅       | Required columns | Update or Create, Update Only, Mirror, Add |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../../syncs/overview.md) documentation.
{% endhint %}

Contact our support team if you want Census to support more BigQuery objects and/or behaviors

## Optimize UI Performance

To optimize loading time within the Census UI when creating and editing syncs limit the visibility of the Census service account to only the tables and schemas you want to use for syncs within Census. This will reduce the number of tables Census needs to load and display.

## Network Access Controls

While BigQuery itself doesn't support IP allow lists, you can use [VPC Service Controls](https://cloud.google.com/vpc-service-controls/docs/overview) to wrap your BigQuery instance and limit access. You can find Census's set of IP address for your region in [regions-and-ip-addresses.md](../../misc/security-and-privacy/regions-and-ip-addresses.md "mention").

When using VPC Service Controls, you will also need to allow BigQuery unloads to the Census GCP bucket. To do that, you'll need to add [`gs://sutrolabs-giza-unloads-production`](gs://sutrolabs-giza-unloads-production) in the allow list for BigQuery unloads.

## Need help connecting to Google BigQuery?

You can contact our support team or start a conversation from the in-app chat.

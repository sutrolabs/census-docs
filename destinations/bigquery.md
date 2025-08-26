---
description: This page describes how to sync data to your BigQuery data warehouse.
---

# BigQuery

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **BigQuery** from the menu.
3. Enter your BigQuery **Project ID** and hit **Connect**.
4. On the next screen, copy the provided Service Account address.
5. Open BigQuery, navigate to the **IAM & Admin** section, and select **Grant Access**. Paste the provided Service Account address under **New principals**, then assign the requested roles as shown in the screenshot below.

<figure><img src="../.gitbook/assets/bigquery-destination.png" alt=""><figcaption><p>Enter your BigQuery Project ID.</p></figcaption></figure>
<figure><img src="../.gitbook/assets/bigquery-destination2.png" alt=""><figcaption><p>Grant the required roles to the Service Account.</p></figcaption></figure>

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys** | **Behaviors**                      |
| --------------: | :------------: | --------------- |------------------------------------|
| Table | ✅ | Primary keys or columns with uniqueness constraints | Update or Create, Update Only, Add |

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

Contact the support team if you want Census to support more BigQuery objects and/or behaviors.

## Need help connecting to BigQuery?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

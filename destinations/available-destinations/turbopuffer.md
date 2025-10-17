---
description: This page describes how to use Census with turbopuffer.
---

# Turbopuffer

{% hint style="info" %}
The Census turbopuffer destination is in beta. Please reach out to [support](mailto:support@getcensus.com) if you have requests or questions about this destination.
{% endhint %}

### Getting Started <a href="#getting-started" id="getting-started"></a>

In this guide, we will show you how to connect to Census and create your first sync.

## 1. Collect your turbopuffer credentials

Census needs the following information to create a turbopuffer connection:

* API Key - instructions to create one can be found [here](https://turbopuffer.com/docs/auth)&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-17 at 2.47.09 PM.png" alt=""><figcaption></figcaption></figure>

## 2. Connect turbopuffer in Census

1. In Census, navigate to [Destinations](https://app.getcensus.com/destinations)
2. Click the **New Destination** button
3. Select **turbopuffer** in the dropdown list
4. Enter your credentials including the region where you'd like us to find and store your Namespaces and click **Connect**

You're all set!&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-17 at 2.48.55 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If you have any questions during setup, or have a use case that is not covered, please write us in-app or [send us an email](mailto:support@getcensus.com) via support@getcensus.com
{% endhint %}

## Supported Objects and Behaviors <a href="#supported-objects-and-behaviors" id="supported-objects-and-behaviors"></a>

turbopuffer stores data within Namespaces. Your existing Namespaces in turbopuffer can be used as objects to sync to from Census, and you can also create **new** Namespaces using Census.

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-17 at 2.51.10 PM (1).png" alt=""><figcaption></figcaption></figure>

| **Object Name** | **Supported?** | **Sync Keys** | **Behaviors**                     |
| --------------- | -------------- | ------------- | --------------------------------- |
| Namespace       | ✅              | ID            | <p>Update or Create<br>Mirror</p> |

### Advanced Configuration

#### Update Mode

By default, Census will update existing records in turbopuffer using [patch](https://turbopuffer.com/docs/write#param-patch_rows) mode, meaning only the fields being synced by Census will be updated on existing records. However, turbopuffer does not accept updates to the Vector Values field in patch mode.

Alternatively, you can use [replace](https://turbopuffer.com/docs/write#param-upsert_rows) mode to replace the entire existing record in turbopuffer. This will result in nullifying any fields on the record which are not synced to from Census.

You can read more about the different write options in the [turbopuffer docs](https://turbopuffer.com/docs/write).

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-17 at 2.58.01 PM.png" alt=""><figcaption></figcaption></figure>

#### Distance Metric

The distance metric to create the new Namespace with, or the distance metric of the existing Namespace.

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-17 at 3.05.27 PM.png" alt=""><figcaption></figcaption></figure>

### Syncing Vector Values

turbopuffer requires bringing your own vector embeddings via external embedding models. Census supports enriching your dataset with vector embeddings via [Embedding Columns](../../datasets/smart-columns/embedding-columns.md). Use OpenAI to generate vector embeddings for your dataset, then sync your Embedding Column to the turbopuffer Namespace Vector Values field.

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-17 at 3.10.20 PM.png" alt=""><figcaption></figcaption></figure>

## Need help connecting to turbopuffer?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

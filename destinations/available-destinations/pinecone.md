---
description: This page describes how to use Census with Pinecone.
---

# Pinecone

{% hint style="info" %}
The Census Pinecone destination is in beta. Please reach out to [support](mailto:support@getcensus.com) if you have requests or questions about this destination.
{% endhint %}

#### Getting Started <a href="#getting-started" id="getting-started"></a>

In this guide, we will show you how to connect to Census and create your first sync.

### 1. Collect your Pinecone Credentials

Census needs the following information to create a Pinecone connection:

* API Key - instructions to create one can be found [here](https://docs.pinecone.io/guides/projects/manage-api-keys)

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-17 at 12.15.39 PM.png" alt=""><figcaption></figcaption></figure>

### 2. Connect Pinecone in Census

1. In Census, navigate to [Destinations](https://app.getcensus.com/destinations)
2. Click the **New Destination** button
3. Select **Pinecone** in the dropdown list
4. Enter your credentials and click **Connect**

You're all set!

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-17 at 12.58.41 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If you have any questions during setup, or have a use case that is not covered, please write us in-app or [send us an email](mailto:support@getcensus.com) via support@getcensus.com
{% endhint %}

### Supported Objects and Behaviors <a href="#supported-objects-and-behaviors" id="supported-objects-and-behaviors"></a>

Pinecone stores data within Indexes. Your Indexes in Pinecone can be used as objects to sync to from Census.

| **Object Name** | **Supported?** | **Sync Keys** | **Behaviors**                     |
| --------------- | -------------- | ------------- | --------------------------------- |
| Index           | ✅              | ID            | <p>Update or Create<br>Mirror</p> |

#### Syncing Vector Values

Pinecone supports generating vector values for your data, or [bringing your own vectors](https://docs.pinecone.io/guides/get-started/overview#bring-your-own-vectors) via external embedding models. Census supports enriching your dataset with vector embeddings via [Embedding Columns](../../datasets/smart-columns/embedding-columns.md). Use OpenAI to generate vector embeddings for your dataset, then sync your Embedding Column to the Pincone Index Vector Values field.

<figure><img src="../../.gitbook/assets/Screenshot 2025-10-17 at 2.37.37 PM.png" alt=""><figcaption></figcaption></figure>

### Need help connecting to Pinecone?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

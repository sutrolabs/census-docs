---
description: >-
  This page describes how to configure Elasticsearch as a destination with
  Census
---

# Elasticsearch

### Getting Started <a href="#getting-started" id="getting-started"></a>

In this guide, we will show you how to connect  to Census and create your first sync.

## 1. Collect your Elasticsearch Credentials

Census needs the following information to create an Elasticsearch cloud connection:

* API Key - instructions to create one can be found [here](https://www.elastic.co/guide/en/kibana/8.13/api-keys.html#create-api-key)&#x20;

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

* Cloud ID - this can be found in your Elasticsearch cloud instance by clicking Help -> Connection Details

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

* Elasticsearch Port - default is 443
* Elasticsearch Scheme - default is https

Other authentication options are available:

* Key ID - required if created through the dev console, the REST API or self-hosted instance
* Username (Cloud)&#x20;
* Password (Cloud)&#x20;
* Elasticsearch Host&#x20;
* Username (Hosted)&#x20;
* Password (Hosted)&#x20;
* CA Certificate
* CA Fingerprint

## 2. Connect Elasticsearch in Census

1. In Census, navigate to [Destinations](https://app.getcensus.com/destinations)
2. Click the **New Destination** button
3. Select **Elasticsearch** in the dropdown list
4. Enter your credentials and click **Connect**

You're all set!&#x20;

<div><figure><img src="../../.gitbook/assets/Screenshot 2024-08-14 at 13.57.36.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/Screenshot 2024-08-14 at 13.57.50.png" alt=""><figcaption></figcaption></figure></div>

{% hint style="info" %}
If you have any questions during setup, or have a use case that is not covered, please write us in-app or [send us an email](mailto:support@getcensus.com) via support@getcensus.com
{% endhint %}

## Supported Objects and Behaviors <a href="#supported-objects-and-behaviors" id="supported-objects-and-behaviors"></a>

Elasticsearch stores data within collections called Models. Your Models in Elasticsearch can be used as objects to sync to from Census.

| **Object Name** | **Supported?** | **Sync Keys** | **Behaviors**                     |
| --------------- | -------------- | ------------- | --------------------------------- |
| Index           | ✅              | Document ID   | <p>Update or Create<br>Mirror</p> |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Elasticsearch.<br>

## Need help connecting to Elasticsearch?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

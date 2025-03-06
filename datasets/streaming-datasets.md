---
description: >-
  Streaming Datasets allow you to define the data you work with in streaming
  sources that organize their data into topics to which new messages are
  published over time.
---

# Streaming Datasets

Use a Streaming Dataset to prepare data for syncing from Kafka, Confluent Cloud, Google Pub/Sub, and HTTP Request, then use your dataset as the source for a [Live Sync](../syncs/core-concept/live-syncs.md) or triggered [Sync](broken-reference).

## Create a Streaming Dataset

Before you create a Streaming Dataset, you’ll need to connect a streaming source. See individual source documentation:

* [Kafka](../sources/available-sources/kafka.md)
* [Confluent Cloud](../sources/available-sources/confluent-cloud.md)
* [Google Pub/Sub](../sources/available-sources/google-pubsub.md)
* [HTTP Request](../sources/available-sources/http-request.md)

Once your streaming source is connected, open **Datasets** and click **New Dataset**. Select **Streaming Dataset** and click **Next**.

### Select your Source

On the left side of the new dataset dialog, select one of your connected streaming sources. For Kafka, Confluent Cloud, and Google Pub/Sub, select the existing topic in the source that you want to work with in Census.

### Add a Sample Message

In the code editor on the right side of the new dataset dialog, enter a sample JSON message for your new Streaming Dataset. Census will use the sample message you provide to infer the fields and data types of the messages in your dataset.

{% hint style="warning" %}
Census does not treat sample messages as customer data, and they are stored with the rest of your organization’s metadata in Census’s US-based control plane. **Do not include real customer data or PII in your sample message.**
{% endhint %}

When you are finished configuring your new Streaming Dataset, click **Create Dataset**.






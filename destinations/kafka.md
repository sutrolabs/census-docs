---
description: This page describes how to use Census with a Kafka destination.
---

# Kafka

In this guide, we will show you how to connect your Kafka destination to Census.

## Getting Started

1. Go to the **Destinations** tab and click **New Destination**.
2. Select **Kafka** from the menu.
3. To connect to Kafka, you'll need to provide the following credentials:

* **Bootstrap Servers**: One (or more) host/port combinations to use for establishing the initial connection to the Kafka cluster. For example, `kafka-1.example.com:9092,kafka-2.example.com:9092`. Sometimes called `metadata.broker.list`.
* **Protocol**: The protocol to use for communicating with Kafka. Currently, only `SASL_SSL` is supported.
* **Mechanism**: SASL mechanism to use for authentication, such as `PLAIN` or `SCRAM-SHA-512`.
* **Username**: The username of your Kafka instance. Called API Key by Confluent.
* **Password**: The password of your Kafka instance. Called API Secret by Confluent.

{% hint style="info" %}
Your Kafka instance must be accessable to the public internet in order for Census to connect. Consider using [Census' IP addresses](../misc/security-and-privacy/regions-and-ip-addresses.md) to limit access to your Kafka instance.
{% endhint %}

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys**         | **Behaviors**                  |
| --------------: | :------------: | --------------------- | ------------------------------ |
|         Message |        ✅       | Any unique identifier | Send, Update or Create, Mirror |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Kafka objects and/or behaviors

### Message Properties

Sending a Kafka Message involves a number of configuration properties, in addition to the actual message payload. Census allows you to configure these properties in the **Advanced Configuration** section of the destination setup, as well as the **Mappings** section of the sync setup.

Within Advanced Configuration, you can set the following properties:

* **Preserve message ordering**: If enabled, Census will send messages to Kafka in the same order they were received by Census. Otherwise, Census will send messages to Kafka as fast as possible, which may result in messages being received out of order.
* **Created/Updated/Deleted record tag**: Census will automatically add an `operation` property to each message sent to Kafka (see below). You can use these properties to change the value of the `operation` property, which can be useful for downstream processing.
* **Message Template**: You can optionally provide a mustache-formatted template to structure your message. By default with no template provided, Census will send all properties as a single flat JSON object.

Within the Mappings section of the sync setup, you can set the following properties:

* **Topic** (required): The Kafka topic to send the message to.
* **Key**: The key to use for the message.
* **Partition**: The partition to send the message to.
* **Partition Key**: The partition key to use for the message.
* **Timestamp**: The timestamp to use for the message.
* **Headers**: Any headers to include with the message, [structured as an object](../syncs/structuring-data/structured-data.md).

### Message Structure

By default, Census will structure messages as a single flat JSON object. You can optionally provide a Message Template to structure your message in a different way. In addition to the properties you provide, Census will automatically add the following properties to each message:

* **operation**: The operation that triggered the sync.
* **synced\_at**: The time the sync was triggered.

[Contact us](mailto:support@getcensus.com) if you want Census to support more Kafka functionality.

## Need help connecting to Kafka?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

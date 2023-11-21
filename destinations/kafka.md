---
description: This page describes how to use Census with a Kafka destination.
---

# Kafka

In this guide, we will show you how to connect your Kafka destination to Census.

## 🏃‍♀️ Getting Started

1. Go to the **Destinations** tab and click **New Destination**.
2. Select **Kafka** from the menu.
3. To connect to Kafka, you'll need to provide the following credentials:

* **Bootstrap Servers**: One (or more) host/port combinations to use for establishing the initial connection to the Kafka cluster. For example, `kafka-1.example.com:9092,kafka-2.example.com:9092`. Sometimes called `metadata.broker.list`.
* **Protocol**: The protocol to use for communicating with Kafka. Currently, only `SASL_SSL` is supported.
* **Mechanism**: SASL mechanism to use for authentication, such as `PLAIN` or `SCRAM-SHA-512`.
* **Username**: The username of your Kafka instance. Called API Key by Confluent.
* **Password**: The password of your Kafka instance. Called API Secret by Confluent.

## 🔀 Supported Objects and Behaviors

| **Object Name** | **Supported?** | **Sync Keys**  | **Behaviors** |
| --------------: | :------------: | ---------------- | --------------|
| Message | ✅ | Any unique identifier | Append, Upsert, Mirror |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Kafka objects and/or behaviors.

## 🚑 Need help connecting to Kafka?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

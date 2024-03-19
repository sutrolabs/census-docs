---
description: This page describes how to configure Kafka as a source for Census.
---

# Kafka

## :globe\_with\_meridians: Connectivity

Census can connect to Kafka clusters over the public internet. Census always connects to your cluster via TLS using [static IP addresses](../../basics/security-and-privacy/regions-and-ip-addresses.md#ip-addresses) that you can add to an allow list.

### Authentication

Census supports the following SASL authentication mechanisms for Kafka:

* Plain
* SCRAM SHA-256
* SCRAM SHA-512

### Permissions

To read data from your Kafka cluster, Census needs the following permissions:

| Operation | Type  | Resource                             |
| --------- | ----- | ------------------------------------ |
| Read      | Topic | Any topic you want to sync data from |
| Read      | Group | `census_group_*`                     |

When used as the source for a Live Sync, Census will also create error topics in your cluster for messages that can’t be processed. To do so, Census needs the following permissions:

| Operation     | Type  | Resource   |
| ------------- | ----- | ---------- |
| Create, Write | Topic | `census_*` |

## Create a Kafka Connection

1. In Census, navigate to **Sources**.
2. Click **New Source** and select **Kafka**.
3. Enter the hostname and port number of your bootstrap server.
4. Select the SASL authentication method your brokers are configured to use.
5. Enter the username and password Census should use to authenticate with your brokers.
6. Click **Connect**.

After you create a Kafka connection, you need to set up message schemas for your topics.

## Define message schemas

Before you can use a Kafka topic as the source for a sync, you must define the schema of the messages on the topic.

1. In Census, navigate to **Models**.
2. From the **Source** dropdown, select your Kafka connection.
3. Census automatically pulls the list of topics from your cluster. You can also click **Refresh topics** to manually refresh the list.
4. Click on the name of the topic you want to define a schema for.
5. Select the format of the messages on your topic from the **Format** drop down. The only supported format is JSON.
6. Click **Import sample message** and enter a sample message. Your sample message should be a JSON object containing any top-level fields you want to use in your pipelines. Make sure the values of the fields in your sample message match the data type of the values in your actual messages.&#x20;

{% hint style="warning" %}
Census does not handle sample messages as customer data. Do not include real data in a sample message.
{% endhint %}

Click **Save Topic**. Review the listed properties and types to ensure the sample message you provided was interpreted as intended.

## 🚑 Need help connecting to Kafka?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

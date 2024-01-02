---
description: This page describes how to configure Confluent Cloud as a source for Census.
---

# Confluent Cloud

## :globe\_with\_meridians: Connectivity

Census can connect to [Confluent Cloud](https://www.confluent.io/confluent-cloud/?utm\_campaign=tm.pmm\_cd.2023\_partner\_cwc\_census\_generic\&utm\_source=census\&utm\_medium=partnerref) clusters over the public internet. Census always connects to your cluster via TLS.

### Permissions

The API key Census uses to access your Confluent Cloud cluster requires read permission to the topics you want to use within Census. Census will also create error topics in your cluster for messages that can’t be processed by pipelines. These topics have names beginning with `census_`. Census needs permission to create and write to topics with this naming pattern.

## Create a Confluent Cloud Connection

1. Log in to your existing Confluent Cloud account, or [start a free trial](https://www.confluent.io/confluent-cloud/tryfree/?utm\_campaign=tm.pmm\_cd.2023\_partner\_cwc\_census\_tryfree\&utm\_source=census\&utm\_medium=partnerref).
2. Create a resource API key for Census to use to collect to your Confluent Cloud cluster.
   1. Refer to the Confluent Cloud documentation for [step-by-step instructions for creating a resource API key](https://docs.confluent.io/cloud/current/access-management/authenticate/api-keys/api-keys.html#resource-api-keys).
   2. Note the **API key** and **secret** as you will need them to connect Census to Confluent Cloud.
3. In Census, navigate to **Sources**.
4. Click **New Source** and select **Confluent Cloud**.
5. Enter the hostname of your bootstrap server.
6. Enter the API key and secret you created in step 2.
7. Click **Connect**.

After you create a Confluent Cloud connection, you need to set up message schemas for your topics.

## Define message schemas

Before you can use a Confluent Cloud topic as the source for a sync, you must define the schema of the messages on the topic.

1. In Census, navigate to **Models**.
2. From the **Source** dropdown, select your Confluent Cloud connection.
3. Census automatically pulls the list of topics from your cluster. You can also click **Refresh topics** to manually refresh the list.
4. Click on the name of the topic you want to define a schema for.
5. Select the format of the messages on your topic from the **Format** drop down. The only supported format is JSON.
6. Click **Import sample message** and enter a sample message. Your sample message should be a JSON object containing any top-level fields you want to use in your pipelines. Make sure the values of the fields in your sample message match the data type of the values in your actual messages.&#x20;

{% hint style="warning" %}
Census does not handle sample messages as customer data. Do not include real data in a sample message.
{% endhint %}

Click **Save Topic**. Review the listed properties and types to ensure the sample message you provided was interpreted as intended.

## 🚑 Need help connecting to Confluent Cloud?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

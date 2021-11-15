---
description: >-
  This page describes how to configure Rockset credentials for use by Census as
  a source.
---

# Rockset

[Rockset](https://rockset.com) is a cloud-based realtime operational analytics database. Census now supports [Rockset](https://rockset.com) as a fully-supported source, allowing you to sync your Rockset data into your business apps. Rockset also supports managed external datasources such as MySQL, MongoDB and Kafka, enabling to you sync data from those alternative sources.

This walks you through the step by step of setting this up.

## 🔩 Create a Rockset connection

{% hint style="danger" %}
These instructions are well tested to connect Census to Rockset. If you're running into connection issues or missing collections, please confirm you've run all of these instructions.
{% endhint %}

#### 🔐 Required permissions

Census needs an API key with at least "member" permissions. Navigate to the [API keys](https://console.rockset.com/apikeys) section of the Rockset console and create an API key with "member" or "admin" permissions. The account you are using in Rockset must have these credentials to be able to correctly create this.

![Make sure to have no spaces in the API key name](<../.gitbook/assets/Screen Shot 2021-11-14 at 4.56.39 PM.png>)

After creating the key, check which region your Rockset instance is deployed to and copy the API key.

![Take a mental note of which region you are deployed to in Rockset](<../.gitbook/assets/Rockset Credentials.png>)

Navigate to the [connections tab](https://app.getcensus.com/connections) of your Census account. Click on the "Add Data Source" dropdown button in the top right and select Rockset. Paste your API key in the API key section and copy and paste the deployment url depending on what region you are deployed in.

![Click Save Configuration, and ](<../.gitbook/assets/Census Rockset Credentials.png>)

Navigate to the Models tab in Census and query your Rockset collections and views in Census. Now you can sync into your operational tools using Rockset as a source.

## 🚑 Need help connecting to Rockset?

Please [contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat if you're interested in syncing data from Rockset to your business apps.

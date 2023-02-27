---
description: >-
  This page describes how to configure Elasticsearch credentials for use by
  Census as a source and why those permissions are needed.
---

# Elasticsearch

Census lets you select an Elasticsearch instance to treat as a source for your syncs.

In order to sync data from Elasticsearch, Census needs your deployment url, port, username, and password. This walks you through the step by step of setting this up.

## 🔩 Create an Elasticsearch connection

* In Census, go to **Connections** or click [here to go to the app](https://app.getcensus.com/connections)
* Under Data Sources, click **Add Data Source** and select **Elasticsearch.**

![Adding the Elasticsearch Connection](../.gitbook/assets/Elasticsearch.png)

* Enter into your Elastic search instance. Click on the deployment name such that it takes you to a url that looks like `https://cloud.elastic.co/deployments/3last1ch3x4d3c1m4lstr1ng` click on the following button to copy your Elasticsearch endpoint string to your clipboard

![Click this button, to paste it to the clipboard](<../.gitbook/assets/Screen Shot 2021-11-02 at 3.56.57 PM.png>)

* Copy and paste this in the "Server Hostname" field. Then take off the :1234 part at the end to paste those four digits in the "Server Port" field. The user and password are the same from logging into your elastic.co account. Click Save Connection.

![This is the Connection credentials setting](<../.gitbook/assets/Screen Shot 2021-11-02 at 4.58.44 PM.png>)

You're all set! Click "test connection" and you can query this from the models tab and use it as a source for syncing data to our library of destinations.

{% hint style="info" %}
If you have any questions during setup, or have a use case that is not covered, please write us in-app or [send us an email](mailto:support@getcensus.com) via support@getcensus.com
{% endhint %}

## 💡 Notes

* We based our connection protocol on Elastic's [SQL JDBC driver](https://www.elastic.co/guide/en/elasticsearch/reference/current/sql-jdbc.html)

## 🚦 Allowed IP Addresses

If you are restricting access by IP addresses, please add Census's IP addresses to the allowlist in your firewall. You can find Census's set of IP address for your region in [Regions & IP Addresses](../basics/security-and-privacy/regions-and-ip-addresses.md#ip-addresses).

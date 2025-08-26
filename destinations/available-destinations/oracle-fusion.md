---
description: This page describes how to use Census with Oracle Fusion Cloud.
---

# Oracle Fusion

Oracle Fusion Cloud is a comprehensive suite of cloud-based enterprise applications. Census enables you to sync your customer data directly to Oracle Fusion Cloud, allowing you to keep your business objects up to date with the latest information from your data warehouse.

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Oracle Fusion** from the list of available destinations.
3.  **Configure the connection details:**

    **Server URL**: Enter your Oracle Fusion Cloud instance URL (e.g., https://your-instance.fa.us2.oraclecloud.com)\
    **Username**: Enter your Oracle Fusion Cloud username\
    **Password**: Enter your Oracle Fusion Cloud password
4. Click **Connect** to establish the connection.
5. Test the connection to verify that Census can successfully connect to your Oracle Fusion Cloud instance.

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Census currently supports syncing to the following Oracle Fusion objects.

|         **Object Name** | **Supported?** | **Sync Keys** | **Behaviors** |
| ----------------------: | :------------: | ------------- | :-----------: |
|     Receivables Invoice |        ✅       | Any Unique ID |      Add      |
| Receivables Credit Memo |        ✅       | Any Unique ID |      Add      |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../../syncs/overview.md) documentation.
{% endhint %}

Contact the support team if you want Census to support more Oracle Fusion objects and/or behaviors

## Need help connecting to Oracle Fusion?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.


---
description: This page describes how to use Census with Freshsales.
---

# Freshsales

## Getting Started

### 1. Generate a Freshsales API Key

In your Freshsales Account:\
1\) Navigate to My Accounts\
2\) Click on your /crm/sales account\
3\) Click on your user icon in the top right corner > Personal Settings\
4\) Go to the API tab\
5\) Copy Your API Key

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### 2. Connect Freshsales to Census

* Head back to Census and navigate to [Destinations](https://app.getcensus.com/destinations).
* Click the New Destination button.
* Select Freshsales in the dropdown list.
* Paste your Freshsales account's **API Key** and **Domain**. Save your connection and if everything is set up correctly, you should see a successful connection test verifying the connection.

## ​Supported Objects and Sync Behaviors

| **Object Name** | **Supported?** | Identifiers | **Behaviors**            |
| --------------: | :------------: | ----------- | ------------------------ |
|         Account |        ✅       | Name        | Update or Create, Update |
|         Contact |        ✅       | Email       | Update or Create, Update |
|            Deal |        ✅       | Name        | Update or Create, Update |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Freshsales objects and/or behaviors

## Need help connecting to Freshsales?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

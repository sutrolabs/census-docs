---
description: This page describes how to use Census with Snapchat Ads.
---

# Snapchat

## ​Getting Started

1. In Census, navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Snapchat** from the menu.
3. Follow the OAuth flow to connect to your Snapchat account.

![Enter your Snapchat credentials to complete the OAuth flow.](<../.gitbook/assets/Screen Shot 2022-04-25 at 4.23.34 PM.png>)

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name**  | **Supported?** | **Identifiers**            | **Behaviors**            |
| ---------------- | :------------: | -------------------------- | ------------------------ |
| Conversion Event |        ✅       | External ID                | Send                     |
| Customer List    |        ✅       | Mobile Ad ID, Email, Phone | Update or Create, Mirror |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

Contact the support team if you want Census to support more Snapchat objects and/or behaviors.

### Field Normalization

Census does not automatically normalize PII fields sent to Snapchat. When providing values to Census, please apply the normalization specified by Snapchat:

* [Conversion Events](https://developers.snap.com/api/marketing-api/Conversions-API/BestPractices)
* [Customer List](https://developers.snap.com/api/marketing-api/Ads-API/customer-lists)

Census also supports passing prehashed PII fields directly to Snapchat for increased data security.

| Property                            | Normalization                                                                                                                                                                                                                                          | Hash Method          |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------- |
| Email                               | <ul><li>Trim leading and trailing whitespace</li><li>Lowercase</li></ul>                                                                                                                                                                               | Lowercase Hex SHA256 |
| Mobile Advertiser ID (IDFA or GAID) | <ul><li>Lowercase</li></ul>                                                                                                                                                                                                                            | Lowercase Hex SHA256 |
| Phone Number                        | <ul><li>Include country code (remove any double 0 in front of the country code)</li><li>If the number itself begins with a 0 this should be removed</li><li>Exclude any non-numeric characters such as whitespace, parentheses, ‘+’, or ‘-’.</li></ul> | Lowercase Hex SHA256 |

## Need help connecting to Snapchat?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com/) chat.

---
description: This page describes how to use Census with Rokt.
---

# Rokt

Rokt is an e-commerce marketing technology company that uses machine learning to help businesses personalize the customer experience and drive revenue. Census can help you sync your data to Rokt, helping you increase order value, acquire new users, and grow revenue.

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Rokt** from the menu.
3. Open Rokt in another browser tab. Take note of your **Account ID**, which can be found in the URL (e.g. https://my.rokt.com/accounts/**123456789**/profile-settings).
4. You'll need to ask your Rokt account manager for credentials.
   * Custom Audiences:  request an API Key
   * Events: request a public/private key pair
5. Return to Census and input these credentials to connect to Rokt.

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys**                  | **Behaviors**            |
| --------------: | :------------: | ------------------------------ | ------------------------ |
|           Event |        ✅       | Any unique ID                  | Send                     |
|        Audience |        ✅       | Email, MD5 Email, SHA256 Email | Update or Create, Mirror |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/core-concept/#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Rokt objects and/or behaviors.

### Audiences

To specify the list to which you want to add members, its name has to be mapped to the `List` field in Rokt. This means it should either be available in the source, or set as a Constant Value.

<figure><img src="../.gitbook/assets/image (57) (1).png" alt=""><figcaption></figcaption></figure>

## Need help connecting to Rokt?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

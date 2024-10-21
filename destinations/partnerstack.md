---
description: This page describes how to use Census with PartnerStack.
---

# Partnerstack

PartnerStack is a partner relationship management platform that helps you manage and scale your partnerships. Use Census to send customer attributes and transaction events to PartnerStack automatically.

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **PartnerStack** from the menu.
3. Open the PartnerStack app in another window. Go to **Settings** > **Integrations** and copy the relevant API keys (either Test or Production).
4. Return to Census and paste them into the **Public Key** and **Secret Key** fields, respectively.

<figure><img src="../.gitbook/assets/partnerstack.png" alt=""><figcaption><p>Get your API keys from the PartnerStack app.</p></figcaption></figure>

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|                                                                                                                     **Object Name** | **Supported?** | **Sync Keys**     | **Behaviors**                 |
| ----------------------------------------------------------------------------------------------------------------------------------: | :------------: | ----------------- | ----------------------------- |
|                                                                                                                            Customer |        ✅       | Customer Key      | Update or Create, Update Only |
| <p>Transaction<br><a href="../basics/defining-source-data/events#defining-event-syncs">Event Sync</a></p> |        ✅       | Unique Identifier | <p>Send<br></p>               |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Partner Stack objects and/or behaviors

### Transactions

Transactions are sent to PartnerStack as events so each transaction must have a unique identifier so Census can correctly identify them, but that ID is not passed along to PartnerStack. Transactions need to be associated with a customer in PartnerStack, so you must include at exactly one of the following keys in your transaction data:

* customer\_key - The PartnerStack unique identifier for the customer
* customer\_external\_key - Your unique identifier for the customer
* customer\_email - The customer's email address

## Need help connecting to Partnerstack?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

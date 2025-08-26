---
description: This page describes how to use Census with Insider.
---

# Insider

Insider is a customer data platform that helps marketers connect customer data across channels and systems, predict their future behavior with an AI-powered engine, and orchestrate and deliver individualized experiences to customers.

## Getting Started

1. First, you'll need to create a new External Integration in Insider. Hover over the **Components icon (bottom left)**, expand **Integration Settings**, and click on **External Platform Integration**. Select **Census** from the list of available integrations. Provide a name for the integration and click **Save**. You will be provided with two details you'll need to connect Census to Insider: the **Integration Key** and **Insider Account Name**. We recommend storing both the key and the name in a secure location like a password manager as you won't be able to access them again.
2. Now you can return to Census. Navigate to the [Destinations](https://app.getcensus.com/destinations) page and click **Add Destination**. Select Insider from the list of destinations. Provide your API Key and Partner Name and click **Save**.

You should now be ready to start creating audiences in Insider!

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|                                                                                        **Object Name** | **Supported?** |       **Sync Keys**       |         **Behaviors**         |
| -----------------------------------------------------------------------------------------------------: | :------------: | :-----------------------: | :---------------------------: |
|                                                                                                  Users |        ✅       | Email, Phone Number, UUID | Update or Create, Update Only |
| <p>Events<br><a href=".../basics/defining-source-data/events/#defining-event-syncs">Event Sync</a></p> |        ✅       |      Unique Event ID      |              Send             |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

Contact our support team if you want Census to support more Insider objects and/or behaviors

### Quirks

* Syncing Events may also cause new User records to be created if the provided User ID does not already exist in Insider.
* Insider has a unique approach to handling clearing values in their API. Census takes care of most of this automatically, with one exception: If you are attempting to write `NULL` values to identifiers, Census will not be able to clear the value in Insider.

## Need help connecting to Insider?

Contact our support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

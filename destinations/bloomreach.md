---
description: This page describes how to use Census with Bloomreach.
---

# Bloomreach

Bloomreach is a digital experience platform that helps businesses create personalized experiences for their customers. Census can sync your customer data to Bloomreach to help you better understand your customers' needs and personalize their experiences.

## Getting Started

Census will need four pieces of information to connect to your Bloomreach account, all of which can be found in Bloomreach's API settings.

1. Within the Bloomreach app, click the gear icon in top right to access **Settings**. Within the left settings menu, click **Access management** > **API**.
2. Now create a new API Key for Census (you can reuse an existing key if you have one, but we recommend creating a new one for Census)
   1. If necessary, create a new API Group for Census. Groups are used for organization and permissions. The group needs the following permissions:
      * The group type must be **Private**
      * Both get and set permissions to all customer properties
      * Both get and set permissions to all event properties
      * All import permissions
   2. Inside the group, click **Add Key** and give it a name like "Census".
3. Now copy both the API Key and the API Secret, as well as the API Base URL and the Project Token above the API Key.
4. Back within Census, go to the [Destinations](https://app.getcensus.com/destinations) page in Census and click **New Destination**.
5. Select **Bloomreach** from the menu.
6. Enter the API Key, API Secret, API Base URL, and Project Token. Hit save and you're done!

You should now be ready to sync your data to Bloomreach.

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|                                                                                                               **Object Name** | **Supported?** | **Sync Keys**                          | **Behaviors**    |
| ----------------------------------------------------------------------------------------------------------------------------: | :------------: | -------------------------------------- | ---------------- |
|                                                                                                                      Customer |        ✅       | Registered (Hard ID), Cookie (Soft ID) | Update or Create |
| <p>Event<br><a href="../basics/data-models-and-entities/defining-source-data/events/#defining-event-syncs">Event Sync</a></p> |        ✅       | Event ID                               | Send             |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Bloomreach objects and/or behaviors.

#### Customer object quirks

There's a few things to note about the customer object in Bloomreach:

* Bloomreach customers can be identified by two different IDs: Hard ID (aka registered, this is equivalent to external ID but they don't use that terminology) or Soft ID (aka cookie). Census supports both of these identifiers. These are also customizable and might not be present in every Bloomreach instance.
* Bloomreach does not currently offer an API to retrieve the schema/properties for the customer object. When mapping to customer fields, please use the exact names (case-sensitive) as they appear in the API Permissions > Properties page in Bloomreach.

#### Event quirks

Like Customer objects, Bloomreach does not currently offer an API to retrieve the schema/properties for the event object either. So again, double check that you're using the exact names (case-sensitive) as they appear in the API Permissions > Properties page in Bloomreach.

## Need help connecting to Bloomreach?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

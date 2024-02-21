---
description: This page describes how to use Census with Klaviyo.
---

# Klaviyo

Klaviyo is a customer data and marketing platform specializing in marketing for Retail, Ecommerce and D2C businesses. It's a powerful, scalable, and secure platform for sending emails, SMS, and more.

## 🏃‍♀️ Getting Started

As always, the first step is connecting Census to your Klaviyo account.

Census requires two API keys, both a Public and Private key, in order to provide full functionality. To access your API Keys,
1. Within Klaviyo, click your organization name in the bottom left.
2. Navigate to **Settings** and click **API keys** from the submenu.

We'll cover how to create both below, and [Klaviyo's Help Center](https://help.klaviyo.com/hc/en-us/articles/7423954176283) provides additional details as well.

#### 1. Private API Key
The Private API Key is used to sync most data to Klaviyo. We recommend creating a new API Key specifically for Census.

Census requires "Full Access" in order to write data to Klaviyo. However, you may use Klaviyo's "Custom Access" Private API Key to limit the access to only the necessary permissions.

#### 2. Public API Key / Site ID
The Public API Key is used solely to access the [Klaviyo API](https://developers.klaviyo.com/en/reference/create_client_profile) that powers Profile Update or Create at higher volume.

Klaviyo only allows a single Site ID so in this case, you can reuse your existing public API Key.

#### 3. Configuring Census

Once you've collected both keys, you can create a new Klaviyo destination in Census.
1. Within Census, navigate to [**Destinations**](https://app.getcensus.com/destinations).
2. Click **New Destination** and select Klaviyo from the dropdown list.
3. Paste in your Klaviyo Private and Public Keys and click **Save**.

You should now be ready to create a new sync to Klaviyo from Census!


## 🗄 Supported Objects and Behaviors

|  **Object Name** | **Supported?** |  **Sync Keys** |  **Behavior**  |
| ---------------: | :------------: | :------------: | :------------: |
|          Profile |        ✅       | External ID (recommended), Email, Phone Number | Update or Create, Update Only, Delete |
|   Profile & List <br> [Audience Sync](https://docs.getcensus.com/basics/core-concept/audience-syncs)|        ✅       | External ID (recommended), Email, Phone Number | Mirror |
|            Event <br> [Event Sync](/basics/data-models-and-entities/defining-source-data/events#defining-event-syncs) |        ✅       | Unique Event ID |  Append  |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional objects for Klaviyo.

### Klaviyo Profile's List Property

To update the **List** property, you'll need to provide the list **ID** or **Name** values as a JSON array of strings, for example:

```
["List A", "List B", "List C"]
```

```
["RYkk48", "Xmpet6", "DyreR0"]
```

### Klaviyo Events

Klaviyo events work like most behavioral event destinations. They require a unique event ID which is used to prevent duplicate events from being created in Klaviyo, as well as a name, timestamp, and custom properties.

One quirk of events in Klaviyo is how events are associated with specific users. Klaviyo will associate events with a user based on the email address provided or the Klaviyo User ID (not an external ID), and so Klaviyo event syncs require at least an email address or Klaviyo ID to be captured properly. If you're using an external ID, you'll need to ensure that the email address is also provided in the event payload. Using [phone numbers as identifiers does not work reliably](https://developers.klaviyo.com/en/reference/update_profile) in some cases depending on how Klaviyo is configured.

## 🚑 Need help connecting to Klaviyo?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

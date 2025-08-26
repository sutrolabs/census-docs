---
description: This page describes how to use Census with Klaviyo.
---

# Klaviyo

Klaviyo is a customer data and marketing platform specializing in marketing for Retail, Ecommerce and D2C businesses. It's a powerful, scalable, and secure platform for sending emails, SMS, and more.

## Getting Started

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

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|                                                                                                         **Object Name** | **Supported?** |                  **Sync Keys**                 |              **Behavior**             |
| ----------------------------------------------------------------------------------------------------------------------: | :------------: | :--------------------------------------------: | :-----------------------------------: |
|                                                                                                                 Profile |        ✅       | External ID (recommended), Email, Phone Number | Update or Create, Update Only, Delete |
| <p>Profile &#x26; List<br><a href="https://docs.getcensus.com/basics/core-concept/audience-syncs">Audience Sync</a></p> |        ✅       | External ID (recommended), Email, Phone Number |                 Mirror                |
|                    <p>Event<br><a href="../basics/defining-source-data/events/#defining-event-syncs">Event Sync</a></p> |        ✅       |                 Unique Event ID                |                  Send                 |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation. Contact our support team if you want Census to support more Klaviyo objects and/or behaviors.
{% endhint %}

### How profile identifiers work in Klaviyo

Though Census supports selecting a primary key for profile syncs, it's important to know that Klaviyo has a specific way of handling profile identifiers that Census cannot override.

Klaviyo supports four identifiers for profiles: Email, Phone Number, External ID, and Klaviyo ID.

Klaviyo will always use Klaviyo ID as the primary identifier for profiles when available (only for Update Only syncs). This is the only key that Klaviyo will use to allow updating other identifiers like Email or Phone Number on existing profiles.

When upserting profiles, Klaviyo ID cannot be used but any combination of the other three identifiers can be used as the primary key. However, Klaviyo will verify that the provided identifiers are unique and reference the same profile.

For example: If you are syncing a profile with an External ID and Email, Klaviyo will check if the External ID and Email are associated with the same profile.

* If a profile with a matching External ID and Email is found, Klaviyo will update the profile with the provided data.
* If a profile with a matching External ID is found but the provided email is different (and not already used by another profile), Klaviyo will update the profile with the provided email.
* If a profile with a matching External ID is found, and a different profile with a matching email is found, Klaviyo will throw an error indicating a conflict in the provided data.

{% hint style="info" %}
Though the API prevents them, duplicate profiles are still possible in Klaviyo. Upserting data when duplicates are present will result in only one of the duplicates being updated (by closest match). We recommend cleaning up duplicates in Klaviyo to avoid confusion caused by updates that appear to be missing.
{% endhint %}

### Klaviyo Events

Klaviyo events work like most behavioral event destinations. They require a unique event ID which is used to prevent duplicate events from being created in Klaviyo, as well as a name, timestamp, and custom properties.

One quirk of events in Klaviyo is how events are associated with specific users. Klaviyo will associate events with a user based on the email address provided, the Klaviyo User ID, or an external ID. Due to this Klaviyo event syncs require at least an email address, Klaviyo ID, or external ID to be captured properly. Using [phone numbers as identifiers does not work reliably](https://developers.klaviyo.com/en/reference/update_profile) in some cases depending on how Klaviyo is configured.

## Need help connecting to Klaviyo?

You can contact our support team or start a conversation from the in-app chat.

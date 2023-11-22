---
description: This page describes how to use Census with HubSpot.
---

# HubSpot

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect HubSpot to Census.

{% embed url="https://www.loom.com/share/3b7ed3624e6542b08c8ea4e25907b6ed?sid=c877f144-d635-4e5b-aeef-c42f848f1522" %}

### Connecting HubSpot

* Within Census, navigate to the [Destinations page](https://app.getcensus.com/destinations).
* Click the **New Destination** button.
* Select HubSpot from the menu and click **Connect.**

![](../.gitbook/assets/screely-1651800460992.png)

Follow the OAuth flow to connect HubSpot. Easy!

## 🗄 Supported Objects and Behaviors

<table data-header-hidden><thead><tr><th width="239" align="right"></th><th width="254"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td><strong>Sync Keys</strong></td><td><strong>Behavior</strong></td></tr><tr><td align="right">Company</td><td>Object ID, any Text/Number</td><td>Update Only, Update or Create, Mirror</td></tr><tr><td align="right">Contact</td><td>Object ID, Email, any Text/Number</td><td>Update Only, Update or Create, Mirror</td></tr><tr><td align="right">Contact &#x26; Static List</td><td>Email</td><td>Update Only, Update or Create, Mirror</td></tr><tr><td align="right">Deal</td><td>Object ID, any Text/Number</td><td>Update Only, Update or Create, Mirror</td></tr><tr><td align="right">Product</td><td>Object ID, any Text/Number</td><td>Update Only, Update or Create, Mirror</td></tr><tr><td align="right">Line Item</td><td>Object ID, any Text/Number</td><td>Update Only, Update or Create, Mirror</td></tr><tr><td align="right">Custom Object</td><td>Object ID, any searchableProperty</td><td>Update Only, Update or Create, Mirror</td></tr><tr><td align="right">Subscription Preferences</td><td>Email</td><td>Mirror</td></tr><tr><td align="right">Custom Behavioral Event</td><td>Unique Event ID</td><td>Append</td></tr><tr><td align="right">Email</td><td>N/A</td><td>Append</td></tr><tr><td align="right">Ticket</td><td>Record ID</td><td>Append</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you're looking for Census to support other HubSpot objects.

{% hint style="info" %}
HubSpot uses Cloudflare to protect their API, which is quiet sensitive to receiving data that appears to be malicious. In order to prevent HubSpot/Cloudflare from blocking all Census customers, our HubSpot connecter automatically sanitizies strings removing common malicious patterns. If you're seeing data discrepencies that may be related to this, please [contact the Census support team](mailto:support@getcensus.com).
{% endhint %}

### Custom Objects

Custom Objects are available to customers on HubSpot's Enterprise plans.

As of March 2021, only properties in the `searchableProperties` set are usable as sync keys in Census. This is a bit confusing as this label only appears in the HubSpot API. A searchable property can be added to a Custom Object via HubSpot's API. The calls to make this update can be found in HubSpot's [Custom Objects API Docs](https://developers.hubspot.com/docs/api/crm/crm-custom-objects) > Object Schema Tab > searchableProperties.

Additionally, HubSpot has some apps available in their marketplace like [Dotsquares](https://hubspot.dotsquares.com/easy-custom-objects-setup/) that can assist with Custom Object management.

If you need a hand making one of your existing Custom Object fields searchable, please [contact the Census support team](mailto:support@getcensus.com) and we can walk you through it.

### Custom Behavioral Events

Custom Behavioral Events require a bit of prep work. You'll first need to go into HubSpot and create your event (see [HubSpot's instructions for how to do that](https://knowledge.hubspot.com/analytics-tools/create-custom-behavioral-events)).

You'll need to both create the event AND add all of the custom properties beforehand. Once you've done so, copy and paste HubSpot's internal name for the object—you'll need to provide that to the `Event Name` property during the Census sync.

Note: The custom fields you've added will not show inside Census. You'll need to use the **New Custom Field** option to create the matching fields in Census. Make sure they're named exactly the same (names are case-sensitive).

### Subscription Preferences

Subscription preferences allow you to manage which users are subscribed or unsubscribed from your existing marketing subscriptions (Currently, HubSpot does not allow external services to programmatically create new subscriptions).&#x20;

HubSpot Subscription Preferences syncs require additional fields when using HubSpot's GDPR portal:&#x20;

* **Legal Basis** One of the following values: `LEGITIMATE_INTEREST_PQL`, `LEGITIMATE_INTEREST_CLIENT`, `PERFORMANCE_OF_CONTRACT`, `CONSENT_WITH_NOTICE`, `NON_GDPR`, `PROCESS_AND_STORE`, `LEGITIMATE_INTEREST_OTHER`.
* **Legal Basis Explanation** A more detailed explanation to go with the legal basis.

The same value provided for these fields will be used for both subscribing and unsubscribing a user.

{% hint style="info" %}
Census can only remove contacts from subscriptions that were originally created by Census.&#x20;
{% endhint %}

### Managing Object Associations

HubSpot supports an advanced method of defining relationships between objects called [Associations](https://knowledge.hubspot.com/crm-setup/create-and-use-association-labels). Associations have a number of different properties:

* They're supported between all HubSpot object pairs, including Custom Objects.
* They can represent one-to-many and many-to-many relationships.
* Associations can be labeled or unlabeled. HubSpot Professional and Enterprise plans also support custom labels.

Many-to-many associations can be updated in Census syncs on either side of the associations, while one-to-many associations can only be set on the child or "many" side.

<figure><img src="../.gitbook/assets/Screenshot 2023-08-01 at 2.54.52 PM.png" alt=""><figcaption><p>Census Company/Contact Association</p></figcaption></figure>

#### Labeled Associations

Labels in HubSpot can be complex. Census provides some advanced configurations to make updating and removing labels a bit more straightforward.

When creating a labeled association between two objects in HubSpot, HubSpot will also automatically create an unlabeled association. Additionally, when creating an association from a Contact to a Company, HubSpot will create another association labeled Primary. That means that adding a labeled association with a Census sync may actually create up to three associations.

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption><p>Hubspot Labeled Association</p></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2023-08-01 at 2.39.44 PM.png" alt=""><figcaption><p>Census Labeled Association Sync Mapping</p></figcaption></figure>

Unfortunately, HubSpot does not offer a way to remove these default associations when they're no longer necessary after removing the labeled association Census created. These associations may have actually been created intentionally so Census also cannot delete them automatically.

To navigate this, Census provides an option to automatically clean up orphaned default associations when removing any associations.

![](../.gitbook/assets/screely-1659672959589.png)

When this behavior is enabled and a Census sync removes a labeled association, we'll also check to see if the remaining associations are only the unlabeled and Primary labeled associations. If so, we'll automatically remove those associations as well.

By default, this feature is not enabled to avoid accidentally deleting associations that were created outside the sync and should still exist.

### Formatting Data for Hubspot Data Types

**Object references (Associations):** will be mapped to a Hubspot Array of Reference data type. The source data should be formatted in an array.

**Example:** `["RecordID_1", "RecordID_2"]`

**Multiple Checkboxes (Enumerated fields):** will be mapped to a Hubspot Array of Enumeration. The source data should also be formatted as an array. Additionally, HubSpot expects the options provided to be the Internal Value as given by Hubspot's property settings page.

**Example:** `["InternalValue1", "InternalValue2", "InternalValue3"]`

## 🏎 Sync Speed

Census uses a variety of APIs to achieve the highest possible speed. With the right sync configuration (see below), Census can **update 10,000 contacts per second**. Census connects to HubSpot via OAuth, which is subject to a limit of 100 requests every 10 seconds (except for the Search API). For more information, see the [HubSpot documentation](https://developers.hubspot.com/docs/api/usage-details).

{% hint style="warning" %}
Your choice of sync key and behavior can have significant performance implications.

Using HubSpot Object IDs or Contact emails as identifiers in HubSpot is fast, but using all other fields as identifiers is very slow. That means any syncs that create new records in HubSpot (other than Contacts by email) will be slow. We're working with HubSpot to increase the speed of their APIs in order to improve sync speed.
{% endhint %}

Please be aware that Custom Objects require additional API calls and are even slower as a result (\~1/3 the speed).

## 🔑 Required Permissions

Census requires that the connecting HubSpot user have Super Admin permissions in order to access all supported HubSpot objects. If you have limited permissions and still want to connect Census to HubSpot, [contact the Census support team](mailto:support@getcensus.com).

## :electric\_plug: Disconnecting HubSpot

If you need to disconnect HubSpot from Census for any reason, you can delete your connection from the Destinations page in Census and/or uninstall the Census app from your HubSpot account by following [these instructions](https://knowledge.hubspot.com/integrations/connect-apps-to-hubspot#uninstall-an-app). Note that you won't be able to sync new data from Census until the connection is restored, but no previously synced data in HubSpot will be impacted.

## 🚑 Need help connecting to HubSpot?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

---
description: This page describes how to use Census with HubSpot.
---

# HubSpot

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect HubSpot to Census and create your first sync.

{% embed url="https://www.loom.com/share/3b7ed3624e6542b08c8ea4e25907b6ed?sid=c877f144-d635-4e5b-aeef-c42f848f1522" %}

### Prerequisites

* Have your Census account ready. If you need one, [start a free trial now](https://app.getcensus.com).
* Have your HubSpot account ready.
* Have the proper credentials to access your data source. If you haven't connected a source to Census yet, [start there](broken-reference).

### 1. Connect HubSpot

* Once you are in Census, navigate to the [Destinations page](https://app.getcensus.com/destinations).
* Click the **New Destination** button.
* Select HubSpot from the menu and click **Connect.**

![](../.gitbook/assets/screely-1651800460992.png)

* Follow the OAuth flow to connect HubSpot.

<figure><img src="../.gitbook/assets/CleanShot 2023-08-14 at 10.33.29@2x.png" alt=""><figcaption></figcaption></figure>

* Your end state should look something like this:

<figure><img src="../.gitbook/assets/CleanShot 2023-08-08 at 15.19.30@2x.png" alt=""><figcaption></figcaption></figure>

### 2. Create your first Sync

You'll need to have connected at least one source to Census before creating a sync. Once you've done that, head to the [Sync page](https://app.getcensus.com/syncs) and click the **New Sync** button.

#### **Select a Source**

This might be a SQL query you've written in Census or just a table in your warehouse.

<figure><img src="../.gitbook/assets/CleanShot 2023-08-08 at 15.38.10@2x.png" alt=""><figcaption></figcaption></figure>

#### **Select a Destination**&#x20;

Select the HubSpot connection you set up in Step 1, then choose the object that you plan to sync to (e.g. Contact or Company).

<figure><img src="../.gitbook/assets/CleanShot 2023-08-08 at 15.42.06@2x.png" alt=""><figcaption></figcaption></figure>

#### **Select a Sync Behavior**

Decide how you want Census to modify records in HubSpot.

<figure><img src="../.gitbook/assets/CleanShot 2023-08-08 at 15.42.28@2x.png" alt=""><figcaption></figcaption></figure>

#### **Select a Sync Key**

Determine how you'd like Census to match records between your source and HubSpot.

<figure><img src="../.gitbook/assets/CleanShot 2023-08-08 at 15.44.11@2x.png" alt=""><figcaption></figcaption></figure>

#### **Set Up Field Mappings**

Decide which columns you'd like to sync from your source data and how they map to fields in the destination.

<figure><img src="../.gitbook/assets/CleanShot 2023-08-08 at 15.46.23@2x.png" alt=""><figcaption></figcaption></figure>

#### **Run a Test Sync**

This step is optional but strongly encouraged. Click **Run Test** to send a test record to HubSpot. This ensures everything is wired up correctly before running a full sync.

<figure><img src="../.gitbook/assets/CleanShot 2023-08-08 at 15.48.54@2x.png" alt=""><figcaption></figcaption></figure>

Click the **Next** button to review the details of your sync. When you're ready check the box next to **Run a sync now?** and click **Create** to start your sync!

### 3. Confirm the data is in HubSpot

Once your sync (or test run) completes, return to HubSpot and search for a record that should have been updated. If everything went as planned, you should see your data in HubSpot.

![](https://s3.amazonaws.com/helpscout.net/docs/assets/5bb7d5d0042863158cc71f7e/images/5f656c764cedfd00176363f8/file-aQC3QWxxq7.png)

That's it! In just a few steps, you've synced data from your warehouse to HubSpot :tada:

## 🏎 Sync Speed

Because Census connects to HubSpot via OAuth, you are only subject to a limit of 100 requests every 10 seconds (except for the Search API). For more information, see the [HubSpot documentation](https://developers.hubspot.com/docs/api/usage-details).

{% hint style="warning" %}
Your choice of sync key and behavior can have significant performance implications.

Using HubSpot Object IDs or Contact emails as identifiers in HubSpot is fast, but using all other fields as identifiers is very slow. That means any syncs that create new records in HubSpot (other than Contacts by email) will be slow. We're working with HubSpot to increase the speed of their APIs in order to improve sync speed.
{% endhint %}

Please be aware that Custom Objects require additional API calls and are even slower as a result (\~1/3 the speed).

## 🗄 Supported Objects

[Contact us](mailto:support@getcensus.com) if you're looking for Census to support other HubSpot objects!

<table data-header-hidden><thead><tr><th width="239" align="right"></th><th width="184.33333333333331" align="center"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Sync Keys</strong></td></tr><tr><td align="right">Company</td><td align="center">✅</td><td>Object ID, any Text/Number</td></tr><tr><td align="right">Contact</td><td align="center">✅</td><td>Object ID, Email, any Text/Number</td></tr><tr><td align="right">Contact &#x26; Static List</td><td align="center">✅</td><td>Email</td></tr><tr><td align="right">Deal</td><td align="center">✅</td><td>Object ID, any Text/Number</td></tr><tr><td align="right">Product</td><td align="center">✅</td><td>Object ID, any Text/Number</td></tr><tr><td align="right">Line Item</td><td align="center">✅</td><td>Object ID, any Text/Number</td></tr><tr><td align="right">Custom Object</td><td align="center">✅</td><td>Object ID, any searchableProperty</td></tr><tr><td align="right">Custom Behavioral Event</td><td align="center">✅</td><td>Unique Event ID</td></tr><tr><td align="right">Email</td><td align="center">✅</td><td>N/A</td></tr><tr><td align="right">Ticket</td><td align="center">✅</td><td>Record ID</td></tr></tbody></table>

### Custom Objects

Custom Objects are available to customers on HubSpot's Enterprise plans.

As of March 2021, only properties in the `searchableProperties` set are usable as sync keys in Census. This is a bit confusing as this label only appears in the HubSpot API. A searchable property can be added to a Custom Object via HubSpot's API. The calls to make this update can be found in HubSpot's [Custom Objects API Docs](https://developers.hubspot.com/docs/api/crm/crm-custom-objects) > Object Schema Tab > searchableProperties.

Additionally, HubSpot has some apps available in their marketplace like [Dotsquares](https://hubspot.dotsquares.com/easy-custom-objects-setup/) that can assist with Custom Object management.

If you need a hand making one of your existing Custom Object fields searchable, please [contact the Census support team](mailto:support@getcensus.com) and we can walk you through it!

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

### Custom Behavioral Events

Custom Behavioral Events require a bit of prep work. You'll first need to go into HubSpot and create your event (see [HubSpot's instructions for how to do that](https://knowledge.hubspot.com/analytics-tools/create-custom-behavioral-events)).

You'll need to both create the event AND add all of the custom properties beforehand. Once you've done so, copy and paste HubSpot's internal name for the object—you'll need to provide that to the `Event Name` property during the Census sync.

Note: The custom fields you've added will not show inside Census. You'll need to use the **New Custom Field** option to create the matching fields in Census. Make sure they're named exactly the same (names are case-sensitive).

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** |                **Objects**                |
| -------------------: | :------------: | :---------------------------------------: |
| **Update or Create** |        ✅       | All except Email, Custom Behavioral Event |
|      **Update Only** |        ✅       | All except Email, Custom Behavioral Event |
|           **Mirror** |        ✅       | All except Email, Custom Behavioral Event |
|           **Append** |        ✅       |   Email, Ticket, Custom Behavioral Event  |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Sync Behaviors for HubSpot.

## 🔑 Required Permissions

Census requires that the connecting HubSpot user have Super Admin permissions in order to access all supported HubSpot objects. If you have limited permissions and still want to connect Census to HubSpot, [contact the Census support team](mailto:support@getcensus.com).

## :electric\_plug: Disconnecting HubSpot

If you need to disconnect HubSpot from Census for any reason, you can delete your connection from the Destinations page in Census and/or uninstall the Census app from your HubSpot account by following [these instructions](https://knowledge.hubspot.com/integrations/connect-apps-to-hubspot#uninstall-an-app). Note that you won't be able to sync new data from Census until the connection is restored, but no previously synced data in HubSpot will be impacted.

## 🚑 Need help connecting to HubSpot?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

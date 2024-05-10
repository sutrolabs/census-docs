---
description: This page describes how to use Census with Braze.
---

# Braze

### Note on Braze API Costs

{% hint style="warning" %}
Braze prices its API on a per data point update basis. Census ensures that only fields that need to be updated are sent (rather than a copy of the entire record). Please be aware that large datasets, which change often can increase your Braze API usage. [Read More](braze.md#supported-objects-1).
{% endhint %}

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Braze to Census and create your first sync.

{% embed url="https://youtu.be/qwa2BEuxEBs" %}

### Prerequisites

* Have your Census account ready. If you need one, [create a Free Trial Census account](https://app.getcensus.com/) now.
* Have your Braze account ready, with create access for Braze API keys.
* Have the proper credentials to access to your data source.

### 1. Create a Braze API key

Braze lets you create a number of API keys, each with their own set of permissions. You'll almost certainly want to create a new API key for Census rather than reusing an existing one.

Within Braze's left navigation bar, scroll down to the very bottom. In the **Settings** tabs, under the subheading **Setup And Testing,** click **API Keys**.

<figure><img src="../.gitbook/assets/CleanShot 2023-08-30 at 08.48.51@2x.png" alt=""><figcaption></figcaption></figure>

Then, inside the **API Settings** tab, under **Rest API Keys**, click **+ Create New API Key**.

![](../.gitbook/assets/screely-1619749695118.png)

Provide a name you'll recognize ("Census" is a good choice) and select the following permissions:

* All User Data permissions, except for `users.delete`

{% hint style="info" %}
You must include users.delete if you want to do the [remove option of Mirroring users](braze.md#mirror-mode-options)
{% endhint %}

* For API-triggered Campaigns: `campaigns.list` and `campaigns.trigger.send`
* For Catalogs: All Catalogs permissions
* This permission set may change as we add support for more Braze objects so you may want to grant more permissions now or plan to update these permissions in the future.

Scroll down and click **Save API Key**.

Finally, copy the long code you see under **Identifier**. We'll use that in a minute.

![](../.gitbook/assets/screely-1619749895841.png)

### 2. Select your Braze API Endpoint

Braze requires that we use a slightly different URL to access your account depending on where it's been set up. See the [full list of all Braze API Endpoints](https://www.braze.com/docs/api/basics/#endpoints). In general, you just need the number from the URL you see in your browser when you're signed into Braze.\
\
For example, if your Braze URL is https://dashboard-**03**.braze.com/, then your API Endpoint should be https://rest.iad-**03**.braze.com.

### 3. Add your Data Import Key (optional)

When syncing to Braze Cohorts you need to provide your Data Import key. To find this key login to your instance in Braze and navigate to **Technology Partners** under **Integrations** and then select Census. You will find your **Data Import Key** and your **Rest Endpoint** here. Paste those values into the respective credential fields when setting up the connection.

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-29 at 2.56.17 PM.png" alt=""><figcaption><p>Census Technology Partner page in Braze</p></figcaption></figure>

### 4. Create the Census Connection

Great! Now let's pull it all together.

1. In the [**Destinations**](https://app.getcensus.com/destinations) page, click on New Destination, and select "Braze"
2. You can provide whatever name you like for the connection
3. Provide the appropriate Braze Endpoint URL
4. Copy and paste your new Braze API key

![Click Connect](<../.gitbook/assets/Braze Connection.png>)

After the Connection Test is Green, you're all set and ready to get syncing! 🎉

## 🗄 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Census currently supports syncing to the following Braze objects.

|               **Object Name** | **Supported?** |                                               **Sync Keys**                                                |              **Behaviors**               |
|------------------------------:| :------------: |:----------------------------------------------------------------------------------------------------------:|:----------------------------------------:|
|                         Event |        ✅      |                                                  Event ID                                                  |                   Send                   |
|                Purchase Event |        ✅      |                                           Any Unique Identifier                                            |                   Send                   |
|        API-Triggered Campaign |        ✅      |                                              External User ID                                              |                   Send                   |
|    API-Triggered Canvas Entry |        ✅      |                                              External User ID                                              |                   Send                   |
|                       Catalog |        ✅      |                                                 Catalog ID                                                 |     Update or Create, Update, Mirror     |
|                        Cohort |        ✅      |                                              External User ID                                              |             Update or Create             |
| Subscription Group Membership |        ✅      | <a href="https://docs.getcensus.com/destinations/braze#braze-subscription-group-memberships">See Here</a>  |                  Mirror                  |
|                          User |        ✅      |                                              External User ID &#x26; User Alias                                              | Update or Create, Update, Delete, Mirror |

Census supports custom fields on both Braze User and Event objects. Additionally, Census supports [sending structured data](../basics/data-defining/defining-source-data/structured-data.md) to Braze:

* [User Push Tokens](https://www.braze.com/docs/api/objects\_filters/user\_attributes\_object#push-token-import) - To send push tokens, your data should be structured as an array of objects with 2-3 values: `app_id`, `token`, and an optional `device_id`.
* [Nested Custom Attributes](https://www.braze.com/docs/user\_guide/data\_and\_analytics/custom\_data/custom\_attributes/nested\_custom\_attribute\_support/#api-request-body) - Both objects and arrays are supported.

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

### Working with User Aliases

In Braze, users can be alternatively identifier by a user alias. A user alias is a JSON object with two keys: `alias_label` and `alias_name` . For example: `{"alias_label":"instagram_id", "alias_name":"7372382492"}`. When updating users by User Alias, you should pass Census the alias as a string from your warehouse (`TEXT`, `CHAR`, `VARCHAR`, or `STRING`) - do not use your warehouse's `OBJECT`, `JSON`, `STRUCT`, or `RECORD` type.

### ✉️ Braze Subscription Group Memberships

Census offers a way to manage your Braze Subscription Groups via your data hub. The current behavior is that you are to "Mirror" the subscribed users from your user base. It is required that you have, within the source:

* The Subscription Group Id in Braze
* Braze User External Id

This source model should be all of your Subscribed users for their Subscription groups. If a previously-synced **subscription group / user pair** no longer appears in your data source, Census will **unsubscribe** that user from that subscription group.

{% hint style="info" %}
If you have a query that returns the external id, subscription group id, and status columns. Your source model should logically look like this:

`SELECT`

`external_id, subscription_group_id`

`FROM`

`subscription_table`

`WHERE`

`status = 'subscribed'`
{% endhint %}

Only the Braze User External Id and the Subscription Group Id should be mapped fields. This is a special unsubscribing mirror for user/group pairs that no longer appear in the data source.

### Braze Cohorts

Braze Cohorts allow users of Census to define and sync user cohorts between Census and Braze. To get started make sure your [data import key](braze.md#3.-add-your-data-import-key-optional) is set on the connection. Then when creating a new sync to Braze select **User & Cohort** as destination object.

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-29 at 3.19.04 PM.png" alt=""><figcaption><p>Braze Sync Configuration for User &#x26; Cohort</p></figcaption></figure>

Select the source column for identifying users that you want to add to a Cohort. Right now we can only identify Braze users for Cohorts by _External User ID._ Then select what Cohort you would like to sync to. You can select an existing Cohort from the dropdown list, define a new Cohort, or select a source column to dynamically get the Cohort name value.

If you want a user to be removed from the Cohort if they are removed from the source dataset then select **remove matching record from cohort** from the dropdown.

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-29 at 3.23.33 PM.png" alt=""><figcaption><p>Cohort Sync Editor Configuration Panel</p></figcaption></figure>

Finally, add any User fields to the mapper. During a sync any fields that you map will first be synced to the User object to update what already exists in Braze and then the updated User will be added to the specified Cohort. Now you can run your sync!

Once you have synced to a Braze Cohort you can take advantage of it in Braze by navigating to **Engagement > Segments** and then either create a new segment or select an existing one. In the Braze Segment builder you can then add a new filter and select **Census Cohorts** from the dropdown. The cohorts that you've created in Census will be available here and any Users in those segments will automatically have the correct filtering logic applied.

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-29 at 3.30.40 PM.png" alt=""><figcaption><p>Census Cohorts custom filter in Braze</p></figcaption></figure>

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-29 at 3.32.17 PM.png" alt=""><figcaption><p>Census Cohort custom filter in Braze</p></figcaption></figure>

### Catalogs

To sync to Catalogs, you'll need to do two additional steps:

* Make sure your API key in Braze provides write access to Catalogs (`catalogs.*`). If you didn't include this permission previously when connecting to Census, you may need to generate a new API Key
* Create the catalog in Braze first, so that it shows as an option in Census.

### API-Triggered Campaign and Canvas Entry

API Triggered Campaign and Canvas Entries are useful for triggering transactional actions within Braze. Like Catalogs, you will need to create the Campaign/Canvas Entry in Braze first before it appears as a destination object in Census.

You can [read more about Braze API-Triggered Campaigns](https://www.braze.com/docs/user\_guide/engagement\_tools/campaigns/building\_campaigns/delivery\_types/api\_triggered\_delivery/) and Canvas Entries in their documentation.

<figure><img src="../.gitbook/assets/Braze Options.png" alt=""><figcaption></figcaption></figure>

### Mirror Mode Options

Braze's Mirror behavior optionally supports a choice of two actions when a record is removed from the source. This can be configured when setting up the sync initially. The first time the sync is performed, the records will be used as a basis for mirroring behaviour in future syncs:

* **Delete record** - This is the typical behavior for most mirror syncs. When a record is removed from the source, the corresponding record will be deleted from Braze.
* **Null out fields** - This is a new behavior for mirror syncs in Braze. In this case, when a record is removed from the source, the currently mapped fields of the synced record will be removed from the destination record (by setting them to Null). The identifier will not be removed from the destination record.
* **Subscription Group Membership** - This will unsubscribe users from the corresponding subscription group, as described [above](braze.md#braze-subscription-groups).

Regardless of which option is selected, mirror syncs identify deletions of each type by comparing against the data they have already sent -- not the data that might or might not already exist in Braze. This means that the first sync will be an upsert for all records, and the second and following syncs will account for deletions from the source data.

[Contact us](mailto:support@getcensus.com) if you want Census to support more sync behaviors for Braze.

## Data Points

In order to minimize your API usage with Braze to ensure that your organization is only updating the [data points](https://www.braze.com/docs/user\_guide/onboarding\_with\_braze/data\_points/) that have actually changed, Census exports the mapped fields from Braze and scans the data in your data source (including on Full Syncs). If there is a difference, Census will send that data point over from the source. If there is not, Census will not send that data point write over.

{% hint style="warning" %}
Note that certain built-in fields in Braze, such as Country and Gender, have automatic standardization that happens in Braze. i.e.: "United States" from SQL becomes "US" from Braze's API.

So when using these type of values, we recommend either:

* Pre-standardize your fields to match Braze’s format (i.e. "US")
* Use Custom Attributes to store them instead
{% endhint %}

### Data Types in Braze

With Census, you know have the ability to specify which Data Type your syncs are referring to. When you change the data type, the next Census sync will be a full sync. If the Census destination field data types match up with the Braze data types, Census will perform the Braze export and comparison with your data.

{% hint style="info" %}
Please make sure you validate the data types on Custom Attributes, that they are as you would expect in the Sync mappings.

An example of this is when the Braze Custom Attribute Type that is "Automatically detect (Time)", we strongly recommend making sure that the Census Destination field type as shown below of type "DateTime" as shown below.
{% endhint %}

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## 🚑 Need help connecting to Braze?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

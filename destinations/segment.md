---
description: This page describes how to use Census with Segment.
---

# Segment

## Getting Started

In this guide, we will show you how to connect Segment to Census.

{% hint style="info" %}
Segment Documentation on Write Keys are [here](https://segment.com/docs/connections/find-writekey/).
{% endhint %}

* Create a new HTTP API Source in the Connections page of Segment (found under "Server")
* Name your connection and optionally label it (We recommend "Census" for ease of debugging)
* Copy your write key from the saved connection
* Navigate to the [Destinations page](https://app.getcensus.com/destinations) of Census, click on the "New Destination" button and select Segment, and paste the created token in the designated field

![](<../.gitbook/assets/Screen Shot 2021-11-12 at 11.16.21 AM.png>)

* Census will convert this right here and now you're all set with the Segment Connection!

![Don't worry if the credential here is different!](<../.gitbook/assets/Screen Shot 2021-11-12 at 11.16.53 AM.png>)

Note: Census's permissions will be the same as this Segment token.

{% hint style="info" %}
Make sure to follow Segment's Documentation on connecting a Production Source [here](https://segment.com/docs/unify/quickstart/#step-3-connect-production-sources).
{% endhint %}

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Segment support is pretty straight forward! [Let us know](mailto:support@getcensus.com) if you want Census to support more objects for Segment.

| **Object Name** | **Supported?** | **Sync Keys**                       | **Behaviors**    |
| --------------: | :------------: | ----------------------------------- | ---------------- |
|            User |        ✅       | User ID or Anonymous ID             | Update or Create |
|           Group |        ✅       | Group ID, or User ID / Anonymous ID | Update or Create |
|   Track (Event) |        ✅       | Any unique identifier               | Send             |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/core-concept/#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Segment objects and/or behaviors.

### Track events

Like most [events.md](../syncs/structuring-data/events.md "mention"), Segment Track Events have the standard set of fields. Though the `event` type field is the only required field, you should typically set at least all the standard event fields.

* `event` (required) - This is the event type field
* `anonymousId` or `userId` (one of these required) - This indicates which user caused or triggered the event
* `timestamp` - The time the event occurred. If not provided, Segment will use their server time when the event was received by them (which can be quite different from when it happened, particularly if you're using Census to backfill events).
* `properties` - Acts as a Properties bundle. See[#using-the-properties-bundle](../syncs/structuring-data/events.md#using-the-properties-bundle "mention") for more information.
* `context` and `integrations` - Optional event context and controls. See [structured-data.md](../syncs/structuring-data/structured-data.md "mention") for more information on how to create objects to map to these fields.
* [Deduplication](https://segment.com/docs/guides/duplicate-data/): Segment will deduplicate events received based on the `messageId` and stores at least 24 hours worth of `messageId`s. Due to this, sync keys should be unique across Segment Event syncs within a 24 hour period.

For more information on the meaning of different Segment fields, take a look at their [documentation](https://segment.com/docs/connections/spec/track/).

### Group Syncs

You can use Group destination object in two different ways:

* Creating and Updating new Groups - Use the Group ID Sync Key to uniquely identify new groups and add `traits` to them.
* Associating Users with Groups - Use the User ID (or Anonymous ID) as Sync Key to associate users with the Group they're a member of.

## Need help connecting to Segment?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

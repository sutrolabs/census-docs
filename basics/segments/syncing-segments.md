---
description: >-
  Sync your segments to any marketing or advertising tool, and automatically
  keep them fresh when your data changes
---

# Syncing Segments

Creating segments is valuable on its own (for more information, take a look at how Census lets you [analyze your segments](analyzing-segments.md) regardless of their destination). But the real value of Census is publishing them to your marketing, advertising, and sales destinations, and automatically keep them up-to-date as your data changes.&#x20;

To publish a segment, you'll need to set up a new sync that defines how the segment should be sent to a specific destination, including which data points should be synced, and how frequently. You can sync a segment in two ways:

#### 1. Quick Sync

For any segment, you can view all of its destinations in the **Syncs** tab. You can also use **Quick Sync** to instantly setup a new sync. Quick Sync uses the most recently previously created sync from the segment's input data set and each destination as a template. Quick Sync will instantly copy the configuration from the last including schedules and field mappings. If it's an audience sync, Quick Sync will automatically pass along your segment's name to the destination as well.&#x20;

<figure><img src="../../.gitbook/assets/screely-1681238303732.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Only active syncs can be used as quick sync templates. Paused and draft syncs will not appear as an option in the quick sync list.
{% endhint %}

#### 2. New Sync

Segments are available as a sync source option through the normal [sync creation workflow](../core-concept/). In this case, you'll first select the entity your segment is based off of, and then select the specific segment you'd like to sync.

<figure><img src="../../.gitbook/assets/screely-1681238384316.png" alt=""><figcaption></figcaption></figure>

## Managing Audiences in Destination

Where available, Census also supports automatically creating new audiences in destinations to match your Segments. For more information on this special sync type, see [Audience Syncs](../core-concept/audience-syncs.md).

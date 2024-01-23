---
description: >-
  Send your segments to any ad platform or marketing tool and automatically keep
  them fresh when your data changes.
---

# Activating Segments

Creating segments is valuable on its own (for example, take a look at how Census lets you [analyze your segments](analyzing-segments.md) regardless of their destination). But the real value of Census is in publishing those segments to ad platforms and marketing tools and automatically keeping them fresh as your data changes.

There are two ways to publish a segment, depending on where (and how) you want to send it.

## One-Click Experience for Ad Platforms

Because most ad platforms work very similarly, we provide a streamlined experience for sending audiences to them. Once you've created a segment, head over to the **Destinations** tab and you'll see a list of all the ad platforms that have been connected in your Census workspace. To start sending your segment to one of those ad platforms, just toggle it on and we'll handle the rest! Yep, it's that simple :tada:

<figure><img src="../../.gitbook/assets/one-click audiences.gif" alt=""><figcaption><p>Sending a segment to popular ad platforms requires a single click.</p></figcaption></figure>

{% hint style="info" %}
**The one-click experience is only available for segments defined on top of "person" entities.** Configuring these entities is typically the responsibility of your data team. As part of that process, they'll tell Census which identifiers are available in the underlying dataset. Then, when you enable a one-click sync to an ad platform we'll automatically determine which identifiers to send based on what the destination allows.
{% endhint %}

### Default Settings

If you've synced to other types of destinations in Census, you'll recognize we make some assumptions behind the scenes to make the one-click experience possible.

* **Matching audience names**—when you enable a one-click sync for the first time, we create an audience in the destination with the same name as your segment in Census. Even if you change the name of your Census segment, the name of your destination audience will remain the same.
* **Only one audience type**—some ad platforms support more than one audience type. In these cases, we default to using the audience type that most marketers will want most of the time. For example, TikTok supports both Partner Audiences and Customer File Audiences, but they recommend using Partner Audiences in most cases (unless you need to run Reach & Frequency campaigns).
* **"Mirror" audience members**—when creating audience syncs using the "classic" sync experience, you can choose whether or not you want Census to remove audience members in the destination when they're removed in your source data. With one-click syncs, we assume you want them to be removed so your destination audience always remains in sync with your source data.
* **Daily sync schedule—**one-click audiences are resent to ad platforms daily, which we've found is sufficient in most cases.

While we believe these defaults are right for most marketers most of the time, there may be times you need to do things differently. While you can't modify the settings for an existing one-click sync, you can still create a "classic" Census sync as described below.

{% hint style="info" %}
When we launched one-click audiences, we migrated existing all ad platform syncs that matched the assumptions above. We also migrated some that didn't, but in those cases we preserved the original configurations. For example, if we migrated a sync on a weekly schedule, it remained weekly. If you have any questions, please contact [support@getcensus.com](mailto:support@getcensus.com) and we'll be happy to help.
{% endhint %}

### Supported Destinations

As of January 2024, our one-click experience supports the following ad platforms:

* [Google Ads](../../destinations/google-ads/)
* [Facebook](../../destinations/facebook-ads.md)
* [LinkedIn](../../destinations/linkedin.md)
* [Microsoft](../../destinations/microsoft-advertising.md)
* [TikTok](../../destinations/tiktok.md)
* [Snapchat](../../destinations/snapchat.md)
* [Pinterest](../../destinations/pinterest.md)
* [X](../../destinations/twitter.md)

We plan to expand this list in the future. If you don't see an ad platform above, it's very likely we support it using our ["classic" sync experience](syncing-segments.md#classic-experience-for-other-destinations). If you still can't find what you're looking for, please contact [support@getcensus.com](mailto:support@getcensus.com).

## "Classic" Experience for Other Destinations

You'll often need to send a segment somewhere other than an ad platform (e.g. a marketing or sales tool). Or perhaps you need to create an ad platform sync that doesn't fit the [default settings](syncing-segments.md#default-settings) described above. In either case, you can access our "classic" sync creation experience one of two ways:&#x20;

**Option 1**: Navigate to your segment, then **Destinations** > **Other Destinations** > **New Sync**

<figure><img src="../../.gitbook/assets/Segments [Destinations - Overview].png" alt=""><figcaption><p>Create a "classic" sync from your Census segment to any destination.</p></figcaption></figure>

**Option 2**: Go to the [**Syncs page**](https://app.getcensus.com/syncs) and select **New Sync**

<figure><img src="../../.gitbook/assets/CleanShot 2023-12-13 at 17.27.44@2x.png" alt=""><figcaption><p>Create a new sync from the Syncs page.</p></figcaption></figure>

Regardless of whether you choose option 1 or 2 above, you'll enter the normal [sync creation workflow](../core-concept/). If you choose option 1, the current segment will be selected as your source. If you choose option 2, you'll need to select the relevant entity, and then choose the segment you want to sync.

<figure><img src="../../.gitbook/assets/CleanShot 2023-12-13 at 17.35.47@2x.png" alt=""><figcaption><p>Select the segment you'd like to sync.</p></figcaption></figure>

Segments and entities have the same capabilities as model-based syncs but also enable the syncing of fields from any related source that is joined on a many-to-one basis.  For example, if syncing contacts you can also sync the company name of each contact. Don't hesitate to reach out to [support@getcensus.com](mailto:support@getcensus.com) if you need help navigating this.

### Automatically Managing Destination Audiences

Where available, Census also supports automatically creating new audiences in destinations to match your segments. For more information on this special sync type, see [Audience Syncs](../core-concept/audience-syncs.md).

### Syncing All Segment Membership Lists

It's common to have many segments created from the same entity, and many of the users or other records may appear in multiple segments. In some cases, it's helpful to be able to access a list of all of the segments each record appears in so that they can be worked with in combination (for example, combining potential offers in a single email) or just-in-time decisions can be made about most important segment.

In this case, the entity has a dynamic value called **Segment Membership** that will return a list of all of the segments each record is a member of. This value is available when syncing the entity rather than any individual segment, so it will include all records of the entity, even if the list of segments they are currently a member of is empty.&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2023-12-13 at 17.38.23@2x.png" alt=""><figcaption><p>Sync "Segment Membership" from the parent entity.</p></figcaption></figure>

You can also sync this field to make segment memberships available via the [Entity API](../developers/entity-api.md).

Syncing Segment Memberships will recalculate segment membership across all syncs for that entity at sync time so depending on the number of segments created, this can slow down your sync.

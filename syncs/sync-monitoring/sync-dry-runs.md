---
description: >-
  Sync with confidence by estimating the impact of a sync before actually
  sending any data to the destination.
---

# Sync Dry Runs

{% hint style="success" %}
This feature is not available for every destination object. If you'd like it somewhere it's not currently supported, please contact the support team!
{% endhint %}

Sometimes it's helpful to know the impact of a sync before actually running it.

Perhaps you're running a new sync for the first time, or just made some big changes to the data model powering an existing sync.&#x20;

Whatever the reason, dry runs help you sync data with confidence by simulating a sync and providing a concise summary of the changes Census _would_ have made in the destination.

## How do I start a dry run?

If dry runs are available for a sync you've created, you'll see a **Start Dry Run** button on the sync overview page. This is true even if you haven't triggered your first sync run yet.

<figure><img src="../../.gitbook/assets/CleanShot 2023-11-07 at 14.08.45@2x.png" alt=""><figcaption><p>Start a dry run from the sync overview page.</p></figcaption></figure>

## What do dry runs tell me?

Every destination API we integrate with provides different capabilities and our dry run experience reflects that. Depending on the circumstances, a dry run will provide you with some combination of the data points below.

<figure><img src="../../.gitbook/assets/CleanShot 2023-11-07 at 14.12.42@2x.png" alt=""><figcaption><p>Dry runs report a number of sync diagnostics.</p></figcaption></figure>

### **Source info**

* **Total records**: total records in the source data
* **Records changed**: records changed since the previous sync (on the first sync, this will equal the total number of records)
* **Records invalid**: records marked as invalid by Census (often due to duplicate identifiers)

### Destination info

* **Records before**: records currently in the destination
* **Records after**: records that would exist in the destination after running the sync
* **Expected creates**: records that would be created as a result of the sync
* **Expected updates**: records that would be updated as a result of the sync
* **Expected deletes**: records that would be deleted as a result of the sync

## How do I view historical dry runs?

You can access the results of historical dry runs at any time. Just visit the **Sync History** tab for a sync and click on the dry run to view the results.

<figure><img src="../../.gitbook/assets/CleanShot 2023-11-07 at 14.38.47@2x.png" alt=""><figcaption><p>View historical dry runs from the Sync History page.</p></figcaption></figure>

## A special case: Braze data point consumption

[Braze](../../destinations/braze.md) is one of our most popular destinations, but their unique pricing model (based on [data point consumption](https://www.braze.com/docs/user\_guide/data\_and\_analytics/data\_points/)) might cause you to hesitate when syncing large amounts of data via Census.

As a result, we've built an enhanced version of dry runs specifically for Braze to help you estimate the number of data point writes a sync will consume (both overall and for each individual field.)

<figure><img src="../../.gitbook/assets/CleanShot 2023-11-07 at 14.26.06@2x.png" alt=""><figcaption><p>View estimated data point consumption for certain Braze syncs.</p></figcaption></figure>

## Need something? We're here to help

If you have questions about dry runs or need help understanding the impact of a sync, reach out to the support team via in-app chat.

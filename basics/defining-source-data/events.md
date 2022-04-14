---
description: >-
  A very common type of user data are their "events", records of each action
  they take. This page details how to define event data in your data source and
  how to sync it to your destinations.
---

# Events

## What Are Events?

Unlike user profile records, event data is tied to specific actions, almost always associated with a user and/or company. Events typically have a specific set of fields

* **Unique ID** - Often used by services to make sure events are not submitted multiple times
* **Timestamp** - The time the event occurred
* **Event Name / Type** - Indication of the type of event that happened at that time
* **User and/or Company ID** - The thing that caused the event to happen or that the event happened to.
* And then optionally some properties about the event, often different properties for each type

In your data model, each event should be represented as a single row/record in the data source. When Census detects a new row in the data source, it will pass it to the destination service as an event/action using the parameters you've configured.

## Defining Event Syncs

Census supports an ever-growing set of destinations that accept event-style data. Often times these are simply labeled as "Events" but some destination services, such as [delighted.md](../../destinations/delighted.md "mention") or [webhook.md](../../destinations/webhook.md "mention") work like events in order to send NPS Surveys and Webhook API messages respectively.&#x20;

To send event data, you'll nee to create a new sync that uses the **Append Only**. Census will treat your event data as an ever-growing append log of data and whenever new rows appear in your data source, will send them over.

The Append Only event sync gives you a few special behaviors to optimize your sync

#### Backfill or just look forward

When setting up an Append Only sync, Census will ask if you'd like to backfill the events already in the data source or simply sync going forward. This option lets you skip any existing data in the data source and only sync new event rows as they appear.&#x20;

#### Detect new records by timestamp

By default, Census uses the Event ID to detect which rows are new and should be synced. This is fine for most use cases but when data sources expand beyond tens of millions or rows, it may be faster to use a timestamp if available.&#x20;

{% hint style="info" %}
Identify new records by timestamp is available on Google BigQuery, Snowflake, and Redshift data warehouses.
{% endhint %}

#### Tracking data history

Census will keep track of events that have been synced by ID (or timestamp) for the life of the sync configuration to avoid syncing them more than once. As a result, the typical Force Full Sync option is not available on event syncs, and event syncs require data warehouses that support writing state. As such, [read-only data sources](https://docs.getcensus.com/basics/core-concept#data-source-permissions-and-read-only-access) are not supported at this time.&#x20;


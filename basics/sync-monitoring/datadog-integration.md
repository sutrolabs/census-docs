---
description: Monitor your syncs in Datadog
---

# Datadog Integration

With Census's Datadog integration, you can centralize your monitoring and alerting within one tool. Census will emit metrics and events that help you understand the health of your data pipelines, alert on anomalies, and manage incidents.

{% hint style="warning" %}
The Datadog integration is accessible for Enterprise Plan accounts. If you would like to enable this integration and are not on the Enterprise Plan, please contact us at [support@getcensus.com](mailto:support@getcensus.com).
{% endhint %}

## Set up

To set up your Datadog integration:

1. Navigate to your workspace's **Settings > Integrations** tab.
2. Click to **configure** your Datadog integration for this workspace.
3. Authenticate with your Datadog account via OAuth.

You're done! Metrics and events will start flowing to Datadog with every sync.

## Recommended Datadog Dashboard

<figure><img src="../../.gitbook/assets/Screen Shot 2023-02-20 at 1.27.52 PM.png" alt=""><figcaption><p>Datadog's Approved Partner Integration Dashboard for Census Observability</p></figcaption></figure>

To view a dashboard of recommended, actionable reports on top of your Census Datadog metrics -- you may take advantage of [Census's listing on the Datadog Integrations marketplace](https://app.datadoghq.com/integrations?search=Census).

Simply:

1. Log into your Datadog account.
2. Head to the Integrations tab, and [search for Census](https://app.datadoghq.com/integrations?search=Census).
3. Click to "Install" the Integration.
4. [Navigate to your list of dashboards](https://app.datadoghq.com/dashboard/lists). You'll now see the dashboard **"Census Sync Observability"** available in your account!

Any data previously sent through the integration will populate these reports.

## Metrics and Events

Census sends the following to Datadog:

### Metrics

* **census.syncs.sync\_completed** - the number of syncs that have completed over a time window
* **census.syncs.rows\_processed** - the volume of rows processed in your syncs, useful for anomaly detection
* **census.syncs.records\_sent** - the volume of records synced to your destinations, also useful for anomaly detection
* **census.syncs.sync\_duration\_from\_scheduled\_start\_time** - the time in seconds it took for a sync to complete once it was expected to begin, including time spent waiting in our job queue
* **census.syncs.sync\_duration\_from\_actual\_start\_time** - the time in seconds it took for a sync to complete once it was picked up from the job queue

### Events

* **census.syncs.triggered** - this event signals that the sync run has been queued&#x20;
* **census.syncs.started** - this event signals that active work on the sync run has started
* **census.syncs.completed** - this event signifies that the sync run has completed, and is fired for _both_ successful and failed sync runs.
  * Successful syncs will have `status: ok`
  * Failed syncs will have `status: emergency`
* **census.syncs.success** - this event is fired on a successfully completed sync run
* **census.syncs.failed** - this event is fired on a failed sync run

### Tags

These will be present for both metrics & events:

* **sync\_run\_id** - your sync run's ID
* **workspace\_id** - your workspace's immutable ID associated with the metric / event
* **workspace\_name** - your workspace's name associated with the metric / event
* **sync\_id** - your sync's immutable ID, also searchable in the [Management API](../developers/api.md) and [Sync Logs ](warehouse-writeback.md)
* **sync\_behavior** - how the sync is updating your destination's records (e.g. upsert, update, mirror)
* **destination\_type** - the destination you're updating with a sync (e.g. Salesforce, Google Sheets, ...)
* **destination\_id** - the ID of the destination connection
* **destination\_object** - the object you're updating within the destination (e.g. Account, User, ...)
* **destination\_object\_id** - the id of the object you're updating within the destination
* **is\_full\_sync** - a boolean flag to indicate whether or not this sync is expected to be a full sync because either a user requested it or the sync is backfilling a newly added column

For the **census.syncs.sync\_completed** metric only:

* **status** - whether the sync was a success or failure

For the **census.syncs.rows\_processed** metric only:

* **type** - containing the following potential values
  * _changed_ - new or updated records that Census will try to sync
  * _deleted_ - the number of removed records that Census will try to delete if the sync behavior is "mirror"
  * _invalid_ - the number of records with a duplicate or NULL identifier in the sync

For the **census.syncs.records\_sent** metric only:

* **destination\_response** - containing the following potential values
  * _accepted_ - the number of records the destination successfully accepted in the sync
  * _rejected_ - the number of records the destination rejected in the sync

---
description: >-
  Census syncs implement a consistent and sophisticated retry strategy to ensure
  the highest possible success rate when sending records by default.
---

# Retry Handling

Whenever a sync runs, Census automatically retries any records that are rejected by the destination. The retries happen in two ways:

* **Within the current Sync run:** When a sync is in progress, any rejected records will automatically be retried following an exponential backoff strategy. This method is in place to give transient issues time to resolve themselves before the next attempt. If Census' integration to the destination uses batch endpoints, the retries will automatically utilize our [split batch upload](retry-handling.md#split-batch-uploads) methodology. [Live Syncs](/broken/pages/ugOnqnOVRo4jQQiOSJkR) also retry failed records with an exponential backoff.
* **On subsequent Sync runs:** Any record that still has not been accepted by the destination after a sync run completes will be retried on the next sync run until it succeeds.&#x20;

## Rejected Records

If specific records are sent over, but rejected by the destination, Census will denote these records as rejected. This is noted in [Observability](sync-monitoring/) to show examples of how it appears.

Some examples of rejected reasons from destination APIs:

* Invalid email domain (e.g. \`nopain,nogain.com\` is not a valid email domain)
* Reference record not found with \`id\` = XXXX (when doing a lookup relationship)
* Value too long (45 character string into a 40 character field in a destination)

These rejected records will be retried upon re-execution of the sync, so that if the upstream data is fixed, it might be able to succeed. Census will retry rejected records each execution based on the primary key that's specified for that record.

{% hint style="info" %}
Note that in Salesforce, there is the scenario of records locking as a rejected record reason. [Read more here](../destinations/salesforce.md#common-errors), but these records will be retried on the following execution. If the problem persists, you can lower the batch size under the "Advanced" toggle on the sync configuration as well.
{% endhint %}



## Rate Limits

Census will respect rate limits where they exist on destination services. Depending on the destination, you might notice 429 errors in the [Census API Inspector](sync-monitoring/#api-inspector), which tracks Census requests to the destination service throughout the process of a sync running. If there is a `Retry-After` header in a rate limit response from a destination type, then Census will respect that parameter, waiting to sync the next batch until this time elapses.

If a batch fails during sync execution, Census will retry that batch based on exponential backoff, although there are certain services that have specific rate limits built-in to make sure that data is able to be sent to the services at the proper cadence.

## Split Batch Uploads

Some destinations count all records in a batch request as rejected if the request contains a single invalid record. Since we don't know which record has been rejected, before retrying, Census will automatically split the batch in half and retry each half independently. If a batch is rejected again, it'll be split again and so on and so forth. The process is repeated until the destination has marked each record in the batch as successful or rejected.

The split batch upload strategy allows you to determine exactly which records are being rejected while ensuring as many records are accepted by a destination as possible.

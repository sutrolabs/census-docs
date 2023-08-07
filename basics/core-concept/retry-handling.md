---
description: >-
  Census is a resilient system that has always had best practices implemented
  for uploading data and interacting with API Endpoints.
---

# Retry Handling

## Batch-based

Where possible and performant, Census will leverage batch/bulk endpoints to upload data in subsets rather than row by row.

If a batch fails during sync execution, Census will retry that batch (and will not re-sync previously successful batch uploads).

Doing so enables performant syncs, to enable the Census system to scale to any of your data needs. In almost all cases, Census will utilize the maximum batch size possible for a supported destination.

{% hint style="info" %}
In certain destinations, like Salesforce, the batch size can be set at the sync level under the "Advanced" toggle on the configuration.
{% endhint %}

## Rate Limits

Census will respect rate limits where they exist on destination services. Depending on the destination, you might notice 429 errors in the [Census API Inspector](../sync-monitoring/#api-inspector), which tracks Census requests to the destination service throughout the process of a sync running. If there is a `Retry-After` header in a rate limit response from a destination type, then Census will respect that parameter, waiting to sync the next batch until this time elapses.

If a batch fails during sync execution, Census will retry that batch based on exponential backoff, although there are certain services that have specific rate limits built-in to make sure that data is able to be sent to the services at the proper cadence.

## Rejected Records

If specific records are sent over, but rejected by the destination, Census will denote these records as rejected. This is noted in [Observability](../sync-monitoring/) to show examples of how it appears.

Some examples of rejected reasons from destination APIs:

* Invalid email domain (e.g. \`nopain,nogain.com\` is not a valid email domain)
* Reference record not found with \`id\` = XXXX (when doing a lookup relationship)
* Value too long (45 character string into a 40 character field in a destination)

These rejected records will be retried upon re-execution of the sync, so that if the upstream data is fixed, it might be able to succeed. Census will retry rejected records each execution based on the primary key that's specified for that record.

{% hint style="info" %}
Note that in Salesforce, there is the scenario of records locking as a rejected record reason. [Read more here](../../destinations/salesforce.md#common-errors), but these records will be retried on the following execution. If the problem persists, you can lower the batch size under the "Advanced" toggle on the sync configuration as well.
{% endhint %}

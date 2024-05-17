---
description: >-
  This is a page for answering some patterns of questions that we have seen.
  Hopefully this can make your Census UX smoother.
---

# FAQ & Gotchas

We try to provide a list for different categories of issues that we have seen customers run into. Please let us know if there are some other categories that you are curious about.

## Destination fields not showing up

> My field isn't showing up as a primary identifier on the service, or as a Lookup by option

Many services need these fields to be marked as an external id in the application. For example, [Salesforce](https://docs.getcensus.com/destinations/salesforce#creating-new-external-identifier-fields) needs this to be the case. You will likely need to have object/property configuration permissions to properly fix this in the destination service.

> Why isn't the `ID` of an Object, in Salesforce, Pipedrive, Hubspot, etc. as an option for a primary identifier?

These `ID`'s are reserved fields that we cannot use as a primary identifier, as they are protected by the destination service. We can however use it as a primary identifier for an Update Only Sync.

> I'm sure this field is in the destination service and is properly set. Why isn't it showing up?

When setting up a sync for the first time, clicking on the Refresh Fields will check to see what fields Census is able to see as a primary identifier or as properties on the destination object.

![Try clicking these buttons to pull available fields from the service and source](<../.gitbook/assets/Refresh Fields.png>)

## Census permissions on dbt schemas/tables

> Why does Census not have permissions to my dbt schema/table. I know I ran the SQL permissions script properly...

We sometimes see permissions being overwritten when running dbt, which rebuilds the table (and sometimes the schema) in the data warehouse. A great way to make sure this does not happen is via [dbt post-hooks](https://docs.getdbt.com/reference/resource-configs/pre-hook-post-hook). Here is some example code that might go in the post hook:

`grant select on {{ this }} to user census`

Or for Snowflake :snowflake:

`GRANT SELECT {{ this }} TO ROLE CENSUS_ROLE`

## `400` or `500` errors on a sync

In general, Census should take care of these as much as possible so feel free to reach out to support at any point.

> I'm seeing a `4XX` error message on a sync. What should I do?

Check to see if any primary identifiers or string/varchar fields don't have any values that might spook a destination service. Examples that we have seen are: `..` in an email field or an XSS-payload in a name field.

> I'm seeing a `5XX` error message on a sync. What should I do?

This is due to a server error, generally on the destination service. Check the error message and see if it provides guidance on what happened.

## Alerting

> My sync has had multiple failures, why did I only get one error message?

We optimize for signal with our alerting on sync failures or passing the threshold, assuming that the user will immediately respond and fix the error. Thus, we only send an error alert on failed records the first time it happens, and then another message once the sync recovers. The same logic is applied to when the connection (to either the source or destination) fails.

## Destination Fields for billing

> What are destination fields?

Destination fields are the total number of fields in downstream SaaS destinations (e.g., Intercom) which Census syncs data into for a workspace. These are measured across all syncs, not individual syncs.

For example, let’s say you have a Salesforce contacts sync and a Hubspot contacts sync. For 10 fields you could sync 1 field to Salesforce and nine to Hubspot, or five to each, or anything in between. If you sync the same five fields to both Hubspot and Salesforce, that would total to 10 fields because it’s relative to the downstream destination.

In the Census UI, destination fields can be found within a sync as the mapped fields and identifiers.

> How are destination fields measured?

Each month a workspace can sync up to the number of destination fields specified by the plan. This includes destination fields updated by Census via scheduled, triggered and/or manual syncs.

Destination fields are unique per destination, so a field (e.g., active\_users\_last\_30d) synced into two different destinations will be counted twice towards the monthly allocation, however if two different syncs send data to that same field within one destination, it will only count once.

## 💡 Ideas About Other Gotchas?

We are constantly building out this page :construction:

Please [contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat to let us know what questions we can help with, or something you found out through using Census.

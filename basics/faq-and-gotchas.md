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

## `400` or `500` errors on a sync

In general, Census should take care of these as much as possible so feel free to reach out to support at any point.

> I'm seeing a `4XX` error message on a sync. What should I do?

Check to see if any primary identifiers or string/varchar fields don't have any values that might spook a destination service. Examples that we have seen are: `..` in an email field or an XSS-payload in a name field.

> I'm seeing a `5XX` error message on a sync. What should I do?

This is due to a server error, generally on the destination service. Check the error message and see if it provides guidance on what happened.

## Alerting

> My sync has had multiple failures, why did I only get one error message?

We optimize for signal with our alerting on sync failures or passing the threshold, assuming that the user will immediately respond and fix the error. Thus, we only send an error alert on failed records the first time it happens, and then another message once the sync recovers. The same logic is applied to when the connection (to either the source or destination) fails.

## 💡 Ideas About Other Gotchas?

We are constantly building out this page :construction:

Please [contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat to let us know what questions we can help with, or something you found out through using Census.

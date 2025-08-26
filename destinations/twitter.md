---
description: This page describes how to use Census with X Ads.
---

# X Ads (formerly Twitter Ads)

## Getting started

This guide shows you how to use Census to connect your X Ads account to your data warehouse and create your first sync.

### **Prerequisites**

Before you begin, you'll need the following:

* Census account: If you don't have this already, [start with a free trial](https://app.getcensus.com/).
* X Ads account
* Credentials for your data warehouse: For details, see the guide for your [specific data source technology](twitter.md#step-2-connect-your-data-warehouse).

{% hint style="info" %}
To sync audiences, X requires a manual approval step. Details can be found in [X docs](https://developer.twitter.com/en/docs/twitter-ads-api/audiences/guides/audience-api-integration).

> For access to the Audience endpoint, you will need to be added to an allowlist. Please fill this form and accept the new [Twitter Ads Products and Services Agreement](https://developer.twitter.com/content/developer-twitter/en/docs/ads/general/overview/adsapi-application) if initially accepted prior to 2018-08-01.
{% endhint %}

### Connect X Ads Account

1. Log into Census and navigate to [Destinations](https://app.getcensus.com/destinations).
2. Click **New Destination**.
3. Select **X Ads** from the menu.
4. Follow the X Ads authentication flow.

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

|         **Object Name** | **Supported?** | **Sync Keys**                                                                     | **Behaviors** |
| ----------------------: | :------------: | --------------------------------------------------------------------------------- | ------------- |
|                Audience |        ✅       | Hashed or Unhashed Email, Hashed or Unhashed Handle, Hashed or Unhashed Device ID | Mirror        |
| Mobile Conversion Event |        ✅       | App ID, Conversion Time, Conversion Type, Hashed Device ID, OS Type               | Send          |
|    Web Conversion Event |        ✅       | Click ID, Hashed or Unhashed Email, Hashed or Unhashed Phone Number               | Send          |

Contact our support team if you want Census to support more X Ads objects and/or behaviors.

### Audiences&#x20;

X Ads does not allow reuse of audience names that have been deleted, described in their [documentation here](https://devcommunity.x.com/t/duplicate-audience-name-validation/171958). If you attempt to reuse an audience name that has been used in the past, the Census sync will fail with a `BadRequestError: the server responded with status 400` error. Looking at the API Inspector, you will see that Census is failing to create a new audience with X returning an error saying `Entity already exists CustomAudience`.&#x20;

To proceed, you will need to rename the audience you're trying to create to use a name that has not been previously used.

### Conversion Events&#x20;

When syncing data to conversion events, the **Use timestamp column to identify new data** setting can help limit the number of API calls. With this setting, Census will check if the record has changed since the last sync occurred and skip syncing for the record if there have been no changes.

To use this setting, you'll also need to include a column in your database/data source that tracks the latest sync for each record.

### Sync speed & limits

Rate limits affect how many records you can sync in a specific period of time. X Ads API has a rate limit of 1,500 calls per minute. Calls to sync audience data and conversion event data share the same rate limit.



## Need help connecting to X Ads?

You can contact our support team or start a conversation from the in-app chat.

---
description: This page describes how to use Census with The Trade Desk.
---

# The Trade Desk

In this guide, we will show you how to connect The Trade Desk to Census.

## 🏃‍♀️ Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **The Trade Desk** from the menu.
3. The Trade Desk needs a few different types of credentials depending on which of the destination objects you intend to use. You can optionally decide which credentials to provide:

- For Ad Groups and/or Campaigns, provide the **API Token**. See [The Trade Desk's documentation](https://api.thetradedesk.com/v3/portal/api/doc/Authentication) for more information on how to generate an API Token. We recommend you generate the long-lived token, and keep in mind that you will need to regenerate one whenver it expires.
- For Conversion Events, provide a **Postback URL**.
- For CRM Data Segments, provide the following:
  - **API Token** (as described above)
  - **Advertiser ID**
  - **Data Region** - One of: `US`, `EU`, or `APAC`. Census will create new CRM Data Segments in the region you specify here. You can create multiple The Trade Desk destinations in Census to sync to multiple regions.


<figure><img src="../.gitbook/assets/tradedesk.png" alt=""><figcaption><p>Generate an API Token from the The Trade Desk developer portal.</p></figcaption></figure>

## 🔀 Supported Objects and Behaviors

|          **Object Name** | **Supported?** | **Sync Keys**         | **Behaviors**       |
| -----------------------: | :------------: | --------------------- | ------------------- |
|                 Ad Group |        ✅      | Any unique identifier | Update Only, Append |
|               Advertiser |        ✅      | Any unique identifier | Update Only, Append |
|                 Campaign |        ✅      | Any unique identifier | Update Only, Append |
|         Conversion Event |        ✅      | Any unique identifier | Append              |
|             Tracking Tag |        ✅      | Any unique identifier | Update Only, Append |
|         CRM Data Segment |        ✅      | Email/Phone           | Mirror              |

[Contact us](mailto:support@getcensus.com) if you want Census to support more The Trade Desk objects and/or behaviors.

### CRM Data Segment PII Normalization

Census will automatically normalize email and phone identifiers to the format expected by The Trade Desk. You can optionally provide Census with a pre-hashed email or phone number. If you do, you must ensure that the data is normalized to the format expected by The Trade Desk. Census cannot determine whether a pre-hashed email or phone number is correctly normalized once it is hashed.

For more details on how The Trade Desk expects email and phone numbers to be normalized, see [The Trade Desk's documentation](https://api.thetradedesk.com/v3/portal/data/doc/DataPiiNormalization).

## 🚑 Need help connecting to The Trade Desk?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

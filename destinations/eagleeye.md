---
description: This page describes how to use Census with Eagle Eye.
---

# Eagle Eye

Eagle Eye is a digital marketing platform that provides a variety of services including loyalty programs, gift cards, and promotions, primarily for the retail industry.

## 🏃‍♀️ Getting Started

1. Communicating with Eagle Eye requires a Client ID and Secret Key, both of which are provided by your Eagle Eye account manager so reaching out to them is your first step. Once you've received both, you can proceed to the next step.
2. In Census, navigate to the Destinations page and click **Add Destination**. Select **Eagle Eye** from the list of destinations. Provide your Client ID and Secret Key. Finally, indicate whether you're connecting to a Sandbox or Production instance of Eagle Eye. **Save** to finish setting up your connection.

You should now be ready to start syncing data to Eagle Eye!

## 🗄 Supported Objects and Behaviors

| **Object Name** | **Supported?** | **Sync Keys**  | **Behaviors** |
| --------------: | :------------: | :------------: |:-------------:|
| Coupon <br> <a href="/basics/core-concept/audience-syncs">Audience Sync</a>        |        ✅      |   Any unique identifier   |      Add      |

### Coupons

Coupons are an [Audience Sync](../basics/core-concept/audience-syncs.md), associating a unique customer (indicated by a Wallet ID) to a Campaign. The Campaign can be selected from a list of existing Campaigns or a Campaign ID can be provided. In addition to the Wallet ID and Campaign ID, Census also needs any unique identifier for a coupon. This isn't required by Eagle Eye but is required by Census to ensure that the same coupon isn't added multiple times. This also allows you to use the same coupon/campaigns multiple times for a single Wallet.

The Coupon object also supports a number of additional optional fields. For more information, see the [Eagle Eye documentation](https://developer.eagleeye.com/reference/createwalletcampaignaccount) (which may require separate user credentials from Eagle Eye).

## 🚑 Need help connecting to Eagle Eye?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

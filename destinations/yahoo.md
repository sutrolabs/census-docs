---
description: This page describes how to use Census with Yahoo Ads.
---

# Yahoo Ads (DSP)

Yahoo Ads is a demand-side platform (DSP) that allows you to programmatically buy and manage your display, video, native, and search ads. Census can sync your audience data to Yahoo Ads for targeting.

## 🏃‍♀️ Getting Started

Before you start, you'll first need to ensure you have Yahoo's DSP API enabled for your account. This must be done by a Yahoo Account Manager or Product Support. See [Yahoo's documentation](https://developer.yahooinc.com/dsp/api/docs/authentication/vmdn-auth-overview.html) for more information.

With the API enabled, you can now connect Census to Yahoo Ads. You'll need three details:

1. Your **Client ID** and **Client Secret** - This is available by clicking on your name in the top right, and selecting **My Account**. You may need to agree to the terms of service to view your Client ID and Client Secret. [Yahoo's documentation](https://developer.yahooinc.com/dsp/api/docs/authentication/vmdn-auth-overview.html#get-your-id) has more details on the steps.
2. Your **Advertiser ID** (or Account ID) - This is available in the URL when you're viewing an advertiser in the Yahoo Ads UI. For example, if the URL is `https://dsp.admanagerplus.yahoo.com/advertiser/12345`, then the Advertiser ID is `12345`.

With these details in hand, you can now connect Census to Yahoo Ads:
1. Back within Census, go to the [Destinations](https://app.getcensus.com/destinations) page in Census and click **New Destination**.
2. Select **Yahoo Ads** from the menu.
3. Enter the values that you copied from Yahoo Ads and click **Save**.

You should now be ready to sync your data to Yahoo Ads.

## 🗄 Supported Objects and Behaviors

|  **Object Name** | **Supported?** |  **Sync Keys** |  **Behavior**  |
| ---------------: | :------------: | :------------: | :------------: |
|   Audience <br> [Audience Sync](https://docs.getcensus.com/basics/core-concept/audience-syncs)|        ✅       | External ID (recommended), Email | Upsert |

[Let us know](mailto:support@getcensus.com) if you want Census to support additional objects for Yahoo Ads.

### Yahoo Ads Audiences

Census uses the [Email Address Audience](https://developer.yahooinc.com/dsp/api/docs/traffic/audience/email-address-audience.html) type to populate Yahoo Ads audiences with email addresses. You can let Census hash email addresses for you, or provide them pre-hashed. Yahoo's API does not specify how they should be normalized, so Census will send them as-is. We recommend apply common normalization practices to your emails before sending them to Yahoo such as removing leading and trailing whitespace, and lowercasing all characters.

## 🚑 Need help connecting to Yahoo Ads?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

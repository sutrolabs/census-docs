---
description: This page describes how to use Census with Reddit Ads.
---

# Reddit Ads

## 🏃‍♀️ Getting Started

1. Click **Add Service**.
2. Select **Reddit Ads** from the menu.
3. Proceed through the OAuth flow to connect your Reddit Ads account to Census.

<figure><img src="../.gitbook/assets/reddit-ads.png" alt=""><figcaption><p>Connect your Reddit Ads account to Census.</p></figcaption></figure>

## 🔀 Supported Objects and Behaviors

| **Object Name** | **Supported?** | **Identifiers**  | **Behaviors** |
| --------------: | :------------: | ---------------- | --------------|
| Conversion Event | ✅ | Any unique ID | Append |

### Field details

* `event_at`: The RFC3339 timestamp when the conversion event occurred
* `tracking_type`: Must be one of the following according to [Reddit's API documentation](https://ads-api.reddit.com/docs/#tag/Conversions/paths/~1api~1v2.0~1conversions~1events~1{account_id}/post): `PageVisit`, `ViewContent`, `Search`, `AddToCart`, `AddToWishlist`, `Purchase`, `Lead`, `SignUp`, `Custom`

[Contact us](mailto:support@getcensus.com) if you want Census to support more Reddit Ads objects and/or behaviors.

## 🚑 Need help connecting to Reddit Ads?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

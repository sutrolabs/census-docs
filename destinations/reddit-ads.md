---
description: This page describes how to use Census with Reddit Ads.
---

# Reddit Ads

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Reddit Ads** from the menu.
3. Proceed through the OAuth flow to connect your Reddit Ads account to Census.

<figure><img src="../.gitbook/assets/reddit-ads.png" alt=""><figcaption><p>Connect your Reddit Ads account to Census.</p></figcaption></figure>

## Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|  **Object Name** | **Supported?** | **Sync Keys** | **Behaviors** |
| ---------------: | :------------: | ------------- | ------------- |
| Conversion Event |        ✅       | Any unique ID | Send          |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Reddit Ads objects and/or behaviors.

### Field details

* `event_at`: The RFC3339 timestamp when the conversion event occurred
* `tracking_type`: Must be one of the following according to [Reddit's API documentation](https://ads-api.reddit.com/docs/#tag/Conversions/paths/\~1api\~1v2.0\~1conversions\~1events\~1{account\_id}/post): `PageVisit`, `ViewContent`, `Search`, `AddToCart`, `AddToWishlist`, `Purchase`, `Lead`, `SignUp`, `Custom`

## Need help connecting to Reddit Ads?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

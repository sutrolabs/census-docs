---
description: This page describes how to use Census with Google Campaign Manager 360.
---

# Google Campaign Manager 360

Google Campaign Manager 360 is a demand-side platform that allows advertisers to manage their digital campaigns across multiple channels.

## 🏃‍♀️ Getting Started

Census uses OAuth to connect to Google Campaign Manager 360. Before you start this flow, please make sure the user and accounts have the correct permissions:

* Your user will need access to the advertiser account you want to connect to
* The Campaign Manager 360 account is enabled for API Access
* Your User Profile permissions also have access to the API. For more information, see Google's [documentation](https://developers.google.com/doubleclick-advertisers/getting\_started).

Once you've confirmed permissions, follow these steps to connect Census to Google Campaign Manager 360:

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Google Campaign Manager 360** from the menu.
3. Complete the OAuth flow to grant Census access. Note that you'll need to create a separate Census connection for each advertiser you wish to send data to.

## 🔀 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

|                                                                                                                     **Object Name** | **Supported?** |  **Sync Keys**  | **Behaviors** |
| ----------------------------------------------------------------------------------------------------------------------------------: | :------------: | :-------------: | :-----------: |
| <p>Conversions<br><a href="../basics/data-models-and-entities/defining-source-data/events/#defining-event-syncs">Event Sync</a></p> |        ✅       | Unique Event ID |      Send     |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](broken-reference) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Google Campaign Manager objects and/or behaviors.

### Conversion Identifiers

Each conversion record will need three things:

* A unique identifier that Census can use to identify new conversion events
* Conversion activity identifers
* Exactly one attribution identifier.

All conversions must be matched to existing activities by specifying the **floodlightActvityId** and **floodlightConfigurationId** values ([Google documentation](https://developers.google.com/doubleclick-advertisers/guides/conversions\_overview#match\_conversions\_to\_activities)). These will appear as required mappings.

Offline conversions must also be attributed to a specific user through one of the [supported methods](https://developers.google.com/doubleclick-advertisers/guides/conversions\_overview#match\_conversions\_to\_activities), so you must add a mapping to exactly one of the following fields:

* Encrypted User ID
* Encrypted User ID Candidates
* Mobile Device ID
* Google Click ID
* Match ID
* Display Click ID

When using the Encrypted User ID, Encrypted User ID Candidates, you must specify Encryption Information in the sync's advanced configuration. See [Google's documentation](https://developers.google.com/doubleclick-advertisers/guides/conversions\_upload#specify\_encryption\_info) for more information.

### Digital Markets Act (DMA)

For syncing audiences to Google Campaign Manager 360, you can include consent information to ensure compatibility with [Google's EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/). Google Campaign Manager 360 now supports an additional field `Consent for ad user data`, which can be set to one of the following values: `GRANTED`, `DENIED`. See Google's [documentation](https://developers.google.com/doubleclick-advertisers/rest/v4/Conversion#FIELDS.ad\_user\_data\_consent) for more information.

## 🚑 Need help connecting to Google Campaign Manager 360?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

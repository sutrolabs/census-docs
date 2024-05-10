---
description: This page describes how to use Census with Google Campaign Manager 360.
---

# Google Campaign Manager 360

Google Campaign Manager 360 is a demand-side platform that allows advertisers to manage their digital campaigns across multiple channels.

## 🏃‍♀️ Getting Started

Census uses OAuth to connect to Google Campaign Manager 360. Before you start this flow, please make sure the user and accounts have the correct permissions:
- Your user will need access to the advertiser account you want to connect to
- The Campaign Manager 360 account is enabled for API Access
- Your User Profile permissions also have access to the API.
For more information, see Google's [documentation](https://developers.google.com/doubleclick-advertisers/getting_started).

Once you've confirmed permissions, follow these steps to connect Census to Google Campaign Manager 360:
1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Google Campaign Manager 360** from the menu.
3. Complete the OAuth flow to grant Census access. Note that you'll need to create a separate Census connection for each advertiser you wish to send data to.

## 🔀 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

| **Object Name** | **Supported?** | **Sync Keys**  | **Behaviors** |
| --------------: | :------------: | :------------: |:-------------:|
| Conversions <br> [Event Sync](/basics/data-models-and-entities/defining-source-data/events#defining-event-syncs)         |        ✅      | Unique Event ID |     Send      |

{% hint style="info" %}
Learn more about our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Google Campaign Manager objects and/or behaviors.

### Conversion Identifiers

Each conversion record will need three things:
- A unique identifier that Census can use to identify new conversion events
- Conversion activity identifers
- Exactly one attribution identifier.

All conversions must be matched to existing activities by specifying the **floodlightActvityId** and **floodlightConfigurationId** values ([Google documentation](https://developers.google.com/doubleclick-advertisers/guides/conversions_overview#match_conversions_to_activities)). These will appear as required mappings.

Offline conversions must also be attributed to a specific user through one of the [supported methods](https://developers.google.com/doubleclick-advertisers/guides/conversions_overview#match_conversions_to_activities), so you must add a mapping to exactly one of the following fields:
- Encrypted User ID
- Encrypted User ID Candidates
- Mobile Device ID
- Google Click ID
- Match ID
- Display Click ID

When using the Encrypted User ID, Encrypted User ID Candidates, you must specify Encryption Information in the sync's advanced configuration. See [Google's documentation](https://developers.google.com/doubleclick-advertisers/guides/conversions_upload#specify_encryption_info) for more information.


## 🚑 Need help connecting to Google Campaign Manager 360?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

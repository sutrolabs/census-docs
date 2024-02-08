---
description: This page describes how to use Census with Kevel.
---

# Kevel

Kevel is an API platform that helps you quickly build custom ad platforms for sponsored listings, internal promotions, native ads, and more.

## 🏃‍♀️ Getting Started

1. Authenticating Kevel is straightforard. Within Kevel's top bar menu, navigate to **Settings > API Keys**. Click the **New API Key** button and give your key a name. Copy the newly created API Key.

2. You'lll also need a Network ID. You can find this in the top bar menu by clicking on the ℹ️ icon in the top right. Copy the Network ID.

3. Back in Census, navigate to the Destinations page and click **Add Destination**. Select Kevel from the list of destinations. Provide your API Key, Network ID, and click **Save**.

You should now be ready to start creating audiences in Kevel!

## 🗄 Supported Objects and Behaviors

| **Object Name** | **Supported?** | **Sync Keys**  | **Behaviors**  |
| --------------: | :------------: | :------------: | :------------: |
| Interests <br> [Audience Sync](https://docs.getcensus.com/basics/core-concept/audience-syncs)|        ✅      | User Key | Mirror |

[Contact us](mailto:support@getcensus.com) if you want Census to support more objects for Kevel.

### Understanding Kevel Interests/Flight Categories

You can think of Kevel interests as "tags" on users within UserDB indicating the types of campaigns that should be targeted at them. Kevel also calls them Flight Categories. Currently, you must first create an Interest/Flight Category in Kevel before you can sync users to it via Census. You can do this by navigating to **Campaigns > Flights** in the top bar menu. Then add categories under the **Behavioral Targeting** section.

Campaigns then can be targeted at users with specific interests via Kevel's Zerkel queries. For more information, see [Kevel's documentation](https://dev.kevel.com/docs/interest-targeting#how-to-target-an-interest-segment).

## 🚑 Need help connecting to Kevel?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

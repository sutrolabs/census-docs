---
description: This page describes how to use Census with Insider.
---

# Insider

Insider is a customer data platform that helps marketers connect customer data across channels and systems, predict their future behavior with an AI-powered engine, and orchestrate and deliver individualized experiences to customers.

## 🏃‍♀️ Getting Started

1. You'll first need to create an API key in Insider. To do this, visit Insider. Navigate to your username (top right) > Settings > InOne Settings > Integration Settings. Census will need an API Key that provides access to the Unified Customer Database. For more information on setting up API Keys in Insider, [see their documentation](https://academy.useinsider.com/docs/api-authentication-tokens).
2. Back in Census, navigate to the Destinations page and click **Add Destination**. Select Insider from the list of destinations. Provide your API Key and click **Save**.

You should now be ready to start creating audiences in Insider!

## 🗄 Supported Objects and Behaviors

| **Object Name** | **Supported?** | **Sync Keys**  | **Behaviors**  |
| --------------: | :------------: | :------------: | :------------: |
| Users           |        ✅      | Email, Phone Number, UUID | Update or Create, Update Only |
| Events <br> [Event Sync](/basics/data-models-and-entities/defining-source-data/events#defining-event-syncs)         |        ✅      | Unique Event ID | Append         |

### Connector Quirks

- Insider has a unique approach to handling clearing values in their API. Census takes care of most of this automatically, with one exception: If you are attempting to write `NULL` values to identifiers, Census will not be able to clear the value in Insider.

## 🚑 Need help connecting to Insider?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

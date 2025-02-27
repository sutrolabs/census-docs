---
description: This page describes how to use Census with LiveIntent.
---

# LiveIntent

LiveIntent is a people-based marketing platform that reaches millions of logged-in people through the LiveIntent Identity Graph. You can use Census to connect your first party data to LiveIntent to create custom audiences and target them.

## Getting Started

1. You'll first need to contact your account team at LiveIntent to get three pieces of information:
  - Access Token
  - Account ID
  - Data Provider ID
2. Click **Add Service** and select **LiveIntent** from the menu.
3. Enter the three pieces of information you received from your account team at LiveIntent.

You should now be ready to start creating audiences in LiveIntent!

## Supported Objects and Behaviors

| **Object Name** | **Supported?** | **Behaviors**  |
| --------------: | :------------: | :------------: |
| Custom Audience<br> [Audience Sync](https://docs.getcensus.com/basics/core-concept/audience-syncs) |        ✅      | Update or Create, Mirror |

{% hint style="info" %}
Unlike most Census destinations, LiveIntent does not provide an indication of which records were rejected. If you're not seeing data in LiveIntent, you may need to reach out to your LiveIntent account team to troubleshoot.
{% endhint %}

### Normalization

LiveIntent supports identifying users with three different identifiers: Email, AAID and IDFA, the two mobile device identifiers for Android and Apple respective. Audiences can be created with any combination of these identifiers.

When sending emails, LiveIntent supports receiving emails in one of the following formats:
- Raw email address - sent to LiveIntent as is
- MD5 hash (32 characters)
- SHA-1 hash (40 characters)
- SHA-256 hash (64 characters)

If you are sending emails to LiveIntent in a hashed format, ensure your emails only contain lowercase letters and numbers. If you are sending emails in a raw format, ensure your emails are all lowercase.

## Need help connecting to LiveIntent?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

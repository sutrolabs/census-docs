---
description: This page describes how to use Census with Mailgun.
---

# Mailgun

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**, and select **Mailgun** from the menu.
2. Census needs two pieces of information to communicate with Mailgun
   1. **API Key** - Under **Account Settings** > **API Keys**, select **Add new key**. In the description, mention Census. The new key should only need the **Developer** permission.
   2. **Mailgun Domain** - Found under the **Send** left hand navigation section, go to **Sending** > **Domains**.
3. Enter the provided credentials.

## Supported Objects and Behaviors

|                                                                      **Object Name** | **Sync Keys** | **Behaviors**    |
| -----------------------------------------------------------------------------------: | ------------- | ---------------- |
| <p>Mailing List Member<br><a href="../syncs/audience-syncs.md">Audience Sync</a></p> | Email Address | Update or Create |
|       <p>Message<br><a href="../syncs/structuring-data/events.md">Event Sync</a></p> | Email Address | Send             |

[Contact us](mailto:support@getcensus.com) if you want Census to support more Mailgun objects and/or behaviors.

#### Mailing Lists

Mailgun [Mailing Lists](https://documentation.mailgun.com/docs/mailgun/user-manual/sending-messages/mailing-lists) allow sending mail to groups of members. They're similar to Google Groups-style email list, rather than a typical marketing list though they can be used that way.&#x20;

Syncing to Mailing Lists allows you to add or update membership of that list. Census supports syncing to existing mailing lists as well as creating new mailing lists. Any mailing list created by&#x20;

**Messages**

Census sync can send messages directly via Census as well. For simple messages, you can populate the `Text` and `HTML` fields with data from the source dataset or using Constant Values. For more advanced messages, create a [template in Mailgun](https://help.mailgun.com/hc/en-us/articles/360021380793-Email-Templates) first and then provide its name as part of the sync definition.&#x20;

You can send messages to a mailing list by sending a message to the list's email address which is visible in the Mailgun UI.

## Need help connecting to Mailgun?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

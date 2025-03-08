---
description: This page describes how to use Census with Criteo.
---

# Criteo

Criteo provides a platform for digital marketing and advertising. With Census, you can sync data from your data warehouse to Criteo to create targeted marketing campaigns.

## Getting Started

The first step is connecting Census to your Criteo account.

{% hint style="warning" %}
Criteo can only be authorized once to any Census instance. In order to create a second connection, you'll need to deauthorize Census first inside the Criteo UI.\
\
This can be done by a Criteo Admin from the page consent.criteo.com
{% endhint %}

1. Log into Census and navigate to [Destinations](https://app.getcensus.com/destinations).
2. Click **New Destination**.
3. Select **Criteo** from the menu
4. Follow the Criteo OAuth authentication flow, which will ask you to log in with your Criteo username and password.
5. Once logged in, select the Portfolio's you want Census to have access to and Approve
6. Finally once back in Census you'll select the Audience

Once complete, you'll see your new connection in the **Destinations** list.

## Supported Objects and Sync Behaviors

|                                                                                                      **Object Name** | **Supported?** | **Sync Keys**                                              |       **Behavior**       |
| -------------------------------------------------------------------------------------------------------------------: | :------------: | ---------------------------------------------------------- | :----------------------: |
| <p>Audience Segment<br><a href="https://docs.getcensus.com/basics/core-concept/audience-syncs">Audience Sync</a></p> |        ✅       | GUM Cookie ID, Mobile Ad ID, Email, LiveRamp Identity Link | Mirror, Update or Create |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../syncs/overview.md) documentation.
{% endhint %}

## Need help connecting to Criteo?

You can send our [support team an email](mailto:support@getcensus.com) at support@getcensus.com or start a conversation from the in-app chat.

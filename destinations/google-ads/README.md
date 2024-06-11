---
description: This page describes how to use Census with Google Ads.
---

# Google Ads

## 🏃‍♀️ Getting Started

Connecting to your Google Ads account is straightforward.

1. From the [Destinations](https://app.getcensus.com/destinations) page, click **New Destination** and select Google Ads from the menu.
2. Complete the OAuth flow. Make sure your are signed into a user account that has permissions to both view all of your accounts, as well as submit data to them (readonly accounts will not work).
3.  Select the Ads account you wish to use with Census. If you'd like to sync to multiple accounts, you will need to add each as its own destination.\\

    <figure><img src="../../.gitbook/assets/Google Ads.png" alt=""><figcaption></figcaption></figure>

## 🗄 Supported Objects and Sync Behaviors <a href="#supported-objects-and-sync-behaviors" id="supported-objects-and-sync-behaviors"></a>

Click the link for more information on each of the services

|                                                                                                 **Object Name** | **Supported?** | **Sync Keys**                                                 | **Behaviors**    |
| --------------------------------------------------------------------------------------------------------------: | :------------: | ------------------------------------------------------------- | ---------------- |
|                                                                                                 Call Conversion |        ✅       | Caller ID                                                     | Update or Create |
|                                                                                                Click Conversion |        ✅       | Google Click ID, Google wBraid, Google gBraid,                | Update or Create |
|                                                                                           Conversion Adjustment |        ✅       | Any unique identifier                                         | Send             |
| [Customer Match Lists (Audiences)](https://docs.getcensus.com/destinations/google-ads/customer-match-audiences) |        ✅       | External ID, MAID, Email, First Name, Last Name, Phone Number | Upsert           |
|                                                                                             Enhanced Conversion |        ✅       | N/A                                                           | Update or Create |

{% hint style="info" %}
Learn more about all of our sync behaviors in our [Syncs](../basics/core-concept#sync-behaviors) documentation.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Google Ads objects and/or behaviors

## 🚑 Need help connecting to Google Ads?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

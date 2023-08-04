---
description: This page describes how to use Census with Google Display & Video 360.
---

# Google Display & Video 360

## 🏃‍♀️ Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Google Display & Video 360** from the menu.
3. Complete the OAuth flow to grant Census access to DV360. Note that you'll need to create a separate Census connection for each advertiser you wish to send data to.

<figure><img src="../.gitbook/assets/google-dv360.png" alt=""><figcaption><p>Complete the OAuth flow to connect to DV360.</p></figcaption></figure>

## Syncing Audiences

DV360 contains a number of different [audience types](https://developers.google.com/display-video/api/reference/rest/v2/firstAndThirdPartyAudiences#audiencetype) but we only support syncing to `CUSTOMER_MATCH_CONTACT_INFO` and `CUSTOMER_MATCH_DEVICE_ID`. Which audience type we sync to depends on the mappings you select in the sync wizard.&#x20;

If you want to sync to an audience of type `CUSTOMER_MATCH_DEVICE_ID` then you should only map to the `appId` and `deviceId` fields.

If you want to sync to an audience of type `CUSTOMER_MATCH_CONTACT_INFO` you can map to any field _except_ `appId` and `deviceId`.&#x20;

{% hint style="warning" %}
You cannot mix audience types in a single sync. If you map to the deviceId field you should not add any customer info fields and vice versa.
{% endhint %}

{% hint style="info" %}
If you are syncing customer info and you map to an address field (First Name, Last Name, Country Code, Zip Code) then you must map _all_ the address fields.
{% endhint %}

## 🔀 Supported Objects and Behaviors

<table data-header-hidden><thead><tr><th width="251" align="right"></th><th width="134" align="center"></th><th width="190"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Identifiers</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Customer Match Audience</td><td align="center">✅</td><td>Any unique identifier</td><td>Update or Create</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more DV360 objects and/or behaviors.

## 🚑 Need help connecting to Google Display & Video 360?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

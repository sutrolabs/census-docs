---
description: This page describes how to use Census with TikTok Ads.
---

# TikTok

## 🏃‍♀️ Getting Started

* Navigate to the **Destinations** page in Census and click **New Destination**.
* Select **TikTok** from the menu.
* Click **Connect** and you will be redirected to sign in to your TikTok for Business account.
* After completing the flow, you'll see your TikTok connection listed on the **Destinations** page.

## 🔀 Supported Objects and Behaviors

<table data-header-hidden><thead><tr><th width="245" align="right"></th><th width="127" align="center"></th><th width="192"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Sync Keys</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Partner Audience</td><td align="center">✅</td><td>Email, IDFA/GAID, Phone</td><td>Update or Create, Mirror</td></tr><tr><td align="right">Customer File Audience</td><td align="center">✅</td><td>Email, IDFA/GAID, Phone</td><td>Update or Create, Mirror</td></tr><tr><td align="right">Offline Event Conversions</td><td align="center">✅</td><td>Any unique identifier</td><td>Append</td></tr><tr><td align="right">Web Event Conversions</td><td align="center">✅</td><td>Any unique identifier</td><td>Append</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more TikTok objects and/or behaviors.

## Understanding TikTok Audiences

TikTok supports two different audience types: Partner Audiences and Customer File Audiences. Though they are similar, there are some important differences to note. When in doubt, we recommend using Partner Audiences.

### Partner Audiences
Partner Audiences are easier to manage with Census as they have no limitations on incremental syncs. The main limitation of Partner Audiences is that they cannot be used in Reach and Frequency campaigns.

### Customer File Audience
Customer File Audience is the older TikTok audience type and can be used with Reach and Frequency campaigns. However, TikTok only allows one **Mirror** operation per 24 hrs (sometimes a bit longer, depends on their processing delays) when using this API. This can present issues. This error will appear as:

```
This replace operation is rejected as there is an existing unfinished replace operation for this audience. Please wait until the current operation completes on this audience before re trying. Recommend no more than one replace operation per day.
```

To work around this limitation, you have a few options:
1. Use a **Partner Audience** instead
2. Move to a less frequent sync schedule (once per 48 hrs)
3. Use the **Update or Create** sync behavior instead of **Mirror**

### Identifiers
TikTok supports the following identifiers across either audience type:

- **Email** - Original value or SHA256 hashed
- **Phone** - Original value or SHA256 hashed
- **IDFA/GAID** - Original value, SHA256 hashed, or MD5 hashed

Prior to hashing, please ensure you are [normalizing your data to TikTok's requirements](https://ads.tiktok.com/gateway/docs/index?identify_key=2b9b4278e47b275f36e7c39a4af4ba067d088e031d5f5fe45d381559ac89ba48&language=ENGLISH&doc_id=1701890972946433#item-link-Before%20you%20begin:~:text=Important%20notes%20for%20passing%20hashed%20values%3A).

#### Important Notes

* All audience identifiers can be provided as either the original value or a hashed value.

## 🚑 Need help connecting to TikTok Ads?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

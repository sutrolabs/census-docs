---
description: This page describes how to use Census with Pinterest.
---

# Pinterest

## 🏃‍♀️ Getting Started

{% hint style="info" %}
Note: You will need admin rights in your organization's Pinterest Business Account to be able to successfully authenticate the connection.
{% endhint %}

1. Click **Add Service**.
2. Select **Pinterest** from the menu.
3. Follow the Pinterest OAuth authentication flow, which will ask you to log in with your Pinterest username and password.

<figure><img src="../.gitbook/assets/Screen Shot 2022-12-01 at 9.04.09 PM.png" alt=""><figcaption><p>Connect Census to Pinterest via OAuth.</p></figcaption></figure>

## 🗄 Supported Objects

| **Object Name** | **Supported?** | **Identifiers**        |
| --------------: | :------------: | ---------------------- |
|   Customer List |        ✅       | Email, IDFA, MAID \*\* |

{% hint style="info" %}
Note: [Pinterest requires](https://developers.pinterest.com/docs/api/v5/#tag/customer\_lists) emails to be lowercase and can be plain text or hashed using SHA1, SHA256, or MD5. MAIDs and IDFAs must be hashed with SHA1, SHA256, or MD5. You have the option to provide plain-text versions of any of these to Census and we will automatically hash the values before passing them along to Pinterest.
{% endhint %}

[Contact us](mailto:support@getcensus.com) if you want Census to support more Pinterest objects.

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about all of our sync behaviors on our [Core Concept page](../basics/core-concept/#the-different-sync-behaviors).
{% endhint %}

|        **Behaviors** | **Supported?** |  **Objects**  |
| -------------------: | :------------: | :-----------: |
| **Update or Create** |        ✅       | Customer List |
|           **Mirror** |        ✅       | Customer List |

## 🚑 Need help connecting to Pinterest?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

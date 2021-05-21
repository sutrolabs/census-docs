---
description: This page describes how to use Census with Mailchimp.
---

# Mailchimp

## 🏃‍♂️ Getting Started

{% embed url="https://youtu.be/tu3hr3BV6Sg" %}

### 1. Connect Census to Mailchimp <a id="1-connect-census-to-braze"></a>

In the **Connections** page in Census, click the **Add Service** button under the **Service Connections** section, and select Mailchimp.

You will be redirected to a page to log in to Mailchimp to authorize your account to Census. Once you enter your credentials and click the **Log In** button, you'll see a page like the image below, confirming you want to authorize Census.

![](../.gitbook/assets/screen-shot-2021-04-13-at-10.08.02-am.png)

Once you've authorized Census, you'll be redirected back to the Connections page in Census and you should see your Mailchimp connection there.

If you want to see your connections in Mailchimp in the future, simply navigate to the **Profile** page, and scroll down to the **Connections and notifications** section.

## 💡 Mailchimp Field Quirks

There are two mandatory fields for the Mailchimp connection: **email** and **status**.

Please note that the mandatory status field only accepts the following values: `"subscribed"`, `"unsubscribed"`, `"cleaned"`, or `"pending"`.

For more details, take a look at Mailchimp's [API documentation](https://mailchimp.com/developer/marketing/api/list-members/update-list-member/).

## 🗄 Supported Objects

| **Object Name** | **Supported?** | Identifiers |
| ---: | :---: | :--- |
| Audience | ✅ | Object ID, any Text/Number  |

## 🔄 Supported Sync Behaviors

{% hint style="info" %}
Learn more about what all of our sync behaviors on our [Core Concept page](../basics/core-concept.md#the-different-sync-behaviors).
{% endhint %}

| **Behaviors** | **Supported?** | **Objects?** |
| ---: | :---: | :---: |
| **Update or Create** | ✅ | All |

## 🚑 Need help connecting to Mailchimp?

Contact us via support@getcensus.com or start a conversion via the [in-app](https://app.getcensus.com) chat.


---
description: This page describes how to use Census with LaunchDarkly.
---

# LaunchDarkly

## 🏃‍♀️ Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **LaunchDarkly** from the menu.
3. Open the LaunchDarkly app in another window to find the following credentials:
   1. **Service Access Token**: create a new token from **Account settings** > **Authorization**. Add a custom role or inline policy that has the action `importEventData` or select the role `Admin` (this is not a best practice), and check the box next to **This is a service token**.
   2. **Client Side ID**: go to **Account settings** > **Projects** and either click on an existing project or create a new one to get this ID.

{% hint style="info" %}
Your access token needs to have permission to perform the action `importEventData`. If your token is an admin token it will work as well but the recommended approach is to use a custom role or policy. [read more](https://docs.launchdarkly.com/home/members/role-create)
{% endhint %}

<figure><img src="../.gitbook/assets/LaunchDarkly (1).png" alt=""><figcaption><p>Create a Service Access Token from the LaunchDarkly app.</p></figcaption></figure>

## 🔀 Supported Objects and Behaviors

<table data-header-hidden><thead><tr><th align="right"></th><th width="169" align="center"></th><th width="159"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Identifiers</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Metric</td><td align="center">✅</td><td>Key</td><td>Update or Create</td></tr><tr><td align="right">Metric Event</td><td align="center">✅</td><td>N/A</td><td>Append</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more LaunchDarkly objects and/or behaviors.

## 🚑 Need help connecting to LaunchDarkly?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

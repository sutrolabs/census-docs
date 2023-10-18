---
description: This page describes how to use Census with LaunchDarkly.
---

# LaunchDarkly

## 🏃‍♀️ Getting Started

1. Click **Add Service**.
2. Select **LaunchDarkly** from the menu.
3. Open the LaunchDarkly app in another window to find the following credentials:
   1. **Service Access Token**: create a new token from **Account settings** > **Authorization**. Select the role `Admin` (not recommended) or add an inline role/custom policy and define granular permissions. You will need to select your desired environment and add the action `importEventData` if you want to sync event data as well as your desired project's metrics and add the `All Actions` action if you want to sync to metrics. Check the box next to **This is a service token**.
   2. **Project Key**: go to **Account settings** > **Projects** and use the **Project Key** as shown in the screenshot below

{% hint style="info" %}
Your access token needs to have permission to perform the action `importEventData`. If your token is an admin token it will work as well but the recommended approach is to use a custom role or policy. [read more](https://docs.launchdarkly.com/home/members/role-create)
{% endhint %}

<figure><img src="../.gitbook/assets/LaunchDarkly (1) (1).png" alt=""><figcaption><p>1 Create a Service Access Token from the LaunchDarkly app.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption><p>2 Find the Project Key </p></figcaption></figure>

## 🔀 Supported Objects and Behaviors

<table data-header-hidden><thead><tr><th align="right"></th><th width="169" align="center"></th><th width="159"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Identifiers</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Metric</td><td align="center">✅</td><td>Key</td><td>Update or Create</td></tr><tr><td align="right">Metric Event</td><td align="center">✅</td><td>N/A</td><td>Append</td></tr><tr><td align="right">Synced Segments</td><td align="center">✅</td><td>User ID</td><td>Mirror</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more LaunchDarkly objects and/or behaviors.

### **Metrics**

Metrics measure audience behaviors affected by the flags in your experiments. You can use metrics to track all kinds of things, from how often customers access a URL to how long that URL takes to load a page, etc

You can use Census to both Create or Update Metric definitions, or also send Metric Events in order to log data points that you've captured separately from your typical LaunchDarkly metric path.

### Synced Segments

Census supports LaunchDarkly's Synced Segments with [audience-syncs.md](../basics/core-concept/audience-syncs.md "mention"). You can use Census to send any of your segments to LaunchDarkly. Synced Segments are very straightforward, with only two details you need to consider:

* **ID** - This whatever Identifier you use with LaunchDarkly to identify those context types. This could be your internal ID for a user or their email address. LaunchDarkly will happily accept whatever value you send here but in order for the segment to be useful, it must match the ID you are using with LaunchDarkly.
* **Context** - This is the "type" of things in your segment. It can be the standard LaunchDarkly contexts such as Users or Companies, or any custom context you have created.

<figure><img src="../.gitbook/assets/LaunchDarkly (2).png" alt=""><figcaption></figcaption></figure>

## 🚑 Need help connecting to LaunchDarkly?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

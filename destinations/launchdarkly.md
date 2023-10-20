---
description: This page describes how to use Census with LaunchDarkly.
---

# LaunchDarkly

## 🏃‍♀️ Getting Started

1. Click **Add Service** and select **LaunchDarkly** from the menu.
2. Open the LaunchDarkly app in another window to find the following credentials:

### **Service Access Token**

You'll need to create a new access token with the appropriate set of permissions. To learn how to create a service token, see [Creating API access tokens](https://docs.launchdarkly.com/home/account-security/api-access-tokens#creating-api-access-tokens) in LaunchDarkly's documentation.

1. Visit **Account settings** > **Authorization** and click **Create token.**&#x20;
2. For your new access token, give it a memorable name such as `Census LaunchDarkly Integration`.
3. For role, you can use any existing role or custom policy that has the following permissions. Alternatively, select **Inline policy**. You can add multiple statements, one for each of the types of resources you intend to use with Census
   * **Synced Segments**
     * Resource:  `proj/*:env/*:segment/*` will grant access to all segments across all projects.
     * Action: `createSegment` and `updateIncluded`
   * **Metric Events**
     * Resource:  `proj/*:env/*` will grant access to all projects.
     * Action: `importEventData`&#x20;
   * **Metrics**
     * Resource: `proj/*:env/*:metric/*` will grant access to all metrics across all projects.
     * Action: All Actions ([See Full List](https://docs.launchdarkly.com/home/members/role-actions#metric-actions))
4. Check the box next to **This is a service token**. You can leave the API version set to the default value.
5. Click **Save Token**. Copy store the token generated somewhere safe while you're connecting it to Census. You will not be able to retrieve it again.

<figure><img src="../.gitbook/assets/LaunchDarkly (8).png" alt=""><figcaption></figcaption></figure>

### **Project Key, Environment Key, and Environment ID**

Go to **Account settings** > **Projects** and copy the **Project Key,** **Environment Key,** and **Environment ID** (LaunchDarkly uses Environment ID and Client-side ID interchangeably) as shown in the screenshot below. You will need to create separate Environment Keys for each Environment you wish to sync to.

<figure><img src="../.gitbook/assets/LaunchDarkly (5).png" alt=""><figcaption></figcaption></figure>

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

---
description: This page describes how to use Census with Emarsys.
---

# Emarsys

## Getting Started

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **Emarsys** from the menu.
3. Open the Emarsys app in another browser tab and navigate to **Management** > **Security Settings** > **API Users**. Select **Create API user** and take note of the **User name** and **Secret** provided (these will only be displayed once).
4. Once you've created the API user, click the pencil icon next to the new user to edit the permissions assigned to it. Enable all `contact` and `field` scopes, then save your changes.
5. Return to Census and input your **User name** and **Secret**.

**Note**: Permission changes do not occur immediately. There could be a delay of a few minutes before permissions take effect. If your connection test fails in Census, your API user permissions may not have saved properly. Revisit step 4.

<figure><img src="../.gitbook/assets/emarsys.png" alt=""><figcaption><p>Create an API user in the Emarsys app.</p></figcaption></figure>

## Supported Objects and Behaviors

<table data-header-hidden><thead><tr><th width="216" align="right"></th><th width="120" align="center"></th><th></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td><strong>Sync Keys</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Contact</td><td align="center">✅</td><td>Email, ID (Update Only)</td><td>Update or Create, Update Only</td></tr><tr><td align="right">Contact &#x26; Contact List<br><a href="../basics/core-concept/audience-syncs/">Audience Sync</a></td><td align="center">✅</td><td>Email</td><td>Mirror</td></tr></tbody></table>

[Contact us](mailto:support@getcensus.com) if you want Census to support more Emarsys objects and/or behaviors.

## Need help connecting to Emarsys?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

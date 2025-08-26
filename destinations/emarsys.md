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

| **Object Name** | **Supported?** | **Sync Keys** | **Behaviors** |
| --------------: | :------------: | ------------- | ------------- |
|  Contact        |        ✅      | Any [indexed field](https://dev.emarsys.com/docs/core-api-reference/75f3acc2c94dc-concepts#keya-namekeya), ID (Update Only) | Update or Create, Update Only |
| <p>Contact &#x26; Contact List<br><a href="../basics/audience-syncs">Audience Sync</a></p> | ✅ | Email | Mirror |

Contact our support team if you want Census to support more Emarsys objects and/or behaviors.

## Need help connecting to Emarsys?

Contact our support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

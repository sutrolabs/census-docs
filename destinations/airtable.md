---
description: This page describes how to use Census with Airtable.
---

# Airtable

## 🏃‍♀️ Getting Started

In this guide, we will show you how to connect Airtable to Census and create your first sync.

{% embed url="https://www.youtube.com/watch?v=-NRDgN65rrg" %}

### 1. Add an Airtable Connection

1. Navigate to the [Destinations page](https://app.getcensus.com/destinations).
2. Click the **New Destination** button and select **Airtable** from the list.
3. Complete the OAuth flow to connect your Airtable account to Census. As part of the OAuth flow, you'll be able to select the specific workspaces and/or bases you'd like to connect to Census. You can always add more workspaces and/or bases later by clicking the **Reauth** button on the destination in Census.

Note: Census's permissions will be the same as the Airtable user you used during OAuth. If you think this Airtable user's permissions may change or the account is removed, you may want to create a special Airtable account just for Census to use.

You should now have a connection to Airtable! Let's start syncing data.

## 🗄 Supported Objects and Behaviors

Airtable support is pretty straight forward!

| **Object Name** | **Supported?** |             **Behaviors**             |
| --------------: | :------------: | :-----------------------------------: |
|           Table |        ✅       | Update Only, Update or Create, Mirror |

Learn more about all of our sync behaviors on our [Core Concepts page](../basics/core-concept.md#the-different-sync-behaviors).

{% hint style="info" %}
Airtable needs a primary key that is a short text field for Census to be able to join from a source table (though the source can be a numerical type).
{% endhint %}

### Column types

| **Airtable Field Types** | **Source SQL**                                                                                                                                                                        |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Short Text               | <p>String<br>Numeric</p>                                                                                                                                                              |
| Single Select            | <p>String<br>Numeric</p>                                                                                                                                                              |
| Checkbox                 | <p>Boolean<br>Numeric (nonzero = checked, 0 = unchecked)</p>                                                                                                                          |
| Attachments              | <p>A <a href="../basics/defining-source-data/structured-data.md">structured column</a> of the following structure:<br><code>[ { "url": "http://path/to/attachment.png" } ]</code></p> |
| The Rest                 | <p>Census will give an informative error</p><p>message if rejected by Airtable</p>                                                                                                    |

## 🚑 Need help connecting to Airtable?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

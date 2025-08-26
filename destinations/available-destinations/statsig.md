---
description: This page describes how to use Census with Statsig.
---

# Statsig

Statsig is a Partner-Built Destination, learn more about Statsig and how to set up Statsig to receive events from Census [here](https://docs.statsig.com/integrations/data-connectors/census/).

### Getting Started

In this guide, we will show you how to connect Statsig to Census and create your first sync.

**1. Generate an API Token within Statsig**

Before setting up the Statsig connection within Census, you'll first need to generate an API key within Statsig. Further instructions on how to configure your API key within Statsig [available here!](https://helpcenter.enterpret.com/en/articles/8317703-census-integration)&#x20;

For instructions more specifically on syncing to Events there is additional documentation [available here](https://docs.statsig.com/integrations/data-connectors/census/).CommentShare feedback on the editor

**2. Add the API Key to Census**

With your API key, return to Census and visit the **Destinations** tab. Click on the **New Destination** button and select **Statsig** from the menu. Copy and paste the value into the dialog and hit save. You should be clear to create a new sync!

<figure><img src="../../.gitbook/assets/Screenshot 2025-05-19 at 4.18.27 PM.png" alt=""><figcaption></figcaption></figure>

#### 3. Configure your Sync <a href="#sync-configuration" id="sync-configuration"></a>

The following fields are required when mapping to Statsig events.

* `Event ID` (Census requires a sync key to uniquely identify each event)
* `User ID` -> `userID`
* `Event Name` -> `eventName`
* `Timestamp` -> `timestamp`
* `Value` -> `value`

All other fields will be included in the `metadata` section of the mapped Statsig event.

#### Supported Objects <a href="#supported-objects" id="supported-objects"></a>

Census currently supports syncing to the following Statsig objects.

| **Object Name** | **Supported?** | **Sync Keys** |
| --------------- | -------------- | ------------- |
| Event           | ✅              | Event Id      |

#### Supported Sync Behaviors <a href="#supported-sync-behaviors" id="supported-sync-behaviors"></a>

Learn more about all of our sync behaviors in our [Syncs](https://app.gitbook.com/o/-MV3syci5ETx7Jfi5l2K/s/-MV3poo0VqVau1o8I79_/syncs/overview) documentation

| **Behaviors**   | **Supported?** | **Objects** |
| --------------- | -------------- | ----------- |
| **Create Only** | ✅              | Event       |

#### Need help connecting to Statsig? <a href="#need-help-connecting-to-enterpret" id="need-help-connecting-to-enterpret"></a>

​Contact our support team or start a conversation with us via the [in-app](https://app.getcensus.com/) chat.

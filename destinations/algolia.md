---
description: This page describes how to use Census with Algolia.
---

# Algolia

## Getting Started

In this guide, we will show you how to connect Algolia to Census and create your first sync.

### 1. Collect your Algolia Credentials

Census needs the following information to create an Algolia connection, both of which can be found in the same page.&#x20;

First, ensure your desired application is selected in the Application dropdown menu of the Algolia UI. Then navigate to the **Settings** page then click on the **API Keys** option under **Teams & Access.**

* **Application ID** - The alphanumeric string at the top of the **Your API Keys** tab.
* **API Key** - Census uses the `listIndexes`, `search`, and `addObject` permissions. We recommend you create a new API key by navigating to the **All API Keys** tab and pressing **New API Key**. Provide at least those permissions in the ACL section. You can optionally restrict Census to a specific set of indexes as well.&#x20;

### 2. Connect Algolia in Census

* In Census, navigate to [Destinations](https://app.getcensus.com/destinations)
* Click the **New Destination** button
* Select Algolia in the dropdown list
* Enter your credentials and click **Connect**

![](<../.gitbook/assets/Screen Shot 2022-04-01 at 2.42.38 PM.png>)

That's it! In 2 steps, you connected Census to Algolia. If you have any questions or if you have any issues getting started, please contact us via the in-app live chat in the bottom right corner or contact the support team

## Supported Objects and Behaviors

Algolia stores data within collections called Indices. Your Indices in Algolia can be used as objects to sync to from Census.

<table data-header-hidden><thead><tr><th align="right"></th><th width="132" align="center"></th><th align="center"></th><th></th></tr></thead><tbody><tr><td align="right"><strong>Object Name</strong></td><td align="center"><strong>Supported?</strong></td><td align="center"><strong>Sync Keys</strong></td><td><strong>Behaviors</strong></td></tr><tr><td align="right">Index</td><td align="center">✅</td><td align="center">Object ID</td><td>Update or Create</td></tr></tbody></table>

Contact the support team if you want Census to support more objects for Algolia.

## Need help connecting to Algolia?

Contact the support team or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

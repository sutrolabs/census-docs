---
description: This page describes how to use Census with ChatGPT's Retrieval Plugin.
---

# ChatGPT Retrieval Plugin

​[ChatGPT Retrieval Plugins](https://github.com/openai/chatgpt-retrieval-plugin) are an open source pattern for making data accessible to querying by ChatGPT. They require setting up a dedicated server to operate. Census communicates with this server to load the data you've synced. To configure one for your company, see our [blog post on using Census with ChatGPT Retrieval Plugins](https://census.dev/blog/turn-your-db-into-a-chatgpt-plug-in-with-census-and-fly).

### Getting Started <a href="#getting-started" id="getting-started"></a>

1. Navigate to the **Destinations** page in Census and click **New Destination**.
2. Select **ChatGPT Retrieval Plugin** from the menu.
3. Enter your **Bearer Token** and **Hostname**. These are configured when you first deploy your plugin instance.

### Supported Objects and Behaviors <a href="#supported-objects-and-behaviors" id="supported-objects-and-behaviors"></a>

<table data-header-hidden><thead><tr><th width="196"></th><th width="156"></th><th width="154"></th><th></th></tr></thead><tbody><tr><td><strong>Object Name</strong></td><td><strong>Supported?</strong></td><td><strong>Sync Keys</strong></td><td><strong>Behaviors</strong></td></tr><tr><td>Document</td><td>✅</td><td>ID</td><td>Update or Create</td></tr></tbody></table>

​[Contact us](mailto:support@getcensus.com) if you want Census to support more ChatGPT objects and/or behaviors.

### Need help connecting to ChatGPT? <a href="#need-help-connecting-to-chatgpt" id="need-help-connecting-to-chatgpt"></a>

​[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com/) chat.

---
description: Learn more about all the ways to programmatically control Census
---

# Developers

Census supports several different APIs for controlling, accessing data, and extending Census. Teams that have the ability to write code can quickly customize Census and make it an even more integrated component of your data infrastructure.

* [Profile API](entity-api.md) - An optional REST API for accessing data stored in your [Entities](../data-defining/entities.md) on demand.
* [Management API](api.md) - A REST API for controlling the Syncs, Models, and Connections configured within Census. This can be used to programmatically read information and perform most actions available in the Census app today.
* [Custom Destination API](custom-api.md) - A rich JSON-RPC API for implementing your own custom destination for Census Syncs. This API supports batching and schemas just like other Census connections.
  * If you're looking for an easy way to send data to a custom destination, you may also want to look at Census's [webhook.md](../../destinations/webhook.md "mention") connector.
* [Orchestration API](../core-concept/triggering-syncs.md#sync-trigger-api) - Use the orchestration API to programmatically trigger Census syncs and read their status. We use this API to power our Airflow, Prefect, and Dagster integrations.

We're always adding more capabilities to our APIs. If you have questions about how to use our existing APIs or are looking for even more functionality, please send us your feedback to [support@getcensus.com](mailto:support@getcensus.com).

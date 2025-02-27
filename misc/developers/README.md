---
description: Learn more about all the ways to programmatically control Census
---

# Developers

Census supports several different APIs for controlling, accessing data, and extending Census. Teams that have the ability to write code can quickly customize Census and make it an even more integrated component of your data infrastructure.

See our [Developer Hub](https://developers.getcensus.com) for a full view of all the interfaces available.

* [Dataset API](entity-api.md) - An optional REST API for accessing data stored in your [Datasets](broken-reference) on demand.
* [Management API](api.md) - A REST API for controlling the Syncs, Models, and Connections configured within Census. This can be used to programmatically read information and perform most actions available in the Census app today.
* Custom Destinations
  * [HTTP Request Destination](../../destinations/http-request.md) - An easy way to send data to a custom destination, without having to build a full destination.
  * [Custom Destination API](custom-api.md) - A rich JSON-RPC API for implementing your own custom destination for Census Syncs. This API supports batching and schemas just like other Census connections.
* [Sync Trigger API](../../syncs/core-concept/triggering-syncs.md#sync-trigger-api) - Use the sync trigger API to programmatically trigger Census syncs and read their status. We use this API to power our Airflow, Prefect, and Dagster integrations.
* [GitLink](gitlink.md) - An integration that allows you to manage Census SQL models and syncs via YAML files in your Git repository.

We're always adding more capabilities to our APIs. If you have questions about how to use our existing APIs or are looking for even more functionality, please send us your feedback to [support@getcensus.com](mailto:support@getcensus.com).

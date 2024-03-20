---
description: >-
  Unleash your entity graph and use your data to power apps far beyond your data
  warehouse.
---

# Profile API

Profile API is designed to make your Entities even more valuable by making them easily accessible to the wider app ecosystem. In addition to using **Census Syncs** to push data to destinations, you can now make your data available to be pulled by your applications.

This opens your data to a whole world of data integration possibilities. A few of the most exciting ones include:

* App Platform - Build sidebars and micro apps such as Chrome Extension to view user data inside operator consoles.
* Personalization - Have your web site personalize pages for the users in session, recommending products or offering promotions to users.
* Enrichment - Use your data to act as an Enrichment Provider for other services. Use your best first-party data wherever you’ve had to rely on spotty third party data in the past.

## **Set up**

{% hint style="info" %}
Profile API is available for customers on the Enterprise Plan.&#x20;
{% endhint %}

The Profile API can be enabled for each Census workspace individually. Once enabled, all Entities within that workspace will be available via the API.

<figure><img src="../../.gitbook/assets/screely-1677722797342 (1).png" alt=""><figcaption></figcaption></figure>

In order to power the API and make responses quick, Census will automatically cache your entity data on Census managed infrastructure. This process will take a few minutes to hours for extremely large data sets when first enabling the Profile API. Going forward, Census will periodically refresh the cache with incremental changes, just like a typical Census sync. This means that some new data may not be immediately available for querying via the Profile API until the cache is refreshed.

Note that this data will be stored in Census infrastructure until the Profile API is disabled. To learn more about how Census handles your data, see our [Security & Privacy](../security-and-privacy/) page.

## Using Profile API Endpoints

**Authentication** - Uses same key as the [Management API](api.md) - This means you shouldn’t use it directly in public code such as javascript on your website. You’ll want to access it server side instead so the key doesn’t leak. A given API key is scoped to a single [Census Workspace](../security-and-privacy/workspaces-and-access-controls.md) and all entities within that workspace will be accessible.

API requests should include a standard authentication header of the form:

```
Authentication: bearer <secret-key>
```

The Profile API provides two endpoints:

* List Entities - Provides the set of all entities available via the API
* Get Entity Record - Retrieve a specific record of an entity based on its primary key.

You can also access these APIs directly with our Postman collection.

{% file src="../../.gitbook/assets/Census Profile API Postman Collection.zip" %}

### List Entities

The List Entities endpoint will return a list of entities that are available through the API as well as their ID which can then be used to construct a query for specific records of an entity type.

```
GET https://app.getcensus.com/api/v1/entities
```

Response

```json
{
  "data": [
    {
      "id": 1,
      "name": "Users",
      "library_id": 1
    },
    {
      "id": 2,
      "name": "Companies",
      "library_id": 1
    },
    {
      "id": 3,
      "name": "Invoices",
      "library_id": 2
    },
  ]
}
```

### Get Entity Record

Each entity has its own API endpoint, specific to each. You can see the API on the entities page. You can look up any record of your entity by providing the `record_id`, which will look up the record by matching against the Primary ID column selected in the Entity definition.

The URL will be of the form:

```
GET https://app.getcensus.com/api/v1/entities/[ENTITY_ID]/record?record_id=[RECORD_ID]
```

Response

<pre class="language-json"><code class="lang-json">{
<strong>  "data": {
</strong>    "id": "478060",
    "created_at": "2018-01-14 15:53:16",
    "email": "boris@getcensus.com",
    "first_name": "Boris",
    "last_name": "Jabes",
    "title": "CEO"
  }
}
</code></pre>


---
description: >-
  Turn your datasets into an API with a single click to power real-time personalization and recommendations.
---

# Dataset API

Dataset API is designed to make your datasets even more valuable by making them easily accessible to the wider app ecosystem. In addition to using **Census Syncs** to push data to destinations, you can now make your data available to be pulled by your applications.

This opens your data to a whole world of data integration possibilities. A few of the most exciting ones include:

* App Platform - Build sidebars and micro apps such as Chrome Extension to view user data inside operator consoles.
* Personalization - Have your web site personalize pages for the users in session, recommending products or offering promotions to users.
* Enrichment - Use your data to act as an Enrichment Provider for other services. Use your best first-party data wherever you’ve had to rely on spotty third party data in the past.

## **Set up**

{% hint style="info" %}
Dataset API is available for customers on the Enterprise Plan.&#x20;
{% endhint %}

The Dataset API can be enabled for each Census workspace individually. Once enabled, all datasets within that workspace will be available via the API.

<figure><img src="../../.gitbook/assets/screely-1677722797342 (1).png" alt=""><figcaption></figcaption></figure>

In order to power the API and make responses quick, Census will automatically cache your datasets on Census managed infrastructure. This process will take a few minutes to hours for extremely large datasets when first enabling the API. Going forward, Census will periodically refresh the cache with incremental changes, just like a typical Census sync. This means that some new data may not be immediately available for querying via the Dataset API until the cache is refreshed.

Note that this data will be stored on Census infrastructure until the Dataset API is disabled. To learn more about how Census handles your data, see our [Security & Privacy](../security-and-privacy/) page.

## Using Dataset API Endpoints

**Authentication** - Uses the same key as the [Management API](api.md). This means you shouldn’t use it directly in public code such as javascript on your website. You’ll want to access it server side instead so the key doesn’t leak. A given API key is scoped to a single [Census Workspace](../security-and-privacy/workspaces-and-access-controls.md) and all Datasets within that workspace will be accessible.

API requests should include a standard authentication header of the form:

```
Authentication: bearer <secret-key>
```

The Dataset API provides two endpoints:

* List Datasets - Provides the set of all datasets available via the API
* Get Dataset Record - Retrieve a specific record of a dataset based on its primary key.

You can also access these APIs directly with our Postman collection.

{% file src="../../.gitbook/assets/Census Dataset API Postman Collection.zip" %}

### List Datasets

The List Datasets endpoint will return a list of datasets that are available through the API as well as their ID which can then be used to construct a query for specific records of a dataset type.

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

### Get Dataset Record

Each dataset has its own API endpoint. You can see the API on the datasets page. You can look up any record of your dataset by providing the `record_id`, which will look up the record by matching against the Primary ID column selected in the dataset definition.

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


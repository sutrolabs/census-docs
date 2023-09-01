---
description: >-
  This page describes how to use the Management API to manage your connections
  and syncs.
---

# Management API

The Management API lets you integrate core bits of Census's functionality right into your workflows. You can view information about your connections and syncs, as well as create and trigger syncs. Each endpoint returns a status field and either a data object or a single value providing context on what was requested.

Tables that include **Response Property** detail the results of the entire response. Tables that include **Data Property** detail the returned data housed in the top level `data` attribute of the response. Tables that include **Attributes** detail relevant bits of info for nested objects used in requests.

## Postman Collection <img src="../../../.gitbook/assets/postman-icon-svgrepo-com.svg" alt="" data-size="line">

Census has a Postman Collection that encompasses all API endpoints that Census offers.  Whether you are looking to quickly test out our API or trying to build custom authentication flows into your application, the Census Postman Collection will help expedite those projects.

Check out our Postman Collection [here](https://www.postman.com/getcensus/workspace/census-api/overview)!

## Getting API Access

Each Census Workspace has its own API key. You can access it within the **Settings** page.

<figure><img src="../../../.gitbook/assets/CleanShot 2022-10-24 at 11.46.55@2x.png" alt=""><figcaption></figcaption></figure>

## Authenticating API Requests

The Census API uses Bearer authentication to provide API credentials. When accessing the Census API, provide an `Authorization` header with your Workspace API Key as Bearer token value.

`Authorization: Bearer <workspace-api-key>`

{% hint style="info" %}
If using a tool to make requests, please make sure to include this in your Headers:

`Accept */*`
{% endhint %}

## Pagination

The Management API uses a common pagination schema for all GET collection endpoints to control the current page and return information about the overall collection.

### Request URL Parameters

You can pass the following URL parameters to control the response:

<table><thead><tr><th width="144">Parameter</th><th width="144">Type</th><th width="138">Default</th><th>Description</th></tr></thead><tbody><tr><td>page</td><td>number</td><td>1</td><td>Specifies which page of results to return. <br>The first page is always <code>1</code>, not <code>0</code>. If <code>0</code> is requested, the first page (1) will be returned.</td></tr><tr><td>per_page</td><td>number</td><td>25 (max 100)</td><td>Specifies number of results per page.<br>If greater than the max is requested, the max will be returned.</td></tr><tr><td>order</td><td><code>asc</code> or <code>desc</code></td><td><code>desc</code></td><td>Sorts the results ascending or descending by creation time.</td></tr></tbody></table>

### Response Pagination Data

The response body of a collection request contains a **`pagination`** object with the following fields:

<table><thead><tr><th width="152">Field</th><th width="100.33333333333331">Type</th><th>Description</th></tr></thead><tbody><tr><td>total_records</td><td>number</td><td>The total number of individual records in the collection.</td></tr><tr><td>per_page</td><td>number</td><td>The number of records in each page.</td></tr><tr><td>prev_page</td><td>number</td><td>The page number prior to the current page.<br>This will be <code>null</code> if the current page is the first page.</td></tr><tr><td>page</td><td>number</td><td>The current page number.</td></tr><tr><td>next_page</td><td>number</td><td>The page number after to the current page.<br>This will be <code>null</code> if the current page is the last page.</td></tr><tr><td>last_page</td><td>number</td><td>The page number of the last page which has records.</td></tr></tbody></table>

**Note**: there is also a **`next`** field on the response body which contains a fully-qualified URL to the next page of results, or null if there is not another page. This field is deprecated in favor of the `pagination` object, but there are no plans to remove it at this time.

### Sample pagination response data:

```json
{
    "next": "https://app.getcensus.com/api/v1/syncs?page=2&per_page=25",
    "pagination": {
        "total_records": 240,
        "per_page": 25,
        "prev_page": null,
        "page": 1,
        "next_page": 2,
        "last_page": 10
    }
}
```

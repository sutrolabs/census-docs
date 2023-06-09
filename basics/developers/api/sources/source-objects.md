# Objects

### GET /sources/\[ID]/objects

This endpoint returns a list of ALL the source objects (i.e. tables, models, entities, filter segments) that this source connection contains.

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the results ascending or descending by creation time.
* `page` - `number`. Specifies which page of results to return. Defaults to 1.
* `per_page` - `number`. Specifies number of results per page. Defaults to 25, max of 100.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources/[ID]/objects' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "success",
    "data": [
        {
            "type": "table",
            "id": 2,
            "table_catalog": "public",
            "table_schema": "development",
            "table_name": "test"
        },
        {
            "type": "model",
            "id": 15,
            "name": "braze_test",
            "created_at": "2021-10-11T20:52:58.293Z",
            "updated_at": "2021-10-14T23:15:18.508Z",
            "query": "select cast('test@getcensus.com' as VARCHAR(2000)) as email, cast('HAAAA' as VARCHAR(2000)) as random_prop"
        },
        {
            "type": "model",
            "id": 18,
            "name": "airtable_test",
            "created_at": "2021-10-20T02:43:07.120Z",
            "updated_at": "2021-10-20T02:50:35.477Z",
            "query": "select cast('testid1' as VARCHAR(2000)) as company_id, cast('company0' as VARCHAR(2000)) as name, cast('test0' as VARCHAR(2000)) as about, array_construct(cast('newindustry' as VARCHAR(2000))) as industries, array_construct(cast('jim' as VARCHAR(2000))) as users\n"
        },
        {
            "type": "model",
            "id": 3,
            "name": "google_ads_test",
            "created_at": "2021-10-06T21:26:44.206Z",
            "updated_at": "2021-10-06T21:39:32.914Z",
            "query": "select cast('test@getcensus.com' as VARCHAR(2000)) as email, array_construct(cast('audience_v1' as VARCHAR(2000))) as list_id\n"
        }
    ],
    "next": "https:app.getcensus.com/api/v1/sources/6/objects"
}
```
{% endtab %}
{% endtabs %}

| Data Property          | Description                                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------------------------- |
| List of source objects | Tables and models associated with this connection. Properties are described in the following endpoints. |

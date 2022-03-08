# Source Objects

### GET /sources/\[ID]/objects

This endpoint returns a list of all the source objects (i.e. tables and models) that this source connection contains.&#x20;

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the sync runs ascending or descending by creation time
* `page` - What offset of results to return
* `per_page` - How many results to return

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID]/objects
```
{% endtab %}

{% tab title="Response" %}
```
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
    ]
}
```
{% endtab %}
{% endtabs %}

| **Data Property**    | **Description**                                                                                         |
| -------------------- | ------------------------------------------------------------------------------------------------------- |
| List of data sources | Tables and models associated with this connection. Properties are described in the following endpoints. |



### GET /sources/\[ID]/models/\[ID]

This endpoint lists information for a given model, including information on what columns it includes.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID]/models/[ID]
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": {
        "type": "model",
        "id": 18,
        "name": "airtable_test",
        "created_at": "2021-10-20T02:43:07.120Z",
        "updated_at": "2021-10-20T02:50:35.477Z",
        "query": "select cast('test1' as VARCHAR(2000)) as company_id, cast('company0' as VARCHAR(2000)) as name, cast('test0' as VARCHAR(2000)) as about, array_construct(cast('newindustry' as VARCHAR(2000))) as industries\n",
        "columns": [
            {
                "name": "ABOUT",
                "type": "text (2000)"
            },
            {
                "name": "NAME",
                "type": "text (2000)"
            },
            {
                "name": "COMPANY_ID",
                "type": "text (2000)"
            },
            {
                "name": "INDUSTRIES",
                "type": "array"
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

| **Data Property** | **Description**                                                                                                                                                                         |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type              | The type of this data source, will always be `model`.                                                                                                                                   |
| id                | The id of this model.                                                                                                                                                                   |
| name              | The name of this model.                                                                                                                                                                 |
| query             | The SQL query associated with this model.                                                                                                                                               |
| created\_at       | When this model was created.                                                                                                                                                            |
| updated\_at       | When this model was last updated.                                                                                                                                                       |
| compiled\_query   | The compiled query associated with this model if it is built atop a DBT instance.                                                                                                       |
| columns           | <p>A list of columns from this model, each with two properties:</p><ul><li><code>name</code> - The name of the column</li><li><code>type</code> - The data type of the column</li></ul> |



### GET /sources/\[ID]/tables/\[ID]

This endpoint lists information for a given table, including information on what columns it includes.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID]/tables/[ID]
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": {
        "type": "table",
        "id": 2,
        "table_catalog": "public",
        "table_schema": "development",
        "table_name": "test",
        "columns": [
            {
                "name": "ABOUT",
                "type": "text (2000)"
            },
            {
                "name": "CUSTOMER_ID",
                "type": "text (2000)"
            },
            {
                "name": "NAME",
                "type": "text (2000)"
            },
            {
                "name": "INDUSTRIES",
                "type": "array"
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

| **Data Property** | **Description**                                                                                                                                                                         |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type              | The type of this data source, will always be `table`.                                                                                                                                   |
| id                | The id of this table.                                                                                                                                                                   |
| table\_catalog    | The catalog associated with this table.                                                                                                                                                 |
| table\_schema     | The schema associated with this table.                                                                                                                                                  |
| table\_name       | The name of this table.                                                                                                                                                                 |
| columns           | <p>A list of columns from this table, each with two properties:</p><ul><li><code>name</code> - The name of the column</li><li><code>type</code> - The data type of the column</li></ul> |


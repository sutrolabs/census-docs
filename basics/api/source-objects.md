# Source Objects

### GET /sources/\[ID]/objects

This endpoint returns a list of all the source objects (i.e. tables and models) that this source connection contains.&#x20;

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the sync runs ascending or descending by creation time.
* `page` - `number`. Specifies which page of results to return. Defaults to 1.
* `per_page` - `number`. Specifies number of results per page. Defaults to 25.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID]/objects
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
    ]
}
```
{% endtab %}
{% endtabs %}

| **Data Property**    | **Description**                                                                                         |
| -------------------- | ------------------------------------------------------------------------------------------------------- |
| List of data sources | Tables and models associated with this connection. Properties are described in the following endpoints. |



### GET /sources/\[ID]/models

This endpoint lists information all the models for a given source, including information on what columns it includes.

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the sync runs ascending or descending by creation time.
* `page` - `number`. Specifies which page of results to return. Defaults to 1.
* `per_page` - `number`. Specifies number of results per page. Defaults to 25.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID]/models
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "success",
    "data": [
        {
            "type": "model",
            "id": 18,
            "source_object_id": 20,
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
        },
        {
            "type": "model",
            "id": 19,
            "source_object_id": 23,
            "name": "airtable_test_v2",
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
    ]
}
```
{% endtab %}
{% endtabs %}

| **Data Property** | **Description**                                                                                          |
| ----------------- | -------------------------------------------------------------------------------------------------------- |
| A list of models  | A list of your models. The properties of a sync are expanded on below in the GET /models/\[ID] endpoint. |



### GET /sources/\[ID]/models/\[ID]

This endpoint lists information for a given model, including information on what columns it includes.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID]/models/[ID]
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "success",
    "data": {
        "type": "model",
        "id": 18,
        "source_object_id": 20,
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

| **Data Property**  | **Description**                                                                                                                                                                         |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type               | The type of this data source, will always be `model`.                                                                                                                                   |
| id                 | The id of this model.                                                                                                                                                                   |
| source\_object\_id | The source object id for this model.                                                                                                                                                    |
| name               | The name of this model.                                                                                                                                                                 |
| description        | The description for this model.                                                                                                                                                         |
| query              | The SQL query associated with this model.                                                                                                                                               |
| created\_at        | When this model was created.                                                                                                                                                            |
| updated\_at        | When this model was last updated.                                                                                                                                                       |
| compiled\_query    | The compiled query associated with this model if it is built atop a DBT instance.                                                                                                       |
| columns            | <p>A list of columns from this model, each with two properties:</p><ul><li><code>name</code> - The name of the column</li><li><code>type</code> - The data type of the column</li></ul> |



### POST /sources/\[ID]/models

This endpoint creates a model with the given data.

{% tabs %}
{% tab title="Request" %}
```
curl --location --request POST 'https://app.getcensus.com/api/v1/models' \
--header 'Authorization: Bearer [API_TOKEN]' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "API Generated Model",
    "description": "This is a description set through the API.",
    "query": "SELECT * FROM \"users\""
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "created",
    "data": {
        "id": 79
    }
}
```
{% endtab %}
{% endtabs %}

| **Request Property** | **Description**                           |
| -------------------- | ----------------------------------------- |
| name                 | The name of this model.                   |
| description          | The description for this model.           |
| query                | The SQL query associated with this model. |

| **Response Property** | **Description**                                                |
| --------------------- | -------------------------------------------------------------- |
| status                | `created` or `error` indicating whether the model was created. |
| data                  | Present if successful. An object containing the `model_id`     |
| message               | Present if error. Contains message describing the error.       |



### PATCH /sources/\[ID]/models/\[ID]

This endpoint updates a model with the given ID.

{% tabs %}
{% tab title="Request" %}
```
curl --request PATCH 'https://app.getcensus.com/api/v1/sources/6/models/98' \
--header 'Authorization: Bearer [API_TOKEN]' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "API Updated Model",
    "description": "This is a description updated through the API.",
    "query": "SELECT * FROM \"users\" LIMIT 1"
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "updated",
    "data": {
    	"type": "model",
    	"data_source_id": 101,
    	"id": 98,
	"name": "API Updated Model",
	"created_at": "2022-03-04T03:47:41.522Z",
	"updated_at": "2022-03-08T18:30:27.389Z",
	"description": "This is a description updated through the API.",
	"query": "SELECT * FROM \"users\" LIMIT 1",
	"columns": [
	    {
	        "name": "user_id",
		"type": "character varying (256)"
	    },
	    {
		"name": "full_name",
		"type": "character varying (256)"
	    }
	]
    }
}
```
{% endtab %}
{% endtabs %}

| **Request Property** | **Description**                           |
| -------------------- | ----------------------------------------- |
| name                 | The name of this model.                   |
| description          | The description for this model.           |
| query                | The SQL query associated with this model. |

| **Response Property** | **Description**                                                |
| --------------------- | -------------------------------------------------------------- |
| status                | `created` or `error` indicating whether the model was created. |
| data                  | Present if successful. An object containing the `model_id`     |
| message               | Present if error. Contains message describing the error.       |



### DELETE /sources/\[ID]/models/\[ID]

This endpoint deletes a model with the given ID.

{% tabs %}
{% tab title="Request" %}
```
curl --request DELETE 'https://app.getcensus.com/api/v1/sources/6/models/98' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "deleted"
}
```
{% endtab %}
{% endtabs %}

| **Response Property** | **Description**                                                        |
| --------------------- | ---------------------------------------------------------------------- |
| status                | `created` or `404` indicating whether the model was found and deleted. |



### GET /sources/\[ID]/tables/\[ID]

This endpoint lists information for a given table, including information on what columns it includes.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID]/tables/[ID]
```
{% endtab %}

{% tab title="Response" %}
```json
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


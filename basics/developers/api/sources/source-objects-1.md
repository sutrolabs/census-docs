# Models

## GET /sources/\[ID]/models

This endpoint lists information all the models for a given source, including information on what columns it includes.

See [Pagination](../#pagination) for standard URL parameters and response data.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources/[ID]/models' \
--header 'Authorization: Bearer [API_TOKEN]'
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
    ],
    "next": "https://app.getcensus.com/api/v1/sources/6/models?page=2&per_page=2",
    "pagination": {
        "total_records": 4,
        "per_page": 2,
        "prev_page": null,
        "page": 1,
        "next_page": 2,
        "last_page": 2
    }
}
```
{% endtab %}
{% endtabs %}

| Data Property    | Description                                                                                              |
| ---------------- | -------------------------------------------------------------------------------------------------------- |
| A list of models | A list of your models. The properties of a sync are expanded on below in the GET /models/\[ID] endpoint. |

### GET /sources/\[ID]/models/\[ID]

This endpoint lists information for a given model, including information on what columns it includes.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources/[ID]/models/[ID]' \
--header 'Authorization: Bearer [API_TOKEN]'
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

| Data Property      | Description                                                                                                                                                                             |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type               | The type of this source object, will always be `model`.                                                                                                                                 |
| id                 | The id of this model.                                                                                                                                                                   |
| source\_object\_id | The source object id for this model.                                                                                                                                                    |
| name               | The name of this model.                                                                                                                                                                 |
| description        | The description for this model.                                                                                                                                                         |
| query              | The SQL query associated with this model.                                                                                                                                               |
| approved           | `boolean` denoting whether the model is approved for Census' Segments Builder.                                                                                                          |
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

| Request Property | Description                                                                    |
| ---------------- | ------------------------------------------------------------------------------ |
| name             | `required`. The name of this model.                                            |
| query            | `required`. The SQL query associated with this model.                          |
| description      | The description for this model.                                                |
| approved         | `boolean` denoting whether the model is approved for Census' Segments Builder. |

| Response Property | Description                                                    |
| ----------------- | -------------------------------------------------------------- |
| status            | `created` or `error` indicating whether the model was created. |
| data              | Present if successful. An object containing the `model_id`     |
| message           | Present if error. Contains message describing the error.       |

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
    	"source_object_id": 101,
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

| Request Property | Description                                                                    |
| ---------------- | ------------------------------------------------------------------------------ |
| name             | The name of this model.                                                        |
| description      | The description for this model.                                                |
| query            | The SQL query associated with this model.                                      |
| approved         | `boolean` denoting whether the model is approved for Census' Segments Builder. |

| Response Property | Description                                                          |
| ----------------- | -------------------------------------------------------------------- |
| status            | `updated` or `error` indicating whether the model was updated.       |
| data              | Present if successful. Returns the same object as `GET /models/[ID]` |
| message           | Present if error. Contains message describing the error.             |

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

| Response Property | Description                                                            |
| ----------------- | ---------------------------------------------------------------------- |
| status            | `deleted` or `404` indicating whether the model was found and deleted. |

### POST /sources/\[ID]/models/\[ID]/refresh\_columns

This endpoint queues a job to refresh the list of columns for a given source model.

{% tabs %}
{% tab title="Request" %}
```
curl --request POST 'https://app.getcensus.com/api/v1/sources/[ID]/models/[ID]/refresh_columns' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "refresh_key": 1647978948
}
```
{% endtab %}
{% endtabs %}

| Response Property | Description                                             |
| ----------------- | ------------------------------------------------------- |
| refresh\_key      | Contains an `id` used to query the refresh objects job. |

### GET /sources/\[ID]/models/\[ID]/refresh\_columns\_status

This endpoint checks whether the the job refreshing columns for a given source model has completed.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources/[ID]/models/[ID]/refresh_columns_status?refresh_key=[refresh_key]' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "completed"
}
```
{% endtab %}
{% endtabs %}

| Query Parameter | Description                                                                                                                 |
| --------------- | --------------------------------------------------------------------------------------------------------------------------- |
| refresh\_key    | `required`. An `id` provided by the `refresh_columns` endpoint, used to check whether the refresh columns job has finished. |

| Response Property | Description                                                   |
| ----------------- | ------------------------------------------------------------- |
| status            | Status of the job. Can be either `completed` or `processing`. |

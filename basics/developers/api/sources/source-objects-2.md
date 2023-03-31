# Tables

## GET /sources/\[ID]/tables/\[ID]

This endpoint lists information for a given table, including information on what columns it includes.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources/[ID]/tables/[ID]' \
--header 'Authorization: Bearer [API_TOKEN]'
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

| Data Property  | Description                                                                                                                                                                             |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type           | The type of this source object, will always be `table`.                                                                                                                                 |
| id             | The id of this table.                                                                                                                                                                   |
| table\_catalog | The catalog associated with this table.                                                                                                                                                 |
| table\_schema  | The schema associated with this table.                                                                                                                                                  |
| table\_name    | The name of this table.                                                                                                                                                                 |
| columns        | <p>A list of columns from this table, each with two properties:</p><ul><li><code>name</code> - The name of the column</li><li><code>type</code> - The data type of the column</li></ul> |

### POST /sources/\[ID]/tables/\[ID]/refresh\_columns

This endpoint queues a job to refresh the list of columns for a given source table.

{% tabs %}
{% tab title="Request" %}
```
curl --request POST 'https://app.getcensus.com/api/v1/sources/[ID]/tables/[ID]/refresh_columns' \
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

### GET /sources/\[ID]/tables/\[ID]/refresh\_columns\_status

This endpoint checks whether the the job refreshing columns for a given source table has completed.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources/[ID]/tables/[ID]/refresh_columns_status?refresh_key=[refresh_key]' \
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

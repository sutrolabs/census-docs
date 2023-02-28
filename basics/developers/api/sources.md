# Sources

### GET /sources

This endpoint will list all of your data sources, such as your connected data warehouse. For information on models and tables associated with a source, query the endpoints for `data_sources`, `models`, and `tables` as described below.

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the results ascending or descending by creation time.
* `page` - `number`. Specifies which page of results to return. Defaults to 1.
* `per_page` - `number`. Specifies number of results per page. Defaults to 25.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
{    
    "status": "success",
    "data": [
        {
            "id": 4,
            "name": "Snowflake - xxxxxxx.us-east-1",
            "label": null,
            "type": "snowflake",
            "last_test_succeeded": null,
            "last_tested_at": null,
            "connection_details": {
                "account": "xxxxxxx.us-east-1",
                "user": "DEV",
                "warehouse": "TEST",
                "use_keypair": false
            },
            "read_only_connection": false
        },
        {
            "id": 10,
            "name": "BigQuery - Development",
            "label": "BigQuery",
            "type": "big_query",
            "last_test_succeeded": true,
            "last_tested_at": "2021-10-07T20:02:19.544Z",
            "connection_details": {
                "project_id": "development",
                "location": "US",
                "service_account": "xxxxxx.iam.gserviceaccount.com",
                "location_editable": false
            },
            "read_only_connection": false
        }
    ],
    "next": "https://app.getcensus.com/api/v1/sources"
}
```
{% endtab %}
{% endtabs %}

| Data Property   | Description                                                                                                  |
| --------------- | ------------------------------------------------------------------------------------------------------------ |
| List of sources | A list containing information on each source. The properties of a source are described in the next endpoint. |

### GET /sources/\[ID]

This endpoint lists information on a specific source.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources/[ID]' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "success",
    "data": {
        "id": 4,
        "name": "Snowflake - xxxxxxx.us-east-1",
        "label": null,
        "type": "snowflake",
        "last_test_succeeded": null,
        "last_tested_at": null,
        "connection_details": {
            "account": "xxxxxxx.us-east-1",
            "user": "DEV",
            "warehouse": "TEST",
            "use_keypair": false
        },
        "read_only_connection": false
    }
}
```
{% endtab %}
{% endtabs %}

| Data Property          | Description                                                                                                                            |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| id                     | The id of this source.                                                                                                                 |
| name                   | The name of this source.                                                                                                               |
| label                  | The label assigned to this source.                                                                                                     |
| type                   | The type of this source (e.g. `redshift`, `big_query`)                                                                                 |
| last\_test\_succeeded  | Whether or not the last connection test on this source was successful.                                                                 |
| last\_tested\_at       | When the last connection test was ran on this source.                                                                                  |
| connection\_details    | Connection details associated with this source.                                                                                        |
| read\_only\_connection | Whether or not Census has write permissions, for tracking sync state, on this source.                                                  |
| data\_sources          | A list of models and tables associated with this source. Model and table properties are described in their respective endpoints below. |

### POST /sources

This endpoint creates a source with the given data.

{% tabs %}
{% tab title="Request" %}
```
curl --location --request POST 'https://app.getcensus.com/api/v1/sources' \
--header 'Authorization: Bearer [API_TOKEN]' \
--header 'Content-Type: application/json' \
--data-raw '{
    "connection": {
        "credentials": {
            "hostname": "<instance>.<region>.redshift.amazonaws.com",
            "port": "5439",
            "user": "redshift_user",
            "password": "redshift_password",
            "database": "demo"
        },
        "label": "Example Redshift Source",
        "type": "redshift"
    }
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "created",
    "data": {
        "id": 12345
    }
}
```
{% endtab %}
{% endtabs %}

| Request Property | Description                                  |
| ---------------- | -------------------------------------------- |
| connection       | Contains the information for the connection. |

| Connection Property    | Description                                                                                  |
| ---------------------- | -------------------------------------------------------------------------------------------- |
| type                   | `required`. The type of this source (e.g. `redshift`, `big_query`)                           |
| credentials            | `required`. Credentials that should be associated with this source (e.g. `hostname`, `port)` |
| label                  | The label assigned to this source.                                                           |
| read\_only\_connection | Whether or not Census has write permissions, for tracking sync state, on this source.        |

### PATCH /sources/\[ID]

This endpoint updates a source with the given data.

{% tabs %}
{% tab title="Request" %}
```
curl --location --request PATCH 'https://app.getcensus.com/api/v1/sources/12' \
--header 'Authorization: Bearer [API_TOKEN]' \
--header 'Content-Type: application/json' \
--data-raw '{
    "connection": {
        "credentials": {
            "database": "demo_v2"
        },
        "label": "Redshift (Demo v2)"
    }
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "updated",
    "data": {
        "id": 6,
        "name": "Redshift (Demo v2)",
        "label": "Redshift (Demo v2)",
        "last_test_succeeded": true,
        "last_tested_at": "2022-01-01T00:00:00.000Z",
        "type": "redshift",
        "connection_details": {
            "user": "redshift_user",
            "hostname": "<instance>.<region>.redshift.amazonaws.com",
            "port": 5439,
            "database": "demo_v2",
            "ssh_tunnel_enabled": null,
            "ssh_tunnel_hostname": null,
            "ssh_tunnel_port": null,
            "ssh_tunnel_user": null,
            "ssh_tunnel_public_key": null
        },
        "read_only_connection": false
    }
}
```
{% endtab %}
{% endtabs %}

| Request Property | Description                                  |
| ---------------- | -------------------------------------------- |
| connection       | Contains the information for the connection. |

| Connection Property    | Description                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------- |
| credentials            | Credentials that should be associated with this source (e.g. `hostname`, `port)`      |
| label                  | The label assigned to this source.                                                    |
| read\_only\_connection | Whether or not Census has write permissions, for tracking sync state, on this source. |

### DELETE /sources/\[ID]

This endpoint deletes a source with the given ID.

{% tabs %}
{% tab title="Request" %}
```
curl --request DELETE 'https://app.getcensus.com/api/v1/sources/6' \
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

### POST /sources/\[ID]/refresh\_tables

This endpoint queues a job to refresh the list of tables for a source.

{% tabs %}
{% tab title="Request" %}
```
curl --request POST 'http://app.getcensus.com/api/v1/sources/[ID]/refresh_tables' \
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

| Response Property | Description                                            |
| ----------------- | ------------------------------------------------------ |
| refresh\_key      | Contains an `id` used to query the refresh tables job. |

### GET /sources/\[ID]/refresh\_tables\_status

This endpoint checks whether the the job refreshing tables for a source has completed.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sources/[ID]/refresh_tables_status?refresh_key=[refresh_key]' \
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

| Query Parameter | Description                                                                                                               |
| --------------- | ------------------------------------------------------------------------------------------------------------------------- |
| refresh\_key    | `required`. An `id` provided by the `refresh_tables` endpoint, used to check whether the refresh tables job has finished. |

| Response Property | Description                                                   |
| ----------------- | ------------------------------------------------------------- |
| status            | Status of the job. Can be either `completed` or `processing`. |

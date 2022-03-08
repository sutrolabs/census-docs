# Sources

### GET /sources

This endpoint will list all of your data sources, such as your connected data warehouse. For information on models and tables associated with a source, query the endpoints for `data_sources`, `models`, and `tables` as described below.

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the sync runs ascending or descending by creation time.
* `page` - `number`. Specifies which page of results to return. Defaults to 1.
* `per_page` - `number`. Specifies number of results per page. Defaults to 25.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources
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

| **Data Property** | **Description**                                                                                              |
| ----------------- | ------------------------------------------------------------------------------------------------------------ |
| List of sources   | A list containing information on each source. The properties of a source are described in the next endpoint. |



### GET /sources/\[ID]

This endpoint lists information on a specific source.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID]
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

| **Data Property**      | **Description**                                                                                                                        |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| id                     | The id of this source.                                                                                                                 |
| name                   | The name of this source.                                                                                                               |
| label                  | The label assigned to this source.                                                                                                     |
| last\_test\_succeeded  | Whether or not the last connection test on this source was successful.                                                                 |
| last\_tested\_at       | When the last connection test was ran on this source.                                                                                  |
| connection\_details    | Connection details associated with this source.                                                                                        |
| read\_only\_connection | Whether or not Census has write permissions, for tracking sync state, on this source.                                                  |
| data\_sources          | A list of models and tables associated with this source. Model and table properties are described in their respective endpoints below. |

&#x20;

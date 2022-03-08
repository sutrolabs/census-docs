# Syncs

### GET /syncs

This endpoint returns a list of your syncs.

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the sync runs ascending or descending by creation time
* `page` - What offset of results to return
* `per_page` - How many results to return

{% tabs %}
{% tab title="Request" %}
```
curl -X GET https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/syncs
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "success",
    "data": [
        {
            "id": 61,
            "label": null,
            "schedule_frequency": "never",
            "schedule_day": null,
            "schedule_hour": null,
            "schedule_minute": null,
            "created_at": "2021-10-22T00:40:11.246Z",
            "updated_at": "2021-10-22T00:43:44.173Z",
            "operation": "upsert",
            "paused": false,
            "status": "Ready",
            "lead_union_insert_to": null,
            "trigger_on_dbt_cloud_rebuild": false,
            "field_behavior": "specific_properties",
            "field_normalization": null,
            "source_attributes": {
                "connection_id": 4,
                "object": {
                    "type": "model",
                    "id": 15,
                    "name": "braze_test",
                    "created_at": "2021-10-11T20:52:58.293Z",
                    "updated_at": "2021-10-14T23:15:18.508Z",
                    "query": "select cast('test@getcensus.com' as VARCHAR(2000)) as email, cast('random' as VARCHAR(2000)) as random_prop"
                }
            },
            "destination_attributes": {
                "connection_id": 15,
                "object": "user"
            },
            "mappings": [
                {
                    "from": "EMAIL",
                    "to": "external_id",
                    "is_primary_identifier": true,
                    "generate_field": false,
                    "preserve_values": false,
                    "operation": null
                },
                {
                    "from": {
                        "value": "test",
                        "basic_type": "text"
                    },
                    "to": "first_name",
                    "is_primary_identifier": false,
                    "generate_field": false,
                    "preserve_values": false,
                    "operation": null
                }
            ]
        },
        {
            "id": 60,
            "label": null,
            "schedule_frequency": "never",
            "schedule_day": null,
            "schedule_hour": null,
            "schedule_minute": null,
            "created_at": "2021-10-22T00:38:32.191Z",
            "updated_at": "2021-10-22T00:43:47.858Z",
            "operation": "upsert",
            "paused": false,
            "status": "Ready",
            "lead_union_insert_to": null,
            "trigger_on_dbt_cloud_rebuild": false,
            "field_behavior": "specific_properties",
            "field_normalization": null,
            "source_attributes": {
                "connection_id": 4,
                "object": {
                    "type": "model",
                    "id": 15,
                    "name": "braze_test",
                    "created_at": "2021-10-11T20:52:58.293Z",
                    "updated_at": "2021-10-14T23:15:18.508Z",
                    "query": "select cast('test@getcensus.com' as VARCHAR(2000)) as email, cast('random' as VARCHAR(2000)) as random_prop"
                }
            },
            "destination_attributes": {
                "connection_id": 15,
                "object": "user"
            },
            "mappings": [
                {
                    "from": "EMAIL",
                    "to": "external_id",
                    "is_primary_identifier": true,
                    "generate_field": false,
                    "preserve_values": false,
                    "operation": null
                },
                {
                    "from": {
                        "value": "usa",
                        "basic_type": "text"
                    },
                    "to": "country",
                    "is_primary_identifier": false,
                    "generate_field": false,
                    "preserve_values": false,
                    "operation": null
                }
            ]
        }
    ]
}
```
{% endtab %}
{% endtabs %}

| Data Property   | Description                                                                                                                                                                                                                                                                                         |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A list of syncs | <p>A list of your syncs. The properties of a sync are expanded on below in the POST /syncs endpoint.</p><p></p><p>Along with the properties mentioned above, this endpoint returns an <code>id</code>, <code>created_at</code>, <code>updated_at</code>, and <code>status</code> for each sync.</p> |



### GET /syncs/\[ID]

This endpoint returns information on a specific sync.

{% tabs %}
{% tab title="Request" %}
```
curl -X GET https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/syncs/[ID]
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "success",
    "data": {
        "id": 61,
        "label": null,
        "schedule_frequency": "never",
        "schedule_day": null,
        "schedule_hour": null,
        "schedule_minute": null,
        "created_at": "2021-10-22T00:40:11.246Z",
        "updated_at": "2021-10-22T00:43:44.173Z",
        "operation": "upsert",
        "paused": false,
        "status": "Ready",
        "lead_union_insert_to": null,
        "trigger_on_dbt_cloud_rebuild": false,
        "field_behavior": "specific_properties",
        "field_normalization": null,
        "source_attributes": {
            "connection_id": 4,
            "object": {
                "type": "model",
                "id": 15,
                "name": "braze_test",
                "created_at": "2021-10-11T20:52:58.293Z",
                "updated_at": "2021-10-14T23:15:18.508Z",
                "query": "select cast('test@getcensus.com' as VARCHAR(2000)) as email, cast('random' as VARCHAR(2000)) as random_prop"
            }
        },
        "destination_attributes": {
            "connection_id": 15,
            "object": "user"
        },
        "mappings": [
            {
                "from": "EMAIL",
                "to": "external_id",
                "is_primary_identifier": true,
                "generate_field": false,
                "preserve_values": false,
                "operation": null
            },
            {
                "from": {
                    "value": "test",
                    "basic_type": "text"
                },
                "to": "first_name",
                "is_primary_identifier": false,
                "generate_field": false,
                "preserve_values": false,
                "operation": null
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

| Data Property | Description                                                                                                                                                                                                                                                                                         |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A sync        | <p>Information on a sync. The properties of a sync are expanded on below in the POST /syncs endpoint.</p><p></p><p>Along with the properties mentioned above, this endpoint returns an <code>id</code>, <code>created_at</code>, <code>updated_at</code>, and <code>status</code> for the sync.</p> |



### POST /syncs

This endpoint creates a sync with the given data.

{% tabs %}
{% tab title="Request" %}
```
curl --location --request POST 'https://app.getcensus.com/api/v1/syncs' \
--header 'Authorization: Bearer [API_TOKEN]' \
--header 'Content-Type: application/json' \
--data-raw '{
    "label": "TEST 1",
    "operation": "mirror",
    "schedule_frequency": "daily",
    "destination_attributes": {
        "connection_id": 15,
        "object": "user_data"
    },
    "source_attributes": {
        "connection_id": 12,
        "object": {
            "type": "model",
            "name": "test_ads"
        }
    },
    "mappings": [
        {
            "from": "hashed_email",
            "to": "user_identifier.hashed_email_PREHASHED",
            "is_primary_identifier": true
        },
        {
            "from": "list_id",
            "to": "list_id",
            "lookup_object": "user_list",
            "lookup_field": "name"
        },
        {
            "from": {
                "value": "cohort_1",
                "type": "text"
            },
            "to": "cohort"
        }
    ]
}'
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "created",
    "data": {
        "sync_id": 4545
    }
}
```
{% endtab %}
{% endtabs %}

| **Request Property**                          | **Description**                                                                                                                                                                                                                                                                                                                                         |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label _(optional)_                            | A label to give to this sync.                                                                                                                                                                                                                                                                                                                           |
| operation                                     | <p>How records are synced to the destination. Valid options:</p><ul><li><code>append</code></li><li><code>insert</code></li><li><code>mirror</code></li><li><code>update</code></li><li><code>upsert</code></li></ul>                                                                                                                                   |
| source\_attributes                            | Attributes used to identify the data source for this sync. The specific properties are described below.                                                                                                                                                                                                                                                 |
| destination\_attributes                       | Attributes used to identify the destination for this sync. The specific properties are described below.                                                                                                                                                                                                                                                 |
| mappings                                      | A list of mappings between the source and destination. The specific properties are described below.                                                                                                                                                                                                                                                     |
| schedule\_frequency _(optional)_              | <p>When this sync should be run. Valid options:</p><ul><li><code>never</code></li><li><code>continuous</code></li><li><code>quarter_hourly</code></li><li><code>hourly</code></li><li><code>daily</code></li><li><code>weekly</code></li></ul>                                                                                                          |
| schedule\_day _(optional)_                    | <p>What day of the week this sync should run. Valid options:</p><ul><li><code>Sunday</code></li><li><code>Monday</code></li><li><code>Tuesday</code></li><li><code>Wednesday</code></li><li><code>Thursday</code></li><li><code>Friday</code></li><li><code>Saturday</code></li></ul>                                                                   |
| schedule\_hour _(optional_)                   | What hour of the day this sync should run. Valid values are integers between 0 and 24 inclusive.                                                                                                                                                                                                                                                        |
| schedule\_minute _(optional)_                 | What minute of the hour this sync should run. Valid values are integers between 0 and 59 inclusive.                                                                                                                                                                                                                                                     |
| paused _(optional)_                           | Whether or not this sync should be paused.                                                                                                                                                                                                                                                                                                              |
| trigger\_on\_dbt\_cloud\_rebuild _(optional)_ | Whether or not this sync should trigger on a DBT cloud rebuild.                                                                                                                                                                                                                                                                                         |
| field\_behavior _(optional)_                  | Specify `sync_all_properties` to configure this to automatically update mappings when the source changes.                                                                                                                                                                                                                                               |
| field\_normalization _(optional)_             | <p>If <code>sync_all_properties</code> is specified, specify how you would like automatic mappings to be named. Valid options are:</p><ul><li><code>start_case</code></li><li><code>lower_case</code></li><li><code>upper_case</code></li><li><code>camel_case</code></li><li><code>snake_case</code></li><li><code>match_source_names</code></li></ul> |
| high\_water\_mark\_attributes _(optional)_    | Attributes used to identify the sync type. Only valid for `append` operation and source warehouse `Snowflake`The specific properties are described below.                                                                                                                                                                                               |



| **Source Attribute**                                                                                          | **Description**                                                                                                    |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| connection\_id                                                                                                | The id used to identify the source connection.                                                                     |
| object                                                                                                        | Attributes of the data source. Properties are expanded on immediately below.                                       |
| id _(optional if type and name **or** type and table\_name, table\_schema, and table\_catalog are specified)_ | The id of the data source.                                                                                         |
| type _(optional if id specifie_d)                                                                             | <p>The type of your data source. Valid options:</p><ul><li><code>table</code></li><li><code>model</code></li></ul> |
| name _(optional if id specified_)                                                                             | If type is `model`, the name of the model. Not used if type is `table.`                                            |
| table\_name _(optional if id specified)_                                                                      | If type is `table`, the name of the table. Not used if type is `model.`                                            |
| table\_schema _(optional if id specified)_                                                                    | If type is `table`, the schema of the table. Not used if type is `model.`                                          |
| table\_catalog _(optional if id specified_)                                                                   | If type is `table`, the catalog of the table. Not used if type is `model.`                                         |



| **Destination Attribute**          | **Description**                                             |
| ---------------------------------- | ----------------------------------------------------------- |
| connection\_id                     | The id used to identify the destination connection          |
| object                             | The full name of the destination object                     |
| lead\_union\_insert\_to (optional) | Where to insert a union object (for Salesforce connections) |



| **Mapping Attribute**                                                                                  | **Description**                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| from                                                                                                   | <p>The name of the column in the source, or an object with the following properties:</p><ul><li><code>value</code> - A constant value</li><li><code>type</code> - The type of this value (can be <code>boolean</code>, <code>datetime</code>, <code>number</code>, or <code>text</code>)</li></ul> |
| to                                                                                                     | The full name of the field to sync in to                                                                                                                                                                                                                                                           |
| is\_primary\_identifier (optional, but exactly one mapping must have this specified and set to `true`) | Whether or not this mapping is the primary identifier for this sync                                                                                                                                                                                                                                |
| generate\_field (optional)                                                                             | Whether or not this mapping generate a custom field                                                                                                                                                                                                                                                |
| preserve\_values (optional)                                                                            | Whether or not an existing destination value should be overwritten                                                                                                                                                                                                                                 |
| operation (optional)                                                                                   | For array types, whether we should `merge` or `overwrite` values                                                                                                                                                                                                                                   |
| lookup\_object (optional)                                                                              | For a reference field, the full name of the object it refers to                                                                                                                                                                                                                                    |
| lookup\_field (optional)                                                                               | For a reference field, the field to lookup the referenced object by                                                                                                                                                                                                                                |

| **High Water Mark Attribute**      | **Description**                                                                                                                         |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| use\_high\_water\_mark\_diff\_type | `true` or `false` to indicate use of high water mark diff type sync. Only valid for `append` operation and source warehouse `Snowflake` |
| column\_name                       | The name of the column in the source                                                                                                    |

| **Response Property** | **Description**                                                 |
| --------------------- | --------------------------------------------------------------- |
| status                | `created` or `error` indicating whether the sync was triggered. |
| data                  | Present if successful. An object containing the `sync_id`       |
| message               | Present if error. Contains message describing the error.        |



### POST /syncs/\[ID]/trigger

This endpoint triggers a specific sync to run.

{% tabs %}
{% tab title="Request" %}
```
curl -X POST https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/syncs/[ID]/trigger
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": {
        "sync_run_id": 1234567890
    }
}
```
{% endtab %}
{% endtabs %}

| URL Argument      | Description                                                                                                                                                                            |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| force\_full\_sync | \[Optional] If this trigger request should be a Full Sync, add `force_full_sync=true` to the request URL. Note that some sync configurations such as Append do not support full syncs. |

| Response Property | Description                                                     |
| ----------------- | --------------------------------------------------------------- |
| status            | `success` or `error` indicating whether the sync was triggered. |
| data              | Present if successful. An object containing the `sync_run_id`   |
| message           | Present if error. Contains message describing the error.        |


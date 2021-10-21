---
description: >-
  This page describes how to use the Census API to manage your connections and
  syncs.
---

# API

The Census API lets you integrate core bits of Census's functionality right into your workflows. You can view information about your connections and syncs, as well as create and trigger syncs. Each endpoint returns a status field and either a data object or a single value providing context on what was requested.

### GET /sources

This endpoint will list all of your data soes, such as your connected data warehouse. For information on models and tables associated with a source, query the endpoint for a specific source as described below.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources
```
{% endtab %}

{% tab title="Response" %}
```
{    
    "status": "success",
    "data": [
        {
            "id": 4,
            "slug": "snowflake-xxxxxxx-us-east-1",
            "name": "Snowflake - xxxxxxx.us-east-1",
            "label": null,
            "last_test_succeeded": null,
            "last_tested_at": null,
            "credentials": {
                "account": "xxxxxxx.us-east-1",
                "user": "DEV",
                "warehouse": "TEST",
                "use_keypair": false
            },
            "read_only_connection": false
        },
        {
            "id": 10,
            "slug": "bigquery-development",
            "name": "BigQuery - Development",
            "label": "BigQuery",
            "last_test_succeeded": true,
            "last_tested_at": "2021-10-07T20:02:19.544Z",
            "credentials": {
                "project_id": "development",
                "location": "US",
                "service_account": "xxxxxx.iam.gserviceaccount.com",
                "location_editable": false
            },
            "read_only_connection": false
        }
    ]
}
```
{% endtab %}
{% endtabs %}

| **Data Property** | **Description**                                                                                              |
| ----------------- | ------------------------------------------------------------------------------------------------------------ |
| List of sources   | A list containing information on each source. The properties of a source are described in the next endpoint. |



### GET /sources/\[ID or SLUG]

This endpoint lists information a specific source. You can supply either an `id` or a `slug`.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID or SLUG]
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": {
        "id": 4,
        "slug": "snowflake-xxxxxxx-us-east-1",
        "name": "Snowflake - xxxxxxx.us-east-1",
        "label": null,
        "last_test_succeeded": null,
        "last_tested_at": null,
        "credentials": {
            "account": "xxxxxxx.us-east-1",
            "user": "DEV",
            "warehouse": "TEST",
            "use_keypair": false
        },
        "read_only_connection": false,
        "data_sources": [
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
}
```
{% endtab %}
{% endtabs %}

| **Data Property**      | **Description**                                                                                                                        |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| id                     | The id of this source                                                                                                                  |
| slug                   | A human readable identifier for this source                                                                                            |
| name                   | The name of this source                                                                                                                |
| label                  | The label assigned to this source                                                                                                      |
| last\_test\_succeeded  | Whether or not the last connection test on this source was successful                                                                  |
| last\_tested\_at       | When the last connection test was ran on this source                                                                                   |
| credentials            | A list of authentication credentials associated with this source                                                                       |
| read\_only\_connection | Whether or not Census has write permissions, for tracking sync state, on this source                                                   |
| data\_sources          | A list of models and tables associated with this source. Model and table properties are described in their respective endpoints below. |

&#x20;

### GET /sources/\[ID or SLUG]/models/\[ID]

This endpoint lists information for a given model, including information on what columns it includes.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID or SLUG]/models/[ID]
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

| **Data Property** | **Description**                                                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type              | The type of this data source, will always be `model`                                                                                                          |
| id                | The id of this model                                                                                                                                          |
| name              | The name of this model                                                                                                                                        |
| query             | The SQL query associated with this model                                                                                                                      |
| created\_at       | When this model was created                                                                                                                                   |
| updated\_at       | When this model was last updated                                                                                                                              |
| compiled\_query   | The compiled query associated with this model if it is built atop a DBT instance                                                                              |
| columns           | <p>A list of columns from this model, each with two properties:</p><ul><li>name - The name of the column</li><li>type - The data type of the column</li></ul> |



### GET /sources/\[ID or SLUG]/tables/\[ID]

This endpoint lists information for a given table, including information on what columns it includes.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID or SLUG]/tables/[ID]
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

{% tab title="Untitled" %}

{% endtab %}
{% endtabs %}

| **Data Property** | **Description**                                                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type              | The type of this data source, will always be `table`                                                                                                          |
| id                | The id of this table                                                                                                                                          |
| table\_catalog    | The catalog associated with this table                                                                                                                        |
| table\_schema     | The schema associated with this table                                                                                                                         |
| table\_name       | The name of this table                                                                                                                                        |
| columns           | <p>A list of columns from this table, each with two properties:</p><ul><li>name - The name of the column</li><li>type - The data type of the column</li></ul> |



### GET /destinations

This endpoint will list all of your connected destinations. For information on objects associated with a destination, query the endpoint for a specific destination as described below.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/destinations
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": [
        {
            "id": 12,
            "slug": "google-sheets",
            "name": "Google Sheets",
            "credentials": {
                "service_account_email": "xxxxxxx.iam.gserviceaccount.com"
            }
        },
        {
            "id": 6,
            "slug": "google-ads-dev",
            "name": "Google Ads Dev",
            "credentials": {
                "account_id": 7515011393,
                "account_name": "Manager Account Test"
            }
        },
        {
            "id": 15,
            "slug": "braze",
            "name": "Braze",
            "credentials": {
                "instance_url": "https://rest.iad-03.braze.com"
            }
        },
        {
            "id": 14,
            "slug": "hubspot",
            "name": "HubSpot",
            "credentials": {}
        }
    ]
}
```
{% endtab %}
{% endtabs %}

| **Data Property**    | **Description**                                                                                                        |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| List of destinations | A list containing information on each destination. The properties of a destination are described in the next endpoint. |



### GET /destinations/\[ID or SLUG]

This endpoint lists information on a specific destination. You can supply either an `id` or a `slug`.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/destinations/[ID or SLUG]
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": {
        "id": 15,
        "slug": "braze",
        "name": "Braze",
        "credentials": {
            "instance_url": "https://rest.iad-03.braze.com"
        },
        "objects": [
            {
                "label": "User",
                "full_name": "user",
                "allow_custom_fields": true,
                "allow_case_sensitive_field_names": true
            },
            {
                "label": "Event",
                "full_name": "event",
                "allow_custom_fields": true,
                "allow_case_sensitive_field_names": true
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

| **Data Property** | **Description**                                                                                                         |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------- |
| id                | The id of this destination                                                                                              |
| slug              | A human readable identifier for this destination                                                                        |
| name              | The name of this source                                                                                                 |
| credentials       | A list of authentication credentials associated with this source                                                        |
| objects           | A list of objects associated with this source. The properties of an object are described in the objects endpoint below. |



### GET /destinations/\[ID or SLUG]/objects/\[OBJECT\_FULL\_NAME]

This endpoint lists information for a given object, including information on what fields it includes.



{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/destinations/[ID or SLUG]/objects/[OBJECT_FULL_NAME]
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": {
        "label": "User",
        "full_name": "user",
        "allow_custom_fields": true,
        "allow_case_sensitive_field_names": true,
        "fields": [
            {
                "label": "First Name",
                "full_name": "first_name",
                "polymorphic": false,
                "createable": true,
                "updateable": true,
                "operations": [],
                "array": false,
                "preserve_values_supported": false,
                "required_for_mapping": false,
                "can_be_upsert_key": false,
                "can_be_update_key": false,
                "can_be_insert_key": false,
                "can_be_reference_key": false,
                "lookup_object": null
            },
            {
                "label": "Last Name",
                "full_name": "last_name",
                "polymorphic": false,
                "createable": true,
                "updateable": true,
                "operations": [],
                "array": false,
                "preserve_values_supported": false,
                "required_for_mapping": false,
                "can_be_upsert_key": false,
                "can_be_update_key": false,
                "can_be_insert_key": false,
                "can_be_reference_key": false,
                "lookup_object": null
            },
            {
                "label": "Company",
                "full_name": "company",
                "polymorphic": false,
                "createable": true,
                "updateable": true,
                "operations": [],
                "array": false,
                "preserve_values_supported": false,
                "required_for_mapping": false,
                "can_be_upsert_key": false,
                "can_be_update_key": false,
                "can_be_insert_key": false,
                "can_be_reference_key": false,
                "lookup_object": "company"
            },
            {
                "label": "External User ID",
                "full_name": "external_id",
                "polymorphic": false,
                "createable": true,
                "updateable": true,
                "operations": [],
                "array": false,
                "preserve_values_supported": false,
                "required_for_mapping": false,
                "can_be_upsert_key": true,
                "can_be_update_key": true,
                "can_be_insert_key": true,
                "can_be_reference_key": true,
                "lookup_object": null
            },
            {
                "label": "Email",
                "full_name": "email",
                "polymorphic": false,
                "createable": true,
                "updateable": true,
                "operations": [],
                "array": false,
                "preserve_values_supported": false,
                "required_for_mapping": false,
                "can_be_upsert_key": false,
                "can_be_update_key": false,
                "can_be_insert_key": false,
                "can_be_reference_key": false,
                "lookup_object": null
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

| **Data Property**              | **Description**                                                                                 |
| ------------------------------ | ----------------------------------------------------------------------------------------------- |
| label                          | The label for this object                                                                       |
| full\_name                     | The full name for this object. This is used to identify the object in the API                   |
| allow\_custom\_fields          | Whether or not you can define custom fields on this object                                      |
| allow\_case\_sensitive\_fields | Whether or not field names and labels are case sensitive on this object                         |
| fields                         | A list of fields associated with this source. Field properties are described in the table below |



#### Destination Field Properties

| **Data Property**           | **Description**                                                                                                                                                                                                                                                     |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label                       | The label for this field                                                                                                                                                                                                                                            |
| full\_name                  | The full name for this field. This is used to identify the field in the API                                                                                                                                                                                         |
| polymorphic                 | Whether or not this field can accept multiple types of input                                                                                                                                                                                                        |
| createable                  | Whether or not this field can be created in the destination if it doesn't exist                                                                                                                                                                                     |
| updateable                  | Whether or not this field can be updated in the destination                                                                                                                                                                                                         |
| operations                  | <p>For an array type, what operations are supported on this field. One of the following types:</p><ul><li><code>overwrite</code> - Overwrite existing values with inputted values</li><li><code>merge</code> - Merge inputted values with existing values</li></ul> |
| array                       | Whether or not this field is an array type                                                                                                                                                                                                                          |
| preserve\_values\_supported | If a value exists in the destination for this field, whether or not it can be overwritten by Census                                                                                                                                                                 |
| required\_for\_mapping      | Whether or not this field is required                                                                                                                                                                                                                               |
| can\_be\_upsert\_key        | Whether or not this field can be the primary identifier for an upsert sync                                                                                                                                                                                          |
| can\_be\_update\_key        | Whether or not this field can be the primary identifier for an update only sync                                                                                                                                                                                     |
| can\_be\_insert\_key        | Whether or not this field can be the primary identifier for a create only sync                                                                                                                                                                                      |
| can\_be\_reference\_key     | Whether or not this field can be the identifier for a lookup on its containing object                                                                                                                                                                               |
| lookup\_object              | What object, if any, that this field references                                                                                                                                                                                                                     |



### GET /sync\_runs/\[ID]

This endpoint returns information on a specific sync run.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sync_runs/[ID]
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": {
        "id": 94,
        "sync_id": 52,
        "source_record_count": 1,
        "records_processed": 1,
        "records_updated": 1,
        "records_failed": 0,
        "records_invalid": 0,
        "created_at": "2021-10-20T02:51:07.546Z",
        "updated_at": "2021-10-20T02:52:29.236Z",
        "completed_at": "2021-10-20T02:52:29.234Z",
        "scheduled_execution_time": null,
        "error_code": null,
        "error_message": null,
        "error_detail": null,
        "status": "completed",
        "canceled": false,
        "full_sync": true,
        "sync_trigger_reason": {
            "ui_tag": "Manual",
            "ui_detail": "Manually triggered by test@getcensus.com"
        }
    }
}
```
{% endtab %}
{% endtabs %}

| Data Properties            | Description                                                                                                                                                                                                |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                         | ID of this sync run                                                                                                                                                                                        |
| sync\_id                   | ID of the parent sync                                                                                                                                                                                      |
| status                     | <ul><li><code>working</code> if the sync is currently executing</li><li><code>completed</code> if the sync finished successfully</li><li><code>failed</code> if the sync failed during execution</li></ul> |
| records\_processed         | Number of new or updated records retrieved from the source                                                                                                                                                 |
| records\_updated           | Number of records successfully sent to the destination                                                                                                                                                     |
| records\_invalid           | Number of records skipped by Census because of data quality issues                                                                                                                                         |
| records\_failed            | Number of records rejected by the destination                                                                                                                                                              |
| created\_at                | When this sync run was created                                                                                                                                                                             |
| updated\_at                | When this sync run was updated                                                                                                                                                                             |
| completed\_at              | When this sync run was completed                                                                                                                                                                           |
| scheduled\_execution\_time | When the sync run was scheduled to run                                                                                                                                                                     |
| error\_code                | The error code, if any                                                                                                                                                                                     |
| error\_message             | The error message, if any                                                                                                                                                                                  |
| error\_detail              | Details about the error, if any                                                                                                                                                                            |
| canceled                   | Whether or not this sync run was canceled                                                                                                                                                                  |
| full\_sync                 | Whether or not this was a full sync                                                                                                                                                                        |
| sync\_trigger\_reason      | Details on why this sync was run                                                                                                                                                                           |



### GET /syncs/\[ID]/sync\_runs

This endpoint returns info on the sync runs for a specific sync. You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the sync runs ascending or descending by creation time
* `page` - What offset of results to return
* `per_page` - How many results to return

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/syncs/[ID]/sync_runs?page=1&per_page=1&order=asc
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": [
        {
            "id": 94,
            "sync_id": 52,
            "source_record_count": 1,
            "records_processed": 1,
            "records_updated": 1,
            "records_failed": 0,
            "records_invalid": 0,
            "created_at": "2021-10-20T02:51:07.546Z",
            "updated_at": "2021-10-20T02:52:29.236Z",
            "completed_at": "2021-10-20T02:52:29.234Z",
            "scheduled_execution_time": null,
            "error_code": null,
            "error_message": null,
            "error_detail": null,
            "status": "completed",
            "canceled": false,
            "full_sync": true,
            "sync_trigger_reason": {
                "ui_tag": "Manual",
                "ui_detail": "Manually triggered by test@getcensus.com"
            }
        },
        {
            "id": 93,
            "sync_id": 52,
            "source_record_count": 1,
            "records_processed": null,
            "records_updated": null,
            "records_failed": null,
            "records_invalid": 0,
            "created_at": "2021-10-20T02:48:40.373Z",
            "updated_at": "2021-10-20T02:49:53.430Z",
            "completed_at": null,
            "scheduled_execution_time": null,
            "error_code": "JSON_ARRAY_ERROR",
            "error_message": "The array field being used does not appear to be valid JSON: Please make sure the field \"custom_field:Users\" with value \"jim\" is formatted as a JSON Array. Don't hesitate to reach out to the Census Support Team if you need help with this.",
            "error_detail": "Please make sure the field \"custom_field:Users\" with value \"jim\" is formatted as a JSON Array. Don't hesitate to reach out to the Census Support Team if you need help with this.",
            "status": "failed",
            "current_step": "Running sync",
            "canceled": false,
            "full_sync": true,
            "sync_trigger_reason": {
                "ui_tag": "Manual",
                "ui_detail": "Manually triggered by test@getcensus.com"
            }
        },
        {
            "id": 92,
            "sync_id": 52,
            "source_record_count": 1,
            "records_processed": 1,
            "records_updated": 1,
            "records_failed": 0,
            "records_invalid": 0,
            "created_at": "2021-10-20T02:44:35.381Z",
            "updated_at": "2021-10-20T02:45:55.949Z",
            "completed_at": "2021-10-20T02:45:55.947Z",
            "scheduled_execution_time": null,
            "error_code": null,
            "error_message": null,
            "error_detail": null,
            "status": "completed",
            "canceled": false,
            "full_sync": true,
            "sync_trigger_reason": {
                "ui_tag": "Manual",
                "ui_detail": "Manually triggered by test@getcensus.com"
            }
        }
    ]
}
```
{% endtab %}
{% endtabs %}



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

| Response Property | Description                                                     |
| ----------------- | --------------------------------------------------------------- |
| status            | `success` or `error` indicating whether the sync was triggered. |
| data              | Present if successful. An object containing the `sync_run_id`   |
| message           | Present if error. Contains message describing the error.        |



### POST /syncs/create

This endpoint creates a sync with the given data.

{% tabs %}
{% tab title="Request" %}
```
curl --location --request POST 'https://app.getcensus.com/api/v1/syncs/create' \
--header 'Authorization: Bearer [API_TOKEN]' \
--header 'Content-Type: application/json' \
--data-raw '{
    "label": "TEST 1",
    "operation": "mirror",
    "schedule_frequency": "daily",
    "destination_attributes": {
        "connection_slug": "google-ads",
        "object": "user_data"
    },
    "source_attributes": {
        "connection_slug": "bigquery",
        "type": "model",
        "model_name": "test_ads"
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

| **Request Property**                   | **Description**                                                                                                                                                                                                                                                                       |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label                                  | A label to give to this sync                                                                                                                                                                                                                                                          |
| operation                              | <p>The type of sync. Valid options:</p><ul><li><code>append</code></li><li><code>insert</code></li><li><code>mirror</code></li><li><code>update</code></li><li><code>upsert</code></li></ul>                                                                                          |
| source\_attributes                     | Attributes used to identify the data source for this sync. The specific properties are described below                                                                                                                                                                                |
| destination\_attributes                | Attributes used to identify the destination for this sync. The specific properties are described below                                                                                                                                                                                |
| mappings                               | A list of mappings between the source and destination. The specific properties are described below                                                                                                                                                                                    |
| schedule\_frequency                    | <p>When this sync should be run. Valid options:</p><ul><li><code>never</code></li><li><code>continuous</code></li><li><code>quarter_hourly</code></li><li><code>hourly</code></li><li><code>daily</code></li><li><code>weekly</code></li></ul>                                        |
| schedule\_day                          | <p>What day of the week this sync should run. Valid options:</p><ul><li><code>Sunday</code></li><li><code>Monday</code></li><li><code>Tuesday</code></li><li><code>Wednesday</code></li><li><code>Thursday</code></li><li><code>Friday</code></li><li><code>Saturday</code></li></ul> |
| schedule\_hour                         | What hour of the day this sync should run. Valid values are integers between 0 and 24 inclusive                                                                                                                                                                                       |
| schedule\_minute                       | What minute of the hour this sync should run. Valid values are integers between 0 and 59 inclusive                                                                                                                                                                                    |
| paused                                 | Whether or not this sync should be paused                                                                                                                                                                                                                                             |
| trigger\_on\_dbt\_cloud\_rebuild       | Whether or not this sync should trigger on a DBT cloud rebuild                                                                                                                                                                                                                        |
| failed\_run\_notifications\_enabled    | Whether or not you should get email alerts when a sync run fails                                                                                                                                                                                                                      |
| failed\_record\_notifications\_enabled | Whether or not you should get email alerts when there are skipped records in a sync run                                                                                                                                                                                               |



| **Source Attribute** | **Description**                                                                                                    |
| -------------------- | ------------------------------------------------------------------------------------------------------------------ |
| connection\_slug     | The slug used to identify the source connection                                                                    |
| type                 | <p>The type of your data source. Valid options:</p><ul><li><code>table</code></li><li><code>model</code></li></ul> |
| model\_name          | If type is `model`, the name of the model. Not used if type is `table`                                             |
| table\_name          | If type is `table`, the name of the table. Not used if type is `model`                                             |
| table\_schema        | If type is `table`, the schema of the table. Not used if type is `model`                                           |
| table\_catalog       | If type is `table`, the catalog of the table. Not used if type is `model`                                          |



| **Destination Attribute** | **Description**                                             |
| ------------------------- | ----------------------------------------------------------- |
| connection\_slug          | The slug used to identify the destination connection        |
| object                    | The full name of the destination object                     |
| lead\_union\_insert\_to   | Where to insert a union object (for Salesforce connections) |



| **Mapping Attribute**   | **Description**                                                                                                                                                                                                                                                                                    |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| from                    | <p>The name of the column in the source, or an object with the following properties:</p><ul><li><code>value</code> - A constant value</li><li><code>type</code> - The type of this value (can be <code>boolean</code>, <code>datetime</code>, <code>number</code>, or <code>text</code>)</li></ul> |
| to                      | The full name of the field to sync in to                                                                                                                                                                                                                                                           |
| is\_primary\_identifier | Whether or not this mapping is the primary identifier for this sync                                                                                                                                                                                                                                |
| generate\_field         | Whether or not this mapping generate a custom field                                                                                                                                                                                                                                                |
| preserve\_values        | Whether or not an existing destination value should be overwritten                                                                                                                                                                                                                                 |
| operation               | For array types, whether we should `merge` or `overwrite` values                                                                                                                                                                                                                                   |
| lookup\_object          | For a reference field, the full name of the object it refers to                                                                                                                                                                                                                                    |
| lookup\_field           | For a reference field, the field to lookup the referenced object by                                                                                                                                                                                                                                |
| object                  | The full name of the destination object                                                                                                                                                                                                                                                            |



| **Response Property** | **Description**                                                 |
| --------------------- | --------------------------------------------------------------- |
| status                | `created` or `error` indicating whether the sync was triggered. |
| data                  | Present if successful. An object containing the `sync_id`       |
| message               | Present if error. Contains message describing the error.        |

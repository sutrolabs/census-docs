---
description: >-
  This page describes how to use the Census API to manage your connections and
  syncs.
---

# API

The Census API lets you integrate core bits of Census's functionality right into your workflows. You can view information about your connections and syncs, as well as create and trigger syncs. Each endpoint returns a status field and either a data object or a single value providing context on what was requested.

In the documentation below, tables that include **Response Property** detail the results of the entire response. Tables that include **Data Property** detail the relevant bits of info in the top level `data` attribute of the response. Tables that include **Attributes** detail relevant bits of info for nested objects used in requests.

### GET /sources

This endpoint will list all of your data sources, such as your connected data warehouse. For information on models and tables associated with a source, query the endpoints for `data_sources`, `models`, and `tables` as described below.

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
    ]
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
```
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

### GET /sources/\[ID]/data\_sources

This endpoint returns a list of all the data sources (i.e. tables and models) that this source connection contains.&#x20;

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the sync runs ascending or descending by creation time
* `page` - What offset of results to return
* `per_page` - How many results to return

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/sources/[ID]/data_sources
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

###

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
            "name": "Google Sheets",
            "connection_details": {
                "service_account_email": "xxxxxxx.iam.gserviceaccount.com"
            }
        },
        {
            "id": 6,
            "name": "Google Ads Dev",
            "connection_details": {
                "account_id": 7515011393,
                "account_name": "Manager Account Test"
            }
        },
        {
            "id": 15,
            "name": "Braze",
            "connection_details": {
                "instance_url": "https://rest.iad-03.braze.com"
            }
        },
        {
            "id": 14,
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



### GET /destinations/\[ID]

This endpoint lists information on a specific destination.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/destinations/[ID]
```
{% endtab %}

{% tab title="Response" %}
```
{
    "status": "success",
    "data": {
        "id": 15,
        "name": "Braze",
        "connection_details": {
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

| **Data Property**   | **Description**                                                                                                         |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| id                  | The id of this destination.                                                                                             |
| name                | The name of this source.                                                                                                |
| connection\_details | Connection details associated with this source.                                                                         |
| objects             | A list of objects associated with this source. The properties of an object are described in the objects endpoint below. |



### GET /destinations/\[ID]/objects/\[OBJECT\_FULL\_NAME]

This endpoint lists information for a given object, including information on what fields it includes.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/destinations/[ID]/objects/[OBJECT_FULL_NAME]
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
                "lookup_object": null,
                "type": "String"
            },
            {
                "label": "Last Name",
                "full_name": "last_name",
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
                "lookup_object": null,
                "type": "String"
            },
            {
                "label": "Company",
                "full_name": "company",
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
                "lookup_object": "company",
                "type": "String"
            },
            {
                "label": "External User ID",
                "full_name": "external_id",
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
                "lookup_object": null,
                "type": "String"
            },
            {
                "label": "Email",
                "full_name": "email",
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
                "lookup_object": null,
                "type": "String"
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}

| **Data Property**              | **Description**                                                                                  |
| ------------------------------ | ------------------------------------------------------------------------------------------------ |
| label                          | The label for this object.                                                                       |
| full\_name                     | The full name for this object. This is used to identify the object in the API.                   |
| allow\_custom\_fields          | Whether or not you can define custom fields on this object.                                      |
| allow\_case\_sensitive\_fields | Whether or not field names and labels are case sensitive on this object.                         |
| fields                         | A list of fields associated with this source. Field properties are described in the table below. |



#### Field Properties

| **Data Property**           | **Description**                                                                                                                                                                                                                                                     |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| label                       | The label for this field.                                                                                                                                                                                                                                           |
| full\_name                  | The full name for this field. This is used to identify the field in the API.                                                                                                                                                                                        |
| createable                  | Whether or not this field can be created in the destination if it doesn't exist.                                                                                                                                                                                    |
| updateable                  | Whether or not this field can be updated in the destination.                                                                                                                                                                                                        |
| operations                  | <p>For an array type, what operations are supported on this field. One of the following types:</p><ul><li><code>overwrite</code> - Overwrite existing values with inputted values</li><li><code>merge</code> - Merge inputted values with existing values</li></ul> |
| array                       | Whether or not this field is an array type.                                                                                                                                                                                                                         |
| preserve\_values\_supported | If a value exists in the destination for this field, whether or not it can be overwritten by Census.                                                                                                                                                                |
| required\_for\_mapping      | Whether or not this field is required.                                                                                                                                                                                                                              |
| can\_be\_upsert\_key        | Whether or not this field can be the primary identifier for an upsert sync.                                                                                                                                                                                         |
| can\_be\_update\_key        | Whether or not this field can be the primary identifier for an update only sync.                                                                                                                                                                                    |
| can\_be\_insert\_key        | Whether or not this field can be the primary identifier for a create only sync.                                                                                                                                                                                     |
| can\_be\_reference\_key     | Whether or not this field can be the identifier for a lookup on its containing object.                                                                                                                                                                              |
| lookup\_object              | What object, if any, that this field references.                                                                                                                                                                                                                    |
| type                        | The type of this field.                                                                                                                                                                                                                                             |



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
        "full_sync": true,.
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
| id                         | id of this sync run.                                                                                                                                                                                       |
| sync\_id                   | id of the parent sync.                                                                                                                                                                                     |
| status                     | <ul><li><code>working</code> if the sync is currently executing</li><li><code>completed</code> if the sync finished successfully</li><li><code>failed</code> if the sync failed during execution</li></ul> |
| records\_processed         | Number of new or updated records retrieved from the source.                                                                                                                                                |
| records\_updated           | Number of records successfully sent to the destination.                                                                                                                                                    |
| records\_invalid           | Number of records skipped by Census because of data quality issues.                                                                                                                                        |
| records\_failed            | Number of records rejected by the destination.                                                                                                                                                             |
| created\_at                | When this sync run was created.                                                                                                                                                                            |
| updated\_at                | When this sync run was updated.                                                                                                                                                                            |
| completed\_at              | When this sync run was completed.                                                                                                                                                                          |
| scheduled\_execution\_time | When the sync run was scheduled to run.                                                                                                                                                                    |
| error\_code                | The error code, if any.                                                                                                                                                                                    |
| error\_message             | The error message, if any.                                                                                                                                                                                 |
| error\_detail              | Details about the error, if any.                                                                                                                                                                           |
| canceled                   | Whether or not this sync run was canceled.                                                                                                                                                                 |
| full\_sync                 | Whether or not this was a full sync.                                                                                                                                                                       |
| sync\_trigger\_reason      | Details on why this sync was run.                                                                                                                                                                          |



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
```
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
                "data_source": {
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
                "data_source": {
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
```
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
            "data_source": {
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
        "data_source": {
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



| **Source Attribute**                                                                                          | **Description**                                                                                                    |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| connection\_id                                                                                                | The id used to identify the source connection.                                                                     |
| data\_source                                                                                                  | Attributes of the data source. Properties are expanded on immediately below.                                       |
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

| Response Property | Description                                                     |
| ----------------- | --------------------------------------------------------------- |
| status            | `success` or `error` indicating whether the sync was triggered. |
| data              | Present if successful. An object containing the `sync_run_id`   |
| message           | Present if error. Contains message describing the error.        |

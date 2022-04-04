# Destination Objects

### GET /destinations/\[ID]/objects

This endpoint lists information for all objects under a given destination.



{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/destinations/[ID]/objects
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "success",
    "data": [
        {
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
        },
        {
            "label": "Organization",
            "full_name": "organization",
            "allow_custom_fields": true,
            "allow_case_sensitive_field_names": true,
            "fields": [
                {
                    "label": "Name",
                    "full_name": "name",
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
                    "label": "Address",
                    "full_name": "address",
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
                }
            ]
        },
    ]
}
```
{% endtab %}
{% endtabs %}

| Data Property                 | Description                                                                                                                                           |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| A list of destination objects | A list of objects for the given destination. The properties of each destination object are expanded on below in the GET /destinations/\[ID] endpoint. |





### GET /destinations/\[ID]/objects/\[OBJECT\_FULL\_NAME]

This endpoint lists information for a given object, including information on what fields it includes.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/destinations/[ID]/objects/[OBJECT_FULL_NAME]
```
{% endtab %}

{% tab title="Response" %}
```json
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

| Data Property                  | Description                                                                                      |
| ------------------------------ | ------------------------------------------------------------------------------------------------ |
| label                          | The label for this object.                                                                       |
| full\_name                     | The full name for this object. This is used to identify the object in the API.                   |
| allow\_custom\_fields          | Whether or not you can define custom fields on this object.                                      |
| allow\_case\_sensitive\_fields | Whether or not field names and labels are case sensitive on this object.                         |
| fields                         | A list of fields associated with this source. Field properties are described in the table below. |



#### Field Properties

| Data Property               | Description                                                                                                                                                                                                                                                         |
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





### POST /destinations/\[ID]/objects/\[OBJECT\_FULL\_NAME]/refresh\_fields

This endpoint queues a job to refresh the list of fields for a given destination object.

{% tabs %}
{% tab title="Request" %}
```
curl --request POST 'http://app.getcensus.com/api/v1/destinations/[ID]/objects/[OBJECT_FULL_NAME]/refresh_fields' \
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





### GET /destinations/\[ID]/objects/\[OBJECT\_FULL\_NAME]/refresh\_fields\_status

This endpoint checks whether the the job refreshing fields for a given destination object has completed.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/destinations/[ID]/objects/[OBJECT_FULL_NAME]refresh_fields_status?refresh_key=1647978948
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
| refresh\_key    | `required`. An `id` provided by the `refresh_objects` endpoint, used to check whether the refresh objects job has finished. |

| Response Property | Description                                                   |
| ----------------- | ------------------------------------------------------------- |
| status            | Status of the job. Can be either `completed` or `processing`. |




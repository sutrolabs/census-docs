# Destinations

### GET /destinations

This endpoint will list all of your connected destinations. For information on objects associated with a destination, query the endpoint for a specific destination as described below.

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the results ascending or descending by creation time.
* `page` - `number`. Specifies which page of results to return. Defaults to 1.
* `per_page` - `number`. Specifies number of results per page. Defaults to 25.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/destinations' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
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
    ],
    "next": "https://app.getcensus.com/api/v1/destinations?page=2&per_page=25"
}
```
{% endtab %}
{% endtabs %}

| Data Property        | Description                                                                                                            |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| List of destinations | A list containing information on each destination. The properties of a destination are described in the next endpoint. |

### GET /destinations/\[ID]

This endpoint lists information on a specific destination.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/destinations/[ID]' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
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

| Data Property       | Description                                                                                                             |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| id                  | The id of this destination.                                                                                             |
| name                | The name of this source.                                                                                                |
| connection\_details | Connection details associated with this source.                                                                         |
| objects             | A list of objects associated with this source. The properties of an object are described in the objects endpoint below. |

### POST /destinations

This endpoint creates a destination with the given data.

{% tabs %}
{% tab title="Request" %}
```
curl --location --request POST 'https://app.getcensus.com/api/v1/destinations' \
--header 'Authorization: Bearer [API_TOKEN]' \
--header 'Content-Type: application/json' \
--data-raw '{
    "service_connection": {
        "name": "Example ActiveCampaign",
        "type": "active_campaign",
        "credentials": {
            "api_token": "example_api_token",
            "instance_url": "https://example.activehosted.com"
        }
    }
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "created",
    "data": {
        "id": 90
    }
}
```
{% endtab %}
{% endtabs %}

| Request Property    | Description                                  |
| ------------------- | -------------------------------------------- |
| service\_connection | Contains the information for the connection. |

| Connection Property | Description                                                                                          |
| ------------------- | ---------------------------------------------------------------------------------------------------- |
| type                | `required`. The type of this destination (e.g. `zendesk`, `active_campaign`)                         |
| credentials         | `required`. Credentials that should be associated with this destination (e.g. `api_token`, `domain)` |
| name                | The name to assign to this destination                                                               |

| Response Property | Description                                                      |
| ----------------- | ---------------------------------------------------------------- |
| status            | `created` or `error` indicating whether the model was created.   |
| data              | Present if successful. An object containing the `destination_id` |
| message           | Present if error. Contains message describing the error.         |

### PATCH /destinations/\[ID]

This endpoint updates a destination with the given ID.

{% tabs %}
{% tab title="Request" %}
```
curl --request PATCH 'https://app.getcensus.com/api/v1/destinations/90' \
--header 'Authorization: Bearer [API_TOKEN]' \
--header 'Content-Type: application/json' \
--data-raw '{
    "service_connection": {
        "name": "ActiveCampaign (Example)",
        "credentials": {
            "api_token": "regenerated_api_token"
        }
    }
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "status": "updated",
    "data": {
        "id": 90,
        "name": "ActiveCampaign (Example)",
        "type": "active_campaign",
        "connection_details": {
            "instance_url": "https://example.activehosted.com"
        },
        "objects": [...]
    }
}
```
{% endtab %}
{% endtabs %}

| Request Property    | Description                                  |
| ------------------- | -------------------------------------------- |
| service\_connection | Contains the information for the connection. |

| Connection Property | Description                                                                              |
| ------------------- | ---------------------------------------------------------------------------------------- |
| name                | The name to assign to this destination                                                   |
| credentials         | Credentials that should be associated with this destination (e.g. `api_token`, `domain)` |

| Response Property | Description                                                          |
| ----------------- | -------------------------------------------------------------------- |
| status            | `updated` or `error` indicating whether the destination was created. |
| data              | Present if successful. An object containing the destination object.  |
| message           | Present if error. Contains message describing the error.             |

### DELETE /destinations/\[ID]

This endpoint deletes a destination with the given ID.

{% tabs %}
{% tab title="Request" %}
```
curl --request DELETE 'https://app.getcensus.com/api/v1/destinations/90' \
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

### POST /destinations/\[ID]/refresh\_objects

This endpoint queues a job to refresh the list of objects for a destination.

{% tabs %}
{% tab title="Request" %}
```
curl --request POST 'https://app.getcensus.com/api/v1/destinations/90/refresh_objects' \
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

### GET /destinations/\[ID]/refresh\_objects\_status

This endpoint checks whether the the job refreshing objects for a destination has completed.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/destinations/[ID]/refresh_objects_status?refresh_key=[refresh_key]' \
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
| refresh\_key    | `required`. An `id` provided by the `refresh_objects` endpoint, used to check whether the refresh objects job has finished. |

| Response Property | Description                                                   |
| ----------------- | ------------------------------------------------------------- |
| status            | Status of the job. Can be either `completed` or `processing`. |

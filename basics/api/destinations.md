# Destinations

### GET /destinations

This endpoint will list all of your connected destinations. For information on objects associated with a destination, query the endpoint for a specific destination as described below.

{% tabs %}
{% tab title="Request" %}
```
curl https://bearer:[API_TOKEN]@app.getcensus.com/api/v1/destinations
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

| **Data Property**   | **Description**                                                                                                         |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| id                  | The id of this destination.                                                                                             |
| name                | The name of this source.                                                                                                |
| connection\_details | Connection details associated with this source.                                                                         |
| objects             | A list of objects associated with this source. The properties of an object are described in the objects endpoint below. |


# Destinations

### GET /destinations

This endpoint will list all of your connected destinations. For information on objects associated with a destination, query the endpoint for a specific destination as described below.

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the results ascending or descending by creation time.
* `page` - `number`. Specifies which page of results to return. Defaults to 1.
* `per_page` - `number`. Specifies number of results per page. Defaults to 25, max of 100.

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

### GET /destinations/authorize\_url

Census now allows you to create OAuth destinations via our Management API using a two-endpoint flow. We support Salesforce, Hubspot, Zendesk, Pinterest, and LinkedIn but will be adding support for more OAuth destinations soon. Please contact support if you require support for another destination connection.

First, you will direct your user to begin the authorization flow by providing them the `authorization url` for a specific destination. You will request a destination’s authorization URL via this endpoint. After the user completes authorization in the destination, we will return the user to your provided `redirect_uri` with the `code`. You will then pass the `code` as `oauth_code` to our[#post-destinations](destinations.md#post-destinations "mention") and [#patch-destinations-id](destinations.md#patch-destinations-id "mention") to create or update an OAuth destination connection.

| Data Property       | Description                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type                | the type of OAuth destination                                                                                                                                                                                                                                                                                                                                                                      |
| redirect\_uri       | URL that we will redirect to after completing the authorization flow. This URL will contain a `code` parameter that you will use to create or update a destination. Note that `codes` can be used only once and some codes have an expiration period.                                                                                                                                              |
| \[other properties] | <p></p><p>Zendesk requires a <code>domain</code> value.</p><p>If you’d like to use Salesforce Sandbox (optional), you will have to pass an encoded state blob that contains <code>sandbox</code> set to <code>true,</code>i.e. <code>{ "sandbox": true }</code>. This base64 URL encoded and passed as a query param, would be <code>state=eyAic2FuZGJveCI6IHRydWUgfQ%3D%3D</code>            </p> |



| Response property | Description                                                                                                                                                                                                                                                                                                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| authorize\_url    | This is a url that you will provide the user which will begin the authorization flow authorization service for the given destination. The authorization flow, if successful, will return a `code` that you can use in our [#post-destinations](destinations.md#post-destinations "mention") and [#patch-destinations-id](destinations.md#patch-destinations-id "mention") |

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



| Connection Property | Description                                                                  |
| ------------------- | ---------------------------------------------------------------------------- |
| type                | `required`. The type of this destination (e.g. `zendesk`, `active_campaign`) |
| credentials         | `required`. See the `Credentials properties explained` table below           |
| name                | The name to assign to this destination                                       |

Credentials properties explained

<table><thead><tr><th width="377.3333333333333">Credentials property</th><th>Description</th></tr></thead><tbody><tr><td>oauth_code</td><td>Required for OAuth destinations. We support Hubspot, Salesforce and Zendesk. This is the <code>code</code> query param that you received after completing the authorization flow. The authorization flow can be initiated after retrieving the authorization url. Note that codes can be used only once and some codes have an expiration period.</td></tr><tr><td>[other properties]</td><td><p>Non-OAuth destinations require specific credential key values like e.g. <code>api_token</code>, <code>domain).</code></p><p><br>OAuth destinations may also require additional information to be passed in <code>credentials</code>. For example, Zendesk requires a <code>domain</code> value.</p><p></p><p>If you’d like to use Salesforce Sandbox, you will have to pass an encoded <code>state</code> string that contains set to true, i.e. <code>{ "sandbox": true }</code>. This encoded and passed in the</p><p>block would be <code>{ "state": "eyAic2FuZGJveCI6IHRydWUgfQ=="</code></p></td></tr><tr><td></td><td></td></tr></tbody></table>



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

| Connection Property | Description                                            |
| ------------------- | ------------------------------------------------------ |
| name                | The name to assign to this destination                 |
| credentials         | See the `Credentials properties explained` table below |

Credentials properties explained

| Credentials property | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| oauth\_code          | Required for OAuth destinations. We support Hubspot, Salesforce and Zendesk. This is the `code` query param that you received after completing the authorization flow. The authorization flow can be initiated after retrieving the authorization url. Note that codes can be used only once and some codes have an expiration period.                                                                                                                                                                                                                                                               |
| \[other properties]  | <p>Non-OAuth destinations require specific credential key values like e.g. <code>api_token</code>, <code>domain).</code></p><p><br>OAuth destinations may also require additional information to be passed in <code>credentials</code>. For example, Zendesk requires a <code>domain</code> value.</p><p></p><p>If you’d like to use Salesforce Sandbox, you will have to pass an encoded <code>state</code> string that contains set to true, i.e. <code>{ "sandbox": true }</code>. This encoded and passed in the</p><p>block would be <code>{ "state": "eyAic2FuZGJveCI6IHRydWUgfQ=="</code></p> |
|                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |



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

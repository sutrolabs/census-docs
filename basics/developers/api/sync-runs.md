# Sync Runs

### GET /syncs/\[ID]/sync\_runs

This endpoint returns info on the sync runs for a specific sync.

You can pass the following URL parameters to control the response:

* `order` - `asc` or `desc`. Sorts the results ascending or descending by creation time.
* `page` - `number`. Specifies which page of results to return. Defaults to 1.
* `per_page` - `number`. Specifies number of results per page. Defaults to 25.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/syncs/[ID]/sync_runs?page=1&per_page=1&order=asc' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
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
    ],
    "next": "https://app.getcensus.com/api/v1/syncs/52/sync_runs"
}
```
{% endtab %}
{% endtabs %}

### GET /sync\_runs/\[ID]

This endpoint returns information on a specific sync run.

{% tabs %}
{% tab title="Request" %}
```
curl 'https://app.getcensus.com/api/v1/sync_runs/[ID]' \
--header 'Authorization: Bearer [API_TOKEN]'
```
{% endtab %}

{% tab title="Response" %}
```json
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

| Data Properties            | Description                                                                                                                                                                                                                                                                                 |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                         | id of this sync run.                                                                                                                                                                                                                                                                        |
| sync\_id                   | id of the parent sync.                                                                                                                                                                                                                                                                      |
| status                     | <ul><li><code>working</code> if the sync is currently executing</li><li><code>completed</code> if the sync finished successfully</li><li><code>failed</code> if the sync failed during execution</li><li><code>skipped</code> if an earlier instance of the sync is still running</li></ul> |
| records\_processed         | Number of new or updated records retrieved from the source.                                                                                                                                                                                                                                 |
| records\_updated           | Number of records successfully sent to the destination.                                                                                                                                                                                                                                     |
| records\_invalid           | Number of records skipped by Census because of data quality issues.                                                                                                                                                                                                                         |
| records\_failed            | Number of records rejected by the destination.                                                                                                                                                                                                                                              |
| created\_at                | When this sync run was created.                                                                                                                                                                                                                                                             |
| updated\_at                | When this sync run was updated.                                                                                                                                                                                                                                                             |
| completed\_at              | When this sync run was completed.                                                                                                                                                                                                                                                           |
| scheduled\_execution\_time | When the sync run was scheduled to run.                                                                                                                                                                                                                                                     |
| error\_code                | The error code, if any.                                                                                                                                                                                                                                                                     |
| error\_message             | The error message, if any.                                                                                                                                                                                                                                                                  |
| error\_detail              | Details about the error, if any.                                                                                                                                                                                                                                                            |
| canceled                   | Whether or not this sync run was canceled.                                                                                                                                                                                                                                                  |
| full\_sync                 | Whether or not this was a full sync.                                                                                                                                                                                                                                                        |
| sync\_trigger\_reason      | Details on why this sync was run.                                                                                                                                                                                                                                                           |

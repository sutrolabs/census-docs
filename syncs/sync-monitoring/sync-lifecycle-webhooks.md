# Sync Lifecycle Webhooks

Sync Lifecycle Webhooks provide a way to connect external systems to Census to listen for events related to a sync lifecycle, including [Sync Alerts](alerts.md).  Webhooks can be configured in Workspace settings under the **Webhooks** tab.&#x20;

## Creating a Webhook

Configure a new webhook under the **Webhooks** tab by clicking **Add Webhook** and providing:

* **Name** - Required name for your webhook
* **Description** - Optional additional details or description for your webhook
* **Endpoint** - Required endpoint to which Census should send payloads to&#x20;
* **Events** - Subscribe to at least one of the supported events (See below)

Once you click **Create**, a one-time secret will be shown that you may use to validate the authenticity of the payloads you receive. Note that this secret will not be accessible later and it is recommended you make a copy of it.

<figure><img src="../../.gitbook/assets/Screenshot 2025-04-04 at 2.00.14 PM (1).png" alt=""><figcaption></figcaption></figure>

## Event Types

There are two main categories of events a webhook can subscribed to: sync alert events and sync run lifecycle events.

**Sync Alert Events**

1. **sync.alert.raised** - when any subscribed sync alert in your workspace is triggered
2. **sync.alert.resolved** - when any subscribed sync alert is resolved

**Sync Run Lifecycle Events**

1. **sync.triggered** - when a sync run has been queued
2. **sync.started** - when active work on the sync run has started
3. **sync.completed** - when the sync run has completed, for both succesful and failed sync runs
4. **sync.success** - when a sync run is completed successfully
5. **sync.failed** - when a sync run has failed

## Payload Fields and Examples

### Fields always present in the payload:

* workspace\_id
* sync\_id
* sync\_run\_id
* event

### Additional fields present by event type:

* **sync.completed**
  * status
* **sync.alert.raised** & **sync.alert.resolved**
  * alert\_instance\_id
  * alert\_type
  * message
  * details
  * followup\_url

### Payload Examples by Event

{% hint style="info" %}
Please note the ids and messages in the below payloads are merely examples and the values will vary based on your individual workspace and configured sync alerts
{% endhint %}

**sync.alert.raised**

```
{
    "workspace_id": 3167,
    "sync_id": 3167956,
    "sync_run_id": 324402082,
    "alert_instance_id": 626248,
    "alert_type": "FailureAlertConfiguration",
    "message": "Sync Failed",
    "details": "Sync has failed with error: A mapped source column has been del
    eted: email",
    "followup_url": "https://app.getcensus.com/workspaces/3167/syncs/316795
    6/sync-history",
    "event": "sync.alert.raised"
}
```

**sync.alert.resolved**

<pre><code>{
    "workspace_id": 3167,
    "sync_id": 3167956,
    "sync_run_id": 324403394,
<strong>    "alert_instance_id": 626248,
</strong>    "alert_type": "FailureAlertConfiguration",
<strong>    "message": "Sync Recovered",
</strong>    "details": "Sync has recovered",
<strong>    "followup_url": "https://app.getcensus.com/workspaces/3167/syncs/316795
</strong>    6/sync-history",
    "event": "sync.alert.resolved"
}
</code></pre>

**sync.triggered**&#x20;

<pre><code>{
<strong>    "workspace_id": 3167,
</strong>    "sync_id": 3167956,
    "sync_run_id": 324399613,
    "event": "sync.triggered"
}
</code></pre>

**sync.started**

```
{
    "workspace_id": 3167,
    "sync_id": 3167956,
    "sync_run_id": 324399613,
    "event": "sync.started"
}
```

**sync.completed**

```
{
    "workspace_id": 3167,
    "sync_id": 3167956,
    "sync_run_id": 324399613,
    "event": "sync.completed",
    "status": "ok"
}

If the sync run fails the status will be "emergency"

{
    "workspace_id": 3167,
    "sync_id": 3167956,
    "sync_run_id": 324402082,
    "event": "sync.completed",
    "status": "emergency"
}
```

**sync.success**

```
{
    "workspace_id": 3167,
    "sync_id": 3167956,
    "sync_run_id": 324399613,
    "event": "sync.success"
}
```

**sync.failed**&#x20;

```
{
    "workspace_id": 3167,
    "sync_id": 3167956,
    "sync_run_id": 324402082,
    "event": "sync.failed"
}
```

## Validating Webhook Payloads

To verify the webhook payloads your server receives are actually coming from Census, use the secret from the creation flow to validate each payload. Each payload will include a HMAC-SHA256 `X-Signature` header calculated using the payload and secret token.&#x20;

Example Python code for validating payloads:&#x20;

```python
import hmac
import hashlib
import base64

def validate_request(request):
    SECRET = b'<secret>' 

    raw_body = request.body  
    received_signature = request.headers.get('X-Signature')

    computed_signature = compute_hmac_signature(raw_body, SECRET)

    return hmac.compare_digest(received_signature, computed_signature)

def compute_hmac_signature(data, secret):
    digest = hmac.new(secret, data, hashlib.sha256).digest()
    return base64.b64encode(digest).decode()

```

## Retries

If your server does not respond with a 2xx status, Census will retry sending the payload up to 5 times. It will wait 4 seconds before retrying the first time, and increasing the wait time before the next retry. The chart below shows the delay between each retry.

| Retry | Delay Before Retry (in seconds) |
| ----- | ------------------------------- |
| 1     | 4.0                             |
| 2     | 8.0                             |
| 3     | 16.0                            |
| 4     | 32.0                            |
| 5     | 64.0                            |

&#x20;Additionally, each payload delivery has a timeout of 10 seconds. If the server does not respond within this time, it will be considered as a failed delivery.&#x20;

## Webhooks via API

See our [developer docs on managing webhooks through the API](https://developers.getcensus.com/api-reference/webhooks/list-webhooks).

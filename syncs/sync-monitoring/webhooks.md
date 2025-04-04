# Webhooks

If you need to listen to sync lifecycle events or when sync alerts are raised or resolved in your workspace, webhooks can be configured in Workspace settings under the **Webhooks** tab.&#x20;

## Event Types

There are two main types of events your webhook can be subscribed to: sync alert events and sync run lifecycle events.&#x20;

**Sync Alert Events**

1. **sync.alert.raised** - when any subscribed sync alert in your workspace is triggered
2. **sync.alert.resolved** - when any subscribed sync alert is resolved

**Sync Run Lifecycle Events**

1. **sync.triggered** - when a sync run has been queued
2. **sync.started** - when active work on the sync run has started
3. **sync.completed** - when the sync run has completed, for both succesful and failed sync runs
4. **sync.success** - when a sync run is completed successfully
5. **sync.failed** - when a sync run has failed

## Creating a Webhook

Configure a new webhook under the **Webhooks** tab by clicking **Add Webhook** and providing:

* **Name** - required name for your webhook
* **Description** - optional additional details or description for your webhook
* **Endpoint** - required endpoint to which Census should send payloads to&#x20;
* **Events** - subscribe to at least one of the supported events&#x20;

Once you click **Create**, a one-time secret will be shown that you may use to validate the authenticity of the payloads you receive. Note that this secret will not be accessible later and it is recommended you make a copy of it.

<figure><img src="../../.gitbook/assets/Screenshot 2025-04-04 at 2.00.14 PM (1).png" alt=""><figcaption></figcaption></figure>

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

## Webhooks via API

See our [developer docs on managing webhooks through the API](https://developers.getcensus.com/api-reference/webhooks/list-webhooks).

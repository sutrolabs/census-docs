---
description: Send data anywhere that accepts standard HTTP requests.
---

# HTTP Request

Overview

Our HTTP Request destination is a Swiss Army knife. It allows you to send data to any service that accepts standard HTTP requests—including standard SaaS APIs and internal systems—and only takes a few minutes to set up via our no-code interface.

To demonstrate how it works, let's look at a real-world example of [creating contacts in Brevo](https://developers.brevo.com/reference/createcontact) when new rows appear in your source data. If you want to follow along, you can create a new Brevo account [here](https://www.brevo.com/).

## Create a destination

* Navigate to the **Destinations** page in Census.
* Click **New Destination** and select **HTTP Request** from the menu.
* Name your destination and enter the **Base URL** for the Brevo API (https://api.brevo.com).
* [Generate a new API key in Brevo](https://app.brevo.com/settings/keys/api) and copy it to your clipboard.
* Click **Add Header**, name the header `api-key` (per Brevo's docs), paste your API key under **Value**, and check the box indicating it's a secret (this will hide it in our UI if you or anyone else attempts to edit this connection later on).
* Click **Connect** to continue.

<figure><img src="../.gitbook/assets/CleanShot 2023-09-25 at 17.00.14@2x (1).png" alt=""><figcaption><p>Create your HTTP Request destination.</p></figcaption></figure>

## Create a sync

Navigate to the **Syncs** page in Census and click **New Sync**.

### Select your source

In this example, we'll use data from a demo Redshift cluster but this could be any source that we support.

<figure><img src="../.gitbook/assets/CleanShot 2023-09-25 at 17.08.55@2x.png" alt=""><figcaption></figcaption></figure>

### Select your destination

Select the **HTTP Request** destination you just created and input the specific endpoint we'll be using to create contacts in Brevo.

<figure><img src="../.gitbook/assets/CleanShot 2023-09-25 at 17.14.00@2x.png" alt=""><figcaption></figcaption></figure>

Note: in this example, the endpoint is static (i.e. `/v3/contacts`), but we also support using the [Liquid](../basics/core-concept/liquid-templates.md)[ template](../basics/core-concept/liquid-templates.md) language to populate values dynamically. For example, if we were sending requests to update existing contacts, we might need to include contact IDs in the endpoint like this: `/v3/contacts/{{ record["id"] }}`.

### Choose your request trigger

Choose the trigger that you want Census to monitor in your source data.&#x20;

<figure><img src="../.gitbook/assets/CleanShot 2023-09-25 at 17.24.32@2x.png" alt=""><figcaption></figcaption></figure>

### Specify the number of records per request

Census allows you to either send one record at a time or batch records for better performance when the destination allows for it. In this case, we'll keep things simple and send one record at a time (which is also what this particular endpoint expects).

<figure><img src="../.gitbook/assets/CleanShot 2023-09-25 at 17.27.23@2x.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If you are using multiple records per request together with a JSON template payload, you will commonly need to use a Liquid `for` [loop](../basics/core-concept/liquid-templates.md#looping) like this using the special `records`:

```liquid
[
  {% raw %}
{% for record in records %}
  {
    "id": "{{ record['ID'] }}",
    "name": "{{ record['NAME'] }}"
  },
  {% endfor %}
{% endraw %}
]
```

The `records` will be set to an array containing all of the records to be sent in the current request.
{% endhint %}

### Select a sync key

This helps Census identify unique records in your source data.

<figure><img src="../.gitbook/assets/CleanShot 2023-09-25 at 17.30.21@2x.png" alt=""><figcaption></figcaption></figure>

### Choose a request method

Census supports all major HTTP request methods. In this case, the endpoint we're syncing to expects a POST request.

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

### Choose your payload type

We currently support the two most common payload types—empty and JSON. If you need more (e.g. XML, SOAP), please send us an email at support@getcensus.com!

This endpoint expects JSON, so we'll go with that.

<figure><img src="../.gitbook/assets/CleanShot 2023-09-25 at 17.32.57@2x.png" alt=""><figcaption></figcaption></figure>

### Define your payload

Census provides three different ways of defining a payload.

* **Template editor**: using the Liquid template language to define an entirely custom payload. This is the most flexible option but requires a bit of elbow grease. See our full documentation to [Liquid templates](../basics/core-concept/liquid-templates.md) for more information.
* **Single source column**: select a single column from your source data that contains the entire JSON payload you want to send.
* **Multiple source columns**: select multiple columns from your source data. Census will combine them into a JSON payload with each column represented as a top-level key-value pair.

We'll use the template editor for this example so we can construct a payload that exactly matches what the Brevo API expects.

<figure><img src="../.gitbook/assets/CleanShot 2023-09-25 at 17.49.11@2x.png" alt=""><figcaption></figcaption></figure>

### Configure rate limits

Brevo's contact endpoints have a rate limit of 10 requests per second (RPS). We can specify that here so that Census respects that limit when sending data.

<figure><img src="../.gitbook/assets/CleanShot 2023-09-25 at 17.39.02@2x.png" alt=""><figcaption></figcaption></figure>

### Save and run your sync :clap:

Once you've saved and run your sync, head over to the API Inspector tab in your sync configuration to confirm the data was sent as expected. In this case, it was and we can confirm the record made it to our contact list in Brevo!

<figure><img src="../.gitbook/assets/CleanShot 2023-09-25 at 18.10.51@2x.png" alt=""><figcaption></figcaption></figure>

## Error Handling

Census will use the HTTP response status code to determine whether records were accepted by the target service. Here is how various response status codes are interpreted:

* 2xx - Success. All records sent in the request were accepted by the destination.
* 4xx - Client failure in the batch. All records sent in the request were rejected by the destination. The sync will continue, but the records sent in the batch will be marked as rejected and reattempted next time the sync is run.
  * NOTE: a 429 status code will trigger up to 7 request retries with exponential backoff
* 5xx - Server failure. The request will be retried up to 7 times with exponential backoff. If the request is unsuccessful within 7 retries, the entire sync will be failed.

## Need help using HTTP Request?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation via the [in-app](https://app.getcensus.com) chat.


---
description: >-
  This page describes how to setup and start using your own HTTP Request source
  to power Census syncs.
---

# HTTP Request

## Background

For certain usecases, the HTTP Request source is the easiest way of getting data to Census for activation. If you have a web application that is generating events or are tracking web events via a service like Segment or Jitsu, you can easily forward them via a webhook to Census and then route them to any [supported destination](available-sources/broken-reference/).

## Initial Setup

Setting up the HTTP Request source is super simple:

* Open Census and navigate to the **Sources** page.
* Click **New Source** and select **HTTP Request** from the list.
* On the next screen hit **Connect** to confirm.
* That's it! Now you'll just need to create a **Topic** to start syncing data. See [#next-steps](http-request.md#next-steps "mention").

## Next Steps

### Creating a Topic

Instead of being organized in schemas and tables like a traditional Census source, the HTTP Request source allows you to create **Topics** to keep your unique categories of data separate when pushing data to Census. A Topic could be something like web-events, user-updates,

1. Navigate to the **Datasets** page
2. Select the **HTTP Request** source you just created and hit **New Topic.**
3. Give your Topic a **Name** and paste in a **sample event** that you'll be sending to Census on this Topic. We'll use this sample event to determine the schema of events. This is important so that we know what properties are available when creating syncs.
4. Hit **Save Topic.**

<figure><img src="../.gitbook/assets/screenshot 2024-03-19 at 11.26@2x.png" alt="" width="563"><figcaption><p>An example of a Web Event topic configured with a sample message.</p></figcaption></figure>

{% hint style="info" %}
Note that for programmatic usecases HTTP Topics can also be managed via the [Census Management API](https://developers.getcensus.com/api-reference/topics/create-a-new-topic).
{% endhint %}

### Pushing Data

With the [Census API](https://developers.getcensus.com/api-reference/sources/http-request-source-events), you can now `POST` data to the specified Topic via your HTTP Request source. This sample `curl` command demonstrates the basic use of our API. Remember to replace the placeholder values with your actual HTTP Request Source ID, topic name, workspace API token, and event payload. Depending on your event source, you might need to set up a webhook through a web interface or modify your application code to make the request.

```bash
curl --request POST \
  --url https://app.getcensus.com/api/v1/sources/{source_id}/topics/{topic_name}/events \
  --header 'Authorization: Bearer <token>' \
  --header 'Content-Type: application/json' \
  --data '{json_event_data}'
```

## Need help using our HTTP Request Source?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.

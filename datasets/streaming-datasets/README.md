---
description: >-
  Streaming Datasets allow you to define the data you work with in streaming
  sources that organize their data into topics to which new messages are
  published over time.
---

# Streaming Datasets

Streaming datasets enable real-time data activation in Census, allowing you to sync data with low latency to your business applications. Unlike traditional batch-based datasets, streaming datasets continuously process data as it arrives, making them ideal for time-sensitive use cases.

## Getting Started

### Connect a Streaming Source

Before you create a Streaming Dataset, you’ll need to connect a streaming source. See individual source documentation:

* [Kafka](../sources/available-sources/kafka.md)
* [Confluent Cloud](../sources/available-sources/confluent-cloud.md)
* [Google Pub/Sub](../sources/available-sources/google-pubsub.md)
* [HTTP Request](../sources/available-sources/http-request.md)

Once your streaming source is connected, open **Datasets** and click **New Dataset**. Select **Streaming Dataset** and click **Next**.

### Create a Streaming Dataset

To create a new streaming dataset:

1. Navigate to the Datasets section in Census
2. Click "New Dataset" and select "Streaming Dataset"
3. Choose your streaming connection (Kafka, Confluent Cloud, etc.)
4. Add a Sample Message (see below)

### Add a Sample Message

In the code editor on the right side of the new dataset dialog, enter a sample JSON message for your new Streaming Dataset. Census will use the sample message you provide to infer the fields and data types of the messages in your dataset.

{% hint style="warning" %}
Census does not treat sample messages as customer data, and they are stored with the rest of your organization’s metadata in Census’s US-based control plane. **Do not include real customer data or PII in your sample message.**
{% endhint %}

When you are finished configuring your new Streaming Dataset, click **Create Dataset**.

## Key Features of Streaming Datasets

### Real-time Processing

Streaming datasets process data continuously as it arrives, enabling:

* Ultra-low latency from data creation to activation
* Immediate reactions to customer behavior or system events
* Real-time personalization and engagement opportunities

### Event-based Architecture

Unlike traditional datasets that operate on tables or views, streaming datasets work with events:

```json
// Example event from a Kafka topic
{
  "event_id": "evt_12345",
  "user_id": "usr_789",
  "event_type": "page_view",
  "page_url": "https://example.com/products/123",
  "timestamp": "2023-06-15T14:22:31Z",
  "session_id": "sess_456",
  "device": "mobile",
  "browser": "chrome"
}
```

### On-the-fly Transformations with Liquid Templates

When activating streaming datasets through syncs, you can apply real-time transformations using Liquid Templates. This powerful feature allows you to:

* Transform data structure and format on-the-fly without modifying the source
* Apply conditional logic to determine what data gets sent to destinations
* Format dates, numbers, and strings to match destination requirements
* Combine multiple fields or extract specific parts of fields
* Create dynamic content based on event properties

For example, you can use a Liquid Template to create a personalized message from a streaming event:

```liquid

<div data-gb-custom-block data-tag="if" data-0='cart_abandon' data-1='cart_abandon'>

  Hi {{ event.user_name }}, we noticed you left some items in your cart. 
  Use code COMEBACK15 for 15% off your purchase of {{ event.product_name }}.

<div data-gb-custom-block data-tag="elsif" data-0='product_view' data-1='product_view'></div>

  Hi {{ event.user_name }}, interested in {{ event.product_name }}? 
  Check out our latest collection!

</div>
```

These transformations happen in real-time as events flow through Census, allowing you to customize and enrich your data without adding latency to your streaming pipeline.

## Use Cases for Streaming Datasets

<details>

<summary>Real-time Customer Engagement</summary>

Streaming datasets enable you to respond to customer actions the moment they happen:

* Trigger immediate follow-up messages when a customer abandons a cart
* Send personalized product recommendations based on browsing behavior
* Update customer segments in real-time based on website or app interactions
* Personalize website experiences based on just-observed actions
* Deliver timely notifications when customers meet specific criteria
* Initiate onboarding sequences the moment a user signs up

</details>

<details>

<summary>Operational Alerting</summary>

Keep your teams informed about critical events as they happen:

* Send notifications to sales teams when high-value prospects take specific actions
* Alert customer success teams when users encounter errors or get stuck
* Notify support teams about potential service disruptions
* Update dashboards in real-time with system performance metrics
* Trigger escalations when SLA thresholds are approached
* Monitor security events and respond to potential threats immediately

</details>

<details>

<summary>Time-sensitive Data Updates</summary>

Ensure your systems stay in sync with minimal delay:

* Keep inventory systems updated across platforms to prevent overselling
* Update pricing information across multiple channels simultaneously
* Propagate user preference changes immediately across all systems
* Sync subscription status changes to prevent access issues
* Update account balances or usage metrics in near real-time
* Reflect order status changes across customer-facing applications

</details>

<details>

<summary>Event-driven Workflows</summary>

Build sophisticated workflows that respond to events as they occur:

* Trigger fulfillment processes when orders are placed
* Initiate verification steps when suspicious activity is detected
* Start onboarding workflows when new accounts are created
* Launch re-engagement campaigns when usage drops below thresholds
* Activate loyalty rewards when qualifying actions are completed
* Coordinate cross-channel marketing based on customer interactions

</details>

## Live Syncs

Streaming datasets are designed to work with Census Live Syncs, which provide continuous data activation:

* **Always On** - Census monitors your streaming source 24/7
* **Immediate Processing** - Data is processed and synced as soon as it arrives
* **Efficient Resource Usage** - Only changed data is processed and synced

## Best Practices for Streaming Datasets

Working with streaming data is different from batch processing. Here are some tips to help you get the most out of your streaming datasets:

* **Include timestamps in your events** to ensure proper ordering and enable time-based processing
* **Add unique identifiers** to each event to prevent duplicate processing and enable idempotent operations
* **Filter events at the source** when possible to reduce unnecessary data transfer and processing
* **Keep your events focused** by including only the data you need for your use cases
* **Set up monitoring** for stream lag and processing delays to catch issues early
* **Create alerts** within Census to detect anomalies
* **Plan for schema evolution** by designing flexible event structures that can accommodate new fields
* **Use Liquid Templates** for on-the-fly transformations rather than modifying your event sources

Remember that streaming datasets are designed for real-time use cases. If you don't need sub-minute latency, consider using basic datasets with scheduled syncs instead, which may be more cost-effective for your use case.

For more information on using streaming datasets with Live Syncs, see our [Live Syncs documentation](../syncs/core-concept/live-syncs.md).

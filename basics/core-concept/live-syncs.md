---
description: Activate Streaming Datasets in Real-time with Live Syncs
---

# Live Syncs

Live Syncs are a type of sync that enable **real-time data activation**. In comparison with traditional "Triggered" syncs, they can provide single-second latency in activating data into a destination. Live syncs are available on our Enterprise plan. While a Live Sync is enabled, Census continually monitors the Source connection, ensuring that any new data is instantly captured and activated.

Live Syncs are available for sources capable of streaming data, such as [Confluent Cloud](../../sources/confluent-cloud.md), [Kafka](../../sources/available-sources/kafka.md), [Materialize](../../sources/materialize.md), [HTTP Requests](../../sources/available-sources/http-request.md), [Snowflake](../../sources/snowflake.md), and [Databricks](../../sources/databricks.md)\*. Please feel free to [request a new integration](https://www.getcensus.com/request-an-integration?hsCtaTracking=a5c60288-2577-4ade-8fc6-e453ba20cd0d%7C5f94cdfe-1f8f-457f-8e34-80e2af1c9fb2) if your streaming infrastructure is not yet supported.

\* Coming soon. Email support@getcensus.com to be added to the private preview.

{% hint style="warning" %}
At this time, a sync's Run Mode (Live vs Triggered) cannot be changed after the sync has been created.
{% endhint %}

The following table summarizes the key differences between a Live and Triggered sync.



| Live                                          | Triggered                                                                                                               |
| --------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Census monitors the source 24/7 automatically | Can be run manually, on a schedule, or via external triggers. See [triggering-syncs.md](triggering-syncs.md "mention"). |
| Only streaming-capable sources are supported  | All Source connections supported                                                                                        |
| Activates data as it changes                  | Activates records in batches                                                                                            |
| Single-second latency                         | Minimum latency at least a few minutes                                                                                  |



<figure><img src="../../.gitbook/assets/screenshot 2024-01-11 at 12.16.png" alt=""><figcaption><p>Setting up the Run Mode for a new Sync</p></figcaption></figure>

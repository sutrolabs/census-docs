# Sync Logs

## 🗄️ What are Sync Logs?

Census can provide granular details on the data you've sent from your data warehouse to destination SaaS applications like Salesforce or Iterable. With these logs, you can answer common questions like:

1. When was my data updated in the destination?
2. Why did the destination's API reject records that I tried to sync?
3. What is the most common reason that the destination's API rejects my data?

{% hint style="warning" %}
At this time, Sync Logs are automatically accessible for Platform Plan accounts. If you would like logging enabled and are not on the Platform Plan, please contact Census Support at support@getcensus.com.
{% endhint %}

## :ballot\_box: Which sources support logging?

Census can provide detailed logging for all data warehouse sources:

* Snowflake
* BigQuery
* Redshift
* PostgreSQL (version 13 or later is required)

## 🧮 Log Data

#### Where can I find the logs?

Census exposes detailed logging information in a view called `sync_log` in your data warehouse. By warehouse, this view can be found as follows:

* **Snowflake**: `CENSUS.CENSUS.SYNC_LOG`
* **BigQuery:** `census.sync_log`
* **Redshift:** `census.sync_log`
* **PostgreSQL**: `census.sync_log`

#### How much log data is stored?

Census will store the previous 7 days of logs in the `sync_log` view.

{% hint style="info" %}
Need data stored for longer? Please reach out at support@getcensus.com.
{% endhint %}

#### What do the columns of the view mean?

| column                   | column description                                                                                                                                                                                |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| log\_id                  | Unique identifier for the log                                                                                                                                                                     |
| sync\_id                 | <p>Unique identifier for the sync configuration. You can find it in the URL of your sync configurations as follows:</p><p>https://app.getcensus.com/syncs/<strong>[sync_id]</strong>/overview</p> |
| sync\\\_run\\\_\_\_id    | Unique identifier for the sync run. Use this value to identify a particular occasion when Census sends data as specified for a given sync configuration.                                          |
| record\_identifier       | The value of the identifier specified in your sync configuration, identifying _which_ record in your source you are trying to send to a destination.                                              |
| record\_payload          | The exact data that Census was attempting to send to a given destination. It is formatted as a JSON object.                                                                                       |
| batch\\\_started\\\_at   | The time when the batch containing this data was sent to the destination.                                                                                                                         |
| batch\\\_completed\\\_at | The time when the batch containing this data completed.                                                                                                                                           |
| operation                | The operation performed by Census. Either: 'upsert', 'update', 'create', or 'delete'... depending on the sync behavior you specified.                                                             |
| status                   | Either 'succeeded' or 'rejected'                                                                                                                                                                  |
| status\_message          | If the status is 'rejected', this field will contain the reason returned by the destination's API.                                                                                                |
| \_census\\\_logged\\\_at | When Census loaded this log record into your data warehouse.                                                                                                                                      |

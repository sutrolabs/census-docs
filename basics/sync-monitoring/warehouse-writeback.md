# Warehouse Writeback

Census can provide row-level details on the data you're syncing to a destination. With these logs, you can answer common questions like:

1. When was my data updated in the destination?
2. Why did the destination's API reject records that I tried to sync?
3. What is the most common reason that the destination's API rejects my data?
4. Which users were a member of this segment at this time?

{% hint style="info" %}
Warehouse Writeback is available for Enterprise Plan accounts. If you would like logging enabled please contact our team at [support@getcensus.com](mailto:support@getcensus.com).
{% endhint %}

## :ballot\_box: Supported data sources

Census can provide detailed logging for all data warehouse sources using the [Advanced Sync Engine](https://docs.getcensus.com/sources/overview#sync-engines):

* Snowflake
* BigQuery
* Redshift
* PostgreSQL (version 13 or later is required)
* Databricks

## 🖥️ Configuring Warehouse Writeback

To enable Warehouse Writeback on a supported source connection:

1. Visit the [Sources page](https://app.getcensus.com/sources).
2. Click **+ New Source** to create a new source connection, or click **Edit** on an existing source connection.
3. Toggle on Warehouse Writeback
4. Optionally, specify how long logs should be retained for (7 days by default). Census will automatically clean up logs after the specified number of days.

<figure><img src="../../.gitbook/assets/Warehouse Writeback.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Please note Census will only clean up the Warehouse Writeback tables according to the retention period for Active syncs. Census will not make any changes or delete logs for syncs that have been Disabled or Deleted.
{% endhint %}

That's it! Logs will start populating for all syncs in this connection on their subsequent runs.

## 🧮 Log Data

Census exposes detailed logging information in a view called `sync_log` in your data warehouse. By warehouse, this view can be found as follows:

* **Snowflake**: `CENSUS.CENSUS.SYNC_LOG`
* **BigQuery:** `census.sync_log`
* **Redshift:** `census.sync_log`
* **PostgreSQL**: `census.sync_log`
* **Databricks**: `census.census.sync_log`

#### `sync_log` View Schema

<table><thead><tr><th width="225">Column</th><th>Description</th></tr></thead><tbody><tr><td>log_id</td><td>Unique identifier for the log</td></tr><tr><td>sync_id</td><td><p>Unique identifier for the sync configuration. You can find it in the URL of your sync configurations as follows:</p><p>https://app.getcensus.com/syncs/<strong>[sync_id]</strong>/overview</p></td></tr><tr><td>sync_run_id</td><td>Unique identifier for the sync run. Use this value to identify a particular occasion when Census sends data as specified for a given sync configuration.</td></tr><tr><td>record_identifier</td><td>The value of the identifier specified in your sync configuration, identifying <em>which</em> record in your source you are trying to send to a destination.</td></tr><tr><td>record_payload</td><td>The exact data that Census was attempting to send to a given destination. It is formatted as a JSON object.</td></tr><tr><td>batch_started_at</td><td>The time when the batch containing this data was sent to the destination.</td></tr><tr><td>batch_completed_at</td><td>The time when the batch containing this data completed.</td></tr><tr><td>operation</td><td>The operation performed by Census. Either: 'upsert', 'update', 'create', or 'delete'... depending on the sync behavior you specified.</td></tr><tr><td>status</td><td>Either 'succeeded' or 'rejected'</td></tr><tr><td>status_message</td><td>If the status is 'rejected', this field will contain the reason returned by the destination's API.</td></tr><tr><td>_census_logged_at</td><td>When Census loaded this log record into your data warehouse.</td></tr><tr><td>destination_id</td><td>Unique identifier for the destination (i.e. service) connection that this sync is writing to.</td></tr><tr><td>destination_object_id</td><td>Unique identifier for the destination (i.e. service) object that this sync is writing to.</td></tr><tr><td>source_id</td><td>Unique identifier for the source connection (e.g. your warehouse) that this sync is sending data from.</td></tr><tr><td>source_object_id</td><td>Unique identifier for the specific object in the source connection that this sync is sending data from. This could be a table, model, entity, or segment.</td></tr></tbody></table>

{% hint style="warning" %}
The `destination_id`, `destination_object_id`, `source_id`, and `source_object_id` columns are not yet supported when using Warehouse Writeback with Databricks.
{% endhint %}

## Metadata Tables

In addition to row level sync logs, Warehouse Writeback will create metadata tables about source objects and destinations involved in syncs. These tables can be joined to the `sync_log` table on their `id` column in order to add additional context.

For example, imagine you have a mirror sync from a [Segment](../audience-hub/syncing-segments.md) to an ads destination like Google. The `sync_log` table will log attempts to send new records (i.e. those that entered the segment) to the destination. It will also log attempts to delete records (i.e. those that left the segment) from the destination. If you join those logs with the source objects table (described below) you can get full insight into who is entering and leaving what segments, by name, and when.

{% hint style="info" %}
Metadata Tables are refreshed every six hours, separate from sync runs history. That means you may see a delay on records appearing in metadata for syncs that are using brand new sources or destinations.&#x20;
{% endhint %}

### Source Objects Table

Source objects are tables, models, entities, or segments. These are what you send data from during a sync. Continue reading the [schema section](warehouse-writeback.md#schema) below for more information.

#### Where

Metadata tables for source objects can be found in the following tables, by warehouse:

* **Snowflake**: `CENSUS.CENSUS.SOURCE_OBJECTS`
* **BigQuery:** `census.source_objects`
* **Redshift:** `census.source_objects`
* **PostgreSQL**: `census.source_objects`
* **Databricks**: not yet supported

#### Schema

<table><thead><tr><th width="198">Column</th><th width="549.3333333333333">Description</th></tr></thead><tbody><tr><td>id</td><td>Unique identifier for the source object. This joins to the <code>source_object_id</code> column in the <code>sync_log</code> table.</td></tr><tr><td>type</td><td>Type of data set. The options with their meaning are:<br>- <code>DataWarehouse::FilterSegmentSource</code> -> A segment<br>- <code>DataWarehouse::Query</code> -> A model<br>- <code>DataWarehouse::BusinessObjectSource</code> -> An entity<br>- <code>DataWarehouse::Table</code> -> A table</td></tr><tr><td>name</td><td>Name of the data set.</td></tr><tr><td>model_id</td><td>For a source object with type <code>DataWarehouse::Query</code>, this points to the SQL, Looker, or dbt model associated with it.<br><br>The model is what you see in the Census UI and is what is responsible for storing a SQL query, dbt reference, etc. The <code>DataWarehouse::Query</code> source object lives between the model and your source and is responsible for translating the model definition into rows and columns.</td></tr><tr><td>business_object_id</td><td>For a source object with type <code>DataWarehouse::BusinessObjectSource</code>, this points to the entity associated with it.<br><br>The entity is what you see in the Census UI and is what you configure to fit your business needs. The <code>DataWarehouse::BusinessObjectSource</code> source object lives between the entity and your source and is responsible for translating the entity definition into rows and columns.</td></tr><tr><td>filter_segment_id</td><td>For a source object with type <code>DataWarehouse::FilterSegmentSource</code>, this points to the segment associated with it.<br><br>The segment is what you see in the Census UI and is where you configure conditional logic to segment your data. The <code>DataWarehouse::FilterSegmentSource</code> source object lives between the segment and your source and is responsible for translating the segment definition into rows and columns.</td></tr></tbody></table>

### Destinations Table

Destinations are where you send data during a sync. An example is Salesforce.

#### Where

Metadata tables for destinations can be found in the following tables, by warehouse:

* **Snowflake**: `CENSUS.CENSUS.DESTINATIONS`
* **BigQuery:** `census.destinations`
* **Redshift:** `census.destinations`
* **PostgreSQL**: `census.destinations`
* **Databricks**: not yet supported

#### Schema

<table><thead><tr><th width="108">Column</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>Unique identifier for the destination. This joins to the <code>destination_id</code> column in the <code>sync_log</code> table.</td></tr><tr><td>type</td><td>Type of the destination. This can be any of the various destinations we support, in the format <code>&#x3C;Destination name>::Connection</code></td></tr><tr><td>name</td><td>Name of the destination.</td></tr></tbody></table>

### Destination Objects Table

Destination objects are the specific objects within a destination that you send data to during a sync. An example is a Salesforce Contact.

#### Where

Metadata tables for destinations can be found in the following tables, by warehouse:

* **Snowflake**: `CENSUS.CENSUS.DESTINATION_OBJECTS`
* **BigQuery:** `census.destination_objects`
* **Redshift:** `census.destination_objects`
* **PostgreSQL**: `census.destination_objects`
* **Databricks**: not yet supported

#### Schema

<table><thead><tr><th width="128">Column</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>Unique identifier for the destination object. This joins to the<code>destination_object_id</code> column in the <code>sync_log</code> table.</td></tr><tr><td>type</td><td>Type of the destination object. This can be any of the various destination objects we support, in the format <code>&#x3C;Destination name>::ObjectTypes::&#x3C;Destination object name></code></td></tr><tr><td>name</td><td>Name of the destination object.</td></tr></tbody></table>

## Example SQL Queries

Here are a few examples of SQL queries you can use as starting point to explore your logged data once Warehouse Writeback has been enabled.

For example, you may want to see all rows that have been synced by a specific sync configuration ID. You can find it in the URL of your sync configurations as follows: https://app.getcensus.com/syncs/**\[sync\_id]**/overview. For this example, we'll look at Sync ID **1234**.

```sql
SELECT * 
FROM CENSUS.CENSUS.SYNC_LOG log
LEFT JOIN CENSUS.CENSUS.SOURCE_OBJECTS source
ON log.source_object_id = source.id
WHERE log.sync_id = 1234;
```

The [Sync History](../core-concept/) page also includes an ID for each sync run which allows you to limit the query to that run. For example, if you'd like to see records that Census deleted on a recent sync run **5678**,

```sql
SELECT * 
FROM CENSUS.CENSUS.SYNC_LOG log 
LEFT JOIN CENSUS.CENSUS.SOURCE_OBJECTS source 
ON log.source_object_id = source.id
WHERE log.sync_run_id = 5678
  AND log.operation = 'delete';
```

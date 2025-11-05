# Sync Tracking

Sync Tracking provides row-level observability into every sync run, along with the ability to

* **Filter** to view invalid or rejected records
* **Search** for a particular record by its by primary identifier
* **Download** samples of the records

To use Sync Tracking, navigate to the [sync-history.md](sync-history.md "mention") page on the relevant sync. If a sync run falls within the 14-day retention period, a "View Records" button will be available. Click this button to open up the Sync Tracking modal and access detailed record information.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

For each record, Census will display

* The primary identifier
* Its status (Invalid, Rejected, or Success)
* The error reason, if applicable
* The source record payload that was processed

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Reporting and Analysis

You can also choose to store Sync Tracking data yourself. This gives you to direct access to your sync tracking data, enabling custom analysis from your  (and also allows you to retain sync tracking data for longer periods of time).&#x20;

To access sync tracking data, follow the instructions in the [Bring Your Own Bucket documentation](https://docs.getcensus.com/misc/security-and-privacy/bring-your-own-blob-storage). Once you configure your own bucket, **Census will automatically use it as storage for all sync run logging going forward.** This data will be maintained permanently in your bucket unless you've specified your own retention policy.

{% hint style="info" %}
Note that this data structure format applies to data written today but may change in the future.
{% endhint %}

Sync Tracking data is updated in batches while a sync is in progress. Census's sync engine processes records in batches of 10-100k. Sync Tracking data will update as each batch is finished processing.

Sync Tracking is not currently available for [Sync Dry Runs](sync-dry-runs.md).

### Sync Run Folder Structure

Sync Tracking data is organized into folders representing each individual sync runs within a hierarchical path.

`s3://[your_bucket]/sync_tracking_datasets/[ORG_ID]/[SYNC_ID]/[SYNC_RUN_ID]/`

Each sync run contains several files:

1. One or more parquet files logging each individual row.
2. A metadata file describing the configuration of the sync itself.

#### Synced Records Logs&#x20;

Sync record data is stored in one or more parquet files of the format  `[batch_type].[batch_number].parquet`, for example `records_updated.0.parquet`. Though there are different batch type prefixes, all files will have the same set of columns and can be joined together.

All files share the same schema so that they can be combined and queried. Sync tracking data includes the following columns:

| Column Name        | Description                                                                                                                                                                                                                                                       |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| identifier         | The value of the sync key for this particular record                                                                                                                                                                                                              |
| record\_payload    | The full record payload extracted from the source as a JSON blob. This is not 1:1 with the data sent to the destination as this data can be conditional applied to the destination                                                                                |
| operation          | In most cases, this is the [sync's behavior](broken-reference) (`update`, `upsert`, `delete`, `append`). Mirror syncs in most cases will be separated into `upsert` vs `delete` operations, though file system and Sheets will continue to use `mirror` operator. |
| status             | `succeeded`, `rejected`, `NULL`, or `DUPLICATE` (the latter two are invalid data checks automatically performed by Census before attempting to sync)                                                                                                              |
| status\_message    | the error message if it was rejected                                                                                                                                                                                                                              |
| batch\_started\_at | Timestamp when Census started sending the batch of records                                                                                                                                                                                                        |
| batch\_ended\_at   | Timestamp finished sending the batch of records                                                                                                                                                                                                                   |

#### Metadata

In addition to the parquet files containing row-level sync tracking data, Census writes a `metadata.json` file in the same path. This file includes sync run metadata:&#x20;

* Organization ID
* Workspace ID
* Sync Configuration ID
* Sync Run ID
* Source and Destination type and IDs
* Sync Run start time
* Record Payload Schema which maps field names in the record\_payload column of the data to their JSON types (string, number, boolean, array)

Use this metadata alongside your sync tracking parquet files to understand the schema and configuration details for each sync run, similar to the metadata tables available in [Warehouse Writeback](warehouse-writeback.md).

### Fact Tables

In addition to row level sync logs, Sync Tracking will create fact tables about source objects and destinations involved in syncs. These tables will appear in the following path as individual parquet files:

`s3://[your_bucket]/metadata/[ORG_ID]/`

{% hint style="info" %}
Fact Tables are refreshed every six hours, separate from sync runs history. That means you may see a delay on records appearing in metadata for syncs that are using brand new sources or destinations.
{% endhint %}

#### Source Objects Table

Source objects are tables, models, datasets, or segments. These are what you send data from during a sync. Continue reading the [schema section](sync-tracking.md#schema) below for more information.

<table><thead><tr><th width="198">Column</th><th width="549.3333333333333">Description</th></tr></thead><tbody><tr><td>id</td><td>Unique identifier for the source object. This joins to the <code>source_object_id</code> column in the <code>sync_log</code> table.</td></tr><tr><td>type</td><td>Type of data set. The options with their meaning are:<br>- <code>DataWarehouse::FilterSegmentSource</code> -> A segment<br>- <code>DataWarehouse::CohortSource</code> -> A cohort<br>- <code>DataWarehouse::Query</code> -> A model<br>- <code>DataWarehouse::BusinessObjectSource</code> -> An entity<br>- <code>DataWarehouse::Table</code> -> A table</td></tr><tr><td>name</td><td>Name of the data set.</td></tr><tr><td>model_id</td><td>For a source object with type <code>DataWarehouse::Query</code>, this points to the SQL, Looker, or dbt model associated with it.<br><br>The model is what you see in the Census UI and is what is responsible for storing a SQL query, dbt reference, etc. The <code>DataWarehouse::Query</code> source object lives between the model and your source and is responsible for translating the model definition into rows and columns.</td></tr><tr><td>business_object_id</td><td>For a source object with type <code>DataWarehouse::BusinessObjectSource</code>, this points to the Dataset associated with it. The Dataset (which is called a businessObject internally) </td></tr><tr><td>filter_segment_id</td><td>For a source object with type <code>DataWarehouse::FilterSegmentSource</code>, this points to the segment associated with it. The segment is what you see in the Census UI and is where you configure conditional logic to segment your data. </td></tr><tr><td>cohort_id</td><td>For a source object with type <code>DataWarehouse::CohortSource</code>, this points to the segment experiment cohort associated with the sync. The cohort is the subset of a segment created when running an experiment.</td></tr></tbody></table>

#### Destinations Table

Destinations are where you send data during a sync. An example is Salesforce.

<table><thead><tr><th width="108">Column</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>Unique identifier for the destination. This joins to the <code>destination_id</code> column in the <code>sync_log</code> table.</td></tr><tr><td>type</td><td>Type of the destination. This can be any of the various destinations we support, in the format <code>&#x3C;Destination name>::Connection</code></td></tr><tr><td>name</td><td>Name of the destination.</td></tr></tbody></table>

#### Destination Objects Table

Destination objects are the specific objects within a destination that you send data to during a sync. An example is a Salesforce Contact.

<table><thead><tr><th width="128">Column</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>Unique identifier for the destination object. This joins to the<code>destination_object_id</code> column in the <code>sync_log</code> table.</td></tr><tr><td>type</td><td>Type of the destination object. This can be any of the various destination objects we support, in the format <code>&#x3C;Destination name>::ObjectTypes::&#x3C;Destination object name></code></td></tr><tr><td>name</td><td>Name of the destination object.</td></tr></tbody></table>

### Querying

Because Sync Tracking data is stored as simple parquet files, you can query them in groups. For example, you can use `duckdb` to find all records that have failed and group by error message (Note: you'll need to grant access `duckdb` access to your object storage separately)

```
SELECT status_message, ARRAY_AGG(identifier) AS rejected_records
FROM read_parquet('s3://your_bucket/sync_tracking_datasets/1/2/3/*.parquet', union_by_name=True)
WHERE status = 'rejected'
GROUP BY 1
```

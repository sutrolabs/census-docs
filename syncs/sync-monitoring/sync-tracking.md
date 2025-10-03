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

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Availability

Sync Tracking data is updated in batches while a sync is in progress. Census's sync engine processes records in batches of 10-100k. Sync Tracking data will update as each batch is finished processing.

By default, Census will retain row-level logs and make them available to you for 14 days. If you would like to retain for longer, see the details on Observability Lake below.

Sync Tracking is not currently available for [Live Syncs](broken-reference) or [Sync Dry Runs](sync-dry-runs.md).

## Observability Lake Data Schema

Enabling [Observability Lake](observability-lake.md) allows you to customize retention for your sync tracking data. You can also query the Sync Tracking directly from your preferred compute environment.

{% hint style="info" %}
Note that this data structure format applies to data written today but may change in the future.
{% endhint %}

### File structure

Sync Tracking data for each sync run is stored across 1 or more parquet files within a hierarchical path.

`s3://[your_bucket]/sync_tracking_datasets/[ORG_ID]/[SYNC_ID]/[SYNC_ID]/`

The files within this path will look like `[batch_type].[batch_number].parquet`, for example `records_updated.parquet`. Though there are different batch type prefixes, all files will have the same set of columns and can be joined together.

### Data structure

All files share the same schema so that they can be combined and queried. Sync tracking data includes the following columns:

| Column Name                          | Description                                                                                                                                                                                                                                                       |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| census\_sync\_tracking\_internal\_id | An internal Census ID that is used to uniquely identify each row                                                                                                                                                                                                  |
| identifier                           | The value of the sync key for this particular record                                                                                                                                                                                                              |
| record\_payload                      | The full record payload extracted from the source as a JSON blob. This is not 1:1 with the data sent to the destination as this data can be conditional applied to the destination                                                                                |
| operation                            | In most cases, this is the [sync's behavior](broken-reference) (`update`, `upsert`, `delete`, `append`). Mirror syncs in most cases will be separated into `upsert` vs `delete` operations, though file system and Sheets will continue to use `mirror` operator. |
| status                               | `succeeded`, `rejected`, `NULL`, or `DUPLICATE` (the latter two are invalid data checks automatically performed by Census before attempting to sync)                                                                                                              |
| status\_message                      | the error message if it was rejected                                                                                                                                                                                                                              |
| batch\_started\_at                   | Timestamp when Census started sending the batch of records                                                                                                                                                                                                        |
| batch\_ended\_at                     | Timestamp finished sending the batch of records                                                                                                                                                                                                                   |

### Querying

Because Sync Tracking data is stored as simple parquet files in your Observability Lake, you can query them in groups. For example, you can use duckdb to find all records that have failed and group by error message (Note: you'll need to grant access duckdb access to your object storage separately)

```
SELECT status_message, ARRAY_AGG(identifier) AS rejected_records
FROM read_parquet('s3://your_bucket/sync_tracking_datasets/1/2/3/*.parquet', union_by_name=True)
WHERE status = 'rejected'
GROUP BY 1
```

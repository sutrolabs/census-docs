# General Object Storage

The data stored in General Object Storage includes

* Snapshots of the data you sync using Basic Sync Engine
* [sync-tracking.md](../../syncs/sync-monitoring/sync-tracking.md "mention") logs of the data you sync
* Temporary files used to load and unload data

By default, this data is stored in Census-provided object storage in your workspace’s region. Census uses Amazon S3 for all General Object Storage needs, with the exception of GCS for temporary files used by BigQuery warehouse connections.&#x20;

You may also choose to [use your own object storage provider](bring-your-own-bucket/). This allows Census to manage data on your behalf, while also maintaining strong guarantees that your data at rest is stored within your cloud.

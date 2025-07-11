# Data Storage

## How we store your data

We store the data you sync using Census, sometimes for the lifetime of your Census workspace, in three ways:&#x20;

* **Your connected warehouse**: for [basic-datasets.md](../../datasets/overview/basic-datasets.md "mention") shared from your warehouse, we write transformations and advanced sync engine logs back to the warehouse itself. This data includes:
  * [ai-columns](../../datasets/smart-columns/ai-columns/ "mention")
  * [enrichment](../../datasets/smart-columns/enrichment/ "mention")
  * [warehouse-writeback.md](../../syncs/sync-monitoring/warehouse-writeback.md "mention")
* [census-store](census-store/ "mention"): this is an Iceberg-based managed storage. Items stored in Census Store can be accessed by external compute, including warehouses. This data includes:
  * [saas-datasets.md](../../datasets/overview/saas-datasets.md "mention")
  * [csv-datasets.md](../../datasets/overview/csv-datasets.md "mention")
  * [entity-resolution.md](../../datasets/entity-resolution.md "mention") datasets
  * Census store is also the storage location for [ai-columns](../../datasets/smart-columns/ai-columns/ "mention"), [enrichment](../../datasets/smart-columns/enrichment/ "mention"), and [warehouse-writeback.md](../../syncs/sync-monitoring/warehouse-writeback.md "mention") logs for any of these dataset types.
* [general-object-storage.md](general-object-storage.md "mention"): this is used to house data related to sync execution. This data includes:
  * Snapshots of the data you sync using Basic Sync Engine
  * [sync-tracking.md](../../syncs/sync-monitoring/sync-tracking.md "mention") logs of the data you sync
  * Temporary files used to load and unload data

Census Store & General Object Storage data is stored in cloud-based object storage providers. Census provides object storage locations in multiple clouds in the US and the EU that you can use to store this data, and your Census organization is configured to use these locations by default. You can also add your own object storage locations to Census.

### Census-provided object storage

New Census organizations are configured to use Census-provided object storage by default. Census manages object storage locations in multiple public clouds, including AWS (S3), GCP (GCS), and Azure (Blob Storage). This includes managing credentials with narrow permissions and short lifetimes, encrypting data at rest and in transit, automatically removing old data once it is no longer in use, and ensuring your workspace is always storing data in the correct region (US or EU). This approach is secure and is used by the vast majority of Census customers.

### Customer-provided object storage

You can also [add your own object storage locations](bring-your-own-bucket/) and configure Census to default to these locations on a per-organization, per-workspace, or per-connection basis. Note that some data warehouses are only compatible with specific object storage providers. If a compatible customer-provided storage location is not available, Census will default to using compatible Census-provided storage.

When you bring your own object storage, you are responsible for managing the retention of data in the object storage location, and for ensuring the object storage is located in an appropriate region for your requirements.

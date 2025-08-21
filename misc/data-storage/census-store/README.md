---
description: >-
  Every Census workspace includes a Census Store catalog, which is used to store
  and retrieve data you create within Census.
---

# Census Store

The data stored in Census Store includes:

* CSV datasets
* [entity-resolution.md](../../../datasets/entity-resolution.md "mention") datasets
* ...plus [ai-columns](../../../datasets/smart-columns/ai-columns/ "mention"), [enrichment](../../../datasets/smart-columns/enrichment/ "mention"), and [warehouse-writeback.md](../../../syncs/sync-monitoring/warehouse-writeback.md "mention") logs for all of these datasets

Your workspace’s Census Store catalog is created for you the first time you create one of these resources.

You can find Census Store settings by clicking **Settings** in the Census left navigation to open the **Workspace Settings** page, then selecting the **Census Store** tab.

## Where data is stored

By default, data in Census Store, along with sync metadata like snapshots, [Sync Tracking](https://docs.getcensus.com/basics/sync-monitoring/sync-tracking) and [API Inspector](https://docs.getcensus.com/basics/sync-monitoring/api-inspector) logs for datasets stored in Census Store, is stored in Census-provided object storage in your workspace’s region.&#x20;

**You may also choose to have Census Store use your own object storage provider.** This allows Census to manage data on your behalf, while also maintaining strong guarantees that your data at rest is stored within your cloud.

{% hint style="info" %}
Census Store is only compatible with AWS S3-based storage at this time.
{% endhint %}

### Using an alternative object storage provider

To use a new or existing object storage location to store the data in your Census Store catalog:

1. Click **Settings** in the left navigation to open **Workspace Settings**, then select the **Census Store** tab.
2. Under the **Storage Provider** heading, the current storage location for your workspace catalog data is shown.
3. Click the name of the current storage location to open a drop down showing available options.
   1. Select **New storage location** to configure a new [S3-based storage location](../bring-your-own-bucket/bring-your-own-s3-bucket.md) to store your workspace catalog data.
   2. Select an existing [Custom Object Storage Provider](https://docs.getcensus.com/misc/security-and-privacy/bring-your-own-blob-storage) in your account, including any currently-configured workspace or organization default provider.

{% hint style="warning" %}
Changing your Census Store catalog’s storage location after you begin using Census Store can break existing datasets and syncs. If you need to migrate existing Census store data to a new storage location, contact Census support.
{% endhint %}

## Iceberg Catalog

Census Store data is stored in the Apache Iceberg format, and Census provides an Iceberg REST Catalog you can use to access this data from external tools and services that support Iceberg REST Catalog, like Apache Spark, DuckDB, and [Snowflake](query-census-store-from-snowflake.md).

{% hint style="info" %}
**Zero-Copy/Zero-ETL** is the ability to query external data, like Census Store, directly from your existing data warehouse, without first having to use ELT to replicate it into your warehouse, using a standardized catalog and table format like Apache Iceberg. Support for this functionality varies by warehouse and is growing.
{% endhint %}

### Endpoints

The Census Store Iceberg REST Catalog endpoints are regional. You must use the endpoint specific to the region associated with your workspace. Your Census Store catalog cannot be accessed from the incorrect regional endpoint.

<table><thead><tr><th width="220">Census data plane region</th><th>Iceberg REST Catalog endpoint</th></tr></thead><tbody><tr><td>US</td><td>https://catalog.us.getcensus.com/api/catalog</td></tr><tr><td>EU</td><td>https://catalog.eu.getcensus.com/api/catalog</td></tr></tbody></table>

### Authentication

The Census Store Iceberg REST Catalog uses OAuth2 client credentials authentication. To configure your tool or library to access the REST catalog, you will need to provide the REST catalog endpoint, catalog name, a client ID, and client secret.

Your credential provides read-only access to the data in Census Store. It is not possible to write catalog data using external tools.

#### Create Credential

To create new OAuth2 client credentials:

1. In Census, navigate to **Workspace Settings**.
2. Choose the **Census Store** tab.
3. Under **Iceberg Catalog**, note your workspace’s **Endpoint** and **Catalog Name**, then click **Create Client Credential**.
4. The newly-created **Client ID** and **Client Secret** are displayed on the screen.

{% hint style="warning" %}
The client secret is only visible when the credential is first created; store it securely.
{% endhint %}

#### Revoke Credential

To revoke an existing client credential:

1. In Census, navigate to **Workspace Settings**.
2. Choose the **Managed Storage** tab.
3. Under **Iceberg Catalog**, locate the credential you want to revoke and click the trash can icon (**Revoke Credential**). The credential is destroyed and can no longer be used to authenticate to the Iceberg REST Catalog.

### Integrate with Census Store

You can use Census Store's Iceberg catalog to integrate the data in Census Store with third-party tools and systems:

* [**Query Census Store from Snowflake**](query-census-store-from-snowflake.md)\
  Integrate Census Store with your Snowflake warehouse using Apache Iceberg for Zero-ETL access to Entity Resolution and CSV datasets

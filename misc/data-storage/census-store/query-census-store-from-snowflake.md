---
description: >-
  Integrate Census Store with your Snowflake warehouse using Apache Iceberg for
  Zero-ETL access to Entity Resolution and CSV datasets
---

# Query Census Store from Snowflake

## Prerequisites

To query Census Store from Snowflake, you will need:

* A Snowflake account
* A Census workspace with one or more CSV datasets materialized in Census Store

## Step 1: Create Census Store Iceberg REST Catalog Credentials

In Census, create OAuth2 client credentials that Snowflake will use to access the Iceberg catalog for your workspace’s Managed Storage:

1. Open Census and navigate to **Workspace settings**.
2. Select the **Census Store** tab.
3. Under **Iceberg Catalog**, click **Create Client Credentials**.
4. Copy the newly-created client ID and secret. The secret is only visible when you first create a set of client credentials. If you lose the secret, you will need to create a new set of client credentials.

## Step 2: Create Snowflake Catalog Integration

Now over to Snowflake. First, create a catalog integration that connects the Census Store Iceberg Catalog. Run the following SQL statement in your Snowflake account.

* Choose a unique name for your catalog integration and substitute it for `<catalog-integration-name>`
* Substitute your Census workspace’s Iceberg catalog endpoint for `<catalog-endpoint>` . You can find your workspace’s Iceberg catalog endpoint on the **Census Store** tab of **Workspace settings** under **Iceberg Catalog**.
* Substitute your Census workspace’s Iceberg catalog name for `<catalog-name>`. You can find your workspace’s Iceberg catalog endpoint on the **Census Store** tab of **Workspace settings** under **Iceberg Catalog**.
* Substitute the client ID and secret for the Iceberg catalog credentials you created in the previous step for `<client-id>` and `<client-secret>`.

```sql
CREATE OR REPLACE CATALOG INTEGRATION <catalog-integration-name>
   CATALOG_SOURCE = ICEBERG_REST
   TABLE_FORMAT = ICEBERG
   CATALOG_NAMESPACE = 'default'
   REST_CONFIG = (
     CATALOG_URI = '<catalog-endpoint>'
     WAREHOUSE = '<catalog-name>'
     ACCESS_DELEGATION_MODE = VENDED_CREDENTIALS
   )
   REST_AUTHENTICATION = (
     TYPE = OAUTH
     OAUTH_TOKEN_URI = '<catalog-endpoint>/v1/oauth/tokens'
     OAUTH_CLIENT_ID = '<client-id>'
     OAUTH_CLIENT_SECRET = '<client-secret>'
     OAUTH_ALLOWED_SCOPES = ('PRINCIPAL_ROLE:ALL')
   )
   ENABLED = TRUE;
```

To test the connection was successful, run the following SQL statement in your Snowflake account to verify connectivity, substituting the name of the catalog integration you just created for `<catalog integration name>`:

```sql
SELECT SYSTEM$VERIFY_CATALOG_INTEGRATION('<catalog integration name>');
```

## Step 3: Mount the catalog

Now you need to make that Iceberg catalog accessible for querying. Snowflake's [Linked Catalog](https://docs.snowflake.com/en/sql-reference/sql/create-database-catalog-linked) feature makes this easy.

* Specify the name of Snowflake database you'd like to use for the tables in Iceberg in the `<catalog-database-name>`.
* Provide the unique name for `<catalog-integration-name>` you created in step 2.

```
CREATE DATABASE <catalog-database-name> 
  LINKED_CATALOG = ( CATALOG = '<catalog-integration-name>' ); 
```

Now all the tables in Census Store should be available for querying under t



## Alternative Step 3: Mount individual tables

Instead of mounting the entire catalog, you can also create individual Snowflake Iceberg tables for the Census Store datasets you want to query from Snowflake.&#x20;

* Choose a unique name for your table in Snowflake. Substitute this name for `<table name>`.
* Substitute the name of the catalog integration you created in the previous step for `<catalog integration name>`.
* Substitute the namespace and table name your Census Store dataset is materialized in for `<dataset namespace>` and `<dataset table name>` respectively. You can find these names on the dataset details page for your dataset in Census.

```sql
CREATE OR REPLACE ICEBERG TABLE <fully.qualified.table_name>
  CATALOG = '<catalog integration name>'
  CATALOG_NAMESPACE = '<dataset namespace>'
  CATALOG_TABLE_NAME = '<dataset table name>'
  AUTO_REFRESH = TRUE;
```

Run a `SELECT` statement against the new table to verify the integration. With auto refresh enabled, Snowflake exposes new data as the data is updated in S3.

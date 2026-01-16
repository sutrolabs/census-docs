---
description: >-
  Query Census Store locally using DuckDB Apache Iceberg integration for
  Zero-ETL access to CSV datasets.
---

# Query Census Store locally using DuckDB

## Prerequisites

To query Census Store from DuckDB, you will need:

* [Download](https://duckdb.org/docs/installation/?version=main\&environment=cli\&platform=macos\&download_method=direct) DuckDB version ≥ 1.3.0
* A Census workspace with one or more Entity Resolution or CSV datasets materialized in Census Store

## Step 1: Create Census Store Iceberg REST Catalog Credentials

In Census, create OAuth2 client credentials that Snowflake will use to access your workspace's Iceberg catalog:

1. Open Census and navigate to **Workspace settings**.
2. Select the **Census Store** tab.
3. Under **Iceberg Catalog**, click **Create Client Credentials**.
4. Copy the newly-created client ID and secret. The secret is only visible when you first create a set of client credentials. If you lose the secret, you will need to create a new set of client credentials.

## Step 2: Install Iceberg Extension

1. Open DuckDB.
2.  Install Iceberg Extension and load it<br>

    ```sql
    FORCE INSTALL iceberg FROM core_nightly;
    LOAD iceberg;
    ```

## Step 3: Attach catalog

In DuckDB attach catalog integration to the Iceberg catalog for your workspace’s Managed Storage:

1. Choose a unique name for your catalog integration and substitute it for `<catalog integration name>`
2. Substitute your Census workspace’s Iceberg catalog endpoint for `<catalog endpoint>` . You can find your workspace’s Iceberg catalog endpoint on the **Census Store** tab of **Workspace settings** under **Iceberg Catalog**.
3. Substitute your Census workspace’s Iceberg catalog name for `<catalog name>`. You can find your workspace’s Iceberg catalog endpoint on the **Census Store** tab of **Workspace settings** under **Iceberg Catalog**.
4. Substitute the client ID and secret for the Iceberg catalog credentials you created in the previous step for `<client id>` and `<client secret>`.

Run the following SQL statement.

```sql
ATTACH '<catalog name>' as <catalog integration name> (
  TYPE ICEBERG,
  ENDPOINT '<catalog endpoint>',
  CLIENT_ID '<client id>',
  CLIENT_SECRET '<client secret>',
  OAUTH2_SCOPE 'PRINCIPAL_ROLE:ALL'
);
```

Run the following SQL statement to verify connectivity and get a list of tables:

```sql
SHOW ALL TABLES;
```

## Step 4: Query Iceberg Tables

1. Substitute the name of the catalog integration you created in the previous step for `<catalog integration name>`.
2. Substitute the namespace and table name your Census Store dataset is materialized in for `<dataset namespace>` and `<dataset table name>` respectively. You can find these names on the dataset details page for your dataset in Census.

```sql
SELECT * FROM <catalog integration name>.<dataset namespace>.<dataset table name> LIMIT 5;
```

---
description: >-
  Integrate Census Store with your Snowflake warehouse using Apache Iceberg for
  Zero-ETL access to SaaS and CSV datasets
---

# Query Census Store from Snowflake

## Prerequisites

To query Census Store from Snowflake, you will need:

1. A Snowflake account
2. A Census workspace with:
   1. a customer S3 bucket configured as its Census Store storage provider
   2. one or more SaaS or CSV datasets materialized in Census Store
3. An AWS account, and permission to create IAM roles and policies granting access to the S3 bucket where your Census Store catalog is stored

## Step 1: Create AWS IAM Policy

In the AWS account where the S3 bucket containing your Census Store catalog is located, create an IAM Policy that Snowflake will use to access your Census Store data:

1. Open the AWS Console and navigate to **IAM**.
2. Select **Policies** in the navigation and click **Create policy**.
3. Select the JSON editor and enter the following policy document.
   * Substitute the name of the S3 bucket your workspace’s Census Store catalog is stored in for `<bucket name>`.
   * Substitute your workspace’s catalog name, found on the **Census Store** tab of **Workspace settings** (under **Iceberg Catalog**), for `<catalog name>`.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:GetObjectVersion"
            ],
            "Resource": "arn:aws:s3:::<bucket name>/census_managed_iceberg/<catalog name>/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetBucketLocation"
            ],
            "Resource": "arn:aws:s3:::<bucket name>",
            "Condition": {
                "StringLike": {
                    "s3:prefix": [
                        "census_managed_iceberg/<catalog name>/"
                    ]
                }
            }
        }
    ]
}
```

1. Click **Next**, name your policy, and click **Create policy**.

## Step 2: Create AWS IAM Role

Next, create the IAM Role that Snowflake will use to access your Census Store data:

1. Open the AWS Console and navigate to **IAM**.
2. Select **Roles** in the navigation and click **Create role**.
3. Under **Trusted entity type**, select **AWS account**.
4. Under **An AWS account**, select **This account**.
5. Click **Next**, find the policy you created in the previous step, and check the checkbox next to the policy name to attach the policy to the new role.
6. Click **Next**, name your role, and click **Create role**.

## Step 3: Create Snowflake External Volume

In Snowflake, create an external volume that allows Snowflake to access your Census Store data:

1. Open the Snowflake console and create a SQL Worksheet.
2. Run the following SQL statement in your Snowflake account.
   * Choose a unique name for this external volume and substitute it for `<external volume name>`.
   * Substitute the name of the S3 bucket your workspace’s Census Store catalog is stored in for `<bucket name>`.
   * Substitute your workspace’s catalog name, found on the **Census Store** tab of **Workspace settings** (under **Iceberg Catalog**), for `<catalog name>`.
   * Substitute the ARN of the role you created in the previous step for `<role arn>`.

```sql
CREATE OR REPLACE EXTERNAL VOLUME <external volume name>
   STORAGE_LOCATIONS =
      (
         (
            NAME = '<bucket name>'
            STORAGE_PROVIDER = 'S3'
            STORAGE_BASE_URL = 's3://<bucket name>/census_managed_iceberg/<catalog name>'
            STORAGE_AWS_ROLE_ARN = '<role arn>'
         )
      )
    ALLOW_WRITES = FALSE;
```

## Step 4: Establish Trust Relationship between Snowflake and AWS IAM Role

Gather the IAM User ARN and External ID Snowflake assigns to your external volume, and use them to establish a trust relationship between Snowflake and the IAM Role you created in step 2.

1. Open the Snowflake console and create a SQL Worksheet (or reuse the worksheet from the previous step).
2. Run the following SQL statement in your Snowflake account. Substitute the name of the external volume you created in the previous step for `<external volume name>` .

```sql
DESC EXTERNAL VOLUME <external volume name>;
```

1. The result set contains 3 rows. In the row `STORAGE_LOCATION_1` in the `property` column, the `property_value` column will contain a JSON object. Locate the `"STORAGE_AWS_IAM_USER_ARN"` and `"STORAGE_AWS_EXTERNAL_ID"` keys and note their values. These are the IAM User ARN and External ID for your external volume, respectively.
2. Open the AWS Console and navigate to **IAM**.
3. Select **Roles** in the navigation and find the role you created in step 2. Click the name of the role to open the role details.
4. Select the **Trust relationships** tab and click **Edit trust policy**.
5. Replace the trust policy with the following trust policy document.
   * Substitute the IAM User Arn for your external volume for `<iam user arn>`.
   * Substitute the External ID for your external volume for `<external id>` .

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Principal": {
				"AWS": "<iam user arn>"
			},
			"Action": "sts:AssumeRole",
			"Condition": {
				"StringEquals": {
					"sts:ExternalId": "<external id>"
				}
			}
		}
	]
}
```

1. Click **Update policy**.

## Step 5: Create Census Store Iceberg REST Catalog Credentials

In Census, create OAuth2 client credentials that Snowflake will use to access the Iceberg catalog for your workspace’s Managed Storage:

1. Open Census and navigate to **Workspace settings**.
2. Select the **Census Store** tab.
3. Under **Iceberg Catalog**, click **Create Client Credentials**.
4. Copy the newly-created client ID and secret. The secret is only visible when you first create a set of client credentials. If you lose the secret, you will need to create a new set of client credentials.

## Step 6: Create Snowflake Catalog Integration

In Snowflake, create a catalog integration to the Iceberg catalog for your workspace’s Managed Storage:

1. Open the Snowflake console and create a SQL Worksheet (or reuse the worksheet from earlier steps).
2. Run the following SQL statement in your Snowflake account.
   * Choose a unique name for your catalog integration and substitute it for `<catalog integration name>`
   * Substitute your Census workspace’s Iceberg catalog endpoint for `<catalog endpoint>` . You can find your workspace’s Iceberg catalog endpoint on the **Census Store** tab of **Workspace settings** under **Iceberg Catalog**.
   * Substitute your Census workspace’s Iceberg catalog name for `<catalog name>`. You can find your workspace’s Iceberg catalog endpoint on the **Census Store** tab of **Workspace settings** under **Iceberg Catalog**.
   * Substitute the client ID and secret for the Iceberg catalog credentials you created in the previous step for `<client id>` and `<client secret>`.

```sql
CREATE OR REPLACE CATALOG INTEGRATION <catalog integration name>
   CATALOG_SOURCE = ICEBERG_REST
   TABLE_FORMAT = ICEBERG
   CATALOG_NAMESPACE = 'default'
   REST_CONFIG = (
     CATALOG_URI = '<catalog endpoint>'
     WAREHOUSE = '<catalog name>'
   )
   REST_AUTHENTICATION = (
     TYPE = OAUTH
     OAUTH_TOKEN_URI = '<catalog endpoint>/v1/oauth/tokens'
     OAUTH_CLIENT_ID = '<client id>'
     OAUTH_CLIENT_SECRET = '<client secret>'
     OAUTH_ALLOWED_SCOPES = ('PRINCIPAL_ROLE:ALL')
   )
   ENABLED = TRUE;
```

1. Run the following SQL statement in your Snowflake account to verify connectivity, substituting the name of the catalog integration you just created for `<catalog integration name>`:

```sql
SELECT SYSTEM$VERIFY_CATALOG_INTEGRATION('<catalog integration name>');
```

## Step 7: Create Snowflake Iceberg Tables

Finally, create Snowflake Iceberg tables for the Census Store datasets you want to query from Snowflake. Follow these instructions to add Census Store datasets to Snowflake:

1. Open the Snowflake console and create a SQL Worksheet (or reuse the worksheet from earlier steps).
2. Select the database and schema where you want your external tables to be created.
3. Run the following SQL statement in your Snowflake database.
   * Choose a unique name for your table in Snowflake. Substitute this name for `<table name>`.
   * Substitute the name of the catalog integration you created in the previous step for `<catalog integration name>`.
   * Substitute the namespace and table name your Census Store dataset is materialized in for `<dataset namespace>` and `<dataset table name>` respectively. You can find these names on the dataset details page for your dataset in Census.
   * Substitute the name of the external volume you created in step 3 for `<external volume name>`.

```sql
CREATE OR REPLACE ICEBERG TABLE <table name>
  CATALOG = '<catalog integration name>'
  CATALOG_NAMESPACE = '<dataset namespace>'
  CATALOG_TABLE_NAME = '<dataset table name>'
  EXTERNAL_VOLUME = '<external volume name>'
  AUTO_REFRESH = TRUE;
```

1. Run a `SELECT` statement against the new table to verify the integration. With auto refresh enabled, Snowflake exposes new data as the data is updated in S3.

---
description: >-
  This page describes how to configure Athena credentials for use by Census and
  why those permissions are needed.
---

# Aws Athena

## 🔐 Required Permissions

Census lets you select Amazon Athena as a source for your syncs. Census needs the following permissions:
1. run queries and get their results
2. write the Athena query results to your specified Athena query results bucket location
3. read the s3 files associated with the source tables
4. read the source tables in AWS Glue Data Catalog  

Please create an IAM Policy that includes the following permissions
```
"athena:StartQueryExecution",
"athena:GetQueryExecution",
"athena:GetQueryResultsStream",
"athena:GetQueryResults",
"athena:CreatePreparedStatement",
"athena:DeletePreparedStatement"

"s3:PutObject",
"s3:GetObject",
"s3:ListBucket",

"glue:GetDatabase",
"glue:GetTables",
"glue:GetDatabases",
"glue:GetTable"
```

For Athena permissions, Census needs access to the Athena workgroup where the source tables are located.

For S3 permissions, Census needs to be able to list all the buckets, read/write the query results bucket,
and read the bucket with the source table data.

For AWS Glue Data Catalog permissions, Census needs to be able to get the databases and tables where the
source tables are located.

### Create an Amazon Athena connection

1\. Ensure that the AWS IAM policy created in the "Required Permissions" section is attached to the IAM user that Census is impersonating.

2\. In Census, go to **Connections** or click [here to go to the app](https://app.getcensus.com/connections)

3\. Under Data Sources, click **Add Data Source** and select **Amazon Athena**

![](<../.gitbook/assets/athena\_setup.png>)

4\. Please specify the AWS access key and secret key associated with the user Census will be impersonating, the S3 query result bucket url, S3 region, and Athena workgroup.

![](<../.gitbook/assets/athena\_setup\_properties.png>)

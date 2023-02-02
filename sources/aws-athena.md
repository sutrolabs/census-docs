---
description: >-
  This page describes how to configure Athena credentials for use by Census and
  why those permissions are needed.
---

# Amazon Athena

## 🔐 Required Permissions

Census lets you select Amazon Athena as a source for your syncs. The following resources need to be available:

1. Athena Workgroup: The default workgroup is "primary". Feel free to specify another workgroup and confirm that it exists.
2. Census database in your AWS Glue Data Catalog: This database stores all Census bookkeeping tables. Please create this database by running the following query

```
CREATE DATABASE census
```

1. s3 query results bucket: This can be any bucket in your AWS account. Please check the following a) that the query results bucket exists in s3 and b) the query result location of your workgroup is set to the query results bucket

Additionally, Census needs the following permissions:

1. For Athena Permissions, Census needs to be able to run queries and get their results in the Athena workgroup.
2. For S3 permissions, Census needs to be able to read/write the Athena query results to your specified Athena query results bucket location. It also needs to be able to list all the buckets and read the bucket with the source table data.
3. For AWS Glue Data Cataglo permissions, Census needs to be able to get the databases and tables where the source tables are located.

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

"glue:CreateTable",
"glue:UpdateTable"
"glue:GetDatabase",
"glue:GetTables",
"glue:GetDatabases",
"glue:GetTable",
"glue:DeleteTable"
```

Here is a sample IAM policy that specifies the resources:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            # Give Census full permissions (read, write, delete) to the census database
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "glue:GetDatabase",
                "glue:CreateTable",
                "glue:GetTables",
                "glue:UpdateTable",
                "glue:DeleteTable",
                "glue:GetDatabases",
                "glue:GetTable"
            ],
            "Resource": [
                "arn:aws:glue:<region>:<aws-account-id>:database/census",
                "arn:aws:glue:<region>:<aws-account-id>:table/census/*",
                "arn:aws:glue:<region>:<aws-account-id>:catalog"
            ]
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                # permissions to run queries and see their results
                "athena:CreatePreparedStatement",
                "athena:StartQueryExecution",
                "athena:GetQueryResultsStream",
                "athena:GetQueryResults",
                "athena:GetQueryExecution",
                "athena:DeletePreparedStatement",
                "glue:GetTable",
                "glue:GetTables",
                "glue:GetDatabase",
                "glue:GetDatabases",
                # permissions to get and write query result
                "s3:PutObject",
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:glue:<region>:<aws-account-id>:table/<database of tables to sync>/*",
                "arn:aws:glue:<region>:<aws-account-id>:database/<database of tables to sync>",
                "arn:aws:glue:<region>:<aws-account-id>:catalog",
                "arn:aws:athena:<region>:<aws-account-id>:workgroup/<workgroup>", # <---- only necessary if workgroup is not primary
                "arn:aws:athena:<region>:<aws-account-id>:workgroup/primary", 
                "arn:aws:s3:::<query-results-bucket>",
                "arn:aws:s3:::<query-results-bucket>/*",
                "arn:aws:s3:::<arn where table lives>",
                "arn:aws:s3:::<arn where table lives>/*"
            ]
        }
    ]
}
```

### Create an Amazon Athena connection

1\. Ensure that the AWS IAM policy created in the "Required Permissions" section is attached to the IAM user that Census is impersonating.

2\. In Census, go to **Connections** or click [here to go to the app](https://app.getcensus.com/connections)

3\. Under Data Sources, click **Add Data Source** and select **Amazon Athena**

![](../.gitbook/assets/athena\_setup.png)

4\. Please specify the AWS access key and secret key associated with the user Census will be impersonating, the S3 query result bucket url, S3 region, and Athena workgroup.

![](../.gitbook/assets/athena\_setup\_properties.png)

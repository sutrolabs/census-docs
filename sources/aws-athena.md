---
description: >-
  This page describes how to configure Athena credentials for use by Census and
  why those permissions are needed.
---

# Amazon Athena

## 🔐 Required Permissions

Census lets you select Amazon Athena as a source for your syncs. The following resources need to be available:

1. Athena Workgroup: The default workgroup is "primary". Feel free to specify another workgroup and confirm that it exists.
2. S3 query results bucket: This can be any bucket in your AWS account. Please check the following a) that the query results bucket exists in s3 and b) the query result location of your workgroup is set to the query results bucket

Additionally, Census needs the following permissions:

1. For Athena Permissions, Census needs to be able to run queries and get their results in the Athena workgroup.
2. For AWS Glue Data Catalog permissions, Census needs to be able to get the databases and tables where the source tables are located.

Please create an IAM Policy that includes the following permissions

```
"athena:StartQueryExecution",
"athena:GetQueryExecution",
"athena:GetQueryResultsStream",
"athena:GetQueryResults",
"athena:CreatePreparedStatement",
"athena:DeletePreparedStatement",

"s3:PutObject",
"s3:GetObject",
"s3:ListBucket",
"s3:GetBucketLocation"

"glue:GetDatabase",
"glue:GetTables",
"glue:GetDatabases",
"glue:GetTable"
```

Here is a sample IAM policy that specifies the resources:

```
{
    "Version": "2012-10-17",
    "Statement": [
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
                "s3:ListBucket",
                "s3:GetBucketLocation"
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

1\. Ensure that the AWS IAM policy created in the "Required Permissions" section is attached to the IAM user that Census is impersonating. 2. In Census, go to **Sources** or click [here to go to the app](https://app.getcensus.com/sources). 3. Click **New Source** and select **Amazon Athena**.

![](../.gitbook/assets/athena\_setup.png)

4\. Please specify the AWS access key and secret key associated with the user Census will be impersonating, the S3 query result bucket url, S3 region, and Athena workgroup.

![](../.gitbook/assets/athena\_setup\_properties.png)

### Using Role-Based Permissions

As an alternative to using keys you may opt to grant Census access to a role in your AWS account. This won't provide any additional functionality from Census, but may be preferable for your AWS configuration. This is a multi-step process with parts happening in Census and inside your AWS console.

Step 1: When configuring the Athena source click the "Use role" checkbox. Provide your region, S3 output location, and workgroup, but leave access and secret key blank. Click Connect:

<figure><img src="../.gitbook/assets/CleanShot 2023-02-14 at 14.13.06@2x.png" alt=""><figcaption></figcaption></figure>

Step 2: The automated connection check will run at this point and fail, this is expected.

Step 3: Click the 'Back' button to return to editing the destination. You should now see an 'External ID' input box with a string in it. You will use this string in the following step.

<figure><img src="../.gitbook/assets/CleanShot 2023-02-14 at 14.15.14@2x.png" alt=""><figcaption></figcaption></figure>

Step 4: Open your AWS Console in a separate tab and browse to the IAM service. Click 'Roles' and 'Create role'.

* When creating the role choose 'AWS Account' for Trusted Entity Type and the 'Another AWS Account' radio button.
* Ask your Census account representative for the Census AWS account to use.
* Check the 'Require external ID' checkbox and enter the External ID string from Step 3.
* Finish setting up your Role. Note that it should have the [required permissions](aws-athena.md#required-permissions) to access the Athena instance and associated S3 buckets you are using as your Census source!
* When done, click on your role and copy its ARN. Go back to the tab where you're editing the Census Athena source and enter the role ARN.
* Click 'Connect'. The tester should re-run and succeed.

## 🚑 Need help connecting to Athena?

[Contact us](mailto:support@getcensus.com) via support@getcensus.com or start a conversation with us via the [in-app](https://app.getcensus.com) chat.
